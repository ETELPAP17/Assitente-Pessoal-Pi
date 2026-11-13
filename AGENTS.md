# Instruções para assistentes de IA neste projecto

## Contexto e prioridade

- O projecto documentado neste vault chama-se PROJECTO JARVIS / Assistente Pessoal Pi.
- A prioridade actual é a Fase 1: transformar o Pi Coding Agent numa assistente pessoal funcional.
- Não antecipar a construção do framework genérico, plataforma Web, múltiplos agentes ou integrações físicas. Esses temas ficam para depois de validar a assistente.
- Consultar `Fase 1 - Assistente pessoal.md` como definição actual da fase.
- `Visão.md` e `Projecto visão arquitectural.md` também descrevem objectivos de longo prazo; não interpretar as capacidades futuras como âmbito imediato.

## Ritmo e tomada de decisões

- Trabalhar devagar, em passos pequenos e compreensíveis.
- Antes da implementação, definir com o utilizador um primeiro caso de uso funcional concreto.
- Não escolher silenciosamente funcionalidades, frameworks, modelos, bases de dados ou permissões quando existem alternativas relevantes.
- Não implementar nem instalar dependências antes de confirmar que são necessárias para o caso de uso.
- Distinguir claramente factos documentados, resultados testados, hipóteses e decisões ainda pendentes.
- Pesquisar a documentação oficial actual antes de depender de APIs ou comportamento de tecnologias.

## Princípios técnicos

- Reutilizar soluções existentes, mas rever código, licença, manutenção, dependências e permissões antes de as adoptar.
- O Pi é o motor inicial; o framework independente de motor é uma fase posterior.
- CopilotKit + AG-UI é uma direcção a validar. Não presumir que qualquer template comunitário usa CopilotKit ou constitui integração oficial.
- O pacote `pi-agui` é um template comunitário em avaliação, não uma dependência aprovada.
- O Pi executa ferramentas com as permissões do processo e não é uma sandbox. Aplicar privilégio mínimo e autorização fora do LLM.
- Separar o histórico de sessões Pi de uma eventual memória pessoal de longo prazo.
- Não expor credenciais nem criar segredos no repositório.

## Documentação e colaboração

- Escrever documentação em português, seguindo a grafia e o estilo dos documentos existentes.
- Actualizar documentação directamente relacionada quando uma decisão de projecto mudar.
- Preservar os objectivos de longo prazo, marcando-os como futuros quando necessário.
- Este directório é actualmente um vault de documentação do Obsidian, não um checkout Git. Não afirmar que alterações locais foram enviadas ao GitHub.
