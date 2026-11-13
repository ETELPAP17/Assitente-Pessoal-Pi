# Assistente Pessoal Pi

Projecto para transformar o Pi Coding Agent numa assistente pessoal funcional, avançando por passos pequenos e validando cada capacidade antes de generalizar a solução.

## Prioridade actual: Fase 1

O foco imediato é a assistente pessoal baseada no Pi. **Não estamos ainda a construir o framework genérico**, a plataforma de gestão, múltiplos agentes nem integrações com dispositivos físicos.

O primeiro caso de uso funcional ainda está por definir. Antes de implementar ou instalar dependências, vamos defini-lo e identificar as ferramentas, permissões e dados mínimos necessários.

## Documentação

- [Definição da Fase 1](Fase%201%20-%20Assistente%20pessoal.md) — objectivo, arquitectura em avaliação, fluxo, segurança, memória e decisões pendentes.
- [Visão do projecto](Vis%C3%A3o.md) — visão geral e princípios.
- [Visão arquitectural de longo prazo](Projecto%20vis%C3%A3o%20arquitectural.md) — arquitectura futura, explicitamente fora do âmbito imediato.
- [Notas e decisões](Algumas%20notas.md) — investigação, estado das opções e riscos.
- [Referências técnicas](Link%20de%20documenta%C3%A7%C3%A3o.md) — documentação oficial e pacotes em avaliação.
- [Instruções para assistentes de IA](AGENTS.md) — prioridades e regras de colaboração.

## Tecnologias e estado actual

- **Pi Coding Agent:** motor inicial.
- **CopilotKit:** interface gráfica seleccionada e necessária na Fase 1; uma experiência apenas de terminal não satisfaz o objectivo.
- **AG-UI:** protocolo previsto para a comunicação, com a ligação efectiva entre Pi e CopilotKit ainda por validar.
- **OpenUI (openui.com):** investigado como alternativa ou complemento para UI generativa, mas não seleccionado nesta fase.
- **`pi-agui`:** template comunitário Pi + AG-UI para estudar; não é uma dependência aprovada nem inclui a interface CopilotKit.
- **Pi Outpost:** referência técnica de interface Web, não é a interface seleccionada.

Nenhum pacote comunitário deve ser instalado sem rever código, licença, manutenção, dependências, compatibilidade e permissões.

## Evolução posterior

Depois de validar a assistente, poderão ser avaliados memória persistente, voz e mais ferramentas. O framework genérico, o Integrador, a L.U, os dispositivos físicos e a plataforma de gestão pertencem a fases futuras.

## Repositório

Este é o repositório do projecto. A pasta `Projecto PAF` do Obsidian é um vault de documentação local separado; alterações nesse vault não são publicadas automaticamente aqui.