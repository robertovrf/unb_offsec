## Questão 1 
Iniciamos identificando o tipo provável do hash com a ferramenta hashid. A intenção deste passo é obter uma lista de possíveis algoritmos (por exemplo MD5, SHA1, bcrypt, etc.) para não tentar adivinhar o modo nas ferramentas de cracking. Para isso executamos hashid hash.txt; quando queríamos uma saída pronta para John the Ripper, usamos hashid -j hash.txt, que gera uma saída em formato JSON/john. Esse comando nos deu os candidatos de algoritmos que guiaram as escolhas seguintes em John e Hashcat.
Comando usado: hashid hash.txt (ou hashid -j hash.txt para saída compatível com John).

A resposta: `password123`


---

## Questão 2 

Depois da identificação, tentamos primeiro uma abordagem com wordlist usando o John the Ripper, porque muitas senhas de CTF estão em listas conhecidas e essa abordagem é rápida. Colocamos o hash em hashes.txt e rodamos:

john --wordlist=/path/to/wordlist.txt --format=raw-sha1 hashes.txt

onde raw-sha1 é o identificador retornado pelo hashid. O John processou a wordlist testando cada entrada contra o(s) hash(es); se encontrasse uma correspondência, seria possível visualizar com john --show hashes.txt.
Comandos usados:

john --wordlist=/path/to/wordlist.txt --format=raw-sha1 hashes.txt

john --show hashes.txt (para exibir senhas recuperadas)

A resposta: `easy`


---
 
## Questão 3

Quando a wordlist não foi suficiente, passamos para um ataque por máscara com o hashcat, eficiente quando temos suspeitas sobre comprimento e tipos de caracteres. Para o caso do modo -m 900 usamos:

hashcat -m 900 -a 3 hash.txt -1 '?l?u?d' '?1?1?1?1?1?1' --status --status-timer=10 --session=alnum6_m900

Aqui o raciocínio foi: o -m 900 especifica o tipo de hash identificado anteriormente; -a 3 é ataque por máscara; -1 '?l?u?d' cria um charset ?1 com letras minúsculas, maiúsculas e dígitos; e a máscara '?1?1?1?1?1?1' limita a busca a combinações de 6 caracteres — muito mais rápido do que testar comprimentos variados sem pista. Usamos --status e --status-timer=10 para monitorar o progresso a cada 10s e --session para nomear a sessão caso fosse necessário retomar depois. Após o término, exibimos a senha encontrada com:

hashcat -m 900 --show hash.txt

Saída obtida:

4149c5cc4c378444d116d65ad5ba4099:0ffs3c

Ou seja, o hash 4149c5cc4c378444d116d65ad5ba4099 corresponde à senha 0ffs3c.
Comandos usados:

hashcat -m 900 -a 3 hash.txt -1 '?l?u?d' '?1?1?1?1?1?1' --status --status-timer=10 --session=alnum6_m900

hashcat -m 900 --show hash.txt (para revelar a senha encontrada)

A resposta: `0ffs3c`



---

## Questão 4

Em outro cenário aplicamos a mesma lógica para um modo de hash diferente (-m 1400). Ajustamos o charset de acordo com nossas suposições (por exemplo, apenas minúsculas e dígitos) e configuramos um arquivo de pot específico para registrar resultados. O comando foi:

hashcat -m 1400 -a 3 hashes.txt -1 ?l?d ?1?1?1?1?1?1 --potfile-path=hc.pot -w 3 --status --status-timer=10

Aqui -m 1400 indica o algoritmo apropriado; -1 ?l?d define ?1 como letras minúsculas e dígitos; a máscara ?1?1?1?1?1?1 limita a 6 caracteres; --potfile-path=hc.pot força o hashcat a gravar as senhas quebradas em hc.pot (útil para auditoria e para evitar repetição de trabalho); -w 3 ajusta o workload para um perfil mais agressivo; e as opções de status mantêm a visibilidade do progresso. Essa configuração é ideal quando temos evidências sobre o formato da senha e queremos que o processo grave resultados em um arquivo específico.
Comando usado:
hashcat -m 1400 -a 3 hashes.txt -1 ?l?d ?1?1?1?1?1?1 --potfile-path=hc.pot -w 3 --status --status-timer=10

A resposta: `ovelha`



---

## Questão 5

Nesta etapa aplicamos um ataque por máscara com o hashcat, já que tínhamos indicação do tipo de hash e suspeita sobre o formato da senha (6 caracteres, apenas letras minúsculas e dígitos).

Comando utilizado:

hashcat -m 1400 -a 3 hashes.txt -1 ?l?d ?1?1?1?1?1?1 --potfile-path=hc.pot -w 3 --status --status-timer=10


Resultado e conclusão:

Ao executar o comando acima com os parâmetros indicados, o hash foi quebrado e a senha encontrada foi:

A resposta: `sawctf`
