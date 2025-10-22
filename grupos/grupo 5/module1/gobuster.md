# Gobuster 

O Gobuster é uma ferramenta de enumeração usada em testes de segurança e pentests.
 A enumeração significa descobrir informações ocultas ou estruturais de um alvo, como diretórios, arquivos e subdomínios.
Ele funciona por meio de força bruta, testando várias palavras de uma wordlist (lista de palavras) contra o alvo, verificando quais retornam resultados válidos.

*gobuster [command] -u IP [flag] diretorio ( Tentativas de dominio)*
*-u IP [flag alvo]*

## Comandos

* gobuster -h: Mostra a página de ajuda com todas as opções disponíveis.
* dir: Enumeração de diretórios e arquivos em um site. Ex: descobrir /admin, /backup.zip, /config.php.
* dns: Enumeração de subdomínios de um domínio. Ex: mail.exemplo.com, dev.exemplo.com
* fuzz: Fuzzing genérico, onde a palavra da wordlist é injetada em um ponto escolhido. Útil para testar parâmetros em URLs, cabeçalhos HTTP ou caminhos específicos.
* gcs: Enumeração de buckets do Google Cloud Storage, verificando se existem expostos ou mal configurados.
* help: Exibe a ajuda detalhada de um comando específico. Ex: gobuster dir -h.
* s3: Enumeração de buckets do Amazon S3, revelando possíveis arquivos sensíveis expostos.
* tftp: Enumeração de arquivos em servidores TFTP (Trivial File Transfer Protocol), que podem expor configurações ou backups.
* version: Mostra a versão atual do Gobuster instalada no sistema

## Flags 

* --debug: Mostra informações detalhadas de depuração, útil para entender o que o Gobuster está fazendo em segundo plano.
* --delay duration: Define um tempo de espera entre cada requisição (ex: --delay 1s espera 1 segundo entre os testes). Útil para evitar sobrecarregar o alvo ou burlar sistemas de proteção.
* -h, --help: Exibe a ajuda geral ou a ajuda de um comando específico.
* --no-color: Remove cores da saída do terminal, deixando apenas texto puro. Bom para salvar logs sem formatação.
* --no-error: Oculta mensagens de erro (não mostra falhas de conexão, timeouts, etc).
* -z, --no-progress: Desativa a barra de progresso. A saída fica mais limpa, útil quando o resultado será redirecionado para arquivos.
* -o, --output string: Salva os resultados da varredura em um arquivo definido pelo usuário. Exemplo: -o resultado.txt
* -q: Modo silencioso (quiet mode). Só mostra resultados encontrados, sem mensagens extras.
* -t: Define o número de threads (conexões simultâneas). Exemplo: -t 50 usa 50 threads, tornando a enumeração mais rápida.
* -v: Modo verbose. Mostra resultados em detalhe, incluindo respostas negativas e mais informações de cada requisição.
* -w ou --wordlist: Define a wordlist (lista de palavras) que será usada no ataque de força bruta. Exemplo: -w /usr/share/wordlists/dirb/common.txt.

