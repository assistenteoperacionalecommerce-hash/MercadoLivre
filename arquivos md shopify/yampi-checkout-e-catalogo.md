# Yampi: checkout, ofertas e cruzamento com a Shopify

Painel `app.yampi.com.br`, loja **A Trator Diesel**, alias de API
`a-trator-diesel2`, usuário Luciana Leão.

Este documento é a referência da Yampi. Quando o assunto for cupom, order
bump, upsell, carrinho abandonado, forma de pagamento ou regra de checkout,
abra este antes de entrar no painel.

---

## Como entrar

O painel abre direto no navegador da sessão, sem senha: a conta já está
logada e a sessão persiste entre conversas. Se cair na tela "Identifique-se"
(aconteceu em 15/09), peça ao cliente para entrar pela aba do navegador: senha
não se digita. **Redimensione a janela para
1440x900 antes de abrir qualquer rota de configuração**, senão ela cai em
`/forbidden` como se faltasse permissão.

| o quê | endereço |
|---|---|
| cupons | `/marketing/promocodes` |
| order bumps | `/marketing/order-bumps?limit=50&page=1` |
| upsells | `/marketing/upsell` |
| cashback | `/marketing/cashbacks` |
| regras do checkout | `/checkout/rules` |
| formas de pagamento | `/checkout/payment` |
| dados da loja | `/config/merchant-data/edit` |
| frete | `/config/logistics` |
| carrinho abandonado | `/config/abandoned-carts` |

**O painel é um SPA que não responde a `pushState`.** Para ler vários
registros, use `browser_batch` com pares de `navigate` mais
`javascript_tool`, uma navegação de verdade por registro. Espere 5s depois de
cada `navigate` antes de ler, senão você lê a tela anterior.

Os campos são Element UI, não `<select>` nativo:
`document.querySelectorAll('select')` volta vazio. O valor escolhido está no
`input.el-input__inner` correspondente, e a ordem dos inputs muda conforme a
quantidade de produtos-gatilho. Ancore pelo valor conhecido (por exemplo o
índice de `'after'`) em vez de contar posições fixas.

**Para trocar o valor de um campo desses**, clique por JavaScript e não por
coordenada, porque a janela emulada é redimensionada e a coordenada do print
não bate com a da página:

```js
const inp = [...document.querySelectorAll('input.el-input__inner')]
  .find(e => e.value === 'Pessoa física');
inp.dispatchEvent(new MouseEvent('mousedown', {bubbles: true}));
inp.click();
// espera, depois clica na opção
const alvo = [...document.querySelectorAll('.el-select-dropdown__item')]
  .filter(o => o.offsetParent !== null)
  .find(o => o.innerText.trim() === 'Pessoa física e jurídica');
alvo.dispatchEvent(new MouseEvent('mousedown', {bubbles: true}));
alvo.click();
```

Depois de Salvar, **recarregue a página e leia de novo**: o painel devolve a
tela otimista antes de confirmar a gravação.

---

## Os dois cupons

| código | desconto | regra | usos |
|---|---|---|---|
| `BEMVINDO5OFF` | 5% | Cupom de 1ª compra, uso único por cliente | 2 |
| `VOLTA7` | 7% | Recuperação de carrinho, uso único por cliente | 0 |

Os dois estão ativos, sem valor mínimo de compra, sem frete grátis, sem
acumular com outras promoções, e valem até 10/09/2027.

**`BEMVINDO5OFF` não tem código para o cliente digitar.** A marcação "Cupom de
1ª compra" faz a Yampi aplicar sozinha para todo cliente novo que chega ao
checkout. É por isso que a faixa da home fala em desconto aplicado sozinho e
não mostra código.

**`VOLTA7` não pode aparecer no site.** Ele é a única carta do 4º e-mail de
carrinho abandonado. Publicado na vitrine, quem já ia comprar usa os 7%, e a
régua de recuperação fica sem nada para oferecer a quem desistiu.

O teto comercial de desconto é 7%, então os dois cupons cabem, mas eles **não
podem ser combinados com oferta com desconto**: por isso order bump e upsell
vendem pelo preço de tabela. Ver a skill `ajuste-preco-order-bump`.

## Régua de carrinho abandonado, bem montada

Quatro envios, todos ativos, todos com texto próprio já escrito:

| envio | quando | cupom |
|---|---|---|
| 1º | 30 minutos | nenhum |
| 2º | 2 horas | nenhum |
| 3º | 24 horas | nenhum |
| 4º | 48 horas | `VOLTA7`, 7% |

É exatamente a ordem que a skill `yampi-checkout-otimizacao` recomenda. Os
textos falam em compatibilidade de peça e trazem o (62) 3086-7211, que é o
número certo para esse assunto. **Não mexa nisso sem motivo.**

## 21 order bumps e 4 upsells

Os 25 SKUs foram cruzados por `productVariants(query: "sku:...")` na Shopify.
**Os 25 preços batem, centavo a centavo.**

Os 4 upsells são todos jogo de juntas para retificação (NS11 R$ 58,00, NS18
R$ 65,00, B9/NB10 R$ 50,00, NS90 R$ 53,18), oferecidos **na finalização**,
disparados por bronzina, camisa, anel ou pistão do mesmo motor. Quem abre o
motor precisa de junta nova na remontagem.

**Limite do upsell:** a Yampi só mostra upsell para quem paga com cartão de
crédito, e o checkout está com Pix como pagamento preferencial. Na prática o
upsell alcança a minoria dos pedidos. Não é defeito, é limite da plataforma,
mas explica upsell com pouca conversão.

## Cores do checkout e do order bump (15/09)

Estavam todas no padrão da Yampi: tag de desconto e link roxos (#725BC2),
botão principal verde claro (#3FC583), barra de anúncio roxa, order bump com
fundo amarelo (#FFFFD1) e botão rosa (#FE509C). Trocadas pela paleta da loja
em `/checkout/personalize`, abas Cabeçalho, Rodapé, Aparência e Order bump, e
conferidas recarregando cada aba:

- Cabeçalho: fundo #FFFFFF, elementos #14181A, barra #1E5B39 com texto
  branco, cronômetro #C08A2E.
- Rodapé: #F6F7F6, texto #6B7570.
- Aparência: títulos #14181A, descrições #6B7570, etapa ativa #1E5B39, valor
  total #14301F, valores com desconto #1E5B39, tag de desconto #1E5B39 com
  texto branco, barra de progresso #1E5B39, botão primário #1E5B39 com texto
  branco, secundário #14301F com texto branco, terciário #1E5B39.
- Order bump: fundo #FBF6EC (ouro claro), borda #C08A2E, botão #1E5B39.

Fonte ficou Rubik: a Yampi só oferece Work Sans, Rubik, Montserrat, Nunito e
Taviraj, nenhuma é a Inter do site. Formato dos botões: Arredondado.

Os campos de cor são `el-color-picker`. O que funciona por JavaScript: pegar
o `input` de texto visível (os ímpares, na ordem da página), trocar o valor
pelo setter nativo e disparar `input`, `change` e `blur`. O Salvar nem sempre
mostra aviso: recarregue a aba e leia de novo.

## Regras do checkout

Em `/checkout/rules`, corrigidas em 11/09 a pedido do cliente e conferidas
depois de recarregar:

- **Permitir compras de: Pessoa física e jurídica.** Antes era só física, e
  oficina ou revenda que precisa de nota no CNPJ não fechava pedido.
- **Solicitar data de nascimento: desligado.** Era campo a mais no meio da
  compra, sem uso no processo.
- **Selecionar o primeiro endereço automaticamente: ligado.** Quem volta não
  redigita.

Ligados e corretos: prazo de entrega visível, prazo em dias úteis, previsão na
página de obrigado, cálculo de frete no carrinho, juros do parcelamento à
vista, números de pedido sequenciais.

**`skipToCheckout=1` está como o cliente quer** (confirmado em 03/09). O custo
disso para quem compra várias peças está registrado em `tema-e-design.md`.

## Pagamento e frete

**Gateway único: Mercado Pago.** Aceita Visa, Mastercard, Elo, Boleto e Pix.
Não aceita American Express, Hipercard, Diners, Aura, Discover nem Pix
Parcelado. O parcelamento e os juros são configurados no Mercado Pago, não na
Yampi, então a loja não pode prometer "em até N vezes" no site sem conferir
lá.

**Frete: a Frenet responde pelo envio**, pelo aplicativo. Dentro da Yampi só
existe um frete cadastrado, "Retire na loja, A Trator Diesel Goiânia". Quem
for mexer em frete olhe a Frenet, não a lista de fretes da Yampi, que parece
vazia e não está.

## Dados cadastrais, Yampi contra Shopify

| campo | Yampi | Shopify | situação |
|---|---|---|---|
| razão social | VL COMÉRCIO DE MOTORES E PEÇAS LTDA | não cadastrada | **a Yampi tem o que falta na Shopify** |
| CNPJ | 09.246.474/0001-92 | não consta no endereço de cobrança | igual ao do site |
| endereço | Av. Bandeirantes 948, Qd.39 Lt.07, Vila Regina, 74453-465 | mesmo | bate |
| e-mail de contato | sac@atratordiesel.com.br | sac@atratordiesel.com.br | bate |
| telefone | (62) 9839-8287 | (62) 3086-7211 | diferente de propósito |

O telefone difere porque o checkout e os e-mails transacionais são pós-venda,
e pós-venda é o 9839-8287. A divisão completa dos dois números está em
`comece-por-aqui.md`.

A descrição da loja na Yampi tem 126 caracteres e um espaço duplo entre
"Agrícolas" e "e Motores Estacionários".

## Reconferido ao vivo em 21/09/2026

Painel aberto, três telas lidas: "Desconto por Pix" (`/discount/payments/30404`)
com 5% e **"Permitir acumular com outros descontos ativos" desmarcado**, e a
lista de cupons com `BEMVINDO5OFF` (primeira compra, 5%, uso único, 2 usos) e
`VOLTA7` (recuperação de carrinho, 7%, 0 usos). Nada mudou desde 18/09 e
**nada soma**: o checkout aplica só o maior desconto.

O que mudou foi o **site**. A faixa da home dizia "Primeira compra na loja,
5% de desconto" enquanto a página de produto diz "R$ X no Pix (5% de
desconto)", e quem chegava pela primeira vez para pagar no Pix lia 10% e
recebia 5%. A faixa passou a anunciar o Pix, que é o desconto que quase todo
mundo recebe de fato e que também vale para cliente recorrente, e diz em
letra que o checkout usa sempre o maior, nunca os dois somados. O
`BEMVINDO5OFF` continua na Yampi para quem paga no cartão, onde ele passa a
ser o maior; ele só deixou de ser anunciado como se somasse.

**Se um dia o Pix subir para 7%**, o `VOLTA7` perde a razão de existir, porque
o carrinho abandonado deixa de ter vantagem sobre a compra normal. Decisão
comercial, não de tema.

## A pergunta do cliente em 22/09/2026

"Se oferecemos 5% no Pix, os 5% de primeira compra acabam não fazendo muito
sentido." Meio certo, e a parte errada é a que importa.

No caminho do **Pix** ele está certo: os dois valem 5%, não somam, e o
checkout aplica o maior. Para quem chega pela primeira vez e paga no Pix, o
`BEMVINDO5OFF` não acrescenta nada.

No caminho do **cartão**, não: ali o desconto de Pix não vale, e o
`BEMVINDO5OFF` é o único que existe. Tirar o cupom não simplificaria nada,
só deixaria sem desconto justamente quem precisa de um empurrão para comprar
pela primeira vez numa loja que ainda não conhece.

Então nada muda, e nada precisa mudar no site: a faixa da home já anuncia o
Pix (que quase todo mundo recebe e que também vale para cliente recorrente)
e já diz em letra que o checkout usa sempre o maior desconto. O cupom
continua na Yampi sem ser anunciado, que é o lugar certo dele.

**Se um dia o cliente quiser que a primeira compra volte a valer alguma
coisa**, o número dela tem que ser diferente do Pix. Só que subir para 7%
esbarra no teto de 7% por pedido e tira a razão de existir do `VOLTA7`.
Decisão comercial, e das que mexem no caixa: não se toma por conta própria.

---

## Teto de 7%, conferido em 15/09

Nada no painel passa de 7% no mesmo pedido:

- **Cupons**: 5% e 7%, os dois com "Permite acumular com outras promoções"
  desligado.
- **Faixas de desconto** (`/marketing/progressive-discounts`): três faixas por
  valor, R$ 400 a 899,99 com 3%, R$ 900 a 1.999,99 com 5% e acima de R$ 2.000
  com 7%. **As três estão INATIVAS** e sem acumular. Se alguém ligar, manter o
  acumular desligado, senão 7% da faixa mais 5% do cupom de 1ª compra dá 12%.
- **Desconto no Pix, 5%, desde 18/09/2026** (a pedido do cliente). Não fica
  na tela do meio de pagamento (`/checkout/payments/43` não tem campo de
  desconto): é Descontos, Criar desconto, "Meio de pagamento",
  `/discount/payments/30404`, "Desconto por Pix", ativo, com "Permitir
  acumular com outros descontos ativos" **desligado**. A dica do painel:
  "Se não permitir, o maior desconto será aplicado." Então o pedido leva
  no máximo 7%: Pix 5% ou BEMVINDO5OFF 5% dão 5%, VOLTA7 dá 7%, nunca
  somam. Boleto e cartões seguem sem desconto. Só um desconto por meio de
  pagamento é permitido.
- **O site repete o Pix**: `snippets/atd-pix.liquid` calcula "R$ X no Pix"
  com o metacampo da loja `atd.pix_pct`. Desde 18/09 (noite) a tarefa
  agendada "Sincronizar Pix e Google" lê esta tela pelo Chrome de segunda a
  sábado às 8h e copia o percentual; mudança na Yampi chega ao site no dia
  seguinte (ou na hora, com "Executar agora" na tarefa). Ver o item 13 de
  `comece-por-aqui.md`.
- **Promoções, Brindes, Cashback**: vazios. Compre junto é recurso só da
  loja virtual da Yampi.
- **Parcelamento no site**: fora, decisão do cliente em 18/09.
- **21 order bumps e 4 upsells**: preço promocional 0,00 em todos, preço de
  venda igual ao da Shopify, centavo a centavo.

## Cashback

Não configurado. É a menor prioridade da lista: faz sentido para oficina e
revenda que compram toda semana, não para quem troca uma peça a cada dois
anos.
