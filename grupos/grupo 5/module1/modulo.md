# CTF Challenge — Nossas Anotações

> Template de notas para desafios de CTF / laboratório de pentest.  
> Cole no `README.md` ou em um `NOTES.md` dentro do diretório do desafio.

---

## Objetivo
Registrar o fluxo de exploração passo a passo, comandos usados, descobertas e possíveis vias de escalonamento/privilege escalation. Use este documento como checklist para organizar sua investigação e facilitar a reprodução.

---

## Processo de Exploração

### 1. Coleta de informação inicial
- Verificar conectividade:
  ```bash
  ping -c 4 <IP>
