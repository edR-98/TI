# 🔌 Interfaces e Cabos de Rede

> Documentação sobre os meios físicos de transmissão de dados em redes de computadores: cabos, conectores, padrões e protocolos.

---

## 📋 Índice

- [O que são Interfaces e Cabos?](#o-que-são-interfaces-e-cabos)
- [O que é RJ-45?](#o-que-é-rj-45)
- [O que é Ethernet?](#o-que-é-ethernet)
- [O que são Protocolos de Rede?](#o-que-são-protocolos-de-rede)
- [O que são Bits e Bytes?](#o-que-são-bits-e-bytes)
- [Padrões Ethernet](#padrões-ethernet)
- [O que é um Cabo UTP?](#o-que-é-um-cabo-utp)
- [10BASE-T e 100BASE-T — 2 pares / 4 fios](#10base-t-e-100base-t--2-pares--4-fios)
- [Cabo Straight-Through](#cabo-straight-through)
- [Cabo Crossover](#cabo-crossover)
- [Auto MDI-X](#auto-mdi-x)
- [1000BASE-T e 10GBASE-T](#1000base-t-e-10gbase-t)
- [Conexões de Fibra Óptica](#conexões-de-fibra-óptica)
- [Fibra Multimodo](#fibra-multimodo)
- [Fibra Monomodo](#fibra-monomodo)
- [Padrões e Especificações de Cabos de Fibra](#padrões-e-especificações-de-cabos-de-fibra)
- [UTP vs Fibra Óptica](#utp-vs-fibra-óptica)

---

## O que são Interfaces e Cabos?

Em redes de computadores, a comunicação entre dispositivos exige dois elementos essenciais: **interfaces** e **cabos** (ou meios de transmissão sem fio).

### Interfaces de Rede

Uma **interface de rede** (também chamada de NIC — *Network Interface Card*) é o componente de hardware que permite a um dispositivo se conectar a uma rede. Ela pode ser:

- **Física** — uma porta no dispositivo onde se encaixa um cabo (ex.: porta RJ-45 em um computador ou switch).
- **Lógica** — uma representação de software de uma conexão de rede (ex.: interface de loopback).

Cada interface possui um endereço único chamado **endereço MAC** (*Media Access Control*), usado para identificar o dispositivo na rede local.

```
┌───────────────────────────────┐
│         Computador            │
│                               │
│  ┌─────────────────────────┐  │
│  │  Placa de Rede (NIC)    │  │
│  │  MAC: AA:BB:CC:DD:EE:FF │  │
│  └────────────┬────────────┘  │
└───────────────┼───────────────┘
                │
          [Porta RJ-45]
                │
            [Cabo UTP]
```

### Cabos de Rede

**Cabos de rede** são os meios físicos por onde os dados trafegam na forma de sinais elétricos ou pulsos de luz. Os principais tipos são:

- **Cabo de par trançado (UTP/STP)** — o mais comum em redes locais.
- **Cabo coaxial** — usado em redes antigas e em TV a cabo.
- **Cabo de fibra óptica** — usado para longas distâncias e alta velocidade.

---

## O que é RJ-45?

**RJ-45** (*Registered Jack 45*) é o **conector padrão** utilizado em cabos de rede Ethernet. É o "plugue" que você encaixa na porta do computador, switch ou roteador.

### Características físicas

- Possui **8 pinos** (posições), numerados de 1 a 8.
- É levemente maior que o conector telefônico RJ-11 (que tem 4 pinos).
- Cada pino corresponde a um fio interno do cabo UTP.

```
Vista frontal do conector RJ-45:

 ┌─────────────────┐
 │ 1 2 3 4 5 6 7 8 │  ← 8 pinos
 └────────┬────────┘
          │
     Trava de encaixe
```

### Padrões de pinagem (T568A e T568B)

A ordem dos fios dentro do conector segue um padrão. Os dois mais comuns são **T568A** e **T568B**:

| Pino | T568A           | T568B           |
|------|-----------------|-----------------|
| 1    | Branco/Verde    | Branco/Laranja  |
| 2    | Verde           | Laranja         |
| 3    | Branco/Laranja  | Branco/Verde    |
| 4    | Azul            | Azul            |
| 5    | Branco/Azul     | Branco/Azul     |
| 6    | Laranja         | Verde           |
| 7    | Branco/Marrom   | Branco/Marrom   |
| 8    | Marrom          | Marrom          |

> 💡 O padrão **T568B** é o mais utilizado em instalações comerciais nos EUA e no Brasil.

---

## O que é Ethernet?

**Ethernet** é a tecnologia de rede local (LAN) mais utilizada no mundo. Ela define as regras de como os dados devem ser transmitidos por um cabo entre dispositivos em uma rede local.

Foi criada na década de 1970 pela Xerox, Intel e DEC, e ao longo dos anos evoluiu de velocidades de **10 Mbps** até os atuais **400 Gbps** em ambientes de data center.

### O que Ethernet define?

A Ethernet especifica dois aspectos principais:

1. **Camada Física** — como os bits são transmitidos pelo cabo (voltagem, frequência, tipo de cabo, conectores).
2. **Camada de Enlace** — como os dispositivos identificam uns aos outros usando **endereços MAC** e como o acesso ao meio é controlado.

### Exemplo simplificado

Quando você conecta um computador a um switch com um cabo Ethernet:

```
[Computador]  ──[Cabo Ethernet]──  [Switch]
  MAC: A1:...                        Porta 1
```

O computador "fala Ethernet" com o switch: os dados são organizados em **quadros (frames)** com endereço MAC de origem e destino, e transmitidos pelos fios do cabo.

---

## O que são Protocolos de Rede?

Um **protocolo de rede** é um conjunto de **regras e convenções** que define como dois ou mais dispositivos devem se comunicar. Sem protocolos, cada fabricante usaria seu próprio formato de dados e os dispositivos não conseguiriam se entender.

Pense em um protocolo como um **idioma comum**: para que duas pessoas se comuniquem, ambas precisam falar o mesmo idioma e seguir as mesmas regras gramaticais.

### Exemplos de protocolos e suas funções

| Protocolo | Função                                              |
|-----------|-----------------------------------------------------|
| **Ethernet** | Transmissão de dados em redes locais (LAN)       |
| **IP**       | Endereçamento e roteamento de pacotes            |
| **TCP**      | Entrega confiável de dados com controle de erros |
| **UDP**      | Entrega rápida de dados sem garantia de entrega  |
| **HTTP/HTTPS** | Transferência de páginas web                   |
| **DNS**      | Tradução de nomes de domínio para endereços IP   |

### Como os protocolos se organizam?

Os protocolos são organizados em **camadas** (modelo OSI ou TCP/IP). Cada camada tem responsabilidades específicas e "conversa" apenas com as camadas acima e abaixo dela:

```
┌────────────────────────┐
│  Aplicação (HTTP, DNS) │  ← o que o usuário usa
├────────────────────────┤
│  Transporte (TCP, UDP) │  ← controle de entrega
├────────────────────────┤
│  Rede (IP)             │  ← endereçamento e rotas
├────────────────────────┤
│  Enlace (Ethernet)     │  ← comunicação local
├────────────────────────┤
│  Física (cabos, fios)  │  ← bits no meio físico
└────────────────────────┘
```

---

## O que são Bits e Bytes?

Toda comunicação em redes digitais é feita com **bits** — a menor unidade de informação em computação.

### Bit

Um **bit** (*binary digit*) representa um de dois estados possíveis: `0` ou `1`. Fisicamente, isso pode ser representado por:
- Presença ou ausência de tensão elétrica num cabo.
- Ausência ou presença de luz num cabo de fibra óptica.

### Byte

Um **byte** é um agrupamento de **8 bits**. É a unidade básica usada para representar um caractere de texto, por exemplo.

```
1 byte = 8 bits
Exemplo: a letra "A" em binário = 01000001
```

### Unidades de medida

| Unidade    | Símbolo | Equivalência          |
|------------|---------|-----------------------|
| Kilobyte   | KB      | 1.000 bytes           |
| Megabyte   | MB      | 1.000.000 bytes       |
| Gigabyte   | GB      | 1.000.000.000 bytes   |
| Terabyte   | TB      | 1.000.000.000.000 bytes |

### Velocidade de rede: bits por segundo

A velocidade de uma rede é medida em **bits por segundo (bps)**, não bytes:

| Unidade | Símbolo | Equivalência     |
|---------|---------|------------------|
| Kilobit por segundo | Kbps | 1.000 bps   |
| Megabit por segundo | Mbps | 1.000.000 bps |
| Gigabit por segundo | Gbps | 1.000.000.000 bps |

> ⚠️ **Atenção:** Quando seu plano de internet é de "100 Mbps", isso são **megabits**, não megabytes. Para converter: 100 Mbps ÷ 8 = ~12,5 MB/s de velocidade de download.

---

## Padrões Ethernet

Os padrões Ethernet são definidos pelo **IEEE** (Instituto de Engenheiros Elétricos e Eletrônicos) sob a norma **IEEE 802.3**. Cada padrão define a velocidade, o tipo de cabo suportado e a distância máxima.

A nomenclatura segue o formato:

```
  [Velocidade] BASE - [Tipo de meio]
       │                    │
    Ex: 100             T = par trançado (Twisted)
                        X = fibra óptica
                        S = fibra de ondas curtas
                        L = fibra de ondas longas
```

### Tabela geral dos padrões

| Padrão       | Velocidade | Cabo             | Distância máx. | Ano  |
|--------------|------------|------------------|----------------|------|
| 10BASE-T     | 10 Mbps    | UTP Cat 3        | 100 m          | 1990 |
| 100BASE-TX   | 100 Mbps   | UTP Cat 5        | 100 m          | 1995 |
| 1000BASE-T   | 1 Gbps     | UTP Cat 5e/6     | 100 m          | 1999 |
| 10GBASE-T    | 10 Gbps    | UTP Cat 6a/7     | 100 m          | 2006 |
| 1000BASE-SX  | 1 Gbps     | Fibra Multimodo  | 550 m          | 1998 |
| 1000BASE-LX  | 1 Gbps     | Fibra Monomodo   | 5 km           | 1998 |
| 10GBASE-SR   | 10 Gbps    | Fibra Multimodo  | 400 m          | 2002 |
| 10GBASE-LR   | 10 Gbps    | Fibra Monomodo   | 10 km          | 2002 |

---

## O que é um Cabo UTP?

**UTP** (*Unshielded Twisted Pair* — Par Trançado Não Blindado) é o tipo de cabo mais usado em redes Ethernet locais. É composto por **4 pares de fios de cobre**, onde cada par é trançado entre si.

### Por que os fios são trançados?

O trançamento dos pares serve para **reduzir interferências eletromagnéticas** (EMI). Quando dois fios conduzem sinais opostos e estão trançados, os campos eletromagnéticos de um cancelam os do outro — fenômeno chamado de **cancelamento de par**.

```
Par trançado:
  ~~~~~~~~~~~~~~~~~~~~
 /                    \
|  fio A (+)  fio B (-) |  → campos se cancelam
 \                    /
  ~~~~~~~~~~~~~~~~~~~~
```

### Categorias de cabo UTP

| Categoria | Velocidade máx. | Frequência | Uso típico             |
|-----------|-----------------|------------|------------------------|
| Cat 3     | 10 Mbps         | 16 MHz     | Telefonia, 10BASE-T    |
| Cat 5     | 100 Mbps        | 100 MHz    | 100BASE-TX             |
| Cat 5e    | 1 Gbps          | 100 MHz    | 1000BASE-T (mais comum)|
| Cat 6     | 1 Gbps          | 250 MHz    | 1000BASE-T / 10GBASE-T |
| Cat 6a    | 10 Gbps         | 500 MHz    | 10GBASE-T              |
| Cat 7     | 10 Gbps         | 600 MHz    | Data centers           |
| Cat 8     | 40 Gbps         | 2000 MHz   | Data centers           |

### Estrutura interna do cabo UTP

```
              Cabo UTP (8 fios = 4 pares)
         ┌──────────────────────────────────┐
         │  ~~Par 1~~  ~~Par 2~~            │
         │  ~~Par 3~~  ~~Par 4~~            │
         └──────────────────────────────────┘
              Revestimento externo (PVC)
```

---

## 10BASE-T e 100BASE-T — 2 pares / 4 fios

Os padrões **10BASE-T** (10 Mbps) e **100BASE-TX** (100 Mbps) utilizam apenas **2 dos 4 pares** do cabo UTP — ou seja, **4 fios** dos 8 disponíveis.

### Quais pinos são usados?

| Pino | Função (T568B)     | Par  |
|------|--------------------|------|
| 1    | TX+ (transmissão)  | Par 2|
| 2    | TX- (transmissão)  | Par 2|
| 3    | RX+ (recepção)     | Par 3|
| 6    | RX- (recepção)     | Par 3|

> Os pinos 4, 5, 7 e 8 (Pares 1 e 4) **não são usados** nestes padrões.

### Como funciona a transmissão?

Cada par trançado é usado para **uma direção** de comunicação:

```
Dispositivo A                    Dispositivo B
                                 
  TX+ (pino 1) ────────────►  RX+ (pino 3)
  TX- (pino 2) ────────────►  RX- (pino 6)
                                 
  RX+ (pino 3) ◄────────────  TX+ (pino 1)
  RX- (pino 6) ◄────────────  TX- (pino 2)
```

- **Par de TX (pinos 1 e 2):** transmite dados.
- **Par de RX (pinos 3 e 6):** recebe dados.
- O uso de pares diferenciais (+ e -) aumenta a resistência a interferências.

---

## Cabo Straight-Through

Um cabo **Straight-Through** (cabo direto) é aquele em que a pinagem dos dois conectores RJ-45 nas extremidades é **idêntica** — o fio que entra no pino 1 de uma ponta sai no pino 1 da outra ponta.

### Quando usar?

Usado para conectar dispositivos de **tipos diferentes**:

- Computador → Switch
- Computador → Hub
- Roteador → Switch

```
Extremidade A                   Extremidade B
(T568B)                         (T568B)

Pino 1 (Branco/Laranja) ──────► Pino 1 (Branco/Laranja)
Pino 2 (Laranja)        ──────► Pino 2 (Laranja)
Pino 3 (Branco/Verde)   ──────► Pino 3 (Branco/Verde)
Pino 4 (Azul)           ──────► Pino 4 (Azul)
Pino 5 (Branco/Azul)    ──────► Pino 5 (Branco/Azul)
Pino 6 (Verde)          ──────► Pino 6 (Verde)
Pino 7 (Branco/Marrom)  ──────► Pino 7 (Branco/Marrom)
Pino 8 (Marrom)         ──────► Pino 8 (Marrom)
```

### Por que funciona entre tipos diferentes?

Porque switches e roteadores já possuem internamente seus pinos de TX e RX invertidos em relação a computadores. Assim, o TX do computador (pino 1) chega exatamente no RX do switch (pino 1 do lado dele, que já é tratado como RX internamente).

---

## Cabo Crossover

Um cabo **Crossover** (cabo cruzado) tem a pinagem **invertida** entre as duas extremidades: os fios de transmissão (TX) de um lado são conectados aos fios de recepção (RX) do outro lado.

### Quando usar?

Usado para conectar dispositivos do **mesmo tipo** diretamente:

- Computador → Computador
- Switch → Switch
- Roteador → Roteador

```
Extremidade A (T568B)            Extremidade B (T568A)

Pino 1 (TX+) Branco/Laranja ──► Pino 3 (RX+) Branco/Verde
Pino 2 (TX-) Laranja        ──► Pino 6 (RX-) Verde
Pino 3 (RX+) Branco/Verde   ──► Pino 1 (TX+) Branco/Laranja
Pino 6 (RX-) Verde          ──► Pino 2 (TX-) Laranja
```

### Por que é necessário o cruzamento?

Dois dispositivos do mesmo tipo possuem TX e RX nos mesmos pinos. Se conectados com um cabo direto, o TX de um chegaria no TX do outro — e ninguém receberia nada. O cruzamento garante que o TX de um chegue no RX do outro:

```
PC-A                              PC-B
TX+ (pino 1) ──────────────────► RX+ (pino 3)  ✔
TX- (pino 2) ──────────────────► RX- (pino 6)  ✔
RX+ (pino 3) ◄────────────────── TX+ (pino 1)  ✔
RX- (pino 6) ◄────────────────── TX- (pino 2)  ✔
```

---

## Auto MDI-X

**Auto MDI-X** (*Automatic Medium Dependent Interface Crossover*) é uma funcionalidade presente em switches, roteadores e placas de rede modernas que **detecta automaticamente** o tipo de cabo conectado (direto ou cruzado) e ajusta a pinagem internamente, sem precisar que o usuário use o cabo correto.

### O que isso significa na prática?

Com Auto MDI-X, você pode usar **qualquer cabo** (direto ou cruzado) para conectar quaisquer dois dispositivos — o hardware se encarrega do ajuste automático.

```
Sem Auto MDI-X:
  PC ──[cabo direto]──► Switch     ✔  (correto)
  PC ──[cabo cruzado]──► Switch    ✗  (não funciona)
  PC ──[cabo direto]──► PC         ✗  (não funciona)
  PC ──[cabo cruzado]──► PC        ✔  (correto)

Com Auto MDI-X:
  PC ──[qualquer cabo]──► Switch   ✔  (sempre funciona)
  PC ──[qualquer cabo]──► PC       ✔  (sempre funciona)
```

### Disponibilidade

A maioria dos switches e placas de rede fabricados a partir dos anos 2000 já possuem Auto MDI-X habilitado por padrão. Isso tornou a distinção entre cabo direto e crossover praticamente irrelevante no dia a dia — embora seja importante conhecer o conceito para fins de estudo e troubleshooting.

---

## 1000BASE-T e 10GBASE-T

### 1000BASE-T (Gigabit Ethernet)

O padrão **1000BASE-T** opera a **1 Gbps** e, ao contrário do 10BASE-T e 100BASE-TX, utiliza **todos os 4 pares** do cabo UTP (8 fios ao total).

#### Como funciona?

Em vez de usar um par para TX e outro para RX separadamente, o 1000BASE-T usa uma técnica chamada **transmissão bidirecional simultânea** em cada par. Cada par transmite e recebe ao mesmo tempo usando circuitos de cancelamento de eco (*echo cancellation*).

```
Par 1 (pinos 1,2) ◄──────────────────►  TX e RX simultâneos
Par 2 (pinos 3,6) ◄──────────────────►  TX e RX simultâneos
Par 3 (pinos 4,5) ◄──────────────────►  TX e RX simultâneos
Par 4 (pinos 7,8) ◄──────────────────►  TX e RX simultâneos
```

Cada par contribui com **250 Mbps**, totalizando 1000 Mbps = 1 Gbps.

- **Cabo recomendado:** Cat 5e ou Cat 6
- **Distância máxima:** 100 metros

### 10GBASE-T (10 Gigabit Ethernet)

O padrão **10GBASE-T** opera a **10 Gbps** e também usa todos os 4 pares, porém com técnicas de sinalização ainda mais avançadas e exige cabos de maior qualidade.

- **Cabo recomendado:** Cat 6a (até 100 m) ou Cat 6 (até 55 m)
- **Distância máxima:** 100 metros (com Cat 6a)
- Usa codificação **PAM-16** (16 níveis de amplitude por símbolo) para transmitir mais dados por ciclo.

### Comparação 10BASE-T vs 100BASE-TX vs 1000BASE-T vs 10GBASE-T

| Padrão       | Velocidade | Pares usados | Cabo mín. | Distância |
|--------------|------------|--------------|-----------|-----------|
| 10BASE-T     | 10 Mbps    | 2 (4 fios)   | Cat 3     | 100 m     |
| 100BASE-TX   | 100 Mbps   | 2 (4 fios)   | Cat 5     | 100 m     |
| 1000BASE-T   | 1 Gbps     | 4 (8 fios)   | Cat 5e    | 100 m     |
| 10GBASE-T    | 10 Gbps    | 4 (8 fios)   | Cat 6a    | 100 m     |

---

## Conexões de Fibra Óptica

Cabos de fibra óptica transmitem dados na forma de **pulsos de luz** ao invés de sinais elétricos. Isso oferece vantagens significativas em relação ao cobre, especialmente para longas distâncias e altas velocidades.

### Como funciona?

A fibra óptica é composta por um **núcleo de vidro ou plástico** extremamente fino pelo qual a luz se propaga. O princípio físico usado é a **reflexão interna total**: a luz entra em um ângulo tal que não consegue "escapar" do núcleo, sendo refletida continuamente pelas paredes até chegar ao destino.

```
              Estrutura de um cabo de fibra óptica:
   ┌────────────────────────────────────────────────────┐
   │  Revestimento externo (jacket)                     │
   │  ┌──────────────────────────────────────────────┐  │
   │  │  Revestimento protetor (buffer coating)      │  │
   │  │  ┌────────────────────────────────────────┐  │  │
   │  │  │  Casca (cladding) - índice de refração │  │  │
   │  │  │  ┌──────────────────────────────────┐  │  │  │
   │  │  │  │  NÚCLEO (core) - luz viaja aqui  │  │  │  │
   │  │  │  └──────────────────────────────────┘  │  │  │
   │  │  └────────────────────────────────────────┘  │  │
   │  └──────────────────────────────────────────────┘  │
   └────────────────────────────────────────────────────┘
```

### Componentes de uma conexão de fibra

- **Transmissor (TX):** converte o sinal elétrico em pulsos de luz (LED ou laser).
- **Cabo de fibra:** conduz os pulsos de luz.
- **Receptor (RX):** converte os pulsos de luz de volta em sinal elétrico.
- **Transceiver (ex.: SFP):** módulo que integra TX e RX em um único componente plugável nos switches.

```
[Switch A]                               [Switch B]
   │                                         │
[SFP TX] ─────────[fibra óptica]──────► [SFP RX]
[SFP RX] ◄────────[fibra óptica]─────── [SFP TX]
```

---

## Fibra Multimodo

A fibra **multimodo** (*multimode fiber* — MMF) possui um **núcleo maior** (tipicamente 50 µm ou 62,5 µm de diâmetro), que permite que múltiplos "raios" de luz (modos) se propaguem simultaneamente pelo núcleo em ângulos diferentes.

### Características

- **Núcleo:** 50 µm ou 62,5 µm
- **Fonte de luz:** LEDs ou lasers VCSEL (mais baratos)
- **Distância:** até ~550 metros (dependendo do padrão)
- **Custo:** menor que a monomodo
- **Uso típico:** redes locais, data centers, conexões entre andares de um prédio

### Limitação: dispersão modal

Como diferentes modos percorrem caminhos diferentes, eles chegam ao destino em momentos ligeiramente diferentes, causando distorção do sinal — fenômeno chamado de **dispersão modal**. Por isso, a fibra multimodo é adequada apenas para distâncias curtas.

```
Fibra Multimodo:

 Núcleo largo (50 µm)
 ┌──────────────────────────────────┐
 │  ╱╲  ╱╲  ╱╲   ← múltiplos modos │
 │ ╱  ╲╱  ╲╱  ╲  percorrem caminhos │
 │                 diferentes       │
 └──────────────────────────────────┘
```

### Identificação visual

Cabos de fibra multimodo geralmente possuem revestimento **laranja** (OM1, OM2) ou **aqua/verde-água** (OM3, OM4, OM5).

| Tipo | Núcleo | Largura de banda | Distância (10G) |
|------|--------|------------------|-----------------|
| OM1  | 62,5 µm | 200 MHz·km      | 33 m            |
| OM2  | 50 µm   | 500 MHz·km      | 82 m            |
| OM3  | 50 µm   | 2000 MHz·km     | 300 m           |
| OM4  | 50 µm   | 4700 MHz·km     | 400 m           |
| OM5  | 50 µm   | 28000 MHz·km    | 400 m (WDM)     |

---

## Fibra Monomodo

A fibra **monomodo** (*single-mode fiber* — SMF) possui um **núcleo muito menor** (tipicamente 8–10 µm), tão estreito que permite apenas **um único modo** de luz se propagar — em linha reta, sem reflexões angulares.

### Características

- **Núcleo:** 8–10 µm
- **Fonte de luz:** lasers de precisão (mais caros)
- **Distância:** dezenas de quilômetros (até 80 km ou mais, com amplificadores)
- **Custo:** maior que a multimodo (especialmente os transceivers laser)
- **Uso típico:** conexões WAN, backbones de operadoras, cabos submarinos, longas distâncias

### Por que vai mais longe?

Como há apenas um modo de luz, não existe dispersão modal. O sinal se degrada muito menos ao longo da distância, permitindo transmissões de longa distância com altíssima fidelidade.

```
Fibra Monomodo:

 Núcleo estreito (9 µm)
 ┌──────────────────────────────────┐
 │  ──────────────────────────────  │  ← apenas um modo
 │    luz viaja em linha reta       │     sem dispersão
 └──────────────────────────────────┘
```

### Identificação visual

Cabos de fibra monomodo geralmente possuem revestimento **amarelo**.

---

## Padrões e Especificações de Cabos de Fibra

### Conectores de fibra óptica

Diferentemente do RJ-45 do cobre, a fibra óptica possui vários tipos de conectores:

| Conector | Características                        | Uso típico              |
|----------|----------------------------------------|-------------------------|
| **LC**   | Pequeno, trava de pressão, muito usado | Data centers, SFP       |
| **SC**   | Quadrado, push-pull, comum             | Equipamentos corporativos|
| **ST**   | Circular, trava bayoneta               | Redes antigas           |
| **MPO/MTP** | Multi-fibra (8, 12, 24 fibras)      | Data centers de alta densidade |

### Transceivers SFP / SFP+ / QSFP

Switches corporativos não têm portas de fibra fixas — eles usam **slots modulares** onde se encaixam transceivers (módulos plugáveis):

| Tipo     | Velocidade | Uso                    |
|----------|------------|------------------------|
| SFP      | 1 Gbps     | Gigabit Ethernet       |
| SFP+     | 10 Gbps    | 10 Gigabit Ethernet    |
| SFP28    | 25 Gbps    | Data centers modernos  |
| QSFP+    | 40 Gbps    | Agregação em data centers |
| QSFP28   | 100 Gbps   | Backbone de alta velocidade |

### Principais padrões de fibra

| Padrão       | Tipo       | Velocidade | Distância máx. |
|--------------|------------|------------|----------------|
| 1000BASE-SX  | Multimodo  | 1 Gbps     | 550 m          |
| 1000BASE-LX  | Monomodo   | 1 Gbps     | 5 km           |
| 10GBASE-SR   | Multimodo  | 10 Gbps    | 400 m (OM3)    |
| 10GBASE-LR   | Monomodo   | 10 Gbps    | 10 km          |
| 10GBASE-ER   | Monomodo   | 10 Gbps    | 40 km          |
| 100GBASE-SR4 | Multimodo  | 100 Gbps   | 100 m          |
| 100GBASE-LR4 | Monomodo   | 100 Gbps   | 10 km          |

---

## UTP vs Fibra Óptica

### Tabela comparativa

| Característica         | Cabo UTP (cobre)            | Fibra Óptica                    |
|------------------------|-----------------------------|---------------------------------|
| **Velocidade**         | Até 40 Gbps (Cat 8)         | Até 100+ Gbps por fibra         |
| **Distância máxima**   | 100 metros                  | Centenas de metros a centenas de km |
| **Interferência EM**   | Susceptível a EMI/RFI       | Totalmente imune                |
| **Segurança física**   | Sinal pode ser captado      | Muito difícil de interceptar    |
| **Custo do cabo**      | Baixo                       | Moderado a alto                 |
| **Custo dos equipamentos** | Baixo (portas RJ-45 nativas) | Maior (transceivers SFP)    |
| **Instalação**         | Simples, conectores fáceis  | Requer fusão ou conector polido |
| **Peso e espessura**   | Mais pesado e grosso        | Muito leve e fino               |
| **Alimentação PoE**    | Sim (Power over Ethernet)   | Não                             |
| **Durabilidade**       | Sensível a dobras e tração  | Frágil a impactos físicos       |
| **Uso típico**         | Redes locais, escritórios   | Backbones, longas distâncias, data centers |

### Quando usar cada um?

**Use cabo UTP quando:**
- A distância entre dispositivos for inferior a 100 metros.
- O orçamento for limitado.
- Precisar de PoE (alimentar câmeras, telefones IP, APs).
- A instalação precisar ser rápida e simples.

**Use fibra óptica quando:**
- A distância for superior a 100 metros.
- Precisar de altíssima velocidade (10 Gbps ou mais).
- O ambiente tiver muita interferência elétrica (fábricas, hospitais).
- A segurança dos dados for crítica.
- Conectar prédios, andares distantes ou localidades diferentes.

### Cenário típico em uma empresa

```
                        ┌─────────────────────────────┐
                        │         DATACENTER           │
                        │  [Core Switch] ◄──────────── │◄── Fibra Monomodo (WAN/ISP)
                        │       │                      │
                        │    [Fibra Multimodo]         │
                        └───────┼─────────────────────┘
                                │
              ┌─────────────────┼─────────────────┐
              │                 │                 │
      [Switch Andar 1]  [Switch Andar 2]  [Switch Andar 3]
              │                 │                 │
    [Cabo UTP Cat 6]   [Cabo UTP Cat 6]  [Cabo UTP Cat 6]
              │                 │                 │
         [PCs/APs]          [PCs/APs]         [PCs/APs]
```

> A fibra óptica conecta o data center aos switches de andar (distâncias maiores, alta velocidade), enquanto o UTP distribui a conexão para os computadores dos usuários finais (distâncias curtas, custo baixo).

---

*Documentação criada para fins de estudo e referência pessoal.*
