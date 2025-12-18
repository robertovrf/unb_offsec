# Challenge: **Pickle Rick**

---

### Resumo do Processo de Exploração

#### 1. Coleta de informações iniciais
No primeiro momento buscamos o máximo de informação possível sobre o sistema alvo.

  ```bash
  ping <IP> # ping / conectividade
  
  nmap <IP> -T4 # Varredura de portas e serviços (Nmap)

  gobuster dir -u <URL_or_IP> -w <wordlist> # Mapeamento de diretórios (Gobuster)
  ```
- **Inspeção de HTML / JS / CSS / assets**
  - Verificamos o código-fonte e identificamos o **nome do usuário**, que guardamos para uso posterior.

---

#### 2. Descoberta de diretórios e página de login
- Durante o `gobuster` encontramos vários possíveis diretórios.  
- A wordlist inicial **não** mapeou `login.php`, mas ao testar manualmente encontramos a página de login.  
- Tínhamos o **nome de usuário**, mas **não** a senha.  
- A inspeção arquivo-a-arquivo não revelou informações úteis.  
- Ao verificar **`robots.txt`** encontramos uma pista que permitiu acessar o portal.

---

### Painel do Portal
- Dentro do portal navegamos por algumas abas.  
- No **painel de comando** executamos `ls` e outros comandos. Alguns funcionaram, outros não.  
- Tivemos dificuldade em visualizar arquivos usando `GET`. Depois de ~1 hora pesquisando, aprendemos a usar:
  ```bash
  less <arquivo>
  ```

---

### Flags Obtidas

1. **Primeira flag**  
   - Encontrada em um arquivo lido com `less`:
   ```
   mr. meeseek hair
   ```

2. **Segunda flag**  
   - Em `clue.txt` havia uma dica; ficamos travados até pesquisar.  
   - Descobrimos que a flag estava associada ao usuário `rick`:
   ```
   jerry tear
   ```

3. **Terceira flag**  
   - Explorando o diretório raiz encontramos a terceira flag, completando a sequência de ingredientes do desafio:
   ```
   fleeb juice
   ```

---

### Dificuldades & Lições Aprendidas
- **Esquecimento de comandos básicos do Linux** — tivemos dificuldade em lembrar comandos essenciais para exploração.  
- **Tentativas longas sem sucesso** — passamos mais de 1 hora tentando abordagens sem progresso até reconhecer a necessidade de pesquisar (vídeos/tutorias).  
- **Lição**: pesquisar e recorrer a referências externas é uma parte natural do processo de pentest/red team para economiza tempo a longo prazo.
- 
---
