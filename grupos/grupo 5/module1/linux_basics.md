# Comandos Linux

## 1. Abertura do Terminal
`Ctrl + Alt + T` → Abre o terminal.

---

## 2. Navegação entre Diretórios
`pwd` → Mostra o diretório atual.

`cd nome` → Vai para o diretório indicado.

`cd ..` → Volta um nível.

`cd /var/` → Acessa pasta a partir da raiz.

`~` → Diretório home do usuário.

---

## 3. Listagem de Arquivos e Pastas
`ls` → Lista arquivos/diretórios.

`ls -l` → Listagem detalhada (permissões, dono, data).

`ls -a` → Mostra ocultos.

`ls -lh` → Tamanhos legíveis (KB, MB).

`ls -ltr` → Ordena por data de modificação.

`ls -ltr /var/` → Lista em /var/.

---

## 4. Criação e Visualização de Arquivos
`touch nome.ext` → Cria arquivo vazio.

`cat nome.ext` → Mostra conteúdo.

`cat -n arquivo.txt` → Mostra com numeração.

`cat arquivo1 arquivo2 > novo.txt` → Junta arquivos.

`nano` ou `vim` arquivo → Editores de texto.

`echo "texto"` → Imprime texto no terminal.

`echo "texto" > arq.txt` → Cria/sobrescreve arquivo.

`echo "texto" >> arq.txt` → Acrescenta no final.

---

## 5. Limpeza e Histórico
`clear` → Limpa tela.

`history` → Mostra histórico.

`Ctrl + R` → Busca no histórico.

`Ctrl + C` → Interrompe execução.

---

## 6. Criação e Remoção de Diretórios
`mkdir nome` → Cria diretório.

`rmdir nome` → Remove diretório vazio.

`rm -d nome` → Remove diretório vazio.

`rm -rf nome` → Remove pasta e conteúdo (cuidado!).

---

## 7. Remoção e Movimentação de Arquivos
`rm nome` → Remove arquivo.

`rm -i nome` → Remove com confirmação.

`mv arquivo destino/` → Move/renomeia arquivo.

`cp arquivo destino/` → Copia arquivo.

---

## 8. Redirecionamento e Encadeamento
`>` → Redireciona saída (sobrescreve arquivo).

`>>` → Redireciona adicionando ao final.

`|` (pipe) → Encadeia comandos.

Exemplo: `ls -l | grep test.txt` → Filtra listagem.

`head -10 arquivo` → Mostra primeiras 10 linhas.

`grep palavra arquivo` → Filtra linhas por padrão.

---

## 9. Processos e Gerenciamento
`ps aux` → Lista todos os processos.

`top` → Processos em tempo real.

`htop` → Interface mais amigável (precisa instalar).

---

## 10. Gerenciamento de Usuários e Grupos
`sudo adduser nome` → Cria usuário.

`getent passwd` → Lista usuários.

`sudo userdel --remove nome` → Remove usuário.

`sudo groupadd nome` → Cria grupo.

`sudo groupdel nome` → Remove grupo.

`groups usuario` → Mostra grupos do usuário.

`sudo usermod -a -G grupo usuario` → Adiciona ao grupo.

`chown usuario arquivo` → Troca dono.

`chgrp grupo arquivo` → Troca grupo.

---

## 11. Permissões no Linux
**Formato:** `drwxr-xr-x`

- `r` = read (leitura)
- `w` = write (escrita)
- `x` = execute (execução)

Alterando permissões:
`chmod 777 arquivo` → Todos com acesso total (evitar).

`chmod 000 arquivo` → Ninguém acessa.

`chmod u+x arquivo` → Dono ganha permissão de executar.

`chmod g-w arquivo` → Remove escrita do grupo.

`chmod a=rwx arquivo` → Todos com acesso total.

---

## 12. Pacotes e Atualizações
`sudo apt-get update` → Atualiza lista de pacotes.

`sudo apt-get upgrade` → Atualiza pacotes.

`sudo apt-get install nome` → Instala pacote.

`sudo apt-get purge nome` → Remove pacote + configs.

---

## 13. Outros Comandos Úteis
`whoami` → Mostra usuário atual.

`uname -a` → Infos do sistema.

`df -h` → Uso do disco.

`du -sh pasta/` → Tamanho da pasta.

`tree /etc` → Estrutura de diretórios.

`man comando` → Manual do comando.

`cron` → Agenda execução de scripts em horários específicos.

`crontab -e` → Edita tarefas agendadas.

`less` → Visualiza conteúdo de arquivos texto.

`echo` → Printar na tela.

`cat` → Ver o que tem dentro do arquivo.

`find -name "*.txt"` → Encontra todos os arquivos com extensão `.txt`.

`grep` → Permite buscar no conteúdo dos arquivos valores específicos que procuramos.

`wc -l arquivo.log` → Permite ver a quantidade de entradas.

### Operadores

- `&` → Permite executar comando em segundo plano.
- `&&` → Comando AND.
- `>` → Redirecionador de saída (sobrescreve a saída).
- `>>` → Em vez de sobrescrever qualquer conteúdo dentro de um arquivo, ele apenas coloca a saída no final.
