# Instrução para as atualizações agendadas

Cada execução agendada começa sem memória da conversa. Preencha os `<...>` e use o texto abaixo como instrução de cada tarefa. No dia do evento, troque o passo 6 pelo bloco "Ranking final"; depois do evento, pelo bloco "Depois do evento".

---

Atualização do Radar de Preços de <nome da pessoa>. Hoje é <data>; o evento é <nome do evento> em <data do evento>. Responda em <idioma>. Nunca compre nada, nunca entre em conta, nunca preencha formulário, nunca invente preço.

PRODUTOS: <lista com id, nome, variante e meta>.
PREFERÊNCIA: <à vista, parcelamento longo sem juros, ou os dois>.

PAINEL: <onde está: link do artifact e como atualizá-lo, ou caminho da pasta radar/ com painel.html e dados.js>.
MONITORAR ATÉ: <data, padrão a segunda depois do evento>.
AVISO POR E-MAIL: <endereço da pessoa e quando avisar, ou "não">.

1. Leia os dados atuais do painel (formato em references/formato-dos-dados.md da skill radar-de-precos, se estiver instalada; senão, siga os campos que já existem).
2. Colete os preços de hoje de cada produto em pelo menos 8 lojas grandes e confiáveis (Amazon, Mercado Livre oficial, Magalu, KaBuM!, Fast Shop, Casas Bahia, Carrefour, Americanas, loja oficial da marca, operadoras quando for celular). Prefira a página do anúncio e o link dela. "Visto na página da loja" só quando viu no anúncio; o resto é "Não verificado" com a fonte. Nada de usado ou recondicionado.
3. Mescle: na oferta de mesmo id, acrescente os valores antigos em `historico` e grave os novos; loja nova vira id novo; oferta que sumiu vira "Esgotado". Não apague linhas.
4. Em cada produto, acrescente ao `historico` do produto um ponto de hoje com o menor preço à vista (o mesmo que o card mostra), a loja e a fonte "Coleta do Radar". Se já houver ponto de hoje, substitua.
5. Atualize `atualizado_em` e `proxima_atualizacao` e salve o painel.
6. Se houver aviso por e-mail e a regra de hoje mandar avisar, envie conforme references/notificacao.md, só para o endereço da pessoa.
7. Responda curto: melhor à vista e melhor parcelado sem juros de cada produto (loja e valor), o que mudou desde a coleta anterior, ofertas suspeitas e o link do painel.

Ranking final (só no dia do evento, no lugar do passo 7):
Para cada produto, top 3 para parcelar e top 3 à vista com loja e valores; compare com o melhor visto antes de hoje (`historico`) e diga se o evento está melhor, igual ou pior, com a diferença; diga se bateu a meta; faça uma recomendação objetiva com os riscos (estoque, vendedor terceiro, cupom com regra, preço não verificado) e lembre de conferir o preço no carrinho antes de pagar.

---

Depois do evento (no lugar do passo 7):
Diga, para cada produto, o melhor preço de hoje e a diferença para o melhor do dia do evento. Avise com destaque se algum ficou abaixo. Na última execução, faça o fechamento: menor preço de todo o período, em que dia e loja, e se ainda vale comprar.

## Quando agendar

- Uma por dia até a véspera, de manhã (ex.: 10h no fuso da pessoa).
- Uma no dia do evento, cedo (ex.: 8h), com o ranking final.
- Uma por dia depois do evento até a data combinada (padrão: a segunda seguinte, Cyber Monday).
