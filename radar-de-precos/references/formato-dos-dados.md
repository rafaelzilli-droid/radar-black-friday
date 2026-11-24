# Formato dos dados

O painel lê um objeto `RADAR`:

```js
window.RADAR = {
  "titulo": "iPhone na Black Friday",
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
