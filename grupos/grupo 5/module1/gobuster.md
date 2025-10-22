# Gobuster — Guia rápido (README)

> Guia rápido de uso do **Gobuster** para enumeração em testes de segurança e pentests.  
> Exemplos e flags comuns prontos para uso no terminal.

---

## Sumário
- [O que é](#o-que-é)  
- [Pré-requisitos](#pré-requisitos)  
- [Instalação](#instalação)  
- [Sintaxe geral](#sintaxe-geral)  
- [Comandos principais](#comandos-principais)  
- [Flags / Opções úteis](#flags--opções-úteis)  
- [Exemplos práticos](#exemplos-práticos)  
- [Boas práticas / Dicas](#boas-práticas--dicas)  
- [Observação legal](#observação-legal)  
- [Licença](#licença)

---

## O que é
**Gobuster** é uma ferramenta de enumeração que realiza força bruta usando *wordlists* para descobrir:
- diretórios e arquivos em aplicações web,
- subdomínios DNS,
- buckets do S3/GCS,
- e outras superfícies expostas.

A enumeração ajuda a encontrar caminhos ocultos (ex.: `/admin`, `/backup.zip`) e recursos sensíveis.

---

## Pré-requisitos
- Sistema Linux / macOS / Windows com ambiente compatível
- `Go` ou binário do Gobuster (dependendo da forma de instalação)
- Wordlists (ex.: `SecLists`, `dirb`, listas personalizadas)
- Permissão explícita para testar o alvo (obrigatório)

---

## Instalação (exemplo via apt/homebrew)
> Ajuste conforme sua distro / método preferido.

```bash
# Exemplo Debian/Ubuntu (pode variar)
sudo apt update
sudo apt install gobuster

# Exemplo usando Go (instalar Go primeiro)
go install github.com/OJ/gobuster/v3@latest
# binário em $GOPATH/bin ou $HOME/go/bin
