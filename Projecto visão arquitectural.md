PROJECTO JARVIS

Framework de Assistentes Pessoais de Inteligência Artificial baseado no Pi

Documento de arquitectura e definição do projecto
Versão: 1.0
Data: Novembro de 2026
Estado: Arquitectura conceptual — preparação para implementação

---

> [!important] Âmbito e sequência actuais
> Este documento descreve a visão futura do framework. **A prioridade agora é transformar o Pi numa assistente pessoal funcional com interface gráfica CopilotKit ligada ao Pi**; uma experiência apenas de terminal não chega. A interface CopilotKit está seleccionada, mas a integração Pi ↔ AG-UI ainda precisa de validação. O template comunitário `pi-agui` é uma referência, não uma integração oficial nem uma dependência aprovada. OpenUI de openui.com foi investigado, mas não seleccionado. O primeiro caso de uso ainda está por definir. Consultar [[Fase 1 - Assistente pessoal]] e [[AGENTS]] para o âmbito e as regras de trabalho actuais.

1. Visão geral

Como visão de longo prazo, o projecto poderá desenvolver um framework capaz de transformar o Pi Coding Agent numa plataforma de assistentes pessoais de inteligência artificial. Esta visão não representa o âmbito de implementação imediato.

A intenção não é desenvolver um agente de IA, um sistema de ferramentas, uma interface ou uma infraestrutura de comunicação inteiramente do zero.

O projecto parte de uma estratégia de integração: aproveitar tecnologias, frameworks, protocolos, bibliotecas e aplicações existentes, desenvolvendo apenas os componentes necessários para os unir e oferecer uma experiência integrada.

O Pi será o motor inicial de execução dos agentes. O nosso framework acrescentará a estrutura necessária para transformar esse motor numa assistente pessoal completa, extensível, configurável e capaz de interagir com o ambiente digital e físico.

A arquitectura também deverá permitir que, no futuro, diferentes motores de agentes possam ser utilizados sem reconstruir todo o ecossistema.

1.1. Objectivo principal

Construir uma plataforma que permita criar, configurar, executar e gerir assistentes pessoais de IA, com capacidades como:

- Conversação por texto e voz.
- Compreensão de linguagem natural.
- Execução de tarefas e utilização de ferramentas.
- Controlo do computador e das aplicações.
- Navegação e interacção com a Web.
- Memória persistente.
- Integração com serviços e APIs.
- Comunicação com outros agentes de IA.
- Integração com dispositivos físicos e IoT.
- Gestão de permissões e aprovações.
- Personalização de personalidade, comportamento e capacidades.

A primeira implementação será uma assistente pessoal inspirada no conceito JARVIS.

2. Estratégia tecnológica

O princípio fundamental é:

Reutilizar antes de desenvolver. Integrar antes de reinventar.

Em vez de desenvolver todas as funcionalidades, vamos aproveitar soluções existentes e criar uma camada de integração que as transforme num sistema coerente.

A tecnologia deve ser seleccionada segundo os seguintes critérios:

1. Existência de implementação funcional.
2. Código aberto ou licença compatível com o projecto.
3. Facilidade de integração.
4. Baixo custo de operação.
5. Compatibilidade com o ambiente de execução.
6. Manutenção e actividade do projecto.
7. Possibilidade de substituição futura.
8. Segurança e controlo sobre os dados.

Não pretendemos construir imediatamente um framework público completo. Primeiro queremos validar uma assistente funcional.

3. Arquitectura geral

A arquitectura será híbrida, combinando uma plataforma Web com um runtime local.

A plataforma Web será responsável pela configuração e gestão das assistentes. O runtime local será responsável pela execução dos agentes e pela interacção com o computador e dispositivos físicos.

3.1. Diagrama conceptual

flowchart TB
    USER["Utilizador"]

    subgraph WEB["PLATAFORMA WEB"]
        UI["CopilotKit — Interface"]
        BUILDER["Gestão de assistentes"]
        CONFIG["Perfis e configurações"]
        CAP["Gestão de capacidades"]
        UI <--> BUILDER
        BUILDER --> CONFIG
        BUILDER --> CAP
    end

    subgraph FRAMEWORK["FRAMEWORK DE ASSISTENTES"]
        CORE["Core / Orquestração"]
        ID["Identidade"]
        MEM["Memória"]
        SEC["Permissões e segurança"]
        AGENTS["Gestão de agentes"]
    end

    subgraph RUNTIME["RUNTIME LOCAL"]
        PI["Pi Agent"]
        EXT["Extensões Pi"]
        INTEG["INTEGRADOR"]
        COMPUTER["Controlo do computador"]
        BROWSER["Browser"]
        VOICE["Voz"]
    end

    subgraph PHYSICAL["AMBIENTE FÍSICO"]
        LU["L.U"]
        ESP["ESP32"]
        ARD["Arduino"]
        IOT["Outros dispositivos"]
    end

    USER <--> UI
    UI <--> CORE
    CORE <--> PI
    CORE <--> ID
    CORE <--> MEM
    CORE <--> SEC
    CORE <--> AGENTS
    PI <--> EXT
    EXT <--> INTEG
    PI <--> COMPUTER
    PI <--> BROWSER
    PI <--> VOICE
    INTEG <--> LU
    LU <--> ESP
    LU <--> ARD
    LU <--> IOT

3.2. Camadas

A. Plataforma Web

Responsável por criar e gerir assistentes pessoais.

Funcionalidades previstas:

- Criar assistentes.
- Definir identidade e personalidade.
- Configurar instruções.
- Seleccionar modelos de IA.
- Gerir capacidades e extensões.
- Configurar permissões.
- Consultar sessões e histórico.
- Gerir dados e memória.
- Administrar integrações.

A plataforma Web não deverá aceder directamente ao computador do utilizador.

B. Interface — CopilotKit

Para a Fase 1, o CopilotKit está seleccionado como interface gráfica necessária para conversar com o Pi. A interface de terminal pode continuar a ser usada para desenvolvimento, mas não satisfaz sozinha a experiência pretendida. A integração efectiva com o Pi ainda precisa de validação.

Funcionalidades pretendidas:

- Interface de chat.
- Streaming das respostas.
- Apresentação da actividade do agente.
- Visualização de resultados de ferramentas.
- Aprovações humanas.
- Estado partilhado entre interface e agente.
- Interfaces dinâmicas, quando necessário.
- Possibilidade de incorporar voz.

Não pretendemos reconstruir manualmente todos estes componentes.

C. Framework de assistentes

Esta será a camada principal desenvolvida no projecto.

O seu papel é transformar o Pi num motor reutilizável de assistentes pessoais.

Responsabilidades:

- Organizar a identidade das assistentes.
- Gerir configurações e perfis.
- Integrar memória.
- Registar e disponibilizar capacidades.
- Gerir permissões.
- Coordenar ferramentas e extensões.
- Integrar diferentes protocolos.
- Gerir sessões e contexto.
- Ligar a interface ao runtime.
- Permitir futura substituição do motor de execução.

D. Runtime local

É o ambiente onde as assistentes executam as suas tarefas.

O Pi será o runtime inicial.

O runtime local poderá:

- Executar agentes.
- Aceder ao computador mediante permissões.
- Interagir com aplicações.
- Controlar browsers.
- Executar ferramentas.
- Comunicar com o Integrador.
- Utilizar serviços locais.
- Processar eventos.
- Interagir com dispositivos físicos.

E. Ambiente físico

Representa o conjunto de dispositivos que a assistente poderá controlar.

Exemplos:

- ESP32.
- Arduino.
- Sensores.
- Actuadores.
- Sistemas de iluminação.
- Equipamentos domésticos.
- Home Assistant.
- Dispositivos IoT.

A comunicação com estes dispositivos será realizada através do Integrador e da L.U.

4. Pi — motor de execução

O Pi será a base tecnológica inicial do projecto.

É um agente extensível desenvolvido em TypeScript, com mecanismos de execução, contexto, sessões, ferramentas e extensões.

A escolha do Pi permite aproveitar uma infraestrutura de agente existente, evitando construir um novo ciclo de execução de LLM.

4.1. Responsabilidades do Pi

- Receber instruções.
- Interagir com o modelo de linguagem.
- Manter contexto de conversação.
- Executar chamadas de ferramentas.
- Processar resultados.
- Coordenar a execução das tarefas.
- Utilizar extensões.
- Comunicar com serviços externos.

4.2. Extensibilidade

O Pi permite acrescentar capacidades através de extensões.

Estas poderão disponibilizar:

- Ferramentas personalizadas.
- Comandos.
- Eventos.
- Integrações.
- Acesso a serviços.
- Adaptadores.
- Capacidades específicas do projecto.

A nossa implementação deverá aproveitar este mecanismo sempre que possível.

4.3. Independência do runtime

Embora o Pi seja o motor inicial, o framework não deverá ficar estruturalmente dependente dele.

A comunicação entre o framework e o motor deverá ser organizada através de uma camada de integração.

Assim, uma futura substituição do Pi por outro runtime não deverá obrigar à reconstrução da interface, da memória, das configurações ou do Integrador.

5. Framework de assistentes pessoais

O framework será a camada responsável por transformar um agente extensível numa assistente pessoal organizada.

5.1. Módulos principais

Módulo| Responsabilidade
Core| Coordenação e integração dos componentes
Identity| Personalidade, nome e instruções
Models| Configuração dos modelos de IA
Memory| Memória persistente e recuperação
Tools| Gestão das ferramentas
Agents| Gestão e delegação entre agentes
Computer| Capacidades de controlo do computador
Browser| Navegação e automação Web
Voice| Reconhecimento e síntese de voz
Integrations| Integrações com serviços externos
Security| Permissões, aprovações e isolamento
Sessions| Gestão de conversas e sessões
Interface| Integração com interfaces de utilizador

Estes módulos representam responsabilidades arquitecturais. Não significa que cada um precise de ser um serviço ou processo independente.

A implementação inicial deve evitar complexidade desnecessária.

5.2. Identidade das assistentes

Cada assistente deverá poder possuir:

- Nome.
- Descrição.
- Personalidade.
- Instruções principais.
- Modelo de IA.
- Configurações.
- Ferramentas autorizadas.
- Memória.
- Permissões.
- Interface.
- Capacidades activadas.

A configuração deverá ser separada da implementação técnica.

5.3. Memória

A memória não deverá depender exclusivamente do histórico de conversação do Pi.

Pretendemos um sistema próprio, capaz de:

- Guardar informações importantes.
- Recuperar informações anteriores.
- Manter contexto entre sessões.
- Armazenar preferências.
- Consultar conhecimento.
- Organizar dados por assistente e utilizador.

O armazenamento poderá começar com SQLite, evoluindo apenas quando existir uma necessidade comprovada.

6. Integrador — adaptador universal de dispositivos

O Integrador é um componente adicional desenvolvido no âmbito do projecto.

A sua função é estabelecer a ligação entre o Pi e os dispositivos físicos, utilizando duas interfaces de comunicação diferentes:

1. Do lado do Pi, funciona como uma extensão que disponibiliza ferramentas ao agente.
2. Do lado dos dispositivos, comunica através da L.U.

O Integrador será a ponte entre a inteligência do agente e o ambiente físico.

6.1. Objectivo

Permitir que o Pi utilize dispositivos físicos sem precisar de conhecer os detalhes internos de comunicação de cada equipamento.

O Pi deverá trabalhar com capacidades compreensíveis, como:

- Ligar iluminação.
- Desligar iluminação.
- Consultar temperatura.
- Ler um sensor.
- Activar um motor.
- Consultar o estado de um equipamento.
- Receber notificações de eventos.

O Integrador será responsável por traduzir essas operações para a comunicação específica da L.U.

6.2. Arquitectura do Integrador

flowchart TB
    PI["Pi Agent"]

    subgraph INTEGRATOR["INTEGRADOR"]
        EXT["Extensão Pi"]
        CORE["Núcleo do Integrador"]
        REG["Registo e descoberta"]
        MAP["Mapeamento de capacidades"]
        CONV["Conversão de mensagens"]
        EVENTS["Gestão de eventos"]
        SEC["Controlo de permissões"]
        LU["Interface L.U"]

        EXT <--> CORE
        CORE <--> REG
        CORE <--> MAP
        CORE <--> CONV
        CORE <--> EVENTS
        CORE <--> SEC
        CORE <--> LU
    end

    subgraph DEVICES["DISPOSITIVOS"]
        D1["ESP32"]
        D2["Arduino"]
        D3["Outros dispositivos"]
    end

    PI <--> EXT
    LU <--> D1
    LU <--> D2
    LU <--> D3

6.3. Interface com o Pi

O Integrador deverá disponibilizar ferramentas através de uma extensão Pi.

Exemplos conceptuais:

- "list_devices"
- "get_device_info"
- "get_device_state"
- "execute_device_action"
- "subscribe_device_events"

Estes nomes são exemplos de ferramentas a definir, não APIs já implementadas.

A extensão deverá permitir que o Pi descubra as capacidades disponíveis e execute operações autorizadas.

6.4. Interface com a L.U

A L.U será a camada utilizada pelo Integrador para comunicar com os dispositivos.

O Integrador não deverá obrigar o Pi a compreender a estrutura das mensagens L.U.

Será responsável por:

- Converter operações em mensagens L.U.
- Enviar comandos.
- Receber respostas.
- Interpretar estados.
- Gerir eventos.
- Identificar dispositivos.
- Mapear capacidades.
- Tratar falhas de comunicação.

Os detalhes da L.U, incluindo formato de mensagens, transporte, endereçamento, descoberta e autenticação, deverão seguir a especificação própria desse sistema.

6.5. Exemplo de funcionamento

Pedido do utilizador:

"Jarvis, liga a iluminação do meu quarto."

Fluxo:

1. O utilizador envia o pedido.
2. O Pi interpreta a intenção.
3. O Pi identifica a ferramenta do Integrador.
4. A extensão envia a operação ao Integrador.
5. O Integrador identifica o dispositivo correspondente.
6. A operação é convertida numa mensagem L.U.
7. O dispositivo recebe o comando.
8. O dispositivo executa a operação.
9. A resposta regressa pela L.U.
10. O Integrador interpreta o resultado.
11. O Pi recebe o resultado.
12. A assistente informa o utilizador.

6.6. Comunicação inversa

O Integrador também deverá suportar comunicação iniciada pelos dispositivos.

Exemplo:

1. Um sensor detecta movimento.
2. O dispositivo envia um evento pela L.U.
3. O Integrador recebe o evento.
4. O evento é identificado e processado.
5. O Pi recebe a informação através de um mecanismo de eventos.
6. A assistente poderá executar uma acção previamente autorizada.

Esta capacidade permite construir sistemas reactivos, não apenas sistemas controlados por comandos do utilizador.

6.7. Independência do Integrador

O Integrador deverá ser independente do Pi.

A extensão Pi será apenas uma das interfaces de utilização.

No futuro, o mesmo Integrador poderá ser utilizado por:

- Outros agentes de IA.
- Aplicações desktop.
- Aplicações Web através de um runtime autorizado.
- Sistemas de automação.
- Outros serviços compatíveis com a L.U.

Esta independência é importante para transformar o Integrador num componente reutilizável do ecossistema.

7. Protocolos e mecanismos de integração

O projecto não deverá depender de um único protocolo.

Cada tecnologia será utilizada conforme a responsabilidade que resolve.

Tecnologia| Função no projecto
AG-UI| Comunicação entre agente e interface
MCP| Integração com ferramentas, recursos e serviços
A2A| Comunicação e delegação entre agentes
A2UI| Representação de interfaces geradas por agentes
APIs HTTP| Integração com aplicações e serviços
CLI| Utilização de programas e ferramentas de terminal
RPC| Comunicação entre processos e runtimes
WebSocket| Comunicação bidireccional e eventos em tempo real
MQTT| Comunicação com sistemas IoT, quando aplicável
L.U| Comunicação entre o Integrador e os dispositivos compatíveis

Os protocolos não são concorrentes directos.

Por exemplo, o MCP pode disponibilizar ferramentas ao agente, enquanto a L.U realiza a comunicação específica com um equipamento.

O A2A não substitui o MCP, e o AG-UI não substitui a comunicação com dispositivos.

Cada camada deverá utilizar o mecanismo mais adequado.

8. Interface e integração Pi

Para a primeira assistente, Pi é o motor e CopilotKit é a interface gráfica seleccionada. AG-UI é a direcção para a comunicação agente-interface. A integração concreta tem de ser validada num caso de uso pequeno; uma interface apenas de terminal não satisfaz o requisito.

8.1. Template comunitário `pi-agui`

O catálogo Pi inclui o pacote [`pi-agui`](https://pi.dev/packages/pi-agui), que gera um template de aplicação com Pi SDK, AG-UI, backend Express e frontend React/Vite. O template implementa uma ligação Pi–AG-UI e pode ser estudado como referência ou protótipo.

Limites conhecidos:

- É um template comunitário, não uma integração oficial Pi–CopilotKit.
- Inclui uma interface própria; não usa a UI do CopilotKit.
- O template publicado declara a dependência `@mariozechner/pi-coding-agent`, marcada como depreciada em favor de `@earendil-works/pi-coding-agent`.
- A compatibilidade com a versão actual do Pi, a segurança e a adequação do código precisam de ser verificadas antes de reutilizar ou instalar.

Portanto, não se deve assumir que seja necessário escrever todo o adaptador desde o início, nem adoptar o template completo sem avaliação. A comparação deve incluir CopilotKit, AG-UI, Pi SDK, `pi-agui` e, como alternativa de interface, Pi Outpost.

O CopilotKit alerta que o seu `BuiltInAgent` chama directamente o modelo e substitui um agente existente; não é a opção adequada quando a intenção é encaminhar a conversa para Pi.

8.2. OpenUI (openui.com)

OpenUI oferece um Agent Interface React para uma experiência de chat completa ligada a um backend existente e também um renderer OpenUI Lang que pode ser incorporado em CopilotKit. Foi investigado, mas não seleccionado para a Fase 1. Poderá ser reconsiderado se houver um requisito de interface generativa ou se CopilotKit não cumprir os requisitos; não há ainda integração Pi pronta confirmada.

8.3. Fluxo mínimo proposto

1. O frontend envia a mensagem ao runtime local.
2. O runtime associa a conversa a uma sessão Pi.
3. O Pi processa o pedido e emite eventos.
4. O runtime aplica as permissões antes de executar qualquer ferramenta.
5. Eventos e resposta são entregues ao frontend através da integração AG-UI escolhida.

Este fluxo é uma proposta para validação, não uma arquitectura já implementada.

9. Comunicação entre plataforma Web e runtime local

A arquitectura híbrida exige uma ligação segura entre a plataforma Web e o runtime local.

O runtime deverá actuar como intermediário de confiança.

A plataforma Web poderá:

- Configurar assistentes.
- Enviar instruções autorizadas.
- Consultar estados.
- Gerir configurações.
- Consultar sessões.

O runtime local será responsável por:

- Executar tarefas.
- Aceder ao computador.
- Utilizar ferramentas locais.
- Comunicar com dispositivos.
- Aplicar permissões.
- Pedir confirmações quando necessário.

A comunicação poderá utilizar HTTPS, WebSocket ou RPC, dependendo dos requisitos concretos.

A plataforma Web não deverá obter acesso arbitrário ao computador.

10. Segurança e permissões

A segurança deverá ser uma característica transversal.

Não podemos deixar que o modelo de IA tenha autoridade ilimitada sobre o computador ou dispositivos físicos.

10.1. Princípios

- Privilégio mínimo.
- Ferramentas autorizadas explicitamente.
- Separação entre interpretação e autorização.
- Confirmação humana para acções sensíveis.
- Registo de operações.
- Autenticação entre componentes.
- Validação de entradas.
- Controlo de acesso aos dispositivos.

10.2. Exemplos de acções que exigem confirmação

- Apagar ficheiros.
- Enviar mensagens.
- Realizar pagamentos.
- Alterar configurações importantes.
- Executar comandos potencialmente destrutivos.
- Controlar dispositivos com implicações de segurança.

A autorização deverá ser aplicada pelo framework ou pelo Integrador, independentemente da decisão do LLM.

11. Estratégia de desenvolvimento

O trabalho será gradual e guiado por casos de uso. O prazo de uma semana que aparecia em versões anteriores não é uma meta acordada nem deve orientar decisões de arquitectura.

### Fase actual — Assistente pessoal

1. Definir em conjunto um primeiro caso de uso funcional.
2. Determinar as ferramentas, permissões e dados mínimos para esse caso.
3. Validar a integração entre Pi, AG-UI e a interface seleccionada, usando o template `pi-agui` apenas após revisão.
4. Implementar e testar apenas o fluxo necessário.
5. Avaliar memória persistente e capacidades adicionais com base no resultado.

Não iniciar a implementação antes da definição do primeiro caso de uso. Ver [[Fase 1 - Assistente pessoal]].

### Fases futuras — após validação

**Assistente ampliada:** voz, mais ferramentas e memória persistente se forem necessárias.

**Framework interno:** separar responsabilidades reutilizáveis, perfis, capacidades e permissões.

**Integrador e dispositivos:** definir primeiro a L.U, depois implementar e testar a ponte com os dispositivos.

**Framework Code-first/No-code:** evolução de longo prazo; não é prioridade nesta fase.

Fases futuras não implicam que todos estes componentes sejam desenvolvidos: cada um depende de uma necessidade validada.

12. Princípios arquitecturais permanentes

As seguintes regras deverão orientar todas as decisões técnicas:

1. O Pi é o runtime inicial, não uma dependência obrigatória de toda a plataforma.
2. O framework deverá separar identidade, memória, capacidades e permissões.
3. A interface não deverá depender dos detalhes internos do Pi.
4. O Integrador deverá ser independente do agente.
5. A L.U deverá manter a sua responsabilidade própria na comunicação com dispositivos.
6. Os protocolos devem ser escolhidos segundo a sua função.
7. Não desenvolver componentes que já existam e sejam adequados.
8. Não criar microserviços sem necessidade comprovada.
9. As permissões não devem depender exclusivamente do LLM.
10. A arquitectura deverá permitir crescimento sem reconstrução integral.
11. A primeira prioridade é uma assistente funcional.
12. O framework público só deverá ser desenvolvido depois da validação da solução.

13. Decisões estabelecidas

Decisão| Estado
Construir primeiro uma assistente pessoal baseada no Pi| Prioridade actual
Desenvolver um framework independente de motor| Visão futura, depois da validação
Utilizar CopilotKit como interface gráfica da Fase 1| Definido; integração Pi por validar
Utilizar AG-UI na ligação agente-interface| Direcção seleccionada; mapeamento com Pi por validar
Utilizar OpenUI de openui.com| Investigado; não seleccionado para a Fase 1
Estudar o template `pi-agui`| Referência comunitária; não aprovado para adopção
Comparar Pi Outpost como alternativa de interface| Investigação, sem decisão
Desenvolver o Integrador| Visão futura, fora da Fase 1
Utilizar L.U entre Integrador e dispositivos| Visão futura; especificação em falta
Definir o primeiro caso de uso antes da implementação| Próximo passo

14. Questões técnicas pendentes

Estas questões precisam de ser resolvidas através de investigação ou testes, sem assumir antecipadamente uma implementação.

Fase 1

- Qual é o primeiro caso de uso funcional?
- O template `pi-agui` é compatível com a versão actual mantida do Pi?
- Que partes do template podem ser reutilizadas sem adoptar a sua UI própria?
- Como ligar Pi a CopilotKit através de AG-UI e se é necessário um adaptador próprio?
- O template `pi-agui` pode acelerar essa ligação com segurança e compatibilidade?
- Que ferramentas e permissões são estritamente necessárias?
- O caso de uso precisa de memória pessoal para além das sessões Pi?
- Que configuração de execução é adequada no Windows?

Fases futuras

- Qual será o formato definitivo das mensagens L.U?
- Como será feita a descoberta de dispositivos e o mapeamento de capacidades?
- Como serão geridos autenticação, estados e eventos no Integrador?
- Como será feita a autenticação entre uma futura plataforma Web e o runtime?
- Como será suportada a substituição de runtime?

15. Resultado final pretendido

O projecto deverá evoluir para um ecossistema composto por três elementos fundamentais:

1. Framework de assistentes pessoais

Transforma motores de agentes existentes em assistentes pessoais configuráveis, extensíveis e reutilizáveis.

2. Integrador

Liga agentes e aplicações ao mundo físico através da L.U, disponibilizando uma interface uniforme para descobrir e controlar dispositivos.

3. Plataforma de gestão

Permite criar, configurar e gerir assistentes através de uma interface Web, enquanto os runtimes locais executam as tarefas e controlam os recursos autorizados.

O Pi será o primeiro motor. CopilotKit é a interface gráfica seleccionada para a Fase 1; a integração via AG-UI será validada. O Integrador e a L.U pertencem a fases futuras.

Declaração central do projecto

Não queremos construir mais um agente de inteligência artificial.

Queremos construir uma arquitectura que permita transformar motores de agentes existentes em assistentes pessoais completas, capazes de compreender, executar, comunicar, aprender com contexto persistente e interagir com o mundo digital e físico.

A nossa vantagem não estará em reinventar cada componente, mas em integrar correctamente tecnologias existentes e desenvolver os componentes de ligação que ainda faltam.

**Primeiro, uma assistente pessoal funcional. Depois, um framework reutilizável. Finalmente, uma plataforma para criar assistentes pessoais.**

---

Este documento mantém a visão de longo prazo. Para o trabalho imediato, prevalece [[Fase 1 - Assistente pessoal]].