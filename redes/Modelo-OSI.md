# Modelo OSI — Guia Completo por Camada

<div align="center">

<small>Referência de estudos — Redes de Computadores</small>

</div>

---

## Sumário

- [Visão Geral](#visão-geral)
- [Camada 7 — Aplicação](#camada-7--aplicação)
- [Camada 6 — Apresentação](#camada-6--apresentação)
- [Camada 5 — Sessão](#camada-5--sessão)
- [Camada 4 — Transporte](#camada-4--transporte)
- [Camada 3 — Rede](#camada-3--rede)
- [Camada 2 — Enlace de Dados](#camada-2--enlace-de-dados)
- [Camada 1 — Física](#camada-1--física)
- [Resumo das Camadas](#resumo-das-camadas)
- [Encapsulamento e Desencapsulamento](#encapsulamento-e-desencapsulamento)
- [Mapeamento de Tecnologias Reais](#mapeamento-de-tecnologias-reais)

---

<div align="center">

## Visão Geral

</div>

O Modelo OSI (*Open Systems Interconnection*) é um framework conceitual que divide a comunicação em rede em **7 camadas**, cada uma com uma responsabilidade específica. Foi criado pela ISO para padronizar como sistemas de diferentes fabricantes se comunicam entre si.

Os dados percorrem as camadas **de cima para baixo** no lado do emissor (encapsulamento) e **de baixo para cima** no lado do receptor (desencapsulamento). Cada camada adiciona seu próprio cabeçalho ao dado enquanto ele passa.

---

<div align="center">

## Camada 7 — Aplicação

<small>PDU: Dados · Dispositivos: Navegador, cliente de e-mail, qualquer aplicação</small>

</div>

### O que faz

É a camada mais próxima do usuário final. Fornece serviços de rede diretamente às aplicações — não à rede em si. Os protocolos aqui definem como o software se comunica pela rede.

### Protocolos e padrões

`HTTP` `HTTPS` `FTP` `DNS` `SMTP` `POP3` `IMAP` `SSH` `Telnet`

### Pontos-chave

- Ponto de entrada para toda comunicação de rede voltada ao usuário
- A resolução de DNS ocorre aqui
- Cada requisição web começa nesta camada
- Lida com a codificação de dados e gerenciamento de sessão para aplicações

---

<div align="center">

## Camada 6 — Apresentação

<small>PDU: Dados · Dispositivos: Terminação SSL/TLS, codec</small>

</div>

### O que faz

Responsável por traduzir dados entre a camada de Aplicação e a rede. Gerencia criptografia, descriptografia, compressão e codificação de caracteres para que os dois lados da comunicação "falem o mesmo idioma".

### Protocolos e padrões

`SSL/TLS` `JPEG` `MPEG` `ASCII` `Unicode` `MIME`

### Pontos-chave

- Criptografa dados antes da transmissão (TLS)
- Descriptografa dados recebidos antes de passar para a aplicação
- Gerencia codificação de caracteres (UTF-8, ASCII)
- Comprime dados para reduzir o tamanho na transmissão

---

<div align="center">

## Camada 5 — Sessão

<small>PDU: Dados · Dispositivos: API gateways, proxies</small>

</div>

### O que faz

Gerencia e controla as conexões (sessões) entre dois dispositivos. Estabelece, mantém e encerra sessões de comunicação, além de lidar com sincronização e checkpointing para transferências longas.

### Protocolos e padrões

`NetBIOS` `RPC` `PPTP` `SAP` `NFS`

### Pontos-chave

- Abre e fecha sessões de comunicação
- Adiciona checkpoints em transferências longas (permite retomada em caso de falha)
- Controla comunicação full-duplex ou half-duplex
- Gerencia handshakes de autenticação

---

<div align="center">

## Camada 4 — Transporte

<small>PDU: Segmento · Dispositivos: Firewalls, load balancers</small>

</div>

### O que faz

Fornece comunicação fim a fim entre aplicações em hosts diferentes. Segmenta os dados, garante entrega confiável (TCP) ou entrega rápida (UDP), e gerencia controle de fluxo e verificação de erros.

### Protocolos e padrões

`TCP` `UDP` `SCTP` `QUIC`

### Pontos-chave

- **TCP:** entrega confiável, ordenada e com verificação de erros
- **UDP:** rápido, sem conexão, sem garantia de entrega
- Números de porta vivem aqui (80, 443, 22, 21...)
- Controle de fluxo evita sobrecarregar o receptor
- O three-way handshake (SYN, SYN-ACK, ACK) é um conceito da Camada 4

---

<div align="center">

## Camada 3 — Rede

<small>PDU: Pacote · Dispositivos: Roteadores, switches Layer 3</small>

</div>

### O que faz

Responsável pelo endereçamento lógico e pelo roteamento de pacotes entre redes diferentes. É aqui que vivem os endereços IP e onde os roteadores decidem o melhor caminho para os dados percorrerem.

### Protocolos e padrões

`IPv4` `IPv6` `OSPF` `BGP` `ICMP` `ARP` `IGMP`

### Pontos-chave

- Endereços IP são endereços da Camada 3
- Roteadores operam nesta camada
- OSPF e BGP são protocolos de roteamento da Camada 3
- O comando `ping` usa ICMP — opera aqui
- Fragmentação de pacotes grandes ocorre nesta camada

---

<div align="center">

## Camada 2 — Enlace de Dados

<small>PDU: Quadro (Frame) · Dispositivos: Switches, bridges, NICs</small>

</div>

### O que faz

Gerencia a comunicação nó a nó dentro de uma mesma rede. Empacota os bits brutos em frames, gerencia endereços MAC e detecta (e às vezes corrige) erros de transmissão.

### Protocolos e padrões

`Ethernet` `Wi-Fi (802.11)` `PPP` `HDLC` `VLANs (802.1Q)` `STP`

### Pontos-chave

- Endereços MAC vivem nesta camada
- Switches operam aqui
- VLANs (802.1Q) são um conceito da Camada 2
- Detecção de erros via CRC
- Dividida em duas subcamadas: LLC e MAC

---

<div align="center">

## Camada 1 — Física

<small>PDU: Bit · Dispositivos: Hubs, cabos, NICs, Access Points</small>

</div>

### O que faz

A camada mais baixa — responsável por transmitir bits brutos (0s e 1s) por um meio físico. Define os sinais elétricos, ópticos ou de rádio utilizados, além dos conectores e cabos físicos.

### Protocolos e padrões

`IEEE 802.3 (Ethernet)` `IEEE 802.11 (Wi-Fi)` `USB` `Bluetooth` `DSL` `SONET`

### Pontos-chave

- Sem endereçamento — apenas bits
- Define níveis de tensão, especificações de cabo, layout de pinos
- Cabo Cat6, fibra óptica e ondas de rádio vivem aqui
- Hubs operam nesta camada (apenas repetem o sinal)
- A NIC traduz entre dados digitais e sinais físicos

---

<div align="center">

## Resumo das Camadas

</div>

| Camada | Nome | PDU | Dispositivos | Protocolos principais |
|--------|------|-----|-------------|----------------------|
| 7 | Aplicação | Dados | Aplicações | HTTP, FTP, DNS, SSH |
| 6 | Apresentação | Dados | SSL/TLS | TLS, JPEG, ASCII |
| 5 | Sessão | Dados | Proxies | NetBIOS, RPC, NFS |
| 4 | Transporte | Segmento | Firewalls | TCP, UDP, QUIC |
| 3 | Rede | Pacote | Roteadores | IP, OSPF, BGP, ICMP |
| 2 | Enlace | Frame | Switches | Ethernet, VLANs, STP |
| 1 | Física | Bit | Hubs, cabos | IEEE 802.3, 802.11 |

---

<div align="center">

## Encapsulamento e Desencapsulamento

</div>

Quando você envia dados pela rede, cada camada adiciona seu próprio cabeçalho ao dado original — esse processo é chamado de **encapsulamento**. No receptor, o processo inverso ocorre — **desencapsulamento**.

```
EMISSOR                              RECEPTOR

[Aplicação]   → Dados            →  [Aplicação]
[Apresentação]→ Dados            →  [Apresentação]
[Sessão]      → Dados            →  [Sessão]
[Transporte]  → Segmento         →  [Transporte]
[Rede]        → Pacote           →  [Rede]
[Enlace]      → Frame            →  [Enlace]
[Física]      → Bits (0s e 1s)   →  [Física]
                    ↓↑
              meio físico
              (cabo, fibra, rádio)
```

Cada camada só se comunica com a camada equivalente do outro lado — a Camada 3 do emissor "fala" com a Camada 3 do receptor, mesmo que os dados passem por todas as camadas abaixo para chegar lá.

---

<div align="center">

## Mapeamento de Tecnologias Reais

</div>

Uma forma prática de fixar o modelo é mapear tecnologias reais às camadas correspondentes:

| Tecnologia / Conceito | Camada OSI |
|---|---|
| Cabo Cat6, fibra óptica, Access Point, hub | Camada 1 — Física |
| Switch, VLANs 802.1Q, STP, endereço MAC | Camada 2 — Enlace |
| Roteador, OSPFv2, BGP, ICMP (ping), endereço IP | Camada 3 — Rede |
| TCP, UDP, portas (80, 443, 22, 21), ACL por porta | Camada 4 — Transporte |
| NetBIOS, RPC, NFS | Camada 5 — Sessão |
| TLS/SSL, HTTPS, compressão | Camada 6 — Apresentação |
| HTTP, FTP, SSH, DNS, SMTP | Camada 7 — Aplicação |

---

<p align="center">
<small>Referência de estudos — Redes de Computadores</small>
</p>