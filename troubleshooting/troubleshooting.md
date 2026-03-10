<h1 align="center"> 🖥️  Minha Base de Conhecimento / Documentação </h1>

<p align="center"> Criei esse arquivo em Markdown com a intenção de demonstrar meus conhecimentos em TI e exemplificar como desenvolver uma documentação simples, clara e de fácil entendimento. Essas qualidades são muito úteis não apenas em ambientes corporativos, mas também pessoalmente ou outros que venham ter os mesmos problemas. </p>

<h2 align="center">  Tabela de Conteúdos </h2>

<p align="center">
  <a href="#-índice-de-problemas">📋 Índice de Problemas</a> •
  <a href="#-modelo-de-documentação">📋 Modelo de documentação</a> •
  <a href="#-boas-práticas-de-documentação">💡 Boas práticas de documentação</a> •
  <a href="#-como-escrever-uma-documentação-voltada-para-solução-de-problemas">📝 Como escrever uma documentação</a> •
  <a href="#-boas-práticas-para-ordem-de-serviço-ou-chamados-tickets">💎 Boas práticas para chamados</a>
</p>
  
---

<h2 align="center"> 📋 Índice de Problemas </h2>

<p align="center"> 📌  Problemas comuns e soluções do dia a dia de um usuário ou que podem ocorrer em um ambiente corporativo. Do básico aos mais "complicados", com possíveis causas, solução passo a passo e dicas de prevenção. </p>

> [!NOTE] 
> Você pode clicar nos *links* na tabela abaixo para ir diretamente num problema específico.




| # | Problema | Categoria | Gravidade |
| --- | --- | --- | --- |
| 01 | <a href="#01--computador-não-liga"> Computador não liga </a> | Hardware / Energia | 🟡 Média |
| 02 | <a href="#02--sem-conexão-com-a-internet-usuário-único"> Sem conexão com a internet (Usuário único) </a> | Rede / Conectividade | 🟡 Média |
| 03 | <a href="#03--impressora-offline--não-imprime"> Impressora offline / Não imprime" </a>| Hardware / Impressão | 🟢 Baixa |
| 04 | <a href="#04--senha-do-windows-esquecida-conta-local"> Senha do Windows esquecida" </a> | Software / Autenticação | 🟡 Média |
| 05 | <a href="#05--computador-lento"> Computador lento </a> | Software / Desempenho | 🟢 Baixa |
| 06 | <a href="#06--blue-screen-of-death-bsod"> Blue Screen of Death (BSOD) </a>| Software / Erro de Sistema | 🟠 Alta |
| 07 | <a href="#07--usuário-não-consegue-entrar-no-domínio-active-directory"> Usuário não consegue entrar no Domínio (Active Directory) </a>| Rede / Autenticação | 🟠 Alta |
| 08 | <a href="#08--outlook-não-envia-ou-recebe-e-mails"> Outlook não envia ou recebe e-mails </a>| Software / E-mail | 🟡 Média |
| 09 | <a href="#09--aplicativo-fecha-ao-iniciar"> Aplicativo fecha ao iniciar </a>| Software / Aplicativo | 🟡 Média |
| 10 | <a href="#10--sem-internet--rede-inteira-afetada"> Sem internet / Rede inteira afetada </a>| Rede / Infraestrutura | 🟠 Alta |
| 11 | <a href="#11--infecção-por-ransomware"> Infecção por Ransomware </a> | Segurança / Malware | 🔴 Crítica |
| 12 | <a href="#12--falha-no-disco-rígido-hdssd"> Falha no disco rígido (HD/SSD) </a>| Hardware / Armazenamento | 🔴 Crítica |
| 13 | <a href="#13--vpn-não-conecta-acesso-remoto"> VPN não conecta (acesso remoto) </a> | Rede / Acesso Remoto | 🟠 Alta |
| 14 | <a href="#14--servidor-sem-resposta--serviço-fora-do-ar">Servidor sem serviço / Serviço fora do ar </a>| Infraestrutura / Servidor | 🔴 Crítica |

---




<div align="center">


 ## 01 — Computador não liga 



>  🟡 **Gravidade: Média | 👤 Afetados: Usuário único | 🗂️ Categoria: Hardware / Energia**



|🚨 Problema|
|:-------------:|  

O usuário relata que o computador não responde ao pressionar o botão de energia.

|🕵️ Possíveis causas|
|-------------------|

Cabo de energia solto, tomada com defeito, fonte de alimentação (PSU) com falha ou bateria CMOS descarregada.

|🛠️ Solução|
|---------|



 Verifique se o cabo de energia está firmemente conectado em ambas as extremidades.<br>
 Teste a tomada com outro dispositivo (luminária, carregador de celular).<br>
 Substitua o cabo de energia por um que esteja funcionando.<br>
 Ouça os *bipes* de POST — bipes múltiplos indicam códigos de erro de hardware.<br>
 Se não houver nenhuma resposta, inspecione a PSU com um multímetro ou troque por uma reserva.<br>
 Escale para inspeção de hardware caso a PSU seja confirmada como defeituosa.

|🏷️ Prevenções|
|-----------|

Realize verificações periódicas de hardware; use um nobreak (UPS) para proteção contra surtos de energia.

---

## 02 — Sem conexão com a Internet (Usuário Único)

> 🟡 **Gravidade: Média | 👤 Afetados: Usuário único | 🗂️ Categoria: Rede / Conectividade**

|🚨 Problema|
|-----------|

O usuário não consegue acessar sites ou recursos internos, mas outros usuários na mesma rede não são afetados.

|🕵️ Possíveis causas|
|-------------------|

Cabo desconectado, IP mal configurado, pilha de rede corrompida ou DNS incorreto.

|🛠️ Solução|
|----------|

 Verifique se o cabo de rede está bem encaixado; observe a luz de link na placa de rede; <br>
 Execute no CMD: *`ipconfig /release`* e depois *`ipconfig /renew`* para renovar o IP; <br>
 Teste a conectividade: *`ping 8`* — se funcionar, o problema é de DNS, não de roteamento; <br>
 Execute: *`netsh winsock reset`* e reinicie o computador; <br>
 Se for Wi-Fi: "esqueça" a rede e reconecte com a senha correta; <br>
 Verifique se o driver da placa de rede está desatualizado no *Gerenciador de Dispositivos*.

|🏷️ Prevenções|
|------|

Use IPs estáticos para desktops em funções críticas; mantenha os drivers de rede atualizados.

---

## 03 — Impressora offline / Não imprime

> 🟢 **Gravidade: Baixa | 👤 Afetados: Usuário único | 🗂️ Categoria: Hardware / Impressão**

|🚨 Problema|
|------|

O usuário envia um trabalho de impressão mas nada acontece, ou a impressora aparece como *'Offline'* no Windows.

|🕵️ Possíveis causas|
|---------|

Serviço *Spooler* travado, trabalhos pendentes bloqueando a fila, impressora padrão incorreta ou problema no driver.

| 🛠️ Solução |
|--------|

 Abra Serviços (*`services.msc`*) e reinicie o serviço *'Spooler de Impressão'*;<br>
 Limpe a fila de impressão: navegue até *`C:\Windows\System32\spool\PRINTERS`* e delete todos os arquivos;<br>
 Verifique se a impressora correta está definida como padrão;<br>
 Clique com o botão direito na impressora >  Ver o que está imprimindo  >  Cancelar todos os documentos ; <br>
 Desinstale e reinstale o driver da impressora pelo site do fabricante.
 Para impressoras de rede, confirme se o IP da impressora não mudou.

|🏷️ Prevenções|
|-------------|

Defina o IP das impressoras como estático/reservado no DHCP para evitar mudanças de endereço.

---

## 04 — Senha do Windows esquecida (conta local)

> 🟡  **Gravidade: Média | 👤 Afetados: Usuário único | 🗂️ Categoria: Software / Autenticação**

|🚨 Problema|
|-----------|

O usuário não consegue entrar no Windows porque esqueceu a senha da conta local.

|🕵️ Possíveis causas|
|-------------------|

Usuário esqueceu as credenciais; nenhuma dica de senha foi configurada.

|🛠️ Solução|
|----------|

 Se houver outra conta de administrador local: faça login e redefina via CMD: *`net user [usuario] [novasenha]`*; <br>
 No Windows 10/11: use as perguntas de segurança na tela de login (se configuradas); <br>
 Inicialize pela mídia de instalação do Windows > *Reparar o computador*  >  *Prompt de Comando*; <br>
 Use o disco de redefinição de senha, se criado anteriormente; <br>
 Para contas de domínio: contate o administrador do *Active Directory*  — nunca tente  *bypass local*.

|🏷️ Prevenções|
|-------------|

Incentive o uso de gerenciadores de senha; configure perguntas de segurança; documente procedimentos de recuperação.

---

## 05 — Computador lento

> 🟢 **Gravidade: Baixa | 👤 Afetados: Usuário único | 🗂️ Categoria: Software / Desempenho**

|🚨 Problema|
|-----------|

O usuário relata que o computador está anormalmente lento, programas demoram para abrir ou o sistema trava.

|🕵️ Possíveis causas|
|-------------------|

Alto uso de CPU/RAM, disco cheio, muitos programas ativos na inicialização, malware ou hardware antigo.

|🛠️ Solução|
|----------|

 Abra o  *Gerenciador de Tarefas* (*`Ctrl+Shift+Esc`*)  e identifique os processos com alto uso de recursos; <br>
 Desative programas desnecessários na inicialização pela aba *'Inicializar'* do *Gerenciador de Tarefas*; <br>
 Execute a  *Limpeza de Disco*  e exclua arquivos temporários e esvazie a *Lixeira*; <br>
 Verifique o uso do disco — se estiver acima de 90%, libere espaço ou recomende upgrade de armazenamento; <br>
 Execute uma varredura completa de malware com o  *Windows Defender*  ou  *Malwarebytes*; <br>
 Se a RAM estiver consistentemente acima de 90%, recomende upgrade de memória.

|🏷️ Prevenções|
|-------------|

Agende manutenção mensal; aplique políticas de uso de disco; execute varreduras regulares de antivírus.

---



## 06 — *Blue Screen of Death* (BSOD)

> 🟠 **Gravidade: Alta | 👤 Afetados: Usuário único | 🗂️ Categoria: Software / Erro de Sistema**

|🚨 Problema|
|-----------|

O computador exibe uma tela azul com código de erro e reinicia automaticamente.

| 🕵️ Possíveis causas|
|--------------------|

Conflito de driver, RAM com falha, arquivos de sistema corrompidos ou superaquecimento.

|🛠️ Solução|
|----------|

 Anote o código de erro exibido no BSOD (ex: *`KERNEL_SECURITY_CHECK_FAILURE`*); <br>
 Inicialize no Modo Seguro: segure *`Shift`* >  *Reiniciar*  >  *Solucionar Problemas*  >  *Opções Avançadas*  >  *Config. de Inicialização*; <br>
 Execute no CMD como administrador: *`sfc /scannow`* para reparar arquivos de sistema; <br>
 Execute: *`chkdsk /f /r`* para verificar a integridade do disco (requer reinicialização); <br>
 Abra o  *Visualizador de Eventos* >  *Logs do Windows* >  *Sistema*  para identificar o componente com falha; <br>
 Reverta drivers instalados recentemente via *Gerenciador de Dispositivos*; <br>
 Execute o  *Diagnóstico de Memória do Windows*  para testar a integridade da RAM; <br>
 Se recorrente, suspeite de falha de hardware — escale para inspeção aprofundada.

|🏷️ Prevenções|
|-------------|

Mantenha drivers e Windows atualizados; monitore temperaturas do hardware; evite drivers não oficiais.

---

## 07 — Usuário não consegue entrar no Domínio (Active Directory)

> 🟠  **Gravidade: Alta | 👤 Afetados: Usuário único | 🗂️ Categoria: Rede / Autenticação**

|🚨 Problema|
|-----------|

O usuário recebe o erro *"A relação de confiança entre esta estação de trabalho e o domínio primário falhou"* ou não consegue autenticar.

|🕵️ Possíveis causas|
|-------------------|

Conta *AD* expirada/bloqueada, máquina fora de sincronia com o domínio ou credenciais incorretas.

|🛠️ Solução|
|---------|

 Abra *Usuários* e *Computadores do Active Directory (ADUC)* no controlador de domínio; <br>
 Pesquise a conta do usuário — verifique se está bloqueada ou desabilitada; <br>
 Desbloqueie a conta e redefina a senha se necessário; <br>
 Se for erro de relação de confiança: faça login com uma conta de administrador local; <br>
 Execute no *PowerShell: `Test-ComputerSecureChannel -Repair -Credential (Get-Credential)`*; <br>
 Se o reparo falhar: remova a máquina do domínio e a adicione novamente; <br>
 Verifique se o DNS da máquina aponta para o controlador de domínio.

|🏷️ Prevenções|
|---------|

Configure políticas de bloqueio de conta; use alertas do AD para tentativas de login repetidas com falha.

---

## 08 — Outlook não envia ou recebe E-mails

> 🟡 **Gravidade: Média | 👤 Afetados: Usuário único | 🗂️ Categoria: Software / E-mail**

|🚨 Problema|
|-----------|

O usuário relata que e-mails ficam presos na Caixa de Saída ou novas mensagens não chegam no Outlook.

|🕵️ Possíveis causas|
|-------------------|

Perfil do Outlook corrompido, configurações de servidor incorretas, caixa de entrada cheia ou modo *'Trabalhar Offline'* ativado.

|🛠️ Solução|
|----------|

 Verifique a barra de status na parte inferior do Outlook — confirme que não diz *'Trabalhando Offline'*; <br>
 Clique em *Enviar/Receber Todas as Pastas (`F9`)* para forçar a sincronização; <br>
 Verifique as configurações da conta (*Arquivo* > *Configurações de Conta*) para confirmar os dados do servidor; <br>
 Execute a ferramenta *Microsoft Support and Recovery Assistant (SaRA)* para diagnóstico automatizado; <br>
 Crie um novo perfil do Outlook: *Painel de Controle* > *Email* > *Mostrar Perfis* > *Adicionar*. <br>
 Verifique o tamanho da caixa de entrada — arquive e-mails antigos se estiver no limite; <br>
 Verifique se a conta não foi bloqueada por suspeita de envio de spam.

|🏷️ Prevenções|
|-------------|

Configure alertas de tamanho de caixa de entrada; treine usuários em arquivamento; use o SaRA preventivamente.

---

## 09 — Aplicativo fecha ao iniciar

> 🟡 **Gravidade: Média | 👤 Afetados: Usuário único | 🗂️ Categoria: Software / Aplicativo**

|🚨 Problema|
|-----------|

Um aplicativo específico fecha imediatamente após ser aberto, às vezes sem exibir nenhuma mensagem de erro.

|🕵️ Possíveis causas|
|-------------------|

Instalação corrompida, dependências ausentes (Visual C++, .NET) ou problemas de permissão.

|🛠️ Solução|
|----------|

 Verifique o *Visualizador de Eventos* > *Logs do Windows* > *Aplicativos* para o erro e módulo com falha; <br>
 Tente executar o aplicativo como Administrador (*clique direito > Executar como administrador*); <br>
 Desinstale e faça uma reinstalação limpa do aplicativo; <br>
 Instale ou repare os *Pacotes Redistribuíveis do Visual C++* e o *.NET Framework* da Microsoft; <br>
 Verifique se o antivírus está bloqueando o aplicativo — adicione uma exclusão temporariamente para testar; <br>
 Verifique as permissões do usuário na pasta de instalação do aplicativo; <br>
 Teste com um perfil de usuário diferente para descartar corrupção de perfil.

|🏷️ Prevenções|
|-------------|

Mantenha uma lista de softwares aprovados; mantenha as dependências atualizadas via gerenciamento de patches.

---

## 10 — Sem internet — Rede inteira afetada

> 🟠 **Gravidade: Alta | 👥 Afetados: Múltiplos usuários / Toda a empresa | 🗂️ Categoria: Rede / Infraestrutura**

|🚨 Problema|
|-----------|

Vários usuários ou toda a empresa perdem acesso à internet simultaneamente.

|🕵️ Possíveis causas|
|-------------------|

Falha no roteador/modem, queda do provedor (ISP), esgotamento do escopo DHCP ou *gateway* mal configurado.

|🛠️ Solução|
|----------|

 Verifique as luzes indicadoras do roteador/modem (sem luz WAN = problema no provedor); <br>
 Reinicie os equipamentos de rede em ordem: modem primeiro, depois roteador, depois switches (aguarde 30s cada); <br>
 Acesse o painel de administração do roteador e verifique o IP WAN — se em branco, o provedor não está fornecendo endereço; <br>
 Contate o provedor de internet para verificar se há quedas na área; <br>
 Se o IP WAN estiver presente mas sem internet: verifique as configurações de DNS no roteador (tente `8.8.8.8`); <br>
 Verifique o escopo DHCP no roteador — se todos os IPs estiverem em uso, aumente o intervalo do pool; <br>
 Documente a duração da interrupção e os usuários afetados para o relatório de incidente.

|🏷️ Prevenções|
|-------------|

Configure uma ferramenta de monitoramento de rede (ex: *PRTG, Zabbix*); mantenha o contato do provedor acessível; considere link de internet redundante.

---


## 11 — Infecção por Ransomware

> 🔴 **Gravidade: Crítica | 👥 Afetados: Um ou múltiplos usuários / Rede inteira | 🗂️ Categoria: Segurança / Malware**

> [!WARNING]
> ⚠️ **ATENÇÃO:** Este é um incidente crítico de segurança. Siga os passos na ordem exata abaixo. 

|🚨 Problema|
|-----------|

O usuário relata que arquivos foram criptografados e uma nota de resgate está visível na tela.

|🕵️ Possíveis causas|
|-------------------|

E-mail de phishing com anexo malicioso, download *drive-by* ou exploração de vulnerabilidade sem patch.

|🛠️ Solução|
|---------|

 **IMEDIATAMENTE** isole a máquina: desconecte o cabo de rede e desative o Wi-Fi; <br>
 **NÃO** desligue a máquina ainda — documente todos os processos em execução via *Gerenciador de Tarefas*; <br>
 Alerte a equipe de Segurança de TI e a gerência conforme o *Plano de Resposta a Incidentes*; <br>
 Identifique o tipo de ransomware usando o site ID Ransomware (*https://id-ransomware.malwarehunterteam.com*); <br>
 Verifique se há um descriptografador gratuito disponível em *'NoMoreRansom.org'* antes de considerar qualquer pagamento; <br>
 Restaure os dados afetados do backup limpo mais recente; <br>
 Formate e reinstale o sistema operacional na máquina infectada antes de reconectá-la à rede; <br>
 Realize uma revisão pós-incidente para identificar o vetor de ataque e aplicar correções.

|🏷️ Prevenções|
|-------------|

Implemente backups regulares offline (regra 3-2-1); treine usuários sobre phishing; aplique patches rapidamente; use ferramentas de detecção e resposta em endpoints (EDR).

---

## 12 — Falha no disco rígido (HD/SSD)

> 🔴 **Gravidade: Crítica | 👤 Afetados: Usuário único | 🗂️ Categoria: Hardware / Armazenamento**

|🚨 Problema|
|-----------|

O usuário relata que o computador está extremamente lento, emitindo sons de clique (HD) ou arquivos estão ficando inacessíveis.

|🕵️ Possíveis causas|
|-------------------|

Desgaste físico, setores defeituosos, corrupção de firmware ou defeito de fabricação.

|🛠️ Solução|
|----------|

 Execute o **CrystalDiskInfo** para verificar o status *S.M.A.R.T.* — se *'Atenção'* ou *'Ruim'*, inicie a recuperação de dados imediatamente; <br>
 Se ainda inicializável: faça backup de todos os dados críticos do usuário em um HD externo imediatamente; <br>
 Execute no CMD elevado: *`chkdsk /f /r`* (requer reinicialização); <br>
 Se o sistema não inicializar: use um pendrive Linux bootável para acessar e recuperar arquivos; <br>
 Use **Recuva** ou **TestDisk** para recuperação de arquivos excluídos, se necessário; <br>
 Substitua o disco com falha por um novo de capacidade igual ou maior; <br>
 Restaure o sistema operacional e os dados do backup no novo disco.

|🏷️ Prevenções|
|-------------|

Monitore dados *S.M.A.R.T* com ferramentas automatizadas; aplique políticas de backup; substitua proativamente discos com mais de 5 anos de uso.

---

## 13 — VPN não conecta (acesso remoto)

> 🟠 **Gravidade: Alta | 👥 Afetados: Um ou múltiplos usuários remotos | 🗂️ Categoria: Rede / Acesso Remoto**

|🚨 Problema|
|-----------|

O funcionário remoto não consegue conectar à VPN da empresa, recebendo erros de autenticação ou mensagens de tempo esgotado.

|🕵️ Possíveis causas|
|-------------------|

Login/senha incorretos, certificado expirado, firewall bloqueando portas de VPN ou cliente VPN desatualizado.

|🛠️ Solução|
|----------|

 Verifique se as credenciais de VPN do usuário estão corretas e se a conta não expirou; <br>
 Certifique-se de que o cliente VPN está atualizado — baixe a versão mais recente com a TI; <br>
 Verifique se as portas necessárias estão abertas: *`UDP 1194`* (OpenVPN), *`UDP 500/4500`* (IPSec/IKEv2), *`TCP 443`* (SSL VPN); <br>
 Alterne o protocolo VPN entre TCP e UDP nas configurações do cliente; <br>
 Desabilite temporariamente o *Firewall do Windows* e o antivírus para testar se estão bloqueando a conexão; <br>
 Verifique os logs do servidor VPN para códigos de erro específicos; <br>
 Se autenticação por certificado: verifique se o certificado não expirou e está corretamente instalado; <br>
 Teste com uma rede diferente (ex: roteador 4G) para descartar bloqueio do provedor de internet.

|🏷️ Prevenções|
|-------------|

Automatize a renovação de certificados; mantenha políticas de atualização do cliente VPN; monitore a disponibilidade do gateway VPN.

---

## 14 — Servidor sem Resposta / Serviço fora do ar

> 🔴 **Gravidade: Crítica| 👥 Afetados: Múltiplos usuários / Toda a Empresa | 🗂️ Categoria: Infraestrutura / Servidor**

 |🚨 Problema|
 |-----------|

Um servidor ou serviço crítico (ex: servidor de arquivos, e-mail, banco de dados) não está respondendo.

|🕵️ Possíveis causas|
|-------------------|

Esgotamento de recursos (CPU/RAM/disco), serviço com falha, hardware defeituoso ou problema de rede.

|🛠️ Solução|
|----------|

 Faça ping no servidor para verificar se está acessível: *`ping [ip-do-servidor] -t`*; <br>
 Tente acesso remoto via *RDP (Windows) ou SSH (Linux)*; <br>
 Se inacessível: use ferramentas de gerenciamento fora de banda (*iDRAC* para Dell, *iLO* para HP); <br>
 Verifique a utilização de recursos: *Gerenciador de Tarefas* (Windows) ou *`top`/`htop`* (Linux); <br>
 Se um serviço específico falhou: reinicie via *`services.msc`* ou: *`systemctl restart [servico]`*; <br>
 Revise os logs do sistema: *Visualizador de Eventos* (Windows) ou *`/var/log/syslog`* (Linux) para identificar a causa; <br>
 Se o disco estiver cheio: identifique arquivos grandes e arquive ou exclua conforme apropriado; <br>
 Se suspeitar de falha de hardware: escale imediatamente para a equipe de infraestrutura sênior; <br>
 Comunique o status da interrupção aos usuários afetados e à gerência.

|🏷️ Prevenções|
|-------------|

Implemente monitoramento de servidor (alertas de CPU, RAM, disco); agende janelas de manutenção regulares; mantenha runbooks documentados.



---

# 📋 Modelo de documentação

>  [!IMPORTANT]
>  A tabela abaixo é apenas um exemplo de como estruturar uma documentação, faça do seu jeito. Se você trabalha em um ambiente corporativo, provavelmente terá processos pré-estabelecidos para documentações. 

| Campo | Preencha com informações |
| --- | --- |
| **Título** |  |
| **Categoria** | Hardware / Software / Rede / Segurança |
| **Gravidade** | 🟢 Baixa / 🟡 Média / 🟠 Alta / 🔴 Crítica |
| **Afetados** | Usuário Único / Departamento / Toda a Empresa |
| **Problema** | O que o usuário relatou... |
| **Possíveis causas** | O que realmente (ou possívelmente) causou o problema... |
| **Solução** |  Primeiro passo /  Segundo passo /  Terceiro passo |
| **Prevenções** | Como evitar que isso aconteça novamente... |
| **Resolvido por** |  |
| **Data** |  |

---

# 💡 Boas práticas de documentação
 
## 📝 Como escrever uma documentação voltada para solução de problemas

 Sempre escreva em linguagem clara e simples — imagine que outras pessoas ou colegas eventualmente irão ler sua documentação;<br>
 Inclua mensagens de erro e códigos de erro exatos sempre que disponíveis;<br>
 Documente o que **NÃO** funcionou, não apenas o que funcionou — isso economiza tempo para a próxima pessoa;<br>
 Adicione capturas de tela sempre que possível (anexe ao chamado ou insira diretamente);<br>
 Revise e atualize os artigos quando uma solução melhor for encontrada; <br>
 Adicione palavras-chave relevantes em cada artigo para facilitar a busca.

## 💎 Boas práticas para ordem de serviço ou chamados (tickets)

  Sempre colete antes de começar: nome do usuário, nome da máquina, versão do SO e mensagem de erro exata; <br>
 Categorize os chamados corretamente desde o início — ajuda na análise de tendências; <br>
 Escale com contexto completo: o que você tentou, o que aconteceu, logs relevantes; <br>
 Feche chamados somente quando o usuário confirmar que o problema foi resolvido. <br>



---

</div>
