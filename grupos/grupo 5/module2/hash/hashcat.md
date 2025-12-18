# Hashcat — Guia Rápido

---

### Instalação
```bash
brew install hashcat
```

---

### Sintaxe básica
```bash
hashcat -m <tipo_hash> -a <modo_ataque> <arquivo_de_hashes> <wordlist>
```

---

### Tela de ajuda
```bash
hashcat -h
```

---

### Comandos importantes
- `-m` → especifica o algoritmo/hash. Ex.: `-m 0` é o MD5.  
- `-a` → modo de ataque:
  - `-a 0` : ataque por dicionário  
  - `-a 3` : ataque de força bruta  
  - `-a 6` : ataque híbrido (wordlist + máscara)  
  - `-a 7` : ataque híbrido inverso (máscara + wordlist)

---

### Agrupamentos (masks)
- `?l` → letras minúsculas  
- `?u` → letras maiúsculas  
- `?d` → dígitos (0-9)  
- `?s` → caracteres especiais

Exemplo: ataque de força bruta de 6 caracteres minúsculos:
```bash
hashcat -a 3 -m 0 hashes.txt '?l?l?l?l?l?l'
```

Criando um agrupamento personalizado (variável `-1`):
```bash
hashcat -a 3 -m 0 hashes.txt -1 ?l?d '?1?1?1?1?1?1'
```

Dica: não tente "todos os agrupamentos" de uma vez; prefira máscaras que sigam padrões humanos comuns (ex.: `?u?l?l?1?1?l?d?d?s`).

---

### Hashes comuns (exemplos)
| Tipo | Hashcat `-m` | john `--format` |
|---|---:|:---|
| MD5 | `0` | `raw-md5` |
| MD2 | (não suportado) | `md2` |
| SHA1 | `100` | `raw-sha1` |
| MD4 | `900` | `raw-md4` |
| NTLM | `1000` | `NT` |
| SHA256 | `1400` | `raw-sha256` |
| bcrypt | `3200` | `bcrypt` (Jumbo) |
| md5(md5($pass)) (double MD5) | `2600` | variante específica |
| sha512crypt | `1800` | `sha512crypt` |
| sha1(sha1($pass)) (double SHA1) | `4500` | variante específica |

> Nota: sempre confirme o `-m` correto para o hash com que está trabalhando.

---

### Filtrar wordlist para X caracteres
```bash
awk 'length($0)==X' rockyou.txt > rockyouX.txt
```

---

### Exemplos de uso avançado

#### 1) Wordlist + regras
```bash
hashcat -m 900 -a 0 hash.txt wordlists/rockyou.txt -r rules/best64.rule --status --status-timer=10 --session=myctf --potfile-path=potfile.pot
```

#### 2) Hybrid (wordlist + máscara)
```bash
hashcat -m 900 -a 6 hash.txt wordlists/rockyou.txt '?d?d?d'  # palavra + 3 dígitos
```

#### 3) Mask (força bruta direcionado)
```bash
hashcat -m 900 -a 3 hash.txt '?u?l?l?l?l?l?d?d?d?d'
```

---

### Boas práticas e observações
- Use `--status` e `--status-timer` para acompanhar o progresso.  
- Use `--session` e `--potfile-path` para retomar sessões.  
- Seja cuidadoso ao usar força bruta: combinações podem explodir em tempo de execução e custo computacional.  
- Para fins legais e educativos: só ataque hashes que você tem autorização para testar (CTFs, exercícios próprios, auditorias contratadas).

---

### Recursos úteis
- Regras: `rules/best64.rule`, `rules/d3ad0ne.rule`, etc.  
- Wordlists populares: `rockyou.txt` (apenas para uso autorizado).  
- Documentação oficial: `hashcat --help` e site do Hashcat.
