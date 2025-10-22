# CTF Challenge - Our Notes

## Processo de Exploração
### 1. Coleta de informações iniciais

* Buscar o máximo de informação possível sobre o sistema alvo.
  - Ping / conectividade.
  - ping IP
* Varredura de portas e serviços com Nmap:
  - nmap IP -T4
* Mapeamento de diretórios com Gobuster:.
  - gobuster dir -u IP -w wordlist
* Inspecionar HTML/JS/CSS/Assets por dicas
  - Verificamos o código-fonte
* Shell
  - Verificar usuário/privileges (ex.: whoami, id, sudo -l, grep).
  - Procurar flags em diretórios de projeto, home, /tmp, root.

* Uploads e Entradas
  

