# 🌐 Dispositivos de Rede

> Documentação introdutória sobre redes de computadores, seus componentes e funcionamento.

---

## 📋 Índice

- [O que é uma rede?](#o-que-é-uma-rede)
- [Clientes e Servidores](#clientes-e-servidores)
- [Switch e Roteador](#switch-e-roteador)

---

## O que é uma rede?

Uma **rede de computadores** é um conjunto de dois ou mais dispositivos interconectados que conseguem trocar dados e compartilhar recursos entre si. Esses dispositivos podem ser computadores, celulares, impressoras, câmeras, servidores, entre outros.

A comunicação entre eles acontece por meio de **meios físicos** (como cabos de rede) ou **meios sem fio** (como Wi-Fi e Bluetooth), seguindo regras chamadas de **protocolos de comunicação** (como o TCP/IP).

### Por que as redes existem?

O principal objetivo de uma rede é permitir:

- **Compartilhamento de recursos** — impressoras, arquivos e conexões com a internet podem ser usados por vários dispositivos ao mesmo tempo.
- **Comunicação** — troca de mensagens, e-mails, chamadas de vídeo etc.
- **Centralização de dados** — armazenar informações em um único lugar acessível a todos da rede.
- **Escalabilidade** — adicionar novos dispositivos sem grandes mudanças na infraestrutura.

### Exemplo prático

Imagine um escritório com 10 computadores. Sem uma rede, cada computador precisaria de sua própria impressora e conexão com a internet. Com uma rede:

```
[Computador 1] ──┐
[Computador 2] ──┤
[Computador 3] ──┼──► [Switch] ──► [Roteador] ──► [Internet]
      ...        ┤        │
[Computador 10]──┘        └──► [Impressora compartilhada]
```

Todos os computadores compartilham a mesma impressora e a mesma conexão com a internet — economizando recursos e facilitando a colaboração.

---

## Clientes e Servidores

Na maioria das redes, os dispositivos assumem papéis distintos na comunicação. Os dois papéis fundamentais são: **cliente** e **servidor**.

### O que é um Cliente?

Um **cliente** é qualquer dispositivo (ou programa) que **solicita** um serviço ou recurso a outro dispositivo. Ele inicia a comunicação fazendo uma requisição e aguarda uma resposta.

**Exemplos de clientes:**
- Seu navegador web (Chrome, Firefox) ao acessar um site
- Um aplicativo de e-mail baixando mensagens
- Um app de streaming pedindo um vídeo para reproduzir
- Um celular conectando ao Wi-Fi para acessar a internet

### O que é um Servidor?

Um **servidor** é o dispositivo (ou programa) que **responde** às requisições dos clientes. Ele fica aguardando conexões, processa os pedidos recebidos e devolve a resposta adequada.

**Exemplos de servidores:**
- Um servidor web que armazena e entrega páginas de sites
- Um servidor de e-mail que gerencia caixas de entrada
- Um servidor de arquivos que centraliza documentos de uma empresa
- Um servidor de banco de dados que responde a consultas

### Como funciona na prática?

O modelo cliente-servidor segue sempre o mesmo fluxo básico:

```
CLIENTE                          SERVIDOR
   │                                │
   │── 1. Requisição ─────────────► │
   │      "GET /index.html"         │
   │                                │── 2. Processa o pedido
   │                                │
   │◄─ 3. Resposta ─────────────── │
   │      "200 OK + conteúdo HTML"  │
```

#### Exemplo 1 — Acessando um site

1. Você digita `https://github.com` no navegador.
2. O **navegador (cliente)** envia uma requisição HTTP ao servidor do GitHub.
3. O **servidor do GitHub** recebe o pedido, busca a página e envia o HTML de volta.
4. O navegador renderiza a página na sua tela.

#### Exemplo 2 — Enviando um e-mail

1. Você clica em "Enviar" no seu cliente de e-mail (ex.: Outlook).
2. O **cliente** envia a mensagem ao **servidor de e-mail** (ex.: servidor SMTP do Gmail).
3. O servidor armazena o e-mail e o encaminha para o servidor de destino.
4. Quando o destinatário abrir seu e-mail, o **cliente dele** fará uma requisição ao servidor e baixará a mensagem.

### Um dispositivo pode ser cliente e servidor ao mesmo tempo?

**Sim!** Em redes **peer-to-peer (P2P)**, um mesmo dispositivo pode atuar como cliente e servidor simultaneamente. Um exemplo clássico são aplicativos de torrent: ao mesmo tempo que você **baixa** partes de um arquivo (cliente), você **envia** outras partes para outros usuários (servidor).

---

## Switch e Roteador

Switch e roteador são dois dos dispositivos mais importantes em uma rede. Embora trabalhem juntos, eles têm funções bem diferentes.

---

### Switch

Um **switch** é um dispositivo que conecta múltiplos dispositivos **dentro de uma mesma rede local (LAN)**, permitindo que eles se comuniquem entre si.

#### Como ele funciona?

O switch opera na **Camada 2 do modelo OSI** (Camada de Enlace) e usa os **endereços MAC** dos dispositivos para saber para onde enviar cada dado.

Quando um dispositivo se conecta ao switch, ele aprende e armazena o endereço MAC desse dispositivo em uma tabela interna chamada **tabela MAC**. A partir daí, toda vez que um dado chega, o switch verifica o endereço de destino e envia o dado **somente** para a porta correta — ao invés de mandar para todos.

```
         [Tabela MAC do Switch]
         ┌──────────────────────────┐
         │ Porta 1 → MAC: AA:BB:... │
         │ Porta 2 → MAC: CC:DD:... │
         │ Porta 3 → MAC: EE:FF:... │
         └──────────────────────────┘

[PC-A]──Porta 1─┐
[PC-B]──Porta 2─┤──[SWITCH]
[PC-C]──Porta 3─┘
```

#### Exemplo prático

PC-A quer enviar um arquivo para PC-B:

1. PC-A envia o dado com o endereço MAC de PC-B como destino.
2. O switch recebe o dado pela **Porta 1**.
3. Consulta a tabela MAC e descobre que PC-B está na **Porta 2**.
4. Encaminha o dado **apenas** para a Porta 2.
5. PC-C, na Porta 3, **não recebe nada** — o tráfego é isolado.

> 💡 **Benefício:** O switch melhora a eficiência e a segurança da rede local, pois os dados vão apenas para quem precisa recebê-los.

---

### Roteador

Um **roteador** é um dispositivo que conecta **redes diferentes** entre si e é responsável por encaminhar os dados ao destino correto, mesmo que ele esteja em outra rede — como a internet.

#### Como ele funciona?

O roteador opera na **Camada 3 do modelo OSI** (Camada de Rede) e usa os **endereços IP** para tomar decisões de roteamento. Ele analisa o endereço IP de destino de cada pacote e consulta sua **tabela de roteamento** para decidir por qual caminho o dado deve seguir.

```
[Rede Local 192.168.1.0/24]          [Internet]
                                         │
[PC-A] ──┐                               │
[PC-B] ──┤── [Switch] ──► [ROTEADOR] ───┤
[PC-C] ──┘                               │
                                     [Servidor remoto]
```

#### Exemplo prático 1 — Acesso à internet

1. PC-A (IP: `192.168.1.10`) quer acessar o Google (`142.250.79.46`).
2. O pacote chega ao **roteador**.
3. O roteador verifica: o destino `142.250.79.46` **não está** na rede local.
4. Ele encaminha o pacote pela interface WAN em direção à internet.
5. O Google responde e o roteador entrega a resposta de volta para PC-A.

#### Exemplo prático 2 — Comunicação entre duas redes locais

Uma empresa tem duas filiais, cada uma com sua própria rede:

```
[Filial A - 192.168.1.0/24]           [Filial B - 192.168.2.0/24]
        │                                        │
   [Roteador A] ◄──── (VPN / Internet) ────► [Roteador B]
```

Os roteadores tornam possível que um computador da Filial A se comunique com um computador da Filial B, mesmo estando em redes com faixas de IP diferentes.

---

### Switch vs Roteador — Resumo comparativo

| Característica       | Switch                          | Roteador                            |
|----------------------|---------------------------------|-------------------------------------|
| Função principal     | Conectar dispositivos na LAN    | Conectar redes diferentes           |
| Endereço utilizado   | Endereço MAC                    | Endereço IP                         |
| Camada OSI           | Camada 2 (Enlace)               | Camada 3 (Rede)                     |
| Alcance              | Rede local (LAN)                | Entre redes (LAN ↔ Internet)        |
| Exemplo de uso       | Ligar PCs a uma rede interna    | Conectar a rede interna à internet  |

---

### Como Switch e Roteador trabalham juntos?

Na prática, eles se complementam:

```
[PC-A] ──┐
[PC-B] ──┤                              ┌── [Internet]
[PC-C] ──┼──► [Switch] ──► [Roteador] ─┤
[PC-D] ──┤                              └── [Outra rede]
[PC-E] ──┘
```

- O **switch** garante a comunicação eficiente **entre os dispositivos da rede local**.
- O **roteador** garante que a rede local possa se comunicar com **o mundo externo**.

---

*Documentação criada para fins de estudo e referência pessoal.*
