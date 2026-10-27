# Whoworks Funnel

Repositório dos exports n8n que automatizam o funil de contato do site Whoworks: recebimento do contato, sugestão e confirmação de reunião, qualificação do briefing e publicação do briefing/plano de ação no WordPress.

## Conteúdo

- [`exports/`](exports/) — cinco exports JSON dos três workflows principais e dois subworkflows.
- [`docs/architecture.md`](docs/architecture.md) — arquitetura observada, integrações, contratos inferidos e pendências.
- [`docs/workflows/index.md`](docs/workflows/index.md) — inventário rápido dos workflows e pontos de atenção dos exports.

## Fluxos

1. **Contato inicial:** recebe os dados do formulário, consulta disponibilidade, propõe horários e registra o lead.
2. **Agendamento:** recebe a escolha do lead, cria evento no Google Calendar e atualiza o lead.
3. **Qualificação do briefing:** recebe o briefing pós-reunião, gera plano e conteúdo e aciona os subworkflows para resolver o usuário WordPress e salvar os artefatos.

Os arquivos são snapshots de configuração. Eles não incluem as credenciais da instância, schema do Supabase, código do site nem evidência de que uma execução foi bem-sucedida. Os nomes, ambientes e dependências descritos precisam ser conferidos na instância n8n de destino antes de importar ou ativar.

## Importação e atualização

Use a interface/API da versão de n8n adotada pela equipe para importar ou exportar workflows. Antes de importar, confira versão compatível, IDs/referências de subworkflows, credenciais, URLs-base e efeitos externos. Faça a revisão em desenvolvimento/staging com dados sintéticos e siga o procedimento de ativação aprovado pela equipe.

Não salve credenciais, tokens, URLs de webhook completos, execuções reais ou dados pessoais de leads neste repositório. Para pontos de validação específicos, consulte [`docs/architecture.md`](docs/architecture.md) e [`docs/workflows/index.md`](docs/workflows/index.md).
