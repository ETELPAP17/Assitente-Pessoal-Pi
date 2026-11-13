# PROJECTO JARVIS

## Transformação do Pi Coding Agent numa assistente pessoal de inteligência artificial

**Documento de definição e visão do projecto**

**Data:** 13 de Novembro de 2026  
**Estado:** Definição e investigação da Fase 1  
**Núcleo tecnológico escolhido:** Pi Coding Agent  
**Linguagem principal do núcleo:** TypeScript

> [!important] Âmbito actual
> A prioridade imediata é transformar o Pi numa assistente pessoal funcional com uma interface gráfica CopilotKit ligada ao Pi; uma experiência apenas de terminal não chega. O framework, a plataforma Web de gestão, os múltiplos agentes, a voz e as integrações IoT são objectivos futuros. Consultar [[Fase 1 - Assistente pessoal]] para as decisões actuais. A implementação ainda não começou; primeiro será escolhido um caso de uso funcional.

---

# 1. Visão geral

O projecto consiste em transformar o **Pi Coding Agent**, um agente de inteligência artificial desenvolvido em TypeScript, numa assistente pessoal inspirada no conceito do JARVIS, do universo Iron Man.

Não pretendemos reproduzir a ficção científica nem construir um sistema com capacidades tecnológicas impossíveis ou indisponíveis actualmente.

O objectivo é desenvolver uma assistente pessoal funcional, capaz de compreender instruções em linguagem natural, conversar por texto e voz, utilizar o computador, interagir com aplicações, pesquisar na Internet, executar tarefas, recordar informações relevantes e comunicar com dispositivos físicos.

A estratégia consiste em aproveitar o máximo possível das tecnologias, ferramentas, extensões e projectos open-source existentes.

**Não queremos construir outro agente de IA do zero. Queremos transformar um agente existente numa assistente pessoal.**

# 2. Objectivo principal

Criar uma assistente pessoal de IA que funcione como uma interface inteligente entre o utilizador e o seu ambiente digital e físico.

A assistente deverá conseguir:

- Compreender pedidos feitos em linguagem natural.
- Conversar por texto e voz.
- Interpretar instruções e organizar tarefas.
- Utilizar ferramentas para executar acções.
- Controlar aplicações e recursos do computador.
- Navegar e interagir com páginas Web.
- Consultar, guardar e recuperar informações.
- Executar tarefas com múltiplas etapas.
- Comunicar com outros agentes de IA.
- Interagir com dispositivos electrónicos e sistemas IoT.
- Pedir autorização antes de executar operações sensíveis.

O objectivo não é apenas responder a perguntas, mas também **conseguir agir em nome do utilizador, dentro das permissões estabelecidas**.

# 3. Escolha do núcleo tecnológico: Pi Coding Agent

O Pi Coding Agent, disponível em [pi.dev](https://pi.dev/), foi escolhido como núcleo do projecto.

É um agente de programação extensível, desenvolvido em TypeScript, cuja filosofia privilegia primitivas simples e extensibilidade em vez de concentrar todas as funcionalidades num sistema fechado.

O Pi já disponibiliza mecanismos importantes:

- Comunicação com modelos de linguagem (LLMs).
- Ciclo de execução de agente e utilização de ferramentas.
- Gestão de contexto e sessões.
- Histórico de interacções.
- Extensões em TypeScript.
- Registo de ferramentas personalizadas.
- Comandos e interfaces extensíveis.
- Gestão de estado persistente pelas extensões.
- Integração com MCP.
- SDK e mecanismos de comunicação por RPC.

A sua arquitectura permite acrescentar funcionalidades sem precisar de reconstruir o núcleo.

## 3.1. Porquê Pi?

A escolha não se baseia simplesmente na quantidade de funcionalidades que o Pi oferece de origem.

Baseia-se principalmente na sua filosofia e arquitectura.

O Pi oferece um núcleo relativamente minimalista, extensível e adaptável. Isso permite seleccionar apenas os componentes necessários para construir a nossa assistente.

Em vez de ficarmos dependentes das funcionalidades e decisões de arquitectura de uma plataforma fechada, podemos combinar ferramentas independentes e criar integrações específicas.

## 3.2. O que não estamos a fazer

Não estamos a:

- Desenvolver um agente de IA do zero.
- Criar um novo motor de raciocínio.
- Treinar um modelo de linguagem próprio.
- Reconstruir protocolos de comunicação existentes.
- Criar ferramentas de controlo do computador quando já existem soluções.
- Desenvolver sistemas de automação que já estejam disponíveis.
- Construir uma plataforma de orquestração complexa sem necessidade.

O Pi será o ponto de partida e o motor principal.

# 4. Arquitectura conceptual

A arquitectura será construída por camadas, aproveitando tecnologias independentes.

## 4.1. Núcleo: agente principal

**Pi Coding Agent**

Responsável por:

- Receber instruções.
- Interagir com o modelo de linguagem.
- Interpretar objectivos.
- Seleccionar ferramentas.
- Executar ciclos de acção.
- Gerir contexto e sessões.
- Coordenar a utilização das integrações disponíveis.

## 4.2. Inteligência artificial: LLMs

Os modelos de linguagem serão responsáveis pelo raciocínio, interpretação, compreensão e geração de respostas.

O Pi funciona como agente que utiliza esses modelos.

Poderemos utilizar APIs de diferentes fornecedores, conforme o custo, qualidade, disponibilidade e compatibilidade.

Não é necessário treinar um modelo próprio.

## 4.3. Extensões e ferramentas

As extensões serão fundamentais para transformar o Pi numa assistente pessoal.

Poderão acrescentar:

- Novas ferramentas.
- Novos comandos.
- Integrações com aplicações.
- Interfaces personalizadas.
- Gestão de memória.
- Execução de tarefas em segundo plano.
- Delegação de tarefas.
- Controlo de permissões.
- Integrações com serviços externos.

A prioridade será encontrar extensões e pacotes já desenvolvidos pela comunidade Pi.

Quando não existir uma solução adequada, poderemos desenvolver uma extensão própria em TypeScript.

## 4.4. Integração com o ambiente digital

A assistente deverá conseguir comunicar com diferentes aplicações e serviços.

Não existe um único mecanismo universal para controlar todos os programas. A integração dependerá das interfaces disponibilizadas por cada aplicação.

Os mecanismos considerados são:

|Tecnologia|Utilização|
|---|---|
|MCP|Expor ferramentas e recursos aos agentes|
|API|Comunicação directa com aplicações e serviços|
|CLI|Controlar programas através do terminal|
|Computer Use|Interagir com interfaces gráficas|
|Playwright|Automatizar navegadores e aplicações Web|
|WebSocket|Comunicação contínua e eventos|
|RPC|Comunicação entre processos e serviços|
|OpenAPI|Descrição e integração de APIs HTTP|
|A2A|Comunicação entre agentes|

A escolha será feita de acordo com cada integração.

## 4.5. Voz e conversação

A assistente deverá permitir uma experiência de conversação natural.

Capacidades pretendidas:

- Reconhecimento de voz (STT).
- Síntese de voz (TTS).
- Entrada por microfone.
- Reprodução de respostas por áudio.
- Conversação por texto.
- Possibilidade de activação por palavra-chave ou mecanismo equivalente.

Deveremos investigar soluções gratuitas e open-source, considerando também o suporte à língua portuguesa.

## 4.6. Memória

A assistente deverá conseguir manter informações relevantes para interacções futuras.

A memória poderá incluir:

- Preferências do utilizador.
- Informações fornecidas pelo utilizador.
- Histórico de tarefas.
- Contexto de projectos.
- Conhecimento armazenado.
- Registos de operações.

A solução deverá ser persistente, pesquisável e controlável pelo utilizador.

## 4.7. Automação e autonomia

A assistente deverá conseguir executar tarefas compostas por várias etapas.

Exemplo:

O utilizador pede para pesquisar determinado assunto, organizar os resultados, criar um documento e guardá-lo numa pasta.

A assistente deverá conseguir decompor o pedido, seleccionar ferramentas, executar as etapas e apresentar o resultado.

A autonomia deverá ser acompanhada por mecanismos de segurança e autorização.

## 4.8. Dispositivos físicos e IoT

Uma das possibilidades mais interessantes do projecto é a integração com o mundo físico.

A assistente poderá comunicar com:

- ESP32.
- Arduino.
- Sensores.
- Actuadores.
- Sistemas de iluminação.
- Dispositivos ligados à rede.
- Sistemas de automação residencial.
- Outros equipamentos electrónicos.

Tecnologias e projectos a investigar:

- Home Assistant.
- ESPHome.
- MQTT.
- HTTP.
- WebSocket.
- Comunicação Serial.
- APIs e servidores MCP para IoT.

O Home Assistant poderá funcionar como uma camada de integração entre a assistente e os dispositivos físicos.

# 5. Identidade do sistema: JARVIS

O Pi será o motor tecnológico, mas a experiência final deverá apresentar-se como uma assistente pessoal.

O nome JARVIS representa a identidade e a experiência que pretendemos construir.

A distinção é importante:

- **Pi:** motor de agente e execução.
- **LLM:** inteligência e raciocínio.
- **Extensões:** funcionalidades adicionais.
- **Ferramentas:** capacidades de acção.
- **Integrações:** comunicação com aplicações e dispositivos.
- **JARVIS:** identidade, interface e experiência da assistente pessoal.

Para a Fase 1, a interface de terminal original do Pi não é suficiente: a experiência pretendida exige uma interface gráfica CopilotKit ligada ao Pi. O terminal pode continuar a ser utilizado para desenvolvimento e diagnóstico.

Poderemos explorar uma interface própria ou reutilizar uma interface existente, recorrendo aos mecanismos de RPC, SDK ou outros meios de comunicação disponibilizados pelo Pi.

# 6. Princípios de desenvolvimento

O projecto deverá obedecer aos seguintes princípios.

### 6.1. Reutilizar antes de desenvolver

Antes de programar uma funcionalidade, procurar se já existe um projecto que a implemente.

### 6.2. Integrar antes de reinventar

Se já existir uma ferramenta capaz de executar determinada tarefa, devemos procurar uma forma de a disponibilizar ao Pi.

### 6.3. Extensibilidade

A arquitectura deverá permitir acrescentar capacidades sem reconstruir o sistema.

### 6.4. Modularidade

As funcionalidades deverão ser independentes sempre que possível.

A falha de uma integração não deverá comprometer todo o sistema.

### 6.5. Open-source e baixo custo

Dar prioridade a:

- Software gratuito.
- Projectos open-source.
- Licenças que permitam utilização e modificação.
- APIs económicas.
- Ferramentas que possam funcionar localmente.
- Soluções que não exijam hardware dispendioso.

### 6.6. Simplicidade operacional

Evitar dependências desnecessárias, instalações excessivamente complexas e infraestruturas difíceis de manter.

### 6.7. Segurança

A assistente deverá trabalhar com permissões controladas.

Operações como apagar ficheiros, enviar mensagens, efectuar pagamentos, alterar configurações importantes ou controlar dispositivos sensíveis deverão exigir autorização adequada.

As extensões também deverão ser verificadas antes da instalação, pois podem executar código com as permissões do próprio processo Pi.

# 7. Estratégia de investigação

Antes de começar a desenvolver funcionalidades, precisamos de realizar uma auditoria do ecossistema.

A investigação deverá identificar soluções existentes e avaliar a possibilidade de integração.

|Área|O que procurar|
|---|---|
|Pi Extensions|Extensões e pacotes existentes|
|Computer Use|Controlo do ambiente de trabalho|
|Browser|Navegação e automação Web|
|Voice|STT, TTS e activação por voz|
|Memory|Memória persistente|
|Subagents|Delegação e coordenação|
|Automation|Agendamento e tarefas em segundo plano|
|IoT|Home Assistant, ESPHome e MQTT|
|Interface|Interfaces desktop e conversacionais|
|Security|Permissões, isolamento e confirmação de acções|

Cada solução encontrada deverá ser avaliada segundo:

1. Funcionalidade.
2. Compatibilidade com Pi.
3. Compatibilidade com Windows ou o sistema operativo escolhido.
4. Licença.
5. Estado de manutenção.
6. Dependências.
7. Facilidade de instalação.
8. Consumo de recursos.
9. Possibilidade de integração.
10. Maturidade e fiabilidade.

## 7.1. Classificação das soluções

Todas as soluções identificadas deverão ser classificadas em quatro categorias:

**A — Instalação imediata:** já existe uma solução pronta e compatível.

**B — Configuração:** a solução existe, mas exige configuração.

**C — Adaptador ou integração:** a solução existe, mas precisa de uma ligação ao Pi através de MCP, API, CLI, RPC ou extensão.

**D — Desenvolvimento próprio:** não existe uma solução suficientemente adequada e será necessário desenvolver.

Esta classificação ajudará a evitar trabalho desnecessário.

# 8. Estratégia de implementação

O desenvolvimento será feito progressivamente, sem prazos artificiais nem implementação simultânea de funcionalidades ainda não validadas.

## Fase actual — Assistente pessoal baseada no Pi

1. Definir em conjunto um primeiro caso de uso pequeno.
2. Derivar desse caso de uso as ferramentas e permissões mínimas.
3. Validar a integração Pi + CopilotKit + AG-UI, usando o template comunitário `pi-agui` como referência após revisão.
4. Implementar apenas o percurso necessário para esse caso de uso.
5. Testar o comportamento real, incluindo autorização e erros.
6. Decidir sobre memória pessoal persistente apenas quando houver uma necessidade concreta.

O documento [[Fase 1 - Assistente pessoal]] é a referência de âmbito e decisões desta fase.

## Fases futuras

Depois de a assistente pessoal estar validada, poderemos acrescentar voz, mais ferramentas, memória persistente e integrações. Só posteriormente será considerada a extracção de um framework genérico, do Integrador e da plataforma de gestão. A integração IoT depende também da definição da L.U.

# 9. Critérios de sucesso

Os critérios da primeira versão serão definidos a partir do caso de uso escolhido. Não se exige que a primeira entrega cubra desde logo todas as capacidades de longo prazo.

Como critérios gerais, a solução deverá:

1. Receber uma instrução em linguagem natural.
2. Executar correctamente o caso de uso definido, usando apenas as ferramentas necessárias.
3. Comunicar o resultado e eventuais erros ao utilizador.
4. Respeitar as permissões e aprovações definidas para esse caso.

Navegação Web, tarefas multi-etapa, voz e dispositivos físicos só serão critérios da primeira entrega se forem necessários ao caso de uso escolhido; caso contrário, ficam para fases posteriores.

# 10. Decisões tomadas e aspectos pendentes

## Decisões tomadas

- O Pi Coding Agent será o núcleo principal.
- O projecto será desenvolvido sobre o ecossistema existente do Pi.
- A identidade e experiência final serão inspiradas no JARVIS.
- A linguagem principal para extensões próprias será TypeScript.
- A prioridade será reutilizar soluções existentes.
- MCP, APIs, CLI, RPC e outros mecanismos serão utilizados conforme a necessidade.
- A primeira fase concentra-se em transformar o Pi numa assistente pessoal funcional no computador.
- CopilotKit é a interface gráfica seleccionada para a Fase 1; AG-UI é a direcção de protocolo, mas a ligação concreta ao Pi ainda não foi validada.
- O template comunitário `pi-agui` é uma referência a inspeccionar, não uma integração ou dependência aprovada.
- OpenUI de openui.com foi investigado, mas não seleccionado para esta fase.
- O framework e as integrações com dispositivos físicos são posteriores à validação da assistente.
- A solução deverá privilegiar software gratuito e open-source.

## Aspectos ainda por decidir

- Sistema operativo e configuração exacta do computador.
- Modelo de linguagem e fornecedor de API.
- Primeiro caso de uso funcional.
- Forma de integrar Pi com AG-UI/CopilotKit.
- Ferramentas estritamente necessárias para esse caso de uso.
- Necessidade de memória para além das sessões do Pi.
- Permissões e isolamento adequados ao caso de uso.
- Voz, delegação, Home Assistant, ESP32 e outros dispositivos, em fases posteriores.

Estas decisões deverão ser tomadas com base na investigação e nos testes, não em suposições.

# 11. Regra fundamental do projecto

O princípio que orientará todas as decisões será:

**Não vamos desenvolver funcionalidades só porque conseguimos programá-las. Primeiro vamos procurar se alguém já as desenvolveu, se podemos reutilizá-las e se podemos integrá-las no Pi. Só desenvolveremos aquilo que realmente estiver em falta.**

O nosso objectivo é aproveitar o trabalho de toda uma comunidade de desenvolvimento para construir, com os recursos disponíveis, uma assistente pessoal cada vez mais capaz.

---

**Visão final:** transformar progressivamente o Pi Coding Agent numa assistente pessoal inteligente e extensível, capaz de compreender, conversar, recordar, executar tarefas, controlar aplicações e, em fases futuras, interagir com dispositivos físicos.

Uma versão realista do conceito JARVIS, construída sobre tecnologias que já existem e evoluindo progressivamente.

---

**Estado actual e fonte de verdade:** a antiga estimativa de entrega em uma semana e a lista ampla de capacidades não definem o âmbito imediato. A Fase 1 avança devagar e começa pela escolha do primeiro caso de uso, conforme [[Fase 1 - Assistente pessoal]].