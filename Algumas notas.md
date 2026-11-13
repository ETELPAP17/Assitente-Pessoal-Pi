# Notas e registo de decisões

Este documento regista resultados de pesquisa e decisões. A definição actual da Fase 1 está em [[Fase 1 - Assistente pessoal]].

## Decisões actuais

| Tema | Estado | Nota |
|---|---|---|
| Objectivo imediato | Definido | Transformar o Pi numa assistente pessoal funcional; não começar pelo framework. |
| Pi | Escolhido como motor inicial | Usa sessões, ferramentas, extensões e SDK; confirmar versões concretas antes da integração. |
| Interface gráfica da Fase 1 | Definida | CopilotKit é obrigatório para a experiência desta fase; terminal apenas não chega. |
| AG-UI | Em avaliação para a ligação agente-interface | É protocolo de eventos, não uma integração automática de qualquer agente. |
| OpenUI de openui.com | Investigado, não seleccionado | Agent Interface pode fornecer chat completo; OpenUI Lang também pode renderizar UI generativa dentro de CopilotKit. |
| `pi-agui` | Referência a inspeccionar | Template comunitário Pi + AG-UI com frontend próprio, não CopilotKit. |
| Primeiro caso de uso | Por definir | Defini-lo antes de escolher ferramentas e iniciar implementação. |
| Memória de longo prazo | Adiada | As sessões Pi cobrem o histórico conversacional; memória pessoal só se o caso de uso justificar. |
| Framework, Integrador e L.U | Futuros | Não fazem parte do âmbito da implementação inicial. |

## Resultados técnicos relevantes

### Pi e segurança

- O Pi pode ser incorporado em aplicações Node.js/Bun através do SDK ou controlado por RPC.
- As sessões do Pi guardam histórico e contexto, mas não são por si só uma memória pessoal estruturada.
- Ferramentas e extensões executam com as permissões do processo Pi. O Pi não é uma sandbox; a pasta de trabalho não impede o acesso a outros recursos disponíveis ao processo.
- Em Windows, o Pi suporta execução nativa e WSL; a configuração do terminal e do shell deve ser validada no ambiente real.

### CopilotKit e AG-UI

- CopilotKit fornece componentes de interface e ligação a agentes.
- A documentação do OpenUI descreve o Agent Interface React como uma UI de chat completa ligada a um backend existente; também documenta a integração de OpenUI Lang em CopilotKit. Não foi identificada uma ligação pronta ao Pi.
- O `BuiltInAgent` do CopilotKit é um agente próprio que chama o modelo; não deve ser escolhido para a integração se o objectivo é executar Pi.
- AG-UI padroniza a comunicação orientada a eventos entre frontend e backend de agente.
- A lista oficial de integrações AG-UI não basta para concluir que Pi tenha suporte de primeira parte. O template `pi-agui` encontrado no catálogo é comunitário.

### `pi-agui`

- O pacote `pi-agui` (MIT) gera uma aplicação a partir de um template full-stack: React/Vite, Express, Pi SDK e AG-UI.
- O frontend incluído é próprio e não é a interface CopilotKit.
- O template anuncia chat em streaming, ferramentas, sessões, modelos, estado e vários endpoints.
- A dependência declarada pelo template é `@mariozechner/pi-coding-agent`; o npm marca esse pacote como depreciado e recomenda `@earendil-works/pi-coding-agent`.
- Antes de reutilizar qualquer parte, inspeccionar a versão actual do template e testar compatibilidade com o Pi actual. Não instalar cegamente.

### Outras opções Pi investigadas

- `pi-outpost`: interface Web para Pi; README descreve configuração segura inicial, em modo de leitura e sem Bash. Pode servir de referência, mas não substitui a interface CopilotKit seleccionada.
- `pi-web-search` e `Pi Web Access`: candidatos para pesquisa/consulta Web; comparar capacidades, modelo/provedor exigidos, manutenção e permissões quando o caso de uso pedir pesquisa.
- `pi-code` e `@gavin-hu/my-pi-agent`: pacotes abrangentes de personalização; não adoptar por inteiro sem rever o código e seleccionar apenas as capacidades necessárias.
- Catálogo de modelos Pi: usar para comparar opções depois de serem conhecidos os requisitos e o orçamento; presença no catálogo não significa recomendação.

## Riscos e pendências

| Tema | Estado actual | Próxima verificação |
|---|---|---|
| Ligação Pi–CopilotKit | Interface escolhida; integração por validar | Confirmar contrato AG-UI/CopilotKit e avaliar se o template `pi-agui` ajuda na ligação ao Pi. |
| Template `pi-agui` | Útil como referência, compatibilidade por confirmar | Inspeccionar código/dependências e verificar com a versão mantida do Pi. |
| Segurança de ferramentas | Risco confirmado | Definir conjunto mínimo, limites locais e aprovações após escolher o caso de uso. |
| Memória pessoal | Não especificada | Não escolher armazenamento até haver requisito concreto. |
| Windows | Suportado segundo documentação Pi | Confirmar shell/runtime e dependências no computador de desenvolvimento. |
| L.U e dispositivos | Fora da Fase 1 | Retomar após validar o assistente no computador. |

## Histórico de investigação anterior

As notas sobre MCP, Codemode, Windows, L.U e plataforma Web reflectem investigação exploratória. Não devem ser tratadas como decisões de implementação da Fase 1 sem nova verificação na documentação actual.
