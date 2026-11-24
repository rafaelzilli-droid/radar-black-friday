# Aviso por e-mail

Só configure se a pessoa pedir. O e-mail vai apenas para o endereço dela, nunca para terceiros, e nunca leva senha, número de cartão ou dado de conta.

## O que perguntar

- Endereço de e-mail.
- Quando avisar: todo dia, só quando um preço bater a meta ou cair mais de X% desde a última coleta, ou só no ranking final e no fechamento.

## Como enviar, do melhor para o pior

1. **Aviso da própria tarefa agendada.** Algumas ferramentas de tarefas agendadas (como as do Claude) avisam por e-mail ou no celular quando uma execução termina. Se a ferramenta tiver essa opção, ligue o aviso por e-mail ao criar as tarefas. É o caminho mais simples e não exige outra integração.
2. **Conector de e-mail da pessoa** (Gmail, Outlook). Se o assistente tiver um conector de e-mail conectado à conta da pessoa, a instrução de cada tarefa diz para enviar o resumo ao próprio endereço dela. O pedido inicial da pessoa, com o endereço e a regra, é a autorização. Se o assistente pedir confirmação antes de enviar, prefira criar um rascunho e avisar.
3. **Sem nenhum dos dois**: diga à pessoa que o aviso por e-mail não está disponível no assistente dela e que o painel continua atualizado; ela pode ativar as notificações do próprio assistente.

## Modelo do e-mail

Assunto: `Radar de Preços: <produto com maior novidade> <o que mudou>` (ex.: "Radar de Preços: iPhone 17 caiu para R$ 5.273 no Pix").

Corpo, curto:
- Uma linha por produto: menor à vista (loja e valor), melhor parcelado (parcelas, valor da parcela e total) e a variação desde a coleta anterior.
- Ofertas que bateram a meta, com destaque.
- Ofertas suspeitas ou não verificadas, numa linha.
- Link do painel.
- "Confira o preço no carrinho antes de pagar."
