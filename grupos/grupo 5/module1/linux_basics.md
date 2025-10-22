# Comandos Básicos no Linux <h1>
🧠 Comandos Básicos do Terminal Linux

### 1. Abertura do Terminal <h3>
Ctrl + Alt + T
→ Abre o terminal.

### 2. Navegação entre Diretórios <h3>
pwd                # Mostra o diretório atual
cd nome            # Vai para o diretório indicado
cd ..              # Volta um nível
cd /var/           # Acessa pasta a partir da raiz
~                  # Diretório home do usuário

### 3. Listagem de Arquivos e Pastas <h3>
ls                 # Lista arquivos/diretórios
ls -l              # Listagem detalhada (permissões, dono, data)
ls -a              # Mostra ocultos
ls -lh             # Tamanhos legíveis (KB, MB)
ls -ltr            # Ordena por data de modificação
ls -ltr /var/      # Lista em /var/

### 4. Criação e Visualização de Arquivos
touch nome.ext                 # Cria arquivo vazio
cat nome.ext                   # Mostra conteúdo
cat -n arquivo.txt             # Mostra com numeração
cat arquivo1 arquivo2 > novo.txt  # Junta arquivos
nano arquivo                   # Editor de texto (modo terminal)
vim arquivo                    # Outro editor de texto
echo "texto"                   # Imprime texto no terminal
echo "texto" > arq.txt         # Cria/sobrescreve arquivo
echo "texto" >> arq.txt        # Acrescenta no final

### 5. Limpeza e Histórico <h3>
clear        # Limpa tela
history      # Mostra histórico
Ctrl + R     # Busca no histórico
Ctrl + C     # Interrompe execução

### 6. Criação e Remoção de Diretórios <h3>
mkdir nome       # Cria diretório
rmdir nome       # Remove diretório vazio
rm -d nome       # Remove diretório vazio
rm -rf nome      # Remove pasta e conteúdo (cuidado!)

### 7. Remoção e Movimentação de Arquivos <h3>
rm nome                  # Remove arquivo
rm -i nome               # Remove com confirmação
mv arquivo destino/      # Move ou renomeia arquivo
cp arquivo destino/      # Copia arquivo

### 8. Redirecionamento e Encadeamento
>     # Redireciona saída (sobrescreve arquivo)
>>    # Redireciona adicionando ao final
|     # Encadeia comandos (pipe)

Exemplo: ls -l | grep test.txt   # Filtra listagem

head -10 arquivo                 # Mostra primeiras 10 linhas
grep palavra arquivo             # Filtra linhas por padrão

### 9. Processos e Gerenciamento <h3>
ps aux      # Lista todos os processos
top         # Mostra processos em tempo real
htop        # Interface mais amigável (precisa instalar)

### 10. Gerenciamento de Usuários e Grupos <h3>
sudo adduser nome                  # Cria usuário
getent passwd                      # Lista usuários
sudo userdel --remove nome         # Remove usuário
sudo groupadd nome                 # Cria grupo
sudo groupdel nome                 # Remove grupo
groups usuario                     # Mostra grupos do usuário
sudo usermod -a -G grupo usuario   # Adiciona usuário ao grupo
chown usuario arquivo              # Troca dono
chgrp grupo arquivo                # Troca grupo

### 11. Permissões no Linux <h3>

Formato: drwxr-xr-x

Letra	Significado	Ação
r	read	leitura
w	write	escrita
x	execute	execução
Alterando permissões
chmod 777 arquivo    # Todos com acesso total (evitar)
chmod 000 arquivo    # Ninguém acessa
chmod u+x arquivo    # Dono ganha permissão de executar
chmod g-w arquivo    # Remove escrita do grupo
chmod a=rwx arquivo  # Todos com acesso total

### 12. Pacotes e Atualizações <h3>
sudo apt-get update       # Atualiza lista de pacotes
sudo apt-get upgrade      # Atualiza pacotes
sudo apt-get install nome # Instala pacote
sudo apt-get purge nome   # Remove pacote + configs

### 13. Outros Comandos Úteis <h3>
whoami                   # Mostra usuário atual
uname -a                 # Infos do sistema
df -h                    # Uso do disco
du -sh pasta/            # Tamanho da pasta
tree /etc                # Estrutura de diretórios
man comando              # Manual do comando

cron                     # Agenda execução de scripts
crontab -e               # Edita tarefas agendadas

less arquivo             # Visualiza conteúdo de texto
echo                     # Imprime texto
cat                      # Exibe conteúdo de arquivo
find -name "*.txt"       # Encontra arquivos com extensão .txt
grep                     # Busca texto dentro de arquivos
wc -l arquivo.log        # Conta linhas no arquivo

# Operadores
Operador	Função
&	Executa comando em segundo plano
&&	Executa o próximo comando apenas se o anterior for bem-sucedido
>	Redireciona saída (sobrescreve)
>>	Redireciona saída (acrescenta ao final)
