# Troubleshooting de Redes com o Modelo OSI

<div align="center">

<small>Guia de referência — Linux & Windows</small>

</div>

---

## Sumário

- [A Lógica do Troubleshooting com OSI](#a-lógica-do-troubleshooting-com-osi)
- [Fluxo de Diagnóstico Rápido](#fluxo-de-diagnóstico-rápido)
- [Camada 1 — Física](#camada-1--física)
- [Camada 2 — Enlace de Dados](#camada-2--enlace-de-dados)
- [Camada 3 — Rede](#camada-3--rede)
- [Camada 4 — Transporte](#camada-4--transporte)
- [Camada 5 — Sessão](#camada-5--sessão)
- [Camada 6 — Apresentação](#camada-6--apresentação)
- [Camada 7 — Aplicação](#camada-7--aplicação)
- [Referência de Comandos](#referência-de-comandos)

---

<div align="center">

## A lógica do *troubleshooting* pelo modelo OSI

</div>

O Modelo OSI é o framework mais eficaz para diagnosticar problemas de rede de forma sistemática. A ideia central é **isolar o problema em uma camada específica** em vez de tentar resolver tudo ao mesmo tempo.

Existem três abordagens:

**Bottom-up** — começa na Camada 1 e sobe. É a mais comum porque problemas físicos são os mais frequentes e os mais rápidos de descartar.

**Top-down** — começa na Camada 7 e desce. Útil quando o problema é claramente de aplicação — por exemplo, apenas um software específico não funciona mas a rede está OK.

**"Divide and conquer"** — começa no meio (normalmente pela camada 3) e vai para cima ou para baixo conforme o resultado. Útil quando você já tem uma pista sobre onde o problema está.

---

<div align="center">

## Fluxo de Diagnóstico Rápido

</div>

Quando alguém reporta *"não consigo acessar"*, use este fluxo mental antes de abrir qualquer ferramenta:

```
O cabo está conectado? LED aceso?              → Camada 1
O switch enxerga o MAC do dispositivo?         → Camada 2
O IP está correto? Consegue pingar o gateway?  → Camada 3
A porta TCP está aberta? Firewall bloqueando?  → Camada 4
A sessão está sendo estabelecida?              → Camada 5
Certificado válido? Encoding correto?          → Camada 6
O serviço está rodando? DNS resolve?           → Camada 7
```

**O ping como primeira triagem:**

| Resultado do ping | Camada suspeita |
|---|---|
| Ping falha para o próprio gateway | Camada 1, 2 ou 3 |
| Funciona para o gateway, falha para hosts remotos | Camada 3 |
| Funciona para o destino, mas a aplicação não conecta | Camada 4 em diante |
| Funciona por IP, falha por nome | Camada 7 (resolução de DNS) |

---

<div align="center">

## Camada 1 — Física

</div>

### Sintomas típicos:

- Sem conectividade alguma;
- Interface com *status down*;
- Perda de pacotes massiva ou intermitente;
- LED de link apagado no switch ou na NIC.

### Verificações

**Linux:**
```bash
ip link show eth0
ethtool eth0
# Observar: "Link detected: yes/no", velocidade e duplex
dmesg | grep eth0
# Erros de driver ou detecção de hardware
```

**Windows:**
```powershell
Get-NetAdapter
Get-NetAdapterStatistics -Name "Ethernet"
# Observar: ReceivedDiscardedPackets, ReceivedErrors
```

### Casos reais

**Cabo com defeito interno**

O cabo parece íntegro por fora mas tem um par de fios quebrado internamente. Sintoma: link sobe e cai de forma intermitente, muitos erros de CRC. Solução: trocar o cabo e testar com certificador de cabos.

**Duplex mismatch**

Uma extremidade negociou full-duplex e a outra half-duplex. Sintoma: a interface fica ativa mas com muitas colisões e retransmissões. Solução: forçar velocidade e duplex manualmente nos dois lados da conexão.

**Adaptador de rede com defeito**

A NIC está com problema de hardware. Sintoma: link nunca sobe mesmo trocando o cabo. Verificar se o driver está carregado corretamente e testar com outra NIC.

```bash
# Linux — verificar se o driver está carregado
lspci | grep -i ethernet
lsmod | grep -i e1000
```

---

<div align="center">

## Camada 2 — Enlace de Dados

</div>

### Sintomas típicos

- Interface ativa mas sem comunicação;
- Dispositivos na mesma VLAN não se enxergam;
- Broadcast storm — rede lenta ou inacessível de forma súbita;
- Endereço MAC não aprendido pelo switch.

### Verificações

**Linux:**
```bash
ip neigh show
# Tabela ARP — verifica se o MAC do gateway foi aprendido
arp -n
bridge fdb show
# Em sistemas com bridge (como servidores com VMs)
```

**Windows:**
```powershell
arp -a
Get-NetNeighbor
# Tabela ARP do Windows
```

### Casos reais

**VLAN errada na porta**

Um dispositivo não consegue se comunicar com outros na mesma rede lógica. Causa comum: a porta do switch está associada a uma VLAN incorreta. Verificar a configuração da porta e corrigir a VLAN de acesso.

**Loop de rede sem STP**

A rede fica completamente lenta ou inacessível de forma repentina. CPUs dos switches disparam. Causa: um cabo conectado em duas portas do mesmo switch criando um loop, com Spanning Tree Protocol desabilitado ou mal configurado. Desconectar cabos um a um até identificar o loop.

**Endereço MAC duplicado**

Dois dispositivos com o mesmo endereço MAC na mesma rede causam conflito. O switch não consegue manter a tabela de MACs consistente e os pacotes chegam ao destino errado ou são descartados.

```bash
# Linux — verificar e alterar MAC temporariamente
ip link show eth0
ip link set eth0 address AA:BB:CC:DD:EE:FF
```

**ARP não resolvendo**

O dispositivo sabe o IP do destino mas não consegue descobrir o MAC correspondente. Sintoma: ping falha com *`Destination Host Unreachable`*. Limpe o cache ARP e testar novamente.

```bash
# Linux
ip neigh flush all

# Windows
arp -d *
netsh interface ip delete arpcache
```

---

<div align="center">

## Camada 3 — Rede

</div>

### Sintomas típicos

- Comunicação funciona na mesma rede mas falha entre redes diferentes;
- *`Destination net unreachable`* ou *`No route to host`*;
- *`traceroute`* mostra onde os pacotes param;
- Rota ausente na tabela de roteamento.

### Verificações

**Linux:**
```bash
ip route show
# Tabela de roteamento completa

ping -c 4 8.8.8.8
# Testar conectividade básica

traceroute 10.0.2.1
# Identificar em qual hop o pacote para

ip route get 10.0.5.1
# Verificar qual rota seria usada para um destino específico
```

**Windows:**
```powershell
route print
tracert 10.0.2.1
Test-Connection -ComputerName 10.0.2.1 -Count 4

# Verificar rota específica
Find-NetRoute -RemoteIPAddress 10.0.5.1
```

### Casos reais

**Gateway padrão ausente ou incorreto**

O dispositivo consegue pingar hosts na mesma sub-rede mas não alcança outras redes. Causa clássica: gateway padrão não configurado ou com IP errado.

```bash
# Linux — verificar e adicionar gateway
ip route show default
ip route add default via 192.168.1.1

# Windows
ipconfig /all
route add 0.0.0.0 mask 0.0.0.0 192.168.1.1
```

**Rota ausente para uma rede específica**


O roteador não sabe como chegar a uma rede de destino. O `traceroute` vai mostrar onde os pacotes param. Adicionar a rota manualmente ou verificar o protocolo de roteamento dinâmico.

```bash
# Linux
ip route add 10.0.5.0/25 via 10.0.1.1

# Windows
route add 10.0.5.0 mask 255.255.255.128 10.0.1.1
```

**IP duplicado na rede**


Dois dispositivos com o mesmo endereço IP causam comportamento errático — a comunicação funciona às vezes e falha em outras. O sistema operacional geralmente alerta sobre conflito de IP.

```bash
# Linux — verificar conflito com arping
arping -I eth0 192.168.1.100
# Se receber resposta de dois MACs diferentes, há conflito
```

**MTU inadequado**


Pacotes grandes são descartados no caminho mas pacotes pequenos (como ping padrão) chegam normalmente. Sintoma: ping funciona, mas transferências de arquivos ou páginas web grandes falham.

```bash
# Linux — testar com diferentes tamanhos de pacote
ping -M do -s 1472 192.168.1.1
# -M do = não fragmentar, -s = tamanho do payload

# Windows
ping -f -l 1472 192.168.1.1
```

---

<div align="center">

## Camada 4 — Transporte

</div>

### Sintomas típicos

- Ping funciona mas a aplicação não conecta;
- *`Connection refused`* em uma porta específica;
- *`Connection timed out`* — pacotes descartados silenciosamente;
- Apenas um serviço específico inacessível.

### Verificações

**Linux:**
```bash
ss -tlnp
# Portas TCP abertas e quais processos estão escutando

nc -zv 10.0.1.10 80
# Testar conectividade em uma porta específica

curl -v telnet://10.0.1.10:443
# Testar handshake TCP manualmente
```

**Windows:**
```powershell
netstat -ano
Get-NetTCPConnection -State Listen

Test-NetConnection -ComputerName 10.0.1.10 -Port 80
# Retorna TcpTestSucceeded: True/False
```

### Casos reais

**Firewall bloqueando a porta**

*`Connection timed out`* — o pacote chega ao destino mas é descartado silenciosamente pelo firewall. Diferente de *`Connection refused`*, que significa que o host recebeu e recusou.

```bash
# Linux — verificar regras do firewall
iptables -L -n -v
ufw status verbose

# Liberar porta temporariamente para teste
iptables -I INPUT -p tcp --dport 8080 -j ACCEPT
```

```powershell
# Windows — verificar regras do firewall
Get-NetFirewallRule | Where-Object {$_.Enabled -eq 'True'} | Select-Object DisplayName, Direction, Action
netsh advfirewall firewall show rule name=all
```

**Serviço não está escutando na porta**


*`Connection refused`* indica que o host chegou mas não há nada escutando naquela porta. O serviço pode estar parado, travado ou configurado em uma porta diferente da esperada.

```bash
# Linux
systemctl status nginx
ss -tlnp | grep :80
journalctl -u nginx --since "5 minutes ago"
```

```powershell
# Windows
Get-Service -Name "W3SVC"
netstat -ano | findstr :80
Get-EventLog -LogName Application -Source "IIS*" -Newest 10
```

**ACL ou regra de firewall bloqueando porta errada**

Uma regra de controle de acesso está bloqueando a porta da aplicação. Para diagnosticar, verificar os contadores das regras — a regra responsável pelo bloqueio vai mostrar hits crescendo.

```bash
# Linux — monitorar pacotes descartados em tempo real
iptables -L -n -v --line-numbers
watch -n 1 'iptables -L -n -v'
```

---

<div align="center">

## Camada 5 — Sessão

</div>

### Sintomas típicos

- Sessões SSH, RDP ou VPN caem inesperadamente;
- Problemas de autenticação intermitentes;
- Transferências longas falham no meio sem erro claro;
- Reconexões frequentes e automáticas.

### Verificações

**Linux:**
```bash
ss -tnp
# Verificar estado das sessões TCP estabelecidas

who
# Sessões ativas no sistema

last
# Histórico de sessões

journalctl -u sshd --since "1 hour ago"
# Logs do serviço SSH
```

**Windows:**
```powershell
query session
# Sessões RDP ativas

Get-EventLog -LogName Security -InstanceId 4624,4625,4634 -Newest 20
# Eventos de logon, falha de logon e logoff
```

### Casos reais

**Timeout de sessão SSH/RDP**


A sessão cai após um período de inatividade. Causa: configuração de timeout muito agressiva no servidor ou em um dispositivo intermediário (firewall, NAT) que encerra conexões ociosas.

```bash
# Linux — ajustar keepalive no servidor SSH
# /etc/ssh/sshd_config
ClientAliveInterval 60
ClientAliveCountMax 3
systemctl restart sshd

# No cliente SSH
# ~/.ssh/config
Host *
    ServerAliveInterval 60
    ServerAliveCountMax 3
```

**Sessões presas em CLOSE_WAIT**


Muitas conexões no estado `CLOSE_WAIT` indicam que a aplicação não está encerrando as sessões corretamente. Isso pode esgotar as conexões disponíveis e causar falhas para novos usuários.

```bash
# Linux — verificar conexões por estado
ss -tn state close-wait
netstat -an | grep CLOSE_WAIT | wc -l
```

**Falha de autenticação intermitente**


A autenticação funciona às vezes e falha em outras sem razão aparente. Causas possíveis: clock desincronizado entre cliente e servidor (crítico para Kerberos), sessão de autenticação expirando antes do processo terminar.

```bash
# Linux — verificar sincronização de tempo
timedatectl status
chronyc tracking
```

---

<div align="center">

## Camada 6 — Apresentação

</div>

### Sintomas típicos

- Erro de certificado SSL/TLS no navegador;
- Caracteres especiais aparecendo corrompidos;
- Falha na negociação de criptografia;
- *`SSL handshake failed`* nos logs.

### Verificações

**Linux:**
```bash
# Verificar certificado de um servidor
openssl s_client -connect site.com.br:443 2>/dev/null | openssl x509 -noout -dates -subject

# Verificar versões TLS suportadas
nmap --script ssl-enum-ciphers -p 443 site.com.br

# Testar handshake TLS manualmente
curl -vI https://site.com.br 2>&1 | grep -E "SSL|TLS|certificate"
```

**Windows:**
```powershell
# Verificar certificados instalados
Get-ChildItem Cert:\LocalMachine\My

# Testar conexão TLS
[Net.ServicePointManager]::SecurityProtocol
Invoke-WebRequest -Uri https://site.com.br -UseBasicParsing
```

### Casos reais

**Certificado expirado**

O navegador ou cliente recusa a conexão HTTPS com erro de certificado inválido. Verificar a data de validade e renovar.

```bash
# Linux — verificar validade
echo | openssl s_client -connect site.com.br:443 2>/dev/null | openssl x509 -noout -enddate

# Verificar certificado local
openssl x509 -in /etc/ssl/certs/meu-cert.pem -noout -dates
```

**Incompatibilidade de versão TLS**

Um servidor antigo aceita apenas TLS 1.0 ou 1.1, mas clientes modernos exigem TLS 1.2 ou 1.3. Sintoma: handshake falha com `ssl_error_no_cypher_overlap` ou similar.

```bash
# Testar versão específica
openssl s_client -connect site.com.br:443 -tls1_2
openssl s_client -connect site.com.br:443 -tls1_3
```

**Encoding incorreto**

Caracteres especiais (acentuação, símbolos) aparecem corrompidos na aplicação. Causa: cliente e servidor usando codificações diferentes (Latin-1 vs UTF-8).

```bash
# Linux — verificar encoding de um arquivo
file -i arquivo.txt
iconv -f latin1 -t utf8 arquivo.txt -o arquivo-utf8.txt

# Verificar header HTTP
curl -I https://site.com.br | grep -i content-type
```

---

<div align="center">

## Camada 7 — Aplicação

</div>

### Sintomas típicos

- Erros HTTP (404, 500, 502, 503);
- DNS não resolve nomes;
- Ping funciona por IP mas não por nome;
- Aplicação retorna erro mesmo com rede funcionando;
- Logs de aplicação com erros de conexão ao banco de dados.

### Verificações

**Linux:**
```bash
# DNS
nslookup google.com
dig google.com @8.8.8.8
host google.com

# HTTP
curl -v https://site.com.br
curl -I https://site.com.br        # apenas headers
wget --server-response https://site.com.br

# Logs de aplicação
journalctl -u nginx --since "10 minutes ago"
tail -f /var/log/nginx/error.log
tail -f /var/log/apache2/error.log
```

**Windows:**
```powershell
# DNS
Resolve-DnsName google.com
nslookup google.com 8.8.8.8

# HTTP
Invoke-WebRequest -Uri https://site.com.br -UseBasicParsing
curl.exe -v https://site.com.br

# Logs de aplicação
Get-EventLog -LogName Application -EntryType Error -Newest 20
```

### Casos reais

**DNS não resolve**

Ping por IP funciona mas por nome falha. Estratégia: testar com um servidor DNS público para isolar se o problema está no servidor DNS interno ou na configuração do cliente.

```bash
# Linux
nslookup servidor.empresa.com.br
# Se falhar, testar com DNS público:
nslookup servidor.empresa.com.br 8.8.8.8
# Se resolver com 8.8.8.8 mas não com o DNS interno:
# → problema no servidor DNS interno

# Verificar qual DNS está configurado
cat /etc/resolv.conf
resolvectl status
```

```powershell
# Windows
ipconfig /displaydns
ipconfig /flushdns
Get-DnsClientServerAddress
```

**Erro 502 Bad Gateway**

O servidor web (Nginx, Apache) está rodando mas a aplicação por trás dele não responde. O problema não é de rede — é na aplicação ou no serviço de backend. Verificar logs da aplicação.

```bash
# Linux — verificar se o serviço backend está rodando
systemctl status php-fpm
systemctl status gunicorn
ss -tlnp | grep :8000

# Logs do Nginx
tail -f /var/log/nginx/error.log
```

**Erro 503 Service Unavailable**

Serviço sobrecarregado ou parado. Verificar recursos do servidor — CPU, RAM e especialmente disco cheio (causa comum e fácil de ignorar).

```bash
# Linux — verificar recursos
top
free -h
df -h
iostat -x 1

# Windows
Get-Process | Sort-Object CPU -Descending | Select-Object -First 10
Get-PSDrive C
```

**Cache DNS desatualizado**

Um serviço mudou de IP mas os clientes ainda resolvem para o IP antigo por causa do cache DNS. Limpar o cache local e testar novamente.

```bash
# Linux
resolvectl flush-caches
systemctl restart systemd-resolved

# Windows
ipconfig /flushdns
Clear-DnsClientCache
```

---

<div align="center">

## Referência de Comandos

</div>

### Linux

| Objetivo | Comando |
|---|---|
| Status da interface | `ip link show` |
| Endereços IP | `ip addr show` |
| Tabela de roteamento | `ip route show` |
| Tabela ARP | `ip neigh show` |
| Portas abertas | `ss -tlnp` |
| Testar conectividade | `ping`, `traceroute`, `mtr` |
| Testar porta específica | `nc -zv host porta` |
| Informações da NIC | `ethtool eth0` |
| Captura de pacotes | `tcpdump -i eth0 -n` |
| DNS | `dig`, `nslookup`, `host` |
| HTTP | `curl -v`, `wget` |
| Certificado SSL | `openssl s_client -connect host:443` |
| Regras de firewall | `iptables -L -n -v`, `ufw status` |
| Logs do sistema | `journalctl -u serviço` |

### Windows

| Objetivo | Comando |
|---|---|
| Status das interfaces | `Get-NetAdapter` |
| Endereços IP | `ipconfig /all` |
| Tabela de roteamento | `route print` |
| Tabela ARP | `arp -a` |
| Portas abertas | `netstat -ano` |
| Testar conectividade | `ping`, `tracert` |
| Testar porta específica | `Test-NetConnection -Port` |
| DNS | `nslookup`, `Resolve-DnsName` |
| Limpar cache DNS | `ipconfig /flushdns` |
| Regras de firewall | `Get-NetFirewallRule` |
| HTTP | `Invoke-WebRequest`, `curl.exe` |
| Logs do sistema | `Get-EventLog`, `eventvwr` |

---

<p align="center">
<small>Guia de referência — Troubleshooting de Redes com o Modelo OSI — Linux & Windows</small>
</p>