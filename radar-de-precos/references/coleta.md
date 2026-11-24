# Como coletar preços

## Lojas (Brasil)

Busque cada produto, no mínimo, em:

| Tipo | Lojas |
| --- | --- |
| Marketplaces grandes | Amazon, Mercado Livre (só loja oficial da marca ou distribuidor autorizado), Magalu, Shopee (só loja oficial), Americanas, Submarino |
| Varejo e eletrônicos | KaBuM!, Fast Shop, Casas Bahia, Ponto, Extra, Carrefour, Kalunga, Girafa |
| Revendas oficiais da marca | iPlace (Apple), Samsung Shop, loja oficial do fabricante |
| Operadoras (celulares) | Vivo, Claro, TIM. Marque `exige_plano: true` quando o preço depender de plano |
| Comparadores (só para achar ofertas) | Zoom, Buscapé, Pelando, Promobit |

Fora do Brasil, troque pela lista equivalente do país (ex.: EUA: Amazon, Best Buy, Walmart, Target, Costco, loja do fabricante, operadoras).

## Como verificar

1. Comece com uma busca ampla ("<produto> preço", "<produto> black friday") para descobrir quem tem oferta.
2. Para cada loja, tente abrir a página do produto. Muitas páginas trazem o preço no HTML (`"price":`, JSON-LD, meta tags).
3. Status:
   - `Visto na página da loja`: você viu o preço no anúncio da própria loja.
   - `Não verificado`: veio de notícia, comparador, agregador de cupons ou listagem de busca.
   - `Referência`: preço de tabela do fabricante.
   - `Esgotado`: a oferta sumiu ou o produto está indisponível.
4. Sempre preencha `visto_em` com a data em que o preço foi visto (não a de hoje, se a fonte for antiga) e `fonte`.

## Parcelamento

- `parcelado` é o total pago no cartão, não o valor da parcela.
- `sem_juros`: `"sim"` só quando a loja diz "sem juros". Se não diz, `"?"`.
- Anote nas condições quando o parcelamento longo exige cartão de banco específico, carnê, crediário ou plano.

## Sinais de alerta (registre nas condições)

- Preço muito abaixo dos outros: oferta relâmpago, cupom só para assinantes, ou vendedor terceiro.
- Vendedor diferente da loja (marketplace): diga quem vende.
- Garantia diferente da oficial.
- Loja em recuperação judicial ou com muitas reclamações recentes.

## Não inclua

Usados, recondicionados, seminovos, importados sem garantia no país, kits com acessórios inflando o preço (a menos que a pessoa peça).
