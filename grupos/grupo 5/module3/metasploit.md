# Metasploit

O **Metasploit** é uma plataforma (conjunto de ferramentas) utilizada para testes de penetração e avaliação de segurança. Reúne módulos prontos para varredura, exploração, geração de payloads e ações de pós-exploração, proporcionando um fluxo organizado para realizar testes **autorizados** em sistemas.

---

## Versões principais

- **Metasploit Pro**  
  Versão comercial com interface gráfica (GUI) e recursos focados em automação e gerenciamento.

- **Metasploit Framework**  
  Versão de código aberto (CLI), amplamente utilizada por pentesters e estudantes para pesquisa e testes técnicos.

---

## Metasploit Framework

O Framework é composto por um conjunto de módulos que permite:

- Coleta de informações  
- Varredura e identificação de serviços  
- Desenvolvimento e uso de exploits  
- Geração e customização de payloads  
- Ações de pós-exploração  

---

## Componentes principais

- **msfconsole**  
  Interface principal em linha de comando para carregar módulos, configurar e executar ações.

- **Módulos**  
  Estruturas reutilizáveis que incluem:
  - `exploits`
  - `auxiliary` (scanners, fuzzers)
  - `post` (pós-exploração)
  - `payloads`

- **Ferramentas**
  - **msfvenom**: gera e customiza payloads  
  - **Hashes and Password Cracking**  
    Artigo:  
    <https://rapid7.github.io/using-metasploit/intermediate>  
    Discute bibliotecas e funcionalidades do Metasploit para lidar com hashes e quebra de senhas.
  - **pattern_create / pattern_offset**: ajudam a identificar offsets em testes de memória.

---

## Conceitos fundamentais

- **Vulnerabilidade**  
  Falha no design, implementação ou lógica de um software que pode ser explorada.

- **Exploit**  
  Código ou técnica que tira vantagem de uma vulnerabilidade para executar uma ação não intencional.

- **Payload**  
  Código executado no sistema alvo após a exploração ter sucesso (ex.: abrir uma sessão, executar comandos, transferir arquivos).

---

## Tipos de módulos e funções

- **Exploit**  
  Explora vulnerabilidades específicas em serviços ou aplicações.

- **Auxiliary**  
  Módulos de suporte (scanners, crawlers, sniffers, fuzzers); focados em coleta de informação.

- **Post**  
  Atividades após obter acesso (coleta de dados, elevação de privilégios, limpeza de rastros em ambientes autorizados).

- **Payloads**  
  Códigos executados no sistema alvo.

---

## Termos importantes

- **Encoders**  
  Transformam payloads para alterar sua assinatura e tentar evitar detecção baseada em padrões.

- **Evasion**  
  Técnicas ou módulos para contornar mecanismos de defesa (avançado e sensível).

- **NOP (No Operation)**  
  Instruções usadas para alinhar áreas de memória e facilitar o funcionamento de exploits.

---

## Estrutura de payloads

- **adapters**  
  Encapsulam payloads em diferentes formatos (ex.: comando PowerShell único).

- **singles**  
  Payloads autossuficientes que executam uma ação direta.

- **stagers**  
  Payloads pequenos que abrem o canal de comunicação inicial.

- **stages**  
  Componentes maiores enviados após o stager, permitindo funcionalidades mais completas.

**Funcionamento geral:**  
Um *stager* pequeno é enviado ao alvo, cria a conexão e então o *stage* maior é transmitido.

---

## Fluxo de uso (passo a passo)

1. **Reconhecimento**: identificar alvos, serviços, portas e versões.  
2. **Seleção do exploit**: escolher módulo compatível.  
3. **Configuração**: definir payload, IPs, portas e opções.  
4. **Execução**: tentar explorar a vulnerabilidade.  
5. **Sessão e pós-exploração**: uso de shell ou Meterpreter conforme o escopo do teste.

---

## Exemplos de payloads (conceito)

- **Reverse shell**: o alvo conecta de volta ao atacante.  
- **Bind shell**: o alvo escuta uma porta e o atacante conecta.  
- **Meterpreter**: payload avançado e modular do Metasploit.

---

## Observações técnicas

- Exploits e payloads são organizados por alvo e versão.  
- Encoders e stagers/stages equilibram tamanho inicial e funcionalidade.  
- Módulos `auxiliary` e `post` reforçam reconhecimento e pós-exploração.

---

## Acessar o console

```bash
msfconsole

