# ROOM 1

## Ferramentas utilizadas

- Haiti: identificador de tipo de hash que já fornece referências para os modos do Hashcat e do John the Ripper
- hashcat
- john the ripper

---

## Hash 1

- **Hash**: 482c811da5d5b4bc6d497ffa98491e38
- **Dificuldade**: fácil

**Comando:**
hashcat -m 0 -a 0 rockyou.txt hash.txt


- **Resposta**: password123
- **Comentários**: conseguimos no primeiro teste

---

## Hash 2

- **Hash**: 861c4f67e887dec85292d36ab05cd7a1a7275228
- **Dificuldade**: fácil

**Comando:**


hashcat -m 100 -a 0 rockyou.txt hash.txt


- **Resposta**: easy
- **Comentários**: conseguimos no primeiro teste

---

## Hash 3

- **Hash**: 4149c5cc4c378444d116d65ad5ba4099
- **Dificuldade**: difícil

**Comando:**


hashcat -m 900 -a 3 hash.txt '?d?d?d?d?d?d'


- **Resposta**: 0ffs3c
- **Comentários**: tentamos hashcat, outras wordlists, john the ripper, rules e máscara, até percebermos que poderia ser outro tipo de hash que não o MD5. Pesquisando, vimos que o MD4 é o mais parecido com o MD5; testamos e finalmente deu certo.

---

## Hash 4 (com salt)

- **Hash**: cdeb746ec095149627348b61d4140fc58b745875
- **Salt**: satech
- **Dificuldade**: média

**Comando:**


hashcat -m 160 -a 0 "cdeb746ec095149627348b61d4140fc58b745875:satech"


- **Resposta**: ovelha
- **Comentários**: a dica fornecida nos poupou tempo, porém ficamos confusos sobre como usar o salt.

---

## Hash 5

- **Hash**: 362fda2183b7ac73400a83f6ab2c359451e48adf6c3d46a2963ee2abdf852912
- **Dificuldade**: média

**Comando:**


hashcat -m 1400 -a 3 hash.txt '?l?l?l?l?l?l'


- **Resposta**: sawctf
- **Comentários**: primeiro testamos com wordlist, mas como já tínhamos entendimento sobre o teste com máscara, não demoramos muito testando outras coisas.

---

## Aprendizados

- Nem sempre a ferramenta identificadora do tipo de hash está correta, então é recomendado testar outros tipos de hash caso o mais provável não funcione.
- É importante saber quais hashes são parecidos entre si.
- Se já sabemos o tamanho da senha e o teste por máscara com todas as combinações não funciona, há grande chance do tipo de hash estar errado.
