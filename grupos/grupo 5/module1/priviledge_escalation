
# Privilege Escalation

### Definição
Privilege Escalation é a exploração de uma vulnerabilidade, falha de design ou configuração incorreta em um sistema operacional ou aplicação para obter acesso não autorizado a recursos normalmente restritos aos usuários.  
Permite alcançar nível de administrador (root): redefinir senhas, obter persistência, executar comandos administrativos.

---

### Enumeração
Primeiro passo após obter acesso a um sistema.

#### Informações do sistema / SO
- `hostname` → retorna o hostname da máquina alvo (pode indicar o papel do sistema).  
- `uname -a` → exibe informações do kernel/SO.  
- `cat /proc/version` → pode revelar versão/build do kernel (ex.: compilador).  
- `cat /etc/issue` → geralmente contém identificação do SO.

#### Usuário / ambiente
- `id` → UID/GID e grupos do usuário atual.  
- `whoami` → usuário atual.  
- `env` → variáveis de ambiente.  
- `history` → histórico do shell (pode vazar comandos/senhas).

#### Arquivos & listagem
- `ls` → lista básica de arquivos não ocultos.  
- `ls -l` → listagem detalhada (não ocultos).  
- `ls -la` → listagem detalhada incluindo ocultos.  
- `cat filename.txt` → imprime conteúdo de arquivo.

#### Processos
- `ps` → exibe processos em execução.  
- `ps -A` → todos os processos.  
- `ps axjf` → árvore de processos.  
- `ps aux` → processos de todos os usuários.

#### Rede / conexões
- `ifconfig` e `ip route` → informações de rede.  
- `netstat` → informações de conexões:  
  - `netstat -a` → todas
