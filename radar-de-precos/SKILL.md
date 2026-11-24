---
name: radar-de-precos
description: Monitora preços de produtos antes, durante e depois de uma data de promoção (Black Friday, Cyber Monday, Prime Day...) em várias lojas, monta um painel visual com o ranking de menor preço à vista e melhor parcelamento e o histórico de preços, agenda atualizações diárias e pode avisar por e-mail. Use quando a pessoa quiser acompanhar, comparar ou monitorar preços de um ou mais produtos antes de comprar.
---

# Radar de Preços

Você vai montar um radar de preços para a pessoa: uma lista de produtos que ela quer comprar, a coleta de preços em várias lojas, um painel visual com links para cada oferta e, quando der, atualizações automáticas até o dia da promoção, terminando com um ranking final.

Regras que valem do começo ao fim:
- Nunca compre nada, nunca entre em conta de ninguém, nunca preencha formulário de loja. A compra é sempre da pessoa.
- Nunca invente preço, parcela ou link. O que você não viu fica `null`. Preço de notícia ou comparador é "Não verificado".
- Fale com a pessoa no idioma dela. Os textos do painel estão em português; traduza se precisar.

## 1. Entender o pedido (uma rodada de perguntas, no máximo)

Descubra, perguntando só o que faltar:
- **Produtos**: nome e variante (capacidade, cor, tamanho). Até 6 produtos funciona bem. Se a pessoa estiver em dúvida entre modelos, coloque todos: comparar é o objetivo.
- **Evento e data**: padrão é a Black Friday (última sexta-feira de novembro do ano atual). Aceite outras datas.
- **Até quando monitorar**: padrão é até a segunda-feira seguinte ao evento (Cyber Monday), porque muitas lojas mantêm ou baixam preços no fim de semana. A pessoa pode pedir para parar no dia do evento.
- **Aviso por e-mail** (opcional): se quer receber um resumo por e-mail, em qual endereço e quando (todo dia, só quando um preço bater a meta ou cair, ou só o ranking final). Detalhes em `references/notificacao.md`.
- **País e moeda**: padrão Brasil, BRL. Para outros países, adapte a lista de lojas.
- **Prioridade**: menor preço à vista, parcelamento longo sem juros, ou os dois (padrão: os dois).
- **Meta de preço** por produto (opcional). Se a pessoa não souber, procure guias de "quanto pagar na Black Friday" e sugira, citando a fonte.

Se o pedido já for claro, comece direto.

## 2. Coleta

Para cada produto, siga `references/coleta.md` (lojas, como verificar, o que descartar). Em resumo:
- Busque em pelo menos 8 lojas grandes e confiáveis do país, mais operadoras quando for celular.
- Prefira a página do anúncio da própria loja e guarde o link dela. Sem a página exata, use o link de busca da loja e marque `link_tipo: "busca na loja"`.
- Registre à vista (Pix), total parcelado, número de parcelas, se é sem juros e as condições (cupom, cartão de banco específico, assinatura, plano de operadora, vendedor terceiro).
- Desconfie de preço muito abaixo do resto do mercado: costuma ser oferta relâmpago, cupom restrito ou vendedor duvidoso. Registre, mas diga isso nas condições.
- Nada de usado, recondicionado ou seminovo, a menos que a pessoa peça.

**Histórico anterior**: antes de começar o registro diário, procure preços dos últimos 7 a 14 dias em notícias e páginas de ofertas datadas (portais de tecnologia, agregadores de promoção, gráficos de histórico de comparadores quando o texto da página mostrar valores). Cada ponto achado entra em `historico` do produto com data, valor, loja e fonte. Sem nada confiável, o histórico começa na coleta de hoje; diga isso à pessoa.

Busque também uma foto oficial de cada produto (imagem de divulgação do fabricante ou a `og:image` da página da loja), 3 ou 4 especificações que ajudem a comparar os modelos e o ícone de cada loja (`loja_logo`).

## 3. Dados

Monte um objeto no formato de `references/formato-dos-dados.md` (produtos + ofertas). Cada oferta tem um `id` estável (ex.: `iphone-17-kabum`) para que as próximas coletas atualizem a mesma linha e guardem o valor antigo em `historico` da oferta. Cada produto tem seu próprio `historico`: um ponto por dia com o menor preço à vista daquele dia (o mesmo que o card mostra), que vira o gráfico do painel. Preencha também `acompanhar_ate` com a última data de monitoramento.

## 4. Painel

O painel pronto está em `assets/painel.html`. Ele lê os dados de `window.RADAR` (arquivo `dados.js` ao lado) ou de um bloco `<script id="radar-dados" type="application/json">` dentro do próprio HTML. `assets/dados-exemplo.js` mostra um exemplo real.

Entregue conforme o ambiente:
- **Claude com artifacts (claude.ai, app)**: publique o `painel.html` como artifact, com os dados colados no bloco `radar-dados` e sem a linha `<script src="dados.js">`. Se o artifact não carregar imagens externas, envie as fotos como assets do artifact ou converta em `data:` URLs pequenas (640px, JPEG).
- **Claude Code ou agente com arquivos**: crie uma pasta `radar/` com `painel.html` e `dados.js` e diga à pessoa para abrir o `painel.html` no navegador.
- **Outras LLMs sem arquivos**: entregue o HTML completo com os dados embutidos, pronto para salvar como `.html`.

O painel já traz cards dos modelos com foto, ficha técnica, melhor preço à vista, melhor parcelado com o valor da parcela e gráfico de histórico, busca por loja, ordenação por parcelado ou à vista, filtro por modelo e grupos de ofertas que abrem e fecham. Mantenha o visual; mude só os dados. Se a pessoa pedir produtos de tipos diferentes (um celular e uma TV, por exemplo), faça um painel por tipo.

## 5. Monitoramento antes, durante e depois do evento

Se você tiver uma ferramenta de tarefas agendadas (scheduled tasks, rotinas, cron do agente):
- Crie uma execução por dia até a véspera do evento (de manhã), uma no dia do evento, cedo, que faz o ranking final, e uma por dia depois do evento até `acompanhar_ate`, que compara com o preço do dia do evento.
- Se a pessoa pediu aviso por e-mail, configure como em `references/notificacao.md`.
- Use o modelo de instrução de `references/rotina.md`, preenchendo onde está o painel, os produtos e a data. Cada execução começa do zero, então a instrução precisa ser completa.
- Diga à pessoa quais dias e horários foram agendados.

Sem ferramenta de agendamento: explique que a pessoa pode voltar a qualquer momento e dizer "atualiza meu radar", e deixe a instrução de `references/rotina.md` pronta para ela colar.

## 6. Ranking final (no dia do evento)

Na última execução:
- Colete de novo as ofertas do dia.
- Para cada produto, compare o melhor preço de hoje com o melhor da semana (campo `historico`) e diga se o evento está melhor, igual ou pior, com a diferença em dinheiro.
- Dê o top 3 para parcelar e o top 3 à vista, diga se bateu a meta e faça uma recomendação objetiva, com os riscos (estoque, vendedor terceiro, cupom com regra, preço não verificado).
- Lembre a pessoa de conferir o preço no carrinho antes de pagar.

## 7. Depois do evento

Nas execuções depois do evento, diga se algum preço caiu abaixo do melhor do dia do evento e quanto. Na última, faça um fechamento: menor preço visto em todo o período, em que dia e loja, e se ainda vale comprar.

## Ao entregar

Responda curto: o que o painel mostra, quais ofertas parecem boas demais para ser verdade, quando são as próximas atualizações e o que ainda não foi possível verificar.
