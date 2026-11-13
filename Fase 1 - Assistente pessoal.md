# Fase 1 — Transformar o Pi numa assistente pessoal

**Estado:** definição e investigação  
**Prioridade actual:** construir e validar uma assistente pessoal funcional baseada no Pi  
**Implementação:** ainda não iniciada  
**Primeiro caso de uso:** por definir em conjunto

## 1. Objectivo

Transformar o Pi Coding Agent numa assistente pessoal útil no computador, começando por uma experiência simples de conversa e execução de tarefas.

Esta fase **não** tem como objectivo construir já o framework geral, a plataforma Web de gestão, um sistema multiagente, o Integrador ou a integração com dispositivos físicos. Essas possibilidades pertencem a fases posteriores, depois de validarmos a assistente.

## 2. Arquitectura mínima em avaliação

```text
Utilizador
    ↕
Interface gráfica obrigatória — CopilotKit (seleccionado)
    ↕ AG-UI
Runtime local — Node.js / TypeScript
    ├── Integração AG-UI ↔ Pi
    ├── Associação entre conversas e sessões Pi
    ├── Aplicação de permissões e aprovações
    └── Memória pessoal, apenas quando necessária ao caso de uso
             ↕
       Pi Coding Agent
       ├── Modelo de linguagem
       ├── Contexto e sessões
       └── Ferramentas estritamente necessárias
```

### Responsabilidades

- **Pi:** motor do agente; gere o ciclo de execução, contexto, sessões e chamadas a ferramentas.
- **CopilotKit:** interface gráfica seleccionada para conversar com o Pi nesta fase. Uma interface apenas de terminal não satisfaz o objectivo.
- **AG-UI:** protocolo de eventos entre agente e interface.
- **Runtime local:** mantém o Pi junto dos recursos do computador e aplica os controlos de acesso.
- **Memória pessoal:** informação duradoura escolhida pelo utilizador; distinta do histórico de uma sessão Pi.

O CopilotKit tem de encaminhar as conversas para o Pi; não utilizar o seu `BuiltInAgent`, porque esse agente chama directamente o modelo e substituiria o Pi em vez de o ligar à interface. A ligação Pi ↔ AG-UI/CopilotKit continua por validar e poderá exigir um adaptador ou reutilização de código após revisão.

### OpenUI

O OpenUI de [openui.com](https://www.openui.com/docs) não é o mesmo que Open WebUI. A documentação descreve duas possibilidades: o Agent Interface React, que fornece uma interface de chat completa e liga a um backend existente, e o OpenUI Lang, que permite renderizar componentes generativos dentro de uma interface existente, incluindo CopilotKit. O OpenUI não foi seleccionado para esta fase; poderá ser reconsiderado se surgir uma necessidade concreta de UI generativa ou se a integração CopilotKit não cumprir os requisitos.

## 3. Integrações investigadas

### `pi-agui`

O pacote [`pi-agui`](https://pi.dev/packages/pi-agui) gera um template de aplicação com Pi, Pi SDK, AG-UI, backend Express e frontend React/Vite. O template inclui chat em streaming, chamadas a ferramentas, sessões, selecção de modelos e outras funcionalidades.

É uma **implementação comunitária e um candidato a referência ou protótipo**, não uma integração oficial de primeira parte do Pi ou do CopilotKit. O seu frontend é próprio; não é a UI CopilotKit. A dependência publicada no template usa `@mariozechner/pi-coding-agent`, que está depreciada em favor de `@earendil-works/pi-coding-agent`. Antes de reutilizar o template, temos de verificar a versão, compatibilidade, código e permissões.

### Pi Outpost

[`pi-outpost`](https://github.com/laurentftech/pi-outpost) fornece uma interface Web para o Pi e pode servir de referência técnica, mas não é a interface seleccionada para a Fase 1.

### Pesquisa Web

Os pacotes [`pi-web-search`](https://pi.dev/packages/pi-web-search) e [`Pi Web Access`](https://pi.dev/packages/pi-web-access) são candidatos para pesquisa e consulta de páginas. Devem ser comparados com o caso de uso escolhido, o fornecedor/modelo e as credenciais necessárias. Não instalar ambos por antecipação.

### Outros pacotes Pi

[`pi-code`](https://pi.dev/packages/pi-code) e [`@gavin-hu/my-pi-agent`](https://pi.dev/packages/@gavin-hu/my-pi-agent) são pacotes de personalizações/extensões mais abrangentes. Só considerar funcionalidades específicas depois de rever o código, a licença, as dependências e o âmbito de permissões.

## 4. Fluxo principal

1. O utilizador envia uma mensagem pela interface.
2. O runtime identifica a conversa e a sessão Pi correspondente.
3. O pedido é encaminhado para o Pi.
4. O Pi responde ou solicita uma ferramenta.
5. Antes da ferramenta executar, o runtime aplica a política de permissões.
6. Se a operação exigir aprovação, o utilizador decide antes da execução.
7. Os eventos e a resposta regressam à interface através de AG-UI.
8. A conversa fica no histórico da sessão Pi; uma memória de longo prazo só é criada segundo regras explícitas.

Este fluxo é uma proposta para validação, não uma implementação existente.

## 5. Permissões e segurança

O Pi executa ferramentas com as permissões do processo e não constitui, por si só, uma sandbox. A pasta de trabalho e a confiança no projecto não limitam o que comandos e extensões podem aceder no sistema.

Princípios para a primeira versão:

- Começar com o menor conjunto de ferramentas possível.
- Manter o runtime local e os seus endpoints inacessíveis a terceiros por defeito.
- Fazer a autorização no backend/ferramenta, não apenas na interface nem por instrução ao modelo.
- Pedir aprovação para acções com efeitos externos, destrutivos ou sensíveis.
- Rever extensões e pacotes antes de os instalar.
- Não expor credenciais desnecessárias ao agente.
- Avaliar isolamento do sistema operativo se a tarefa exigir acesso a ficheiros ou comandos com maior impacto.

A aprovação humana é um controlo de produto; não substitui sandbox ou privilégio mínimo.

## 6. Memória e sessões

- O histórico de conversa e a gestão de sessões Pi são a memória de curto prazo da interacção.
- A memória pessoal de longo prazo é uma decisão separada, controlável pelo utilizador e não necessária antes de existir um caso de uso que a justifique.
- Não seleccionar ainda SQLite, vector database ou outro armazenamento.
- Não guardar automaticamente qualquer dado que apareça numa conversa.

## 7. Fora do âmbito actual

- Framework genérico ou suporte a outros motores.
- Plataforma Web de criação e gestão de assistentes.
- Múltiplos agentes, delegação e workflows avançados.
- Voz (STT/TTS).
- Integrador, L.U, Home Assistant, ESP32, Arduino e IoT.
- A2A, A2UI e construtor Code-first/No-code.
- Automatização irrestrita do computador.

A utilização do Pi no terminal pode continuar útil para desenvolvimento e diagnóstico, mas não substitui a interface gráfica CopilotKit exigida como parte da experiência desta fase.

## 8. Decisões e questões em aberto

### Definido

- A primeira meta é transformar o Pi numa assistente pessoal funcional.
- O framework e a abstracção para múltiplos motores ficam para depois da validação.
- Pi é o motor inicial.
- CopilotKit está seleccionado como interface gráfica necessária nesta fase; a integração Pi ↔ AG-UI/CopilotKit ainda não está validada.
- O `pi-agui` é uma referência concreta a inspeccionar, não uma decisão de adopção.
- O OpenUI de openui.com foi investigado como alternativa/complemento, mas não foi seleccionado.
- O trabalho deve avançar devagar, em passos curtos, sem começar a implementação antes da escolha do primeiro caso de uso.

### Ainda por decidir

- Qual é o primeiro caso de uso funcional.
- Como ligar Pi ao CopilotKit através de AG-UI e se é necessário um adaptador próprio.
- Se o template `pi-agui` é compatível, seguro e útil como referência.
- Qual o modelo/provedor, sistema operativo e forma de execução.
- Quais as ferramentas mínimas exigidas pelo caso de uso.
- Se esse caso de uso necessita de memória para além das sessões Pi.
- Quais as operações que exigem aprovação e que isolamento será necessário.

## 9. Próximo passo

Escolher **um** primeiro caso de uso pequeno e concreto. Só depois de o definir serão seleccionados as ferramentas, as permissões e a persistência necessárias. A implementação começa após essa definição.

## 10. Fontes técnicas consultadas

- [Documentação do Pi](https://docs.pi.dev/latest/)
- [Pi SDK](https://docs.pi.dev/latest/sdk)
- [Sessões e contexto do Pi](https://docs.pi.dev/latest/sessions)
- [Segurança do Pi](https://docs.pi.dev/latest/security)
- [Pi no Windows](https://docs.pi.dev/latest/windows)
- [Documentação do CopilotKit](https://docs.copilotkit.ai/)
- [Quickstart do CopilotKit](https://docs.copilotkit.ai/quickstart)
- [OpenUI — documentação](https://www.openui.com/docs)
- [OpenUI Agent Interface](https://www.openui.com/docs/agent/getting-started/introduction)
- [OpenUI — integrações](https://www.openui.com/docs/integrations)
- [Visão geral AG-UI](https://docs.ag-ui.com/introduction)
- [Integrações AG-UI](https://docs.ag-ui.com/integrations)
- [Template `pi-agui` no catálogo Pi](https://pi.dev/packages/pi-agui)
- [README do template `pi-agui`](https://unpkg.com/pi-agui@0.1.1/template/README.md)
- [Pi Outpost](https://github.com/laurentftech/pi-outpost)
- [Catálogo de pacotes Pi](https://pi.dev/packages)
- [Catálogo de modelos Pi](https://pi.dev/models)
