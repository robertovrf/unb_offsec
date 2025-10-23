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
  - `netstat -a` → todas portas em escuta e conexões estabelecidas.  
  - `netstat -at` / `netstat -au` → listar TCP / UDP, respectivamente.  
  - `netstat -l` → portas em escuta (use com `-t` para TCP).  
  - `netstat -s` → estatísticas por protocolo (pode combinar `-t`/`-u`).  
  - `netstat -tp` → mostra serviço e PID (dependente da distro).  
  - `netstat -ano` detalhado:  
    - `-a`: exibir todos sockets  
    - `-n`: não resolver nomes  
    - `-o`: exibir timers

---

### Comando `find` (busca de arquivos / propriedades)
- `find . -name flag1.txt` — encontra `flag1.txt` no diretório atual.  
- `find /home -name flag1.txt` — encontra em `/home`.  
- `find / -type d -name config` — encontra diretório `config` sob `/`.  
- `find / -type f -perm 0777` — arquivos com permissão 777.  
- `find / -perm a=x` — arquivos executáveis.  
- `find /home -user frank` — arquivos do usuário `frank` em `/home`.  
- `find / -mtime 10` — arquivos modificados há 10 dias.  
- `find / -atime 10` — arquivos acessados há 10 dias.  
- `find / -cmin -60` — metadados alterados nos últimos 60 minutos.  
- `find / -amin -60` — arquivos acessados nos últimos 60 minutos.  
- `find / -size 50M` — arquivos de ~50 MiB (use `+`/`-` para maior/menor).

#### Observações / dicas
`find` costuma gerar muitos erros de permissão; use `2>/dev/null` para ocultar:  
- `find / -type f 2>/dev/null`

Diretórios world-writable / executáveis:  
- `find / -writable -type d 2>/dev/null`  
- `find / -perm -222 -type d 2>/dev/null`  
- `find / -perm -o w -type d 2>/dev/null`  
- `find / -perm -o x -type d 2>/dev/null`

#### Procurar ferramentas/linguagens
- `find / -name perl*`  
- `find / -name python*`  
- `find / -name gcc*`

---

### SUID / bits especiais
SUID faz o arquivo rodar com privilégios do dono do arquivo (vetor clássico de escalada).  
Ex.:  
- `find / -perm -u=s -type f 2>/dev/null` — arquivos com SUID.

---

### Outros comandos úteis / dicas
- `cat /etc/passwd` → lista contas (usado para enumeração; hashes normalmente ficam em `/etc/shadow`).  
- `sudo -l` → lista comandos que o usuário atual pode rodar via sudo.  
- `history` → pode revelar entradas sensíveis.  
- Utilitários gerais: `find`, `locate`, `grep`, `cut`, `sort`, etc.

---

### Ferramentas automatizadas de enumeração
Agilizam o processo, mas podem perder vetores. Exemplos:
- `linPEAS` — https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/linPEAS  
- `LinEnum` — https://github.com/rebootuser/LinEnum  
- `LES (Linux Exploit Suggester)` — https://github.com/mzet-/linux-exploit-suggester  
- `Linux Smart Enumeration` — https://github.com/diego-treitos/linux-smart-enumeration  
- `Linux Priv Checker` — https://github.com/linted/linuxprivchecker

---

### Privilege Escalation: Exploits de Kernel

#### Metodologia
1. Identificar versão do kernel.  
2. Procurar código de exploit compatível.  
3. Executar o exploit.

#### Cuidados
- Exploit mal-sucedido pode travar o sistema (kernel panic).  
- Bases de CVE / buscas (ex.: https://www.cvedetails.com/) ajudam.  
- Ferramentas como LES auxiliam, mas podem gerar falsos-positivos/negativos.
