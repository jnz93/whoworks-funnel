# Inventário dos workflows

Este inventário descreve o que está configurado nos exports em [`../../exports/`](../../exports/). A presença de um nó ou workflow no arquivo não comprova que esteja habilitado, acessível ou funcionando na instância n8n.

## Workflows principais

| Export | ID observado | Entrada | Responsabilidade observada |
|---|---|---|---|
| [`Website Funil_ 1. Contato Inicial.json`](../../exports/Website%20Funil_%201.%20Contato%20Inicial.json) | `SqdLWQoWZZwInhEM` | Webhook `POST` | Normaliza contato, consulta disponibilidade no Google Calendar, solicita ao WordPress a criação do agendamento, envia opções por e-mail e registra lead/interação no Supabase. |
| [`Website Funil 2_ Agendamento Google Calendar.json`](../../exports/Website%20Funil%202_%20Agendamento%20Google%20Calendar.json) | `wcjJCjVpDwcietDK` | Webhook `POST` | Interpreta o slot selecionado, cria evento no Google Calendar, atualiza lead no Supabase e notifica via Telegram. |
| [`Website Funil 3_ Qualificação Briefing + Plano de ação.json`](../../exports/Website%20Funil%203_%20Qualifica%C3%A7%C3%A3o%20Briefing%20%2B%20Plano%20de%20a%C3%A7%C3%A3o.json) | `SYR33lQfc5eW6Qef` | Webhook `POST` | Normaliza e persiste o briefing, atualiza lead, gera plano com OpenAI e chama os subworkflows WordPress. |

## Subworkflows

| Export | ID observado | Entrada | Responsabilidade observada |
|---|---|---|---|
| [`[SubWorkflow] WF3_ Resolve WP USER.json`](../../exports/%5BSubWorkflow%5D%20WF3_%20Resolve%20WP%20USER.json) | `n4pOFy9HVbIYGhSh` | Executado por outro workflow | Procura usuário WordPress pelo e-mail; cria quando não existe e retorna o ID. |
| [`[SubWorkflow] WF3_ Save Briefing & Action Plan.json`](../../exports/%5BSubWorkflow%5D%20WF3_%20Save%20Briefing%20%26%20Action%20Plan.json) | `Omd2ldR7ehbUz0bs` | Executado por outro workflow | Gera relatório e cria briefing, caso e plano de ação no WordPress. |

## Pontos que precisam de validação

- No workflow de agendamento, `Atualiza Interação` está desativado, embora apareça conectado no grafo.
- No workflow de qualificação há nós desconectados/desativados e um filtro exportado de interação com `lead_id` fixo. Confirmar se são testes ou configuração pretendida.
- O subworkflow de gravação contém valores de exemplo em payloads de caso/plano, incluindo datas fixas. Confirmar ou substituir antes de uso operacional.
- As expressões de seleção de ambiente nos nós `Code in JavaScript`, `Setup` e `Edit Fields` devem ser conferidas na instância, pois aparentam atribuição onde seria esperada comparação.
- A autenticação dos webhooks não está explícita nos parâmetros exportados. Confirmar controles do n8n, proxy ou site.
- Confirmar contratos de payload entre site, webhooks e APIs WordPress, além de timezone, idempotência, retries e respostas HTTP.

As pendências e dependências estão detalhadas em [`../architecture.md`](../architecture.md). Os exports não trazem credenciais nem provam o estado da instância ou das integrações externas.
