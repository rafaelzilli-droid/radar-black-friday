# Formato dos dados

O painel lê um objeto `RADAR`:

```js
window.RADAR = {
  "titulo": "iPhone na Black Friday",
  "subtitulo": "iPhone 17, 17 Pro e 18 Pro de 256 GB",   // opcional
  "metas_fonte": "Metas: guias de preço da Tekimobile e do TecMundo.", // opcional, aparece no rodapé
  "evento": { "nome": "Black Friday", "data": "2026-11-27" },
  "moeda": "BRL",
  "atualizado_em": "2026-11-24T09:00:00-03:00",
  "proxima_atualizacao": "qua 25/11, 10h",        // texto livre, opcional
  "produtos": [ /* ... */ ],
  "ofertas": [ /* ... */ ]
};
```

## Produto

| Campo | Tipo | Observação |
| --- | --- | --- |
| `id` | texto | estável, em kebab-case (`iphone-17`) |
| `nome` | texto | `iPhone 17` |
| `variante` | texto ou null | `256GB`, `Preto`, `55 polegadas` |
| `imagem` | URL https ou `data:` ou null | foto oficial; sem foto, o card mostra um espaço cinza |
| `imagem_alt` | texto | opcional |
| `specs` | lista de `[rótulo, valor]` | 3 ou 4 itens que ajudem a comparar |
| `meta_preco` | número ou null | preço à vista que a pessoa considera bom |
| `nota` | texto ou null | aviso curto (ex.: "saiu de linha") |

## Oferta

| Campo | Tipo | Observação |
| --- | --- | --- |
| `id` | texto | estável: `<produto>-<loja>` |
| `loja_id` | texto | identificador da loja (`amazon`, `kabum`), opcional |
| `loja_logo` | URL ou null | ícone da loja. Sem ele, o painel mostra as iniciais. Uma opção é o ícone do domínio: `https://www.google.com/s2/favicons?domain=<dominio>&sz=64` |
| `produto_id` | texto | o `id` do produto |
| `loja` | texto | nome como a pessoa reconhece; diga o vendedor se for terceiro |
| `pix` | número ou null | preço à vista |
| `parcelado` | número ou null | total no cartão |
| `parcelas` | número ou null | quantidade máxima |
| `sem_juros` | `"sim"`, `"nao"` ou `"?"` | |
| `condicoes` | texto | cupom, cartão de banco, plano, vendedor, garantia, alertas |
| `exige_plano` | true/false | plano de operadora ou assinatura obrigatória |
| `status` | `Visto na página da loja`, `Não verificado`, `Referência`, `Esgotado` | |
| `visto_em` | `AAAA-MM-DD` | quando o preço foi visto |
| `fonte` | texto | onde foi visto |
| `link` | URL https | anúncio, ou busca da loja |
| `link_tipo` | `anúncio`, `busca na loja`, `página de ofertas`, `loja`, `onde vi` | |
| `historico` | lista de `{data, pix, parcelado}` | valores antigos; a coleta seguinte acrescenta aqui antes de sobrescrever |

Números sem separador de milhar (`5273.5`), nunca texto. Nada de `NaN`.

## Campos de publicação (opcionais)

- `logos_base`: pasta com os logos das lojas, como `/img/lojas/`. O painel usa `logos_base + loja_id + ".png"` quando a oferta não tem `loja_logo`.
- `inicio`: endereço para onde o nome "Radar de Preços" no topo leva.
- Para publicar vários comparativos num site, coloque no `<body>` do painel `data-dados="/pasta/"`, com `categorias.json` (lista de `{id, titulo, subtitulo, imagem}`) e um `<id>.json` por categoria. O painel mostra as categorias no topo e abre `?c=<id>`.
