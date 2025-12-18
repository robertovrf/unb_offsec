# NMAP

Em pentesting (ou CTFs), o primeiro passo é descobrir o que existe na rede, quais máquinas estão ativas, que portas estão abertas e que serviços (web, ssh, ftp, etc.) estão sendo executados. Essa fase chama-se reconhecimento/enumeração e é feita com ferramentas como o nmap. 

O Nmap é uma ferramenta poderosa de varredura de redes e hosts. Ele pode identificar máquinas ativas, portas abertas, serviços rodando e até sistemas operacionais.

`sudo nmap 10.129.2.0/24 -sn -oA tnet | grep for | cut -d" " -f5`

- **sudo**: executa com privilégios de administrador (necessário para varreduras que mexem em pacotes de rede).  
- **nmap**: ferramenta usada.  
- **10.129.2.0/24**: especifica a rede inteira (endereços de 10.129.2.0 até 10.129.2.255).  
- **-sn → "ping scan"**: apenas descobre quais hosts estão ativos, sem checar portas.  
- **-oA tnet**: salva os resultados em 3 formatos (tnet.nmap, tnet.gnmap, tnet.xml).  
- **|**: envia a saída para outro comando.  
- **grep for**: filtra linhas contendo "for", que indicam hosts ativos.  
- **cut -d" " -f5**: pega o quinto campo da linha (normalmente o IP).

**Resultado:** lista dos IPs ativos na rede.

## Tipos de Escaneamento no Nmap

- **Descobrir hosts ativos (ping scan):**  
  `nmap -sn IP` → Mostra apenas quais máquinas estão ligadas na rede.

- **Escanear portas padrão do alvo:**  
  `nmap IP` → Escaneia as portas mais comuns (top 1000).

- **Escanear portas específicas:**  
  `nmap -p 22,80,443 IP` → Verifica apenas as portas escolhidas (SSH, HTTP, HTTPS).

- **Escanear todas as portas (1–65535):**  
  `nmap -p- IP` → Escaneia todas as portas possíveis (mais demorado).

- **Detecção de versão dos serviços:**  
  `nmap -sV IP` → Identifica versões de serviços (ex: Apache, OpenSSH).

- **Executar um conjunto de scripts básicos:**  
  `nmap -sC IP` → equivalente a `--script=default` que ajuda a coletar banner e info úteis. 

- **Detecção de sistema operacional:**  
  `sudo nmap -O IP` → Tenta descobrir qual SO (Linux, Windows, etc).

- **Escaneamento agressivo (completo):**  
  `sudo nmap -A IP` → Combina detecção de SO, versão, traceroute e scripts comuns.

- **Escaneamento rápido (menos portas):**  
  `nmap -F IP` → Escaneia apenas as portas mais usadas (mais rápido).

- **Escanear múltiplos alvos:**  
  `nmap 192.168.1.10 192.168.1.20 192.168.1.30` ou `nmap 192.168.1.0/24` → Permite escanear vários IPs ou redes inteiras.

- **Escanear usando arquivo de IPs:**  
  `nmap -iL lista.txt` → Lê os alvos a partir de um arquivo.

- **Escanear portas UDP:**  
  `sudo nmap -sU IP` → Escaneia serviços que usam UDP (DNS, SNMP, DHCP).

- **Escaneamento TCP SYN (rápido e furtivo):**  
  `sudo nmap -sS IP` → Usa "half-open scan", mais rápido e menos detectável.

- **Escaneamento TCP Connect (completo):**  
  `nmap -sT IP` → Estabelece conexão completa TCP (mais visível).

- **Escanear múltiplas portas em faixa:**  
  `nmap -p 1-1000 IP` → Escaneia da porta 1 até a 1000.

- **Escaneamento com scripts NSE (Nmap Scripting Engine):**  
  `nmap --script=vuln IP` → Executa scripts prontos para buscar vulnerabilidades.

- **Detecção de versão em portas específicas:**  
  `nmap -sV -p 21,80,2222 10.201.41.227` → Escaneia apenas as portas 21, 80 e 2222 e tenta identificar o serviço e sua versão (banner/version detection), útil para saber que software está rodando e procurar vulnerabilidades ou ferramentas específicas para cada serviço.

- **Host seems down:**  
  `nmap -Pn IP` → Força o scan mesmo se o Nmap concluir que o host está “down”. 

## Exportar resultados

- `nmap -oN resultado.txt IP` → salva em formato normal.  
- `nmap -oG resultado.gnmap IP` → salva em formato para grep.  
- `nmap -oX resultado.xml IP` → salva em formato XML.  
- `nmap -oA tnet IP` → salva em todos os formatos de uma vez (gera `tnet.nmap`, `tnet.gnmap`, `tnet.xml`).

