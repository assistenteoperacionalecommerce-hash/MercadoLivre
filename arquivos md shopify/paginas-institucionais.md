# Páginas institucionais e acertos de interface

Tudo medido no tema DEV (`145492672560`, cdn `/t/23/`; até 16/09 era o `144975724592`, `/t/21/`). O código está em
`assets/atd-sistema.css` e `assets/atd-paginas.css`, com a medição escrita ao
lado de cada regra.

---

## As três políticas não são páginas

Termos de serviço, Política de privacidade e Política de reembolso são
**documentos do painel da Shopify**, em Configurações, Políticas. Não aparecem
em Páginas, e é por isso que ninguém as encontrava na lista.

**O editor delas apaga o atributo `class` do que você cola.** Só estilo em
linha sobrevive, e para vencer estilo em linha a partir do CSS só com
`!important`. Foi assim que o título das políticas saiu do branco sobre
branco: `body .shopify-policy__body h1` e `h1 + p` voltam para a tinta
`#14181a` e o cinza `#6b7570`, com `!important`.

As três hoje trazem o (62) 9839-8287, que é o número de pós-venda. O link
delas entrou no rodapé.

**Página e política dizem a mesma coisa em dois lugares.**
`/pages/politica-de-devolucao` e `/policies/refund-policy` têm o mesmo texto,
e o mesmo vale para a privacidade. Mudou uma, mude a outra.

## A faixa de quatro fatos cortava o e-mail

São os quadradinhos abaixo da capa em troca e devolução, central de ajuda,
fale conosco e privacidade.

A grade tem `overflow: hidden` por causa dos cantos arredondados. Com quatro
fatos numa coluna de 1032px, cada caixa fica com 257 e sobram 209 por dentro,
e `sac@atratordiesel.com.br` em 17px pede 214. Os cinco pixels que faltavam
não quebravam linha, eram **cortados pela borda**: o endereço aparecia sem o
fim.

Corrigido com valor em 16px, que pede 202, mais `overflow-wrap: anywhere`. No
celular rótulo e valor dividem a mesma linha, e quando o par não cabe o valor
desce sozinho com a largura inteira. Medido depois: Central de ajuda caiu de
371px para 203px de faixa, Fale conosco 223px, nada cortado a 320, 375 nem
1440.

`.atd-doc__destaque` seguiu a mesma lógica: 20px cortava o e-mail a 320px,
caiu para 18px com `overflow-wrap: anywhere`.

## Fale conosco: o formulário é nativo e fica

É `{% form 'contact' %}`, posta em `/contact`, e a Shopify entrega no e-mail
de atendimento do admin. Não é app nem integração.

Hoje `contactEmail` é `sac@atratordiesel.com.br` e o e-mail da conta é
`lucianaleao@atratordiesel.com.br`. **Só um envio de teste confirma para qual
dos dois cai.**

Trocar por um `mailto:` seria pior: abre o programa de e-mail do aparelho, que
em muito desktop não está configurado, e o contato morre ali. O formulário
chega com e-mail e telefone do cliente, e o balcão responde direto.

**Feito.** `blocks/contact-form.liquid` ganhou o campo
`contact[Modelo da máquina]`, que é a primeira coisa que o balcão pergunta.
Campo extra em formulário nativo aparece na notificação com o nome que você
deu, sem app.

### O formulário fora do prumo, 18/09

Medido no DEV a 1440, antes: o formulário usava os trilhos do tema e ficava
mais estreito que a capa da página, e os campos de um par (nome e telefone,
por exemplo) saíam com 330px cada.

Três consertos, em `assets/atd-paginas.css`:

1. **Voltou para a medida do documento**, 199 a 1231, exatamente onde começa
   e termina a capa. Antes ele obedecia à régua do tema, não à da página.
2. **Os dois campos por linha viraram grade de duas colunas, com o rótulo em
   cima.** Os rótulos já existiam no HTML: estavam `visually-hidden`, com
   `position: absolute !important`, e por isso o formulário parecia uma
   pilha de caixas sem nome. Campos passaram de 330 para 506px, com 58px de
   altura mínima.
3. **Abaixo de 750px vira uma coluna só**, sem rolagem lateral.

**Acerto de iniciativa, não pedido:** o botão de enviar tinha 106px, do
tamanho exato do texto, e ficava perdido embaixo de um campo de 506. Ganhou
200px de largura mínima.

## Mesma largura e menos vão, 18/09 noite

Relatos: "as páginas não estão na mesma largura" e "a distância entre o bloco
verde e o menu está muito grande". Em `assets/atd-paginas.css`:

- **Menu até a capa: 112px viraram 32** (20 no celular). Eram três vãos que
  ninguém decidiu juntos: 40 de recuo da seção, 32 de vão por causa do bloco de
  título (fica vazio, o H1 mora na capa) e 40 de margem da capa.
- **Texto sem teto de 66ch.** Vai da borda esquerda do miolo até o fim da capa:
  no Contato, sem índice, de 705 para 1032px; nas páginas com índice, de 705
  para 752.
- **Políticas na mesma coluna**, 199 a 1231 a 1440. O texto colado no painel
  vem num `<div>` com `max-width: 840px` e a fonte do sistema em linha; a folha
  desfaz as duas coisas com `!important`. O H1 da Shopify ("Termos de
  serviço") saiu, porque o documento já tem o dele ("Termos de uso").
- **Celular: 16px de lado** em capa, texto, formulário e políticas, a régua do
  resto do site. Era 24 só nas páginas.

## Régua de 1280 com o título na esquerda, 18/09 (tarde)

Decisão do cliente: páginas e políticas na régua do site (75 a 1355 a 1440,
`--doc-largura` 1328 menos 24 de cada lado, a mesma conta das faixas da
home), e para a linha de texto não passar de 140 caracteres, cada assunto
em duas colunas a partir de 990px:

- `.atd-doc__bloco` vira grade `300px | 1fr` com 72 de vão. O `h2` ocupa as
  linhas 1 a 40 da grade (as vazias medem zero) e fica `sticky` a 144px, logo
  abaixo do cabeçalho fixo de 120. Texto de 447 a 1355.
- Bloco sem `h2` (a abertura da privacidade) usa a largura inteira.
- "Nesta página" deixa de ser coluna e vira linha de pastilhas acima do
  texto: os títulos já estão na esquerda.
- **Políticas** não têm classe. A grade é o `div` que tem dois ou mais `h2`
  como filhos (`div:has(> h2 ~ h2)`); o `h2` fica na linha do primeiro
  parágrafo do assunto. O que vem antes do primeiro `h2` e a caixa "A versão
  curta" (`border-left` em linha) usam a largura inteira.
- Formulário do Contato e contêiner das políticas também em 1328.

## As caixas do topo das políticas, 18/09 (tarde)

O editor tinha tirado a separação entre rótulo e valor ("Prazo para
desistir7 dias corridos"). Reescritas pelo TinyMCE do admin
(`tinymce.get()`, `setContent`, disparar `input` e `change`, clicar
Salvar). **O que sobrevive na vitrine**: `span` e `strong` com
`display:block`, `margin` (inclusive negativa), `padding`, `border`,
`background`, `flex`. **O que a Shopify apaga do HTML servido**:
`<header>`, `gap`, `box-sizing`, `text-transform`, `overflow-wrap`. Por isso
o vão entre as caixas é margem (`0 10px 10px 0` na caixa, `0 -10px 20px 0`
no invólucro) e o rótulo não vem em versalete.

---

## Acertos de interface do produto

**Menos e mais da quantidade.** As duas caixas mediam 44x48 e os dois ícones
16x16, iguais. A diferença era o desenho: o menos é um traço único de 9,7px e
o mais é o mesmo vão repartido em dois braços de 4,85px, então o olho compara
traço cheio com meio braço. Traço dos dois foi de 1 para 1,6px e o menos
encolheu para 72% da largura. A caixa de 44px não mudou.

**Divisórias da quantidade (16/09).** Relato: com 1 unidade o fio do lado
do menos sumia e menos mais número viravam um quadrado branco grande, com o
mais parecendo bem menor. Medido: a borda do menos desabilitado ia a 0px e
nenhuma regra legível explicava (nem seletor de dois níveis com `!important`
vencia; suspeita na folha do Yampi, de outro domínio). A divisória saiu dos
botões e virou sombra interna dos dois lados do campo, em
`assets/atd-botao-carrinho.css`. Caixas 44 | 46 | 44, traço do botão
desabilitado em cinza `#aab2ad`.

16/09 (noite), segundo relato com print: o mais ainda parecia menor e o botão
verde tinha a borda direita cortada. Causa medida a 961px: caixa da quantidade
com 124px para 134px de conteúdo, e botão 12px além da coluna. Agora a caixa
tem 136px fixos, o botão encolhe até a coluna, desce para a linha de baixo a
partir de 750px quando não cabe, e perde o ícone abaixo de 420px. Conferido em
1440, 1100, 961, 768 e 375px. Mesmo arquivo, `assets/atd-botao-carrinho.css`.

**Marcadores da galeria.** Cada bolinha saía 18x48 por causa de um
`min-height: 48px` que o tema põe em todo botão. Agora são quatro bolinhas de
10x10, o alvo de toque volta por um `::after` transparente, e **só a cor muda**
entre a ativa e as outras: verde `--atd-verde-700` contra cinza
`--atd-cinza-200`. Uma primeira tentativa esticou a ativa para 26x10 e o
cliente recusou: quando o pedido é "só a bolinha pintada", tamanho igual faz
parte do pedido.

**Linha de compra no celular.** A 375px a linha saía 343x114, quebrada, com a
quantidade sozinha em cima. Agora é uma linha só, 343x52: no celular a
quantidade encolhe (botões de 38 em vez de 44, campo de 34 em vez de 46, dando
112px) e o botão divide a sobra em vez de ter largura automática.

**Faixa do vídeo da home.** A logo chegava com 0x0: o arquivo é um SVG sem
tamanho próprio e a regra do bloco só escrevia `max-width` com `height: auto`,
que sem largura declarada resolve em zero. A caixa virou linha, com a logo em
`order: -1` e largura declarada, 120px no desktop e 92px no celular. A caixa
continua absoluta e centrada pelo `transform` do bloco: **não mexa naquele
transform.** Medido depois, a 1440px: logo em 75, frase terminando em 1355.

O seletor da logo do vídeo precisa de `img` na frente:
`[class*='ai-video-banner__logo-']` sozinho casa também com `logo-wrapper-` e
`logo-placeholder-`.
