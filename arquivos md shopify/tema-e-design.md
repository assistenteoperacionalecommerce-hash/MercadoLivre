# Tema e design

Funde `tema-dev-direcao-visual.md`, `tema-dev-estado.md`,
`tema-dev-pagina-de-produto.md` e `home-largura-marcas-e-zoom-04-09.md`.
Medido no tema de trabalho. **Atenção, os papéis viraram em 18/09/2026**: o
`145492672560` (cdn `/t/23/`), que este documento chamava de DEV, é hoje o
tema **publicado**. A cópia despublicada de mesmo nome, `144975724592`, é um
retrato antigo e não serve. O tema de trabalho passou a ser **"DEV - Filtros,
carrinho e celular 18-09", `gid://shopify/OnlineStoreTheme/145546182704`, cdn
`/t/24/`**, duplicado do publicado com OK do cliente. Tudo o que está escrito
aqui como medido no "DEV" vale para os dois, porque um é cópia do outro.
O `ATUAL` (`142522941488`, cdn `/t/6/`) saiu do ar e nunca foi tocado.

Base: documento "Análise UX e CRO Site Trator". Restrições do cliente: manter
a logo como desenho, sem travessão nos textos.

---

## 1. Direção visual e paleta

Um só lugar define cor: o `:root` de `assets/atd-catalogo.css`.

```
--atd-tinta      #14181a   texto e títulos
--atd-verde-900  #14301f   preço, rodapé
--atd-verde-700  #1e5b39   botões, ações
--atd-verde-050  #f1f5f2   faixas claras
--atd-ouro       #c08a2e   acento único
--atd-cinza-600  #6b7570   apoio
--atd-cinza-200  #e4e7e4   linhas
```

Antes havia quatro verdes brigando (#18290e, #2A4E15, #143d27, #1f5e3b) e
dois dourados. Os nomes antigos continuam como apelido apontando para os
mesmos valores, então nada quebra.

**Regra de cor: verde cheio (`#1e5b39`) é a ação de comprar, e a ação que
confirma uma escolha** (por exemplo "Ver 62 itens" da gaveta de filtros).
Nada mais usa. Por isso "Filtrar" e o X de fechar a gaveta viraram vazados:
fechar não é ação principal de lugar nenhum.

**Título de produto é preto em todo lugar**, catálogo, página do produto e
similares. O verde ficou só no preço, em negrito, que é o número que decide a
compra.

**Ouro como acento único, três lugares:** risco embaixo de "Produtos" com o
menu aberto, filete no topo do painel e anel de foco dos ícones do cabeçalho.

As linhas douradas acima dos títulos de seção foram removidas: pareciam erro
de renderização. A linha que "não completava" era um `::before` com
`width: 1920px` fixo, agora é `inset-inline: 0`.

### Tipografia, duas fontes, sem sobreposição

- **Barlow Condensed 700 é a voz da loja.** Título de seção, título de página.
- **Inter é o dado.** Texto corrido, nome de peça, código, medida, preço,
  botão, etiqueta. Por isso **o título do produto fica em Inter mesmo sendo
  `h1`**: ele não é a voz da loja, é o nome da peça com marca, modelo e
  medida dentro.

Escala única: `h1` `clamp(30px, 8.4vw, 42px)`, `h2` `clamp(26px, 7vw, 32px)`,
título de produto `clamp(22px, 5.8vw, 30px)`. Preço em Inter com
`tabular-nums`, para a coluna de preços do catálogo não dançar de linha em
linha.

Poppins estava escrita no CSS do preço dos cartões da home e **nunca era
carregada** pelo tema. Continua em `blocks/produtos_em_destaque.liquid`
(25KB), neutralizada por CSS, não removida da origem.

**Efeito colateral aceito:** o campo "Tamanho do título" dos blocos do editor
deixou de valer, porque a regra usa `!important`. Para mudar, mexe-se a
escala, não o campo do editor.

Regra de sistema (tipografia, prumo, controles) mora em
`assets/atd-sistema.css`, a última folha da fila. Regra de sistema nova entra
lá, nunca numa folha nova.

### Dados de contato

Endereço correto, igual no site inteiro: Av. Bandeirantes, 948, Qd.39 Lt.07,
Vila Regina, Goiânia, GO, 74453-465.

Arquivos com número escrito: `snippets/atd-contato.liquid` (referência),
`atd-whatsapp.liquid`, `atd-whatsapp-float.liquid`, `atd-schema-loja.liquid`
(JSON-LD), `blocks/atd_produto_ficha.liquid`, `sections/footer-group.json`.

O Shopify não aceita `{% include %}` dentro de blocks do editor novo, só
`render`, e `render` não devolve variáveis. Por isso o número está copiado em
vez de centralizado. Mudou? Procure por `556230867211` no tema.

---

## 2. Régua e largura das faixas

Arquivo: **`assets/atd-regua.css`**, ligado por último em
`layout/theme.liquid`, depois de `atd-paginas.css`. Ele tem a palavra final
sobre largura de faixa, zoom e tamanho da logo.

### A loja inteira estava encolhida em 15%

`assets/base.css`, do próprio tema, traz `--page-zoom: 0.85 !important` e
`html { zoom: var(--page-zoom) }`. A loja era desenhada em tamanho normal e
reduzida em 15% na exibição.

| a 1440px | desenhado | chegava na tela |
|---|---|---|
| coluna de conteúdo | 1280px | 1088px |
| margem lateral | 201px | 171px |
| logo do cabeçalho | 52px | 44px |

`atd-regua.css` devolve o zoom para 1, com `!important`. Para desfazer, troque
o `1` por `0.85` nessa única linha.

### Uma régua só, da tarja de benefícios ao rodapé

`--atd-recuo: max(24px, calc((100% - 1280px) / 2))`, usada por home, listagem,
cabeçalho e rodapé. Medido depois: **todas as faixas começam em 80 e terminam
em 1360** numa tela de 1440. A 1280 dá 0 e 1280, a 375 dá 16 e 359, sem
rolagem horizontal.

O que cada conserto fez:

- **Tarja de benefícios**: `justify-content: space-between` no lugar de
  `center`, e o recuo de 20px sai só do primeiro e do último item. O recuo do
  meio fica, porque é ele que dá ar ao fio divisório.
- **Vídeo**: a caixa do texto era absoluta, 800px, com
  `transform: translate(-50%, -50%)`. Passou a ocupar a régua inteira, texto à
  esquerda e marca à direita. Ao trocar `left` e `right` por zero, o
  `transform` precisa perder o `translateX`, senão o texto sai meia tela para
  o lado. E a logo precisa de `width: auto`.
- **Rodapé**: `padding-inline: 100px` virou `var(--atd-recuo)`, e o bloco
  centrado virou duas colunas, contato à esquerda, documentos e redes à
  direita.

### Cabeçalho, régua resolvida

O cabeçalho usava 91px de recuo contra os 24px do resto do site a 1280px. A
regra que impunha 91px não aparece em nenhuma folha legível pelo navegador,
nem numa varredura de `document.styleSheets`. Causa provável: o tema declara
a regra dentro de uma `@layer`, e para `!important` a ordem entre camadas se
inverte.

**Causa achada em 15/09:** a regra estava no bloco Liquid personalizado
"Ajustes do cabeçalho" (`sections/header-group.json`, `custom_liquid_ijMwMp`),
com `calc((100% - 1088px) / 2)`, valor da época do zoom. É um `<style>` no
corpo, por isso ganhava das folhas do head. O remendo antigo
(`snippets/atd-regua-cabecalho.liquid`, estilo inline por JS com 60ms de
atraso) corrigia depois de cada redesenho do tema, e a logo e o menu pulavam
96px de cada lado ao abrir a página. A regra agora usa `var(--atd-recuo)` na
origem e o snippet foi esvaziado. Medido: logo em 75 a 1440, sem estilo
inline.

**Fio do cabeçalho.** O CSS compilado do tema pintava sombra e fio em marrom
`#5c3d1e`. Sobrescrito no mesmo bloco por um fio `#e4e7e4` de 1px.

**Logo do cabeçalho: 60px**, com a faixa subindo de 76px para 88px. A
proporção continua 0,68 de logo para faixa. Com o zoom em 100%, a marca chega
na tela como 60px contra 44px antes, 36% maior. A regra vale em
`atd-regua.css`; a antiga continua em `atd-home.css` como histórico, mas quem
manda é a nova, porque carrega depois.

**Linha única desde 750px (16/09).** Entre 750 e 989px o menu caía numa
segunda linha, com o estilo antigo do `styles.css` (20px, marrom `#3b2a1a`,
peso 600, `!important`) e 70px de recuo à esquerda. A regra de linha única
do bloco "Ajustes do cabeçalho" passou a valer desde 750px, e o menu ficou em
tinta, largura só dos links. **Menu em 16px, peso 500 (15/09):** estava em 15px
e 600, mas o tema só carrega Inter 400, 500, 700 e 800, e o navegador desenhava
o 600 em 700. O menu era o texto mais pesado do cabeçalho e destoava da busca
e do mega menu. Antes de usar um peso, confira `document.fonts`. Entre 750 e 989px o botão da busca
fica só com a lupa. Medido: 88px de altura a 954 e 768, sem rolagem lateral.

**Busca do cabeçalho sempre à vista (16/09).** Antes ela sumia na home
enquanto a busca do banner estava na tela, e a linha ficava com 650px vazios
entre o menu e os ícones a 1440. A regra que escondia continua no bloco
`ai_gen_block_baca937`, anulada no "Ajustes do cabeçalho". As duas buscas
empilhadas incomodaram o cliente, e a do banner saiu (ver "Hero").

**Menu Produtos com os tipos mais procurados primeiro (16/09).** O corte de
12 tipos por marca era alfabético, e na Yanmar parava em Escapamento: Filtro,
Juntas, Pistão e Virabrequim ficavam fora e Decalque ficava dentro. A lista
`prioridade` (Filtro, Juntas, Anéis, Bronzinas, Pistão, Camisa, Virabrequim,
Válvula, Faca para Rotativa) vem primeiro em `snippets/atd-menu-produtos.liquid`
e em `snippets/atd-nav-categorias.liquid`, que é a fila do celular e perdeu o
corte de 14 (ela rola de lado). Tipo novo e importante entra nas duas listas.

**Busca do celular (16/09).** Vinha do `base.css` com borda de 2px azul-marinho
`rgb(44, 62, 148)` e cantos de pílula. Regra 4 de
`snippets/atd-ajustes-mobile.liquid`: borda `#cfd6d1`, 4px de canto e foco
verde, igual ao desktop.

**Armadilha de medição:** com o painel do navegador escondido, transição de
CSS não avança, e `getComputedStyle` devolve o valor inicial para sempre
(o menu parecia continuar em 20px). Meça com
`*{transition:none !important}` injetado.

**Cabeçalho de 162px para 87px.** Logo no alto à esquerda, menu ao lado,
ícones à direita, numa linha só. Com o cabeçalho menor, o catálogo alcança a
dobra e o banner deixa de empurrar a loja para baixo.

---

## 3. As seis faixas da home, na ordem

1. Hero, "Máquina parada não espera", com o botão "Ver o catálogo"
2. Marcas, seis logos
3. Tipos de peça, nove atalhos com desenho
4. Vitrine, nove produtos
5. **Primeira compra**, faixa verde escura com os 5% do checkout Yampi
6. Não sabe qual peça, WhatsApp

**15/09: placa e vídeo saíram da home.** A placa repetia CNPJ, endereço,
telefones, e-mail e retirada que o rodapé mostra logo abaixo; o vídeo repetia
a frase do hero e não levava a lugar nenhum. O desenho da placa virou o
rodapé (`blocks/atd_rodape.liquid`). Os dois continuam no tema de backup
`BACKUP DEV 15-09 (antes do rodape novo)`, `145465606192`, e
`blocks/atd_placa.liquid` segue no DEV, sem uso.

A faixa 5 é `blocks/atd_primeira_compra.liquid`, com CSS próprio e editável
pelo painel.

### Tipos de peça com desenho (21/09)

A faixa 3 eram nove caixas iguais com uma palavra no meio, a parte mais
apagada da home: nada separava "Camisas" de "Válvulas" antes de ler. Cada
atalho virou uma linha com o desenho da peça num círculo verde claro à
esquerda, o nome no meio e a seta à direita, 286x78 no desktop, três por
linha. No celular a caixa vira coluna, 155x104, duas por linha, com o desenho
em cima do nome e sem seta, porque em 375 não cabem desenho e palavra lado a
lado sem cortar "Virabrequins".

Os desenhos são de traço, 24x24, em `snippets/atd-icone-peca.liquid`, e
herdam a cor por `currentColor` (verde parado, branco em fundo verde no
ponteiro). **O desenho é escolhido pelo nome do tipo**, passado pelo
`handleize`: "Anéis" vira `aneis`, "Pistões" vira `pistoes`. Tipo novo sem
desenho próprio cai na engrenagem e nada quebra; para dar desenho a ele,
acrescente um `when` no snippet. Existem doze: filtros, juntas, anéis,
bronzinas, pistões, virabrequins, camisas, plantadeira, válvulas, mancais,
retentores e rolamentos.

Nada mudou no schema do bloco, então o `index.json` não foi tocado.

### Vitrine, o nono produto (18/09)

Entrou o Jogo de Juntas da Caixa de Transmissão Yanmar TC11/TC14, 31 em
estoque, que conversa com o cabo de embreagem TC11 que já estava na vitrine.
Medido depois: quatro colunas mostram 8, três colunas mostram 9 e duas
colunas mostram 8, porque a grade completa a última linha.

Duas armadilhas apareceram nessa gravação, e as duas valem para qualquer
bloco do editor novo:

1. **O bloco tinha `for i in (1..8)` escrito na mão.** O nono produto só
   passou a existir depois de mexer no Liquid de
   `blocks/produtos_em_destaque.liquid`. Antes disso o campo estava gravado
   e nada aparecia.
2. **A Shopify aceitou o `index.json` com `userErrors` vazio e descartou o
   `product_9`.** O schema do bloco ainda não declarava essa chave, e o que
   o schema não conhece a Shopify normaliza para fora, em silêncio. **Grave
   sempre o bloco primeiro e o template depois**, e confira lendo o
   `index.json` de volta.

### Rodapé

`blocks/atd_rodape.liquid`, em `sections/footer-group.json`. Verde `#14301f`,
logo branca, nome em Barlow, filete ouro de 1px, quatro colunas com rótulo
ouro (Loja física, Atendimento, Horário, Pagamento) e linha final com razão
social, CNPJ e documentos. Envio e retirada em 24h ficam de fora porque a
tarja do topo já diz. Medido: colunas de 75 a 1355 a 1440, duas colunas a
900, uma a 375, sem rolagem horizontal. Telefone vira `tel:` a partir do
texto; os números estão nos campos do bloco, no `footer-group.json`.

**Acertos de 18/09, medidos no DEV.** O verde acima da logo caiu de 64 para
36px: era a maior folga do rodapé inteiro e empurrava a marca para longe do
topo da faixa. O valor de cada coluna (`.atd-rodape__valor`) subiu de 1,6
para 1,75 de entrelinha, que medidos dão 25,375px, e o nome da empresa de
1,0 para 1,15, que dão 25,3px: os dois passam a ter o mesmo ritmo de linha.

Abaixo de 640px o recuo de cima era 44px. Com o desktop caindo para 36, o
celular ficaria com mais folga que a tela grande, então baixou para 32px.
Foi acerto de iniciativa, não pedido, e está marcado como tal.

### Busca no hero, desligada em 16/09

Entre 15 e 16/09 o botão do hero virou campo de busca a partir de 750px, e o
campo do cabeçalho sumia enquanto ela estava à vista. Com a busca do
cabeçalho sempre visível, eram duas buscas no topo, e o cliente não gostou.
Desligada pelo campo "Mostrar busca" no `templates/index.json`: o código
continua no bloco, e religar é marcar o campo de volta.

A faixa de primeira compra não mostra código porque o `BEMVINDO5OFF` é cupom
de 1ª compra na Yampi e entra sozinho. **Se essa regra mudar na Yampi, o texto
muda junto.**

### Hero

Texto de 23/09, trocado pelo cliente no editor: título **"Máquina parada
custa caro"**, subtítulo **"Cada hora parada é prejuízo. Encontre a peça
certa para colocar sua máquina de volta ao trabalho."** Título sem ponto
final, como todo título da home; subtítulo com ponto, porque são duas frases.

**Hierarquia (23/09, tema 25).** Título em Barlow Condensed 700, 54px, numa
linha em toda largura (533px a 1440). Subtítulo em Inter 400, branco a 90%,
**uma frase por linha**: o bloco parte o texto no primeiro ". " e cada frase
vira um `.atd-hero-frase` em bloco. Antes, o `max-width: 46ch` do
`atd-vitrine.css` fechava a caixa em 500px e a quebra caía no meio da frase
("...a peça certa para / colocar sua máquina..."). Tamanho
`clamp(16px, 0.6vw + 11.5px, 20px)`, entrelinha 1,45 e teto de 34em, no
`atd-sistema.css`. Medido depois: 20px a 1440, frases com 265 e 638px e o
localizador logo abaixo com 640px; 17,6px a 1024 e 16px a 768, uma linha por
frase; a 375, 16px em 3 linhas ("Cada hora parada é prejuízo." / "Encontre a
peça certa para colocar" / "sua máquina de volta ao trabalho."). Conteúdo de
234 a 594 no banner de 164 a 664, a 1440.

**Tudo numa linha só foi descartado:** 97 caracteres passam da medida de
leitura, sairiam mais largos que o localizador e quebrariam de qualquer jeito
no celular. **Os sliders "Tamanho do título" e "Tamanho do subtítulo" do
editor não mandam:** o `!important` do `atd-sistema.css` ganha deles.

Até ali: título "Máquina parada não espera", subtítulo "A peça certa, hoje.
Sua máquina volta a trabalhar amanhã." (18/09). Antes, o subtítulo era "Cada
peça mostra em quais motores ela serve. Você confere antes de comprar.". Não cita código de
fabricante, decisão do cliente: facilita achar a peça fora da loja. Fica
centralizado de propósito, porque texto encostado no canto briga com o assunto
de uma foto de bancada cheia de peças.

Para alternar entre centralizado e alinhado à esquerda:
`--atd-hero-alinha` no topo do `assets/atd-sistema.css` (`center` ou `start`).

**Tamanho do título (18/09):** `clamp(34px, 3.2vw + 8px, 54px)`, medido 54 a
1440, 40 a 1000 e 34 a 375. Estava preso em 32 pelo h2 do sistema, igual aos
títulos de faixa, sem hierarquia. A regra mora no `atd-sistema.css`, logo
depois da escala de h2.

**Cor do hero (16/09).** A máscara em `assets/atd-vitrine.css` era um
gradiente da esquerda, feito para texto à esquerda, e ficou para trás com o
texto no centro: uns 30% de escuro atrás do título e quase nada à direita. A
foto é laranja de fim de tarde e brigava com o verde e o dourado. Agora a foto
tem `saturate(0.55)`, a máscara é radial verde quase preto (`rgba(11,22,15)`,
0,82 no centro e 0,45 na borda) e o botão é dourado `--atd-ouro` com texto
tinta, porque verde sobre máscara verde sumia. A opacidade do editor (60) é
anulada no CSS. **Se voltar para texto à esquerda, a máscara volta a ser
gradiente da esquerda.**

**Truque para trocar copy presa em `templates/index.json` sem reescrever o
arquivo:** renomear os campos do schema (`heading`/`subheading` para
`titulo`/`subtitulo`). O texto antigo gravado sob o nome velho vira órfão e a
Shopify ignora; o campo novo nasce sem valor e cai no padrão escrito no
schema. Serve para qualquer texto preso em template JSON.

**Banner esticado, mantido.** A Baymard mostra que carrossel de home é
implementado errado em 75% dos casos e que conteúdo estático rende igual. O
problema nunca foi a largura, era altura somada a cabeçalho gordo. Ficou
estático, com foto real de produto, na mesma coluna de 1280px.

### Faixa de marcas, algoritmo de área igual

Substitui qualquer versão anterior. Célula do tamanho do logo com
`object-fit: contain` deixa a fila **matematicamente alinhada e visualmente
torta**: quem é quadrado sobra espaço dos lados, quem é deitado sobra em cima
e embaixo, e o olho lê isso como espaçamento irregular (chegou a variar 2,3x
em área de tinta entre a maior e a menor logo).

**A correção iguala a área de tinta, não a caixa:**
`altura = raiz(área / proporção)`, `largura = altura x proporção`, com a área
comum saída do logo mais quadrado da fila (quem primeiro bate no teto de
altura). Não é a maior área que caiba na linha inteira: testado e descartado,
porque encher a linha faz metade dos logos baterem no teto e a regra de área
para de valer. O que sobra vira vão, dividido por igual.

Calculado em `snippets/atd-marcas-medida.liquid`. Teto de 200px de largura
para qualquer logo, senão a Lavrale, que é uma placa vermelha cheia, fica
com o dobro do peso visual das marcas recortadas.

**A faixa virou cartão em 23/09/2026, e o desenho tem um dono só.** Antes
disso, quatro arquivos a desenhavam ao mesmo tempo e discordavam: o bloco
pedia célula de 160x100, `atd-vitrine.css` impunha grade de 8 colunas,
`atd-regua.css` impunha fila sem quebra com item elástico, e
`atd-sistema.css` impunha altura, vão e um `border-bottom` em cada logo, com
`!important`. O filete que o cliente reprovou duas vezes vinha desse último:
tirar a borda no bloco não apagava a linha da tela.

Hoje **as regras de marcas moram só em `blocks/marcas.liquid`**, e o script
de medida escreve apenas o tamanho da imagem, lendo a célula que o CSS
desenhou. O `data-atd-medido` ainda existe, mas só serve para revelar os
logos depois da conta: ninguém lê o valor dele para decidir layout.

O cartão: fundo branco, borda de 1px, canto de 4px, hover com borda verde e
subida de 2px, que é o mesmo desenho dos atalhos de tipo de peça logo
abaixo. Uma linha só no computador (`flex: 1 1 0` reparte a régua entre
quantos cartões houver), quatro por linha abaixo de 1100px, duas abaixo de
750px. Medido a 1440: sete cartões de 170x100, primeiro em 75 e último
terminando em 1355. A 375: duas colunas de 162px em 16 e 198, idêntico às
colunas dos tipos de peça.

**O bloco não escreve `max-width` nem `margin: 0 auto`**, senão ganha da
régua do `atd-vitrine.css` e a faixa sai do prumo do resto da home (medido
antes: home começando em 80 e marcas em 155). E usa `padding-block`, nunca
`padding` inteiro, que apagaria o `padding-inline` da régua.

A fila de tipos de peça usa a mesma célula, o mesmo vão de 32px e o mesmo
filete que a fila de marcas. Alinhamento pela esquerda
(`justify-content: flex-start`), não centralizado, para o atalho sozinho da
última linha não flutuar no meio da faixa. Abaixo de 1000px a fila quebra em
linhas e volta a ser centrada, que é o certo quando a última linha tem menos
itens.

**Marcas em cor cheia.** Começar em cinza fazia a fileira parecer apagada. O
hover sobe 2px em vez de colorir.

**Logo com fundo branco de JPEG** (caso Lombardini): `mix-blend-mode:
multiply` faz o branco sumir contra o fundo `#f6f7f6` da seção sem editar o
arquivo. Vale para qualquer logo que subir depois.

**No mega menu a marca é texto, não logo** (testado e revertido): numa coluna
estreita a Yanmar quase quadrada encolhe a uns 35px e vira selo minúsculo, e
com uma marca em logo e cinco em texto a coluna desalinha.

A linha de texto abaixo dos logos: "Para Toyama, Tramontini, Agritech, Buffalo
e outras marcas, mande o modelo no WhatsApp que a gente localiza."

---

## 4. Cabeçalho, mega menu e celular

**Mega menu** (`snippets/atd-menu-produtos.liquid` mais `atd-catalogo.js`).
Passar o mouse em "Produtos" abre um painel de 900px: marcas na coluna da
esquerda, tipos de peça daquela marca na área da direita. Sem número nenhum. O
rodapé do painel lista os tipos gerais, para quem não sabe a marca. No celular
o primeiro toque abre e o segundo leva para o catálogo.

Duas armadilhas:

1. O tema **redesenha a seção do cabeçalho depois do DOMContentLoaded**, e o
   MutationObserver no `#header-group` não pega. Por isso o JS religa os
   ouvintes num intervalo de 300ms por 9 segundos, além do observer e do
   `shopify:section:load`. Sem isso o menu não abre.
2. O painel não pode ser movido para dentro do cabeçalho: o redesenho o
   apagaria. Ele fica no fim do `#header-group` e é posicionado por JS. Só que
   `position: fixed` ali cai **28px acima** do esperado, porque algum
   ancestral cria contexto de posicionamento. O JS mede onde o painel foi
   parar e compensa numa passada só, nunca em laço.

**Painel mais baixo, 19/09.** Relato: "o menu está muito alto, muito
grande". Medido antes, a 1440: 860x480, com a coluna das 8 marcas mandando na
altura (52px por linha) e a área de tipos usando pouco mais de um terço dela.
Nada saiu do menu: as mesmas 8 marcas e os mesmos 12 tipos continuam lá, o que
mudou foi o peso de cada linha. Linha de marca de 52 para 38px e nome de 16
para 15px; recuo da coluna de 18 para 14; a marca escolhida deixou de ser
faixa verde inteira e virou papel-2 com o nome em verde e um fio de 2px na
borda, que cresce de 0 para 20px na troca; o tipo de peça perdeu o fundo verde
no ponteiro e ficou só com a cor do texto, para a área da direita parar de
piscar blocos; a abertura ganhou 14 centésimos de subida e transparência,
desligados em `prefers-reduced-motion`. Medido depois: **860x357**, 26% mais
baixo, mesmo conteúdo. Tudo na seção 1 de `assets/atd-catalogo.css`.

> Onde fica a navegação do desktop: `<nav class="custom-nav">` dentro de
> `.custom-nav-wrapper`, em `snippets/atd-cabecalho.liquid`, chamado por
> `sections/header.liquid` (35KB). **Não** é o menu padrão do tema nem o
> menu do admin.

**Cabeçalho em duas linhas** (tema DEV, 15/09, comentários marcados 17/09).
Referência: Mercado Livre, Tractor Supply, Dutra Máquinas. Linha 1 (76px):
logo, busca de até 680px centrada e só com a lupa, conta e carrinho no mesmo
traço e sem fundo. Linha 2 (44px): Início, Produtos (mega menu), atalhos
Yanmar, Tobatta, Branco e Agrale (`atd_marcas_nav` no snippet) e Sobre Nós
encostado à direita. Medido: a 1440 a busca centra no meio exato da página e
fica a 204px dos ícones; a 1024 o campo tem 626px para um texto de 239px; a
800 tem 477px. Celular sem mudança. Três camadas antigas mandam no cabeçalho
com `!important` (styles.css, atd-home.css e a seção `custom_liquid_ijMwMp` do
grupo do cabeçalho, que vem depois no documento e forçava linha única em
flex), por isso o snippet usa `#header-group #header-component` e ganha por
especificidade. O carrinho era verde cheio por `body .button` do
atd-custom.css: anulado no fim de `assets/atd-botao-carrinho.css`. O
`header-actions` do tema tem margem de -14,4px, zerada.

**Ajustes de 16/09 no cabeçalho** (comentários do tema marcados 17/09):
- Busca no centro exato da coluna: colunas `minmax(100px, 1fr) minmax(0,
  680px) minmax(100px, 1fr)`. Antes era `auto 1fr auto` e ficava 13px para o
  lado da logo. Medido: 375 a 1055 a 1440 (centro 715, coluna de 75 a 1355),
  167 a 847 a 1024, 148 a 642 a 800 (a 43px da logo).
- Linha de baixo sem o vão de 700px: as 8 marcas do menu Produtos, mais
  Contato e Sobre Nós à direita. Lavrale, Lombardini e Tramontini somem
  abaixo de 1180px; Agritech abaixo de 900px. Sem rolagem lateral em 1440,
  1280, 1024, 900 e 800.
- **Hover do Produtos**: `atd-catalogo.js` decidia "mouse" por
  `(min-width: 990px) and (hover: hover)`. Janela entre 750 e 989px ou
  notebook com tela de toque caía no caminho do toque: hover ignorado, o foco
  do clique abria o painel e o clique ia para o catálogo (exatamente o
  relato do cliente). Agora decide pelo `pointerType` do último ponteiro; a
  largura só escolhe lado a lado ou sanfona. Conferido com mouse real (abre,
  segue aberto ao descer para o painel, fecha ao sair) e com toque simulado
  (primeiro toque abre e bloqueia a navegação).

**Peso do menu (18/09, revisão geral).** Todos os links em Inter 16px 500.
Marcas e Produtos em tinta; Início, Contato e Sobre Nós em cinza-600. O
Produtos em 700 (rodada da noite de 18/09) foi desfeito, porque lia como
erro: o que marca que ele abre um painel é uma seta pequena cinza, que vira
para cima com o painel aberto. Seção 11 de `atd-filtros.css`.

**Menu Produtos** lista 8 marcas: Yanmar, Agritech, Tobatta, Branco, Agrale,
Lavrale, Lombardini, Tramontini. Agritech é coleção por etiqueta, não por
título. A faixa de logos da home ficou com 5 (Lombardini saiu a pedido).

**Listagem**: a linha de apoio com a descrição da coleção saiu de
`blocks/atd_atalhos.liquid` a pedido. **Contato**: `blocks/contact-form.liquid`
ganhou `contact[Modelo da máquina]`.

A barra verde de catálogo (`atd-menu-catalogo.liquid`) foi aposentada.

**Ícones de conta e carrinho.** Ganharam 10px de folga e realce só no que está
sob o mouse.

**Cabeçalho da listagem** (`blocks/atd_atalhos.liquid`) perdeu os chips de
filtro e a contagem de itens, a pedido do cliente. Ficou trilha (Início /
Yanmar / Juntas), H1 e a primeira linha da descrição da coleção.

### Navegação no celular

Até 09/09 o celular **não tinha navegação por marca nem por tipo**. O cabeçalho
troca para a gaveta do tema, montada da lista de links do admin, e o painel
`atd-mega` só existe no desktop. A única navegação era "Filtrar", que abre
facetas começando por "Fabricante da peça" (quem fez a peça, não em que
máquina ela serve).

- **`atd-nav-categorias`**: duas filas de chips que rolam de lado, Marca da
  máquina e Tipo de peça, abaixo de 750px. Renderizado no cabeçalho da coleção
  (`blocks/atd_atalhos.liquid`) e na página de busca, **inclusive quando a
  busca não acha nada** (`sections/atd-busca-resumo.liquid`).
- **`atd-menu-celular`**: gaveta redesenhada. Nasceu com superfície escura
  `#14301f` (a mesma do rodapé) e rótulo em ouro; **em 18/09 virou branca**, a
  pedido do cliente ("o fundo verde está muito forte"), com filete de ouro no
  topo, nome da marca em tinta, fios em cinza-200, verde no ponteiro e rótulo
  em cinza-600. A troca está em `assets/atd-filtros.css`, não no snippet: como
  o snippet escreve o próprio `<style>` no corpo e usa `!important`, a classe
  aparece duas vezes no seletor (`.menu-drawer.menu-drawer`) para ganhar por
  especificidade e não por ordem. Marca em Barlow Condensed uma por linha
  com filete e seta (nome escrito, não logo: numa lista vertical curta o nome
  alinha e tem sempre o mesmo peso). Tipo de peça em Inter, duas colunas. No
  fim, WhatsApp, endereço e horário. O tema monta a gaveta sem gancho para
  trocar o conteúdo, então o snippet nasce escondido dentro do `#header-group`
  e um script copia para dentro de `.menu-drawer__navigation`, escondendo a
  lista original em vez de apagá-la (se o script não rodar um dia, a gaveta
  antiga continua funcionando).

**Marca ou tipo novo entra em três listas de handles**, de propósito, porque
snippet do editor novo não devolve variável: `atd-menu-produtos` (mega menu
desktop), `atd-nav-categorias` (chips) e `atd-menu-celular` (gaveta).

---

## 5. Página de produto e o bloco `atd_produto_ficha`

A ficha (`blocks/atd_produto_ficha.liquid`) mostra marca, código, motores ou
microtratores, estoque, entrega e WhatsApp, nessa ordem. O padrão de
preenchimento está em `catalogo-e-busca.md`.

- **Título duplicado removido.** O bloco de descrição repetia o nome. Saiu de
  `templates/product.json`. A ficha extrai só o texto corrido da descrição,
  cortando "Motores Compatíveis", "Especificações" e "SKU", que já aparecem em
  campo próprio acima.
- **Botão de adicionar ao carrinho** era branco vazado sobre fundo branco.
  Virou verde sólido, 44px de altura mínima.
- **Setas da galeria** saíam rosa. Causa: `mix-blend-mode: difference` no
  `slideshow-arrows`, que inverte o verde sobre foto branca. Forçado para
  `normal` com `isolation: isolate`, botões brancos com contorno cinza.
- **WhatsApp flutuante cobria o botão de comprar** (72x36px a 1440x900).
  Desde 15/09 `snippets/atd-whatsapp-float.liquid` recolhe o flutuante, só
  no template de produto, enquanto o primeiro `.add-to-cart-button` fora da
  barra fixa ou o `.atd-ficha__whats` estão na tela. Observar todos os
  botões de adicionar escondia o flutuante na home e na listagem, por causa
  dos cartões.
- **Retirada duplicada** ("Retirada disponível em A Trator Diesel, pronto em
  24 horas") saiu do card. A informação já está na ficha, com o endereço certo.
- **Coluna da foto em 600px**, medida com o zoom em 100%.
- **"Produtos vindo do ML" não aparece na trilha.**
  `blocks/atd_breadcrumb.liquid` tem lista de coleções a pular (`all`,
  `produtos-vindo-do-ml`, `produtos-exclusivos-ecommerce`,
  `vehicles-and-parts-example-products`). Para garantia total, despublique
  essas coleções do canal Loja Virtual.
- **H1 da página de produto era zero.** Agora é o título.
- **Preço e compra na primeira tela do celular (15/09).** A 375x812 a
  galeria era um quadrado de 375px mesmo com foto deitada, e a ficha (301px)
  ficava entre o preço e o botão: título em 682, botão em 1136. Abaixo de
  750px a moldura passou para 4:3 e a ficha desceu para depois do botão
  (`snippets/atd-ajustes-mobile.liquid`, regra 3). Medido: título em 588,
  preço em 662, botão de 722 a 774. No desktop nada muda.

### As duas colunas, 18/09

A coluna de texto tinha 400px numa tela de 1440, contra 600 da foto, e o
resto era vazio. A causa não estava em folha nenhuma: era
`--size-style-width: fit-content` escrito no próprio elemento pelo editor,
por isso as regras novas precisam de `!important`.

A grade de `assets/atd-home.css` passou a ser
`var(--atd-recuo) minmax(0, 628px) minmax(0, 1fr) var(--atd-recuo)`. Medido
a 1440: foto de 75 a 675 (600 quadrados, encostada na régua), texto de 731 a
1355 (624, era 400), 56px de vão. A altura da coluna direita caiu de 975
para 855, e o vazio embaixo da foto de 355 para 255.

**Faixa "peças para o mesmo motor".** `.atd-mm` fechava com 8px de respiro e
passou a fechar com 64, que é o respiro das outras faixas.

### A foto e a redistribuição da coluna de compra, 19/09

Quatro relatos do cliente na mesma mensagem, quatro causas diferentes. O
código está em `assets/atd-botao-carrinho.css`, que é a folha da área de
compra, e em `blocks/atd_compra_segura.liquid`. A medição de cada regra está
escrita ao lado dela.

- **"Um quadrado branco parecendo que foi jogado".** O quadrado da foto era
  branco puro sobre o `#f7f7f7` da página, sem moldura, sem canto e sem
  sombra, e a foto encostava na borda. Agora é uma moldura: branco, fio de
  1px a 7% de tinta, canto de 10px, sombra baixa e respiro por dentro.
  Medido a 1440: quadrado de 600x600 em 75, foto de 534x534 em 108. O
  respiro muda com a largura, porque a moldura não muda e o quadrado sim:
  32px no desktop, 20px entre 750 e 989 (a 768 o quadrado tem 315 e 32
  comiam um quinto da foto, que subiu de 251 para 273), e a 375 a moldura
  sai inteira, fica só o branco com 16px, porque fio e canto encostados na
  beirada da tela pareciam cartão grande demais.

- **"Algumas fotos sem fundo e outras com fundo branco".** O tema pinta o
  `<img>` com a cor de fundo da loja, num `<style>` que ele imprime na
  própria página: foto de JPEG com fundo branco ficava branca, foto
  recortada em PNG ou WEBP ficava `#f7f7f7`. Toda foto de peça passa a ter
  fundo branco, **na loja inteira**, cartões da listagem e da vitrine
  inclusive. Como o `<img>` ocupa a caixa toda com `object-fit: contain`, o
  branco dele e o branco da moldura viram a mesma superfície.

- **"Setas exageradas, e no mouse fica verde e a seta some".** A seta media
  44x44 com ícone de 32. No ponteiro, `body .button:hover` do
  `atd-custom.css` pintava o fundo de verde (a seta também tem a classe
  `.button`) e `body .slideshow-control:hover` do `atd-home.css` pintava o
  ícone de verde escuro: verde sobre verde, a seta sumia. Agora é um
  círculo de 38px quase branco com ícone de 18, e no ponteiro só a moldura e
  o ícone ficam verdes, com o fundo em branco cheio. O alvo de toque de 44px
  volta por um `::after` transparente, o mesmo truque das bolinhas. Medido a
  1440: setas em 91 e 621, 16px de folga de cada lado do quadrado.

- **"A parte da direita está sobrecarregada, redistribua nos espaços
  vazios".** Medido antes, a 1440: foto de 199 a 799 e coluna de compra de
  199 a 1071, 872px de altura, com 272px de branco parado sobre a foto. O
  cartão de garantias (228px) é a parte que menos decide a compra e a que
  mais ocupa altura. **A partir de 990px ele desce para debaixo da foto**,
  onde o vazio estava, e lá vira faixa deitada de três colunas, sem moldura,
  separada por um fio. Os 600px de largura cabem as três garantias lado a
  lado, o que os 400px da coluna de compra não cabiam (é por isso que três
  colunas tinham sido recusadas em 17/09: o argumento valia para aquela
  largura, não para esta). Medido depois, a 1440: coluna da foto de 199 a
  961, com a faixa de 600x162 e cada garantia em 191px; coluna de compra de
  199 a 819. O vazio caiu de 272 para 142 e mudou de lado, e a coluna de
  compra encolheu de 872 para 620.

  **Quem move é o próprio bloco**, no fim do `<script>` dele, e não uma
  folha de estilo: CSS não troca um elemento de pai. **Desde 18/09 à noite o
  limite é 750px**, onde a página já tem duas colunas; abaixo de 560px de
  coluna uma container query põe uma garantia por linha. Duas guardas: abaixo
  de 750px o cartão volta para o lugar de origem (uma marca de comentário
  guarda a posição exata), e a cara "Avise-me quando chegar" **nunca** desce,
  porque é formulário e precisa ficar onde o botão de comprar estaria.
  Conferido em 1440, 990, 768 e 375, com peça em estoque e peça esgotada,
  sem rolagem lateral.

Os acertos finos (botões de quantidade, marcadores da galeria, linha de compra
no celular) estão em `paginas-institucionais.md`.

### O respiro da coluna de compra, 19/09

Relato: "as informações estão muito amontoadas". Medido antes, a 1440 numa
peça em estoque: migalha em 223, título em 275, preço em 351, ficha em 424,
botão em 744. Vãos de 20, 40, 20 e 20, e dentro da ficha 14 fixos entre seis
itens de naturezas diferentes (código, marca, motor, estoque, caixa cinza de
entrega e um botão de WhatsApp de 624px).

O problema não era falta de espaço, era espaço sem hierarquia: quase tudo
separado por 20px, então o olho não distinguia identidade da peça, preço,
dados técnicos e compra. E o maior vão da coluna, os 40px entre título e
preço, que são o mesmo grupo, vinha de acidente: dois blocos de altura zero
(o `view-product-title`, oculto do tema, e o selo do Judge.me sem avaliação)
consomem um vão de 20px cada sem desenhar nada.

Todo o CSS mora no `{% style %}` do `blocks/atd_produto_ficha.liquid`, numa
seção chamada "Respiro da página de produto". O vão base de 20px continua
sendo o `--gap` do editor; as regras novas só somam por cima, com margem.

Régua em degraus, medida depois a 1440: migalha 235, título 295 (28), preço
355 (24), ficha 428 (20, mais 28 por dentro até o fio, dão 48), botão 834
(40). Peça esgotada segue a mesma régua, com "Avise-me quando chegar" no fim.

O que mudou dentro da ficha:

- **Entrega sem caixa.** Era fundo cinza com canto arredondado, caixa dentro
  de caixa. Virou texto em cinza-600 com fio de 1px em cima e 24px de
  respiro, e só o "Retirada em Goiânia" e o "Envio para todo o Brasil" em
  tinta. Separa sem pesar.
- **WhatsApp deixou de ser barra.** Era um botão vazado de 624px logo acima
  do "Adicionar ao carrinho", duas ações do mesmo tamanho competindo. Agora
  tem 282px e fica alinhado à esquerda. Armadilha: o botão é `display: flex`,
  então largura automática ainda preenche a coluna; quem encolhe é
  `align-self: flex-start` no invólucro mais `width: fit-content` no botão.
  Abaixo de 750px ele volta a ocupar a linha inteira.
- **Rótulo mais discreto**, 11px com 0,08em de entreletra contra 12px, e
  coluna de 104px (88 abaixo de 1259). Valor com entrelinha 1,6, prosa da
  descrição limitada a 62ch.

Fora da ficha, no mesmo `{% style %}`: a faixa "Compra garantida" ganhou 32px
de afastamento da foto, onde encostava com vão 0, e a seção do produto passou
de 36/40 para 48/64 de recuo vertical (24/40 no celular).

**Resolvido em 18/09, com autorização do cliente.** Entre 990 e 1259px a foto
ficava com 628px de coluna e a de compra com 304, o que esticava a ficha de
338 para 506px de altura. A coluna da foto passou de `minmax(0, 628px)` para
`minmax(0, min(628px, 54%))`, em `assets/atd-filtros.css`. Não precisa de
media query: acima de 1163px de régua o valor volta a ser 628 e nada muda.
Medido a 990, depois: foto 529, coluna de compra 403, ficha 375x383, altura da
coluna 861 contra 1057. A 1100: foto 589 e coluna 453. A 1259 e a 1440 nada
mudou, e a foto continua 600x600.

### O carrinho não existe no fluxo

Medido: clicar em "Adicionar ao carrinho" leva direto para
`seguro.atratordiesel.com.br/checkout?skipToCheckout=1`, o checkout da Yampi.
A página nem chega a ficar parada para o painel lateral abrir.

Custo de conversão: quem precisa de cinco peças não junta o pedido, cada peça
vira uma ida ao checkout. Mecânico com a máquina parada costuma comprar junto
(junta, anel, bronzina). A troca é configuração da Yampi, não do tema. O
cliente confirmou em 03/09 que o `skipToCheckout=1` está como ele quer.

---


### Filas de chips: as três em prumo (21/09)

A listagem no celular tem três filas que rolam de lado, e as três nasciam
diferentes. Medido a 375, antes: "Marca da máquina" e "Tipo de peça"
(`.atd-navcat__fila`, em `snippets/atd-nav-categorias.liquid`) sangravam de 0
a 375 com recuo interno de 16, mas nasciam com `scrollLeft: 16` e o primeiro
chip em **x=0**; "Modelo da máquina" (`.atd-modelos__fila`, estilo dentro do
bloco `atd_atalhos`) ia de 16 a 359, com o primeiro chip em 16.

A causa do chip em zero é `scroll-snap-type: x proximity` com
`scroll-snap-align: start` **sem `scroll-padding-inline`**: o encaixe do snap
gruda o primeiro item no início da área que rola e come o recuo. As duas
filas ganharam `scroll-padding-inline: 16px`, e a de modelos ganhou a mesma
sangria de margem negativa mais recuo. Medido depois: as três de 0 a 375, com
`scrollLeft: 0` e o primeiro chip em 16.

### Marcas e tipos de peça no mesmo prumo, no celular (21/09)

Relato: "as marcas estão ajustadas para a esquerda, porém todo o outro site
no celular fica centralizado". Medido a 375, eram duas coisas somadas:

- **vão diferente**: célula de marca com 155 e vão de 32 (coluna 2 em 203),
  célula de tipo com 155 e vão de 20 (coluna 2 em 191). As duas faixas são
  vizinhas e ficavam 12px fora de prumo, e a de marcas parava em 358 contra
  uma régua que vai a 359;
- **conteúdo alinhado diferente**: o logo ficava encostado à esquerda da
  célula, com até 120px de vazio à direita, ao lado de cartões de tipo de
  peça que são centrados. É isso que o olho lê como "as marcas estão à
  esquerda".

As duas faixas passam a dividir a régua em `calc(50% - 10px)` com vão de 20,
e o logo fica centrado na célula. Medido depois: colunas em 16 e 197,5
fechando em 359 nas duas. No computador nada muda, porque lá a fila é `1x` e
encostar à esquerda alinha o primeiro logo com o título da seção.

Entrou junto uma regra de celular que vale **antes** da medida e também com
`sem-medida`: o `atd-marcas-medida` só mede depois que a imagem carrega, e
até lá a fila usava a célula de 102px do bloco e pulava para 161 quando a
conta fechava. Agora a grade já nasce certa e ao script sobra só o tamanho de
cada logo. O logo também deixou de ser `loading="lazy"` (a faixa é a segunda
da home) e o script mostra o que houver depois de 2 segundos sem medir.

### Peça esgotada: a garantia desce, o formulário fica (21/09)

`blocks/atd_compra_segura.liquid` era uma caixa só com duas metades, e a
caixa inteira descia para debaixo da foto **apenas com estoque**. Medido a
1100 numa peça esgotada: foto de 24 a 585 terminando em 772, e o cartão de
425x255 sozinho em x=641, y=1223, com quase 500px de branco embaixo da foto.

Agora são duas caixas irmãs, cada uma com a classe base `.atd-cs-<id>`:

- `[data-atd-cs-garantia]` desce para `.product-information__media` a partir
  de 750px, com estoque ou sem, e ganha `.atd-cs--sob-foto`;
- `[data-atd-cs-avise]` nunca desce, porque é formulário e ocupa o lugar do
  botão de comprar.

A garantia **deixou de ficar `hidden` na peça esgotada**. Medido depois: 768
com a faixa em 40 a 355 logo abaixo da foto, 990 em 24 a 525, 1440 em 75 a
675 (600x162) e o "Avise-me" em 731, 624px.

Duas armadilhas que apareceram na troca:

1. **O invólucro `.shopify-block` fica para trás.** Antes o JS movia o
   `.shopify-block` inteiro; agora ele move só a div da garantia, e o
   invólucro continua na coluna de compra. Numa peça com estoque ele fica
   sem nada dentro e mesmo assim consome um vão de 20px, que é a mesma
   armadilha dos blocos de altura zero entre o título e o preço. O script
   esconde o invólucro quando não sobra nada visível nele.
2. **No celular a ordem é do template, não do DOM.** Tentado pôr a garantia
   depois do bloco da ficha para os dados técnicos virem antes: a coluna do
   celular é uma cadeia de `display: contents` com ordem de pintura própria,
   e o resultado foi a garantia subir para y=678, **antes** da ação. Desfeito.
   A ordem a 375 numa peça esgotada é "Avise-me" em 766, garantia em 1130 e
   ficha em 1421.

### A ficha: medida com desenho, estoque com estado (21/09)

Relato: "a medida de alguns produtos está sem o design, está só a escrita
seca, a parte do estoque também". Medido: MOTORES e TRATORES viravam
pastilha, e MEDIDA ("STD, 85 mm") e ESTOQUE saíam em prosa, do mesmo tamanho
e cor da descrição.

- **Modo `spec`**, novo, em `blocks/atd_produto_ficha.liquid`. Quebra por
  vírgula e barra como o modo `auto`, mas pinta a pastilha com o fio em ouro
  e sem o fundo de papel: é especificação DA PEÇA, não modelo em que ela
  serve, e se as duas ficassem iguais "85 mm" leria como mais um motor.
  Vale para Medida, Modelo, Tipo, Furos, Diâmetro, Espessura, Carreira e
  Capacidade. Conteúdo, tecnologia, sensibilidade, certificações e
  equivalências continuam em prosa, porque são frase e não valor.
- **Estoque** virou ponto colorido de 8px mais o texto no peso 600 (verde
  com estoque, âmbar acabando, cinza esgotado) e o complemento numa segunda
  linha em cinza 13px. Sem caixa: a coluna de compra já tem moldura demais.
  A mesma régua está no script que repinta na troca de variante.

### O botão "Ver todos os produtos" (21/09)

Medido a 1280, antes: 230x48, moldura verde de 1px, fundo transparente, canto
de 4px, texto verde de 15px no peso 400. Os outros cinco botões da home estão
no peso 600 e nenhum é vazado. Ele fica, porque é o único caminho para o
catálogo inteiro depois que o hero sai da tela, mas no computador virou link
com seta e no celular, onde cai sozinho no fim da faixa, virou botão verde
cheio.

**A regra teve que ir para `atd-filtros.css`, seção 13, e não para o
`{% style %}` do bloco**: a moldura vem de
`body [class*="ai-product-showcase-button-"]` no `atd-vitrine.css` e a altura
de `html body :is(...)` na seção 12 da própria `atd-filtros.css`, e as duas
ganham de uma classe só. Regra de botão desta loja mora em folha.

### O localizador com os modelos mais procurados em cima (21/09)

**A lista de modelos não abria ao trocar de marca (22/09/2026).** Relato:
"quando eu troco de marca e aperto em modelo ela não me mostra a lista,
apenas se eu escrever algo e apagar aí começa a mostrar". Eram dois defeitos
somados, os dois reproduzidos por medição antes de mexer:

1. O clique que **escolhe** a marca no `<select>` chega DEPOIS do evento
   `change`, e o `change` acabou de abrir a lista de modelos. O ouvinte de
   clique no documento, que fecha o painel quando se clica fora dele, não
   conhecia o `<select>` e fechava o que tinha acabado de abrir. Medido:
   `depoisDoChange` aberto, `depoisDoClickNoSelect` fechado.
2. Campo que **já está com o foco** não dispara `focus` de novo. Como o
   `change` foca o campo por código, o toque do cliente em cima dele caía no
   vazio. Por isso só digitar e apagar (que dispara `input`) trazia a lista
   de volta.

Conserto: o ouvinte do documento ignora cliques vindos do `<select>` de
marca, e o campo de modelo ganhou um ouvinte de `mousedown` que abre o painel
quando ele está fechado. Medido depois: change abre, clique no select mantém
aberto com as 14 opções da Tobatta, clique no campo reabre, clique fora ainda
fecha.

Medido: o segundo campo do "Qual é a sua máquina?" trazia 83 opções da Yanmar
em ordem alfabética, de 2TNV70 a YT22. Quem tem um TC11 ou um NS18 precisava
rolar a lista inteira. `snippets/atd-localizador.liquid` passou a montar dois
`optgroup`: "Mais procurados", com os modelos que têm coleção própria (o
critério já estava no mapa do snippet, então não há lista nova para manter), e
"Outros modelos" com o resto em ordem alfabética. Marca sem modelo mapeado
(Branco, por exemplo) continua com um bloco só e sem rótulo de grupo. Medido
depois: Yanmar 37 mais 45, Agrale 7 mais 17, nada perdido.

---

### Linha do horizonte da pagina de produto (22/09/2026)

Regra que fica: **no computador as duas colunas da pagina de produto comecam
e terminam na mesma linha.** Quem garante isso e a secao 14 de
`assets/atd-filtros.css`, e sao tres pecas que precisam continuar juntas:

- `padding-top: 0` no `.group-block` da coluna de compra, acima de 750px. E
  o involucro do editor, e a coluna da foto nao tem um igual.
- `flex: 1` no cartao `.atd-cs--sob-foto`, para ele crescer ate o pe da
  coluna quando a direita for mais alta.
- O revezamento de `.atd-ficha__entrega` e `.atd-cs__entrega`: o mesmo
  texto existe nos dois blocos e a folha mostra so um, escolhendo pelo
  estado do "Avise-me" com `:has()`. Sao 88px que vao sempre para a coluna
  curta.

Se algum dia entrar um bloco novo na coluna de compra, conferir os dois
casos (peca com estoque e peca esgotada) antes de dar por pronto. Medido em
22/09: topo com 0px de diferenca em 768, 990 e 1440; fim com 0px na peca
esgotada e entre 13 e 50px na peca com estoque.

### A página de produto, segunda volta (21/09/2026)

Regra que fica, acima da anterior: **quem estica é a foto, nunca o cartão.**

A altura da foto acompanha a largura da coluna; a altura da coluna de compra
quase não muda. Entre 750 e 1440 a diferença entre as duas balança uns
200px, e até 21/09 o vão todo ia para o cartão de garantias, que ficava com
o texto boiando no meio (medido a 961: 430px de caixa para 213px de texto).

Agora:

- `.product-information__media` vira `container-type: inline-size`;
- `media-gallery` fica `flex: 100 1 0`, com `min-height: 75cqw` e
  `max-height: 125cqw`. O 100 contra o 1 do cartão faz quase toda a sobra ir
  para a foto; o cartão só entra quando ela bate no limite;
- a cadeia `slideshow-component / container / slides / slide / .product-media`
  passa a `height: 100%`, e o `aspect-ratio: 1/1` da moldura cai. O
  `!important` no `height` é obrigatório: `atd-home.css` já escreve
  `height: auto !important` ali, então a briga é com um `!important` que já
  existia, não força bruta;
- o cartão fica `flex: 1 1 auto` com `justify-content: space-between`, para a
  sobra se repartir entre as faixas dele em vez de virar um buraco;
- `padding-bottom: 0` no `.group-block` da coluna de compra, para a
  comparação ser de TEXTO contra texto e não de caixa contra caixa.

A imagem continua em `object-fit: contain` e centrada: a moldura muda de
altura, o desenho nunca deforma nem corta.

**Código mora em DECIDIR**, logo depois da marca. Ele desceu para DETALHE na
primeira volta e o cliente devolveu na hora.

**Retirada e envio moram do lado da foto, sempre**, acima de 750px. O
revezamento conforme o estoque acabou.

**No celular a entrega fica na ficha**, e a cópia do cartão é escondida por
`html body .product-information__grid .atd-cs__entrega`. O
`.product-information__grid` no seletor não é enfeite: sem ele a regra pesa
0,1,2 e perde para o `.atd-cs-<id> .atd-cs__entrega` do bloco, que pesa
0,2,0, e a linha sai duas vezes.

Medido, fim de texto contra fim de texto, 0px em tudo: cabo a 768, 900, 990,
1259 e 1440; bronzina de 5 variações a 768, 990 e 1440; escala do regulador,
esgotada, a 1440 e 768.

### A ordem da página de produto (23/09/2026)

Regra que fica, e que vale mais que a linha do horizonte: **na coluna de
compra, o que decide vem antes do botão e o que é referência vem depois.**

A ficha (`blocks/atd_produto_ficha.liquid`) sai em dois blocos irmãos:
`.atd-ficha__decidir` (marca, compatibilidade, medida, observação, estoque) e
`.atd-ficha__detalhe` (código, conteúdo, equivalências, prosa, retirada e
envio, WhatsApp). O invólucro do editor vira `display: contents` e uma regra
só, `.atd-ficha__detalhe { order: 1 }`, põe o botão de comprar entre eles, no
computador e no celular.

Três coisas para não esquecer:

- o atributo do editor e o `data-atd-ficha` moram no grupo DECIDIR, que tem
  caixa própria. Se forem para um invólucro em `display: contents`, o bloco
  deixa de ser selecionável com um clique no editor;
- o JS da ficha procura o código por `document`, e não dentro da raiz, porque
  ele mudou de grupo;
- no celular, invólucro em `display: contents` não pinta margem. O recuo
  lateral de 16px teve que descer para os cartões (`.atd-ficha__grupo`,
  `.atd-cs--avise`, `.atd-cs--garantia`), senão eles encostam na borda.

Medido em 390, 768, 990 e 1440, com peça em estoque e peça esgotada: topo 0px
e fim 0px em todas. Botão de comprar a 1440 subiu de y=889 para y=692.

### "Peças para o mesmo motor" só pelo motor (24/09/2026, tema de trabalho `166112100400`)

Relato do cliente, com print do Conjunto do Pistão Agrale 4100 / 4118 /
4120: "diz que ele serve para os motores MD, porém lá embaixo, no peças para
o mesmo motor, estão os Agrale M90, M85... são o mesmo motor?" Não são. O
MD é Ruggerini de 2 cilindros; o M80, o M85 e o M90 são Agrale de 1. A
seção `sections/atd-mesmo-motor.liquid` casava a peça com qualquer outra
que dividisse **um valor qualquer** do metacampo, e o metacampo tem trator,
microtrator e escavadeira junto com motor. O trator Agrale 4100 saiu de
fábrica com mais de um motor, e o Agrale 4200 também (M790 e MAN).

Simulado nas 118 peças com metacampo, com a mesma ordem e o mesmo limite de
8 da seção: **69 sugestões erradas em 30 páginas**. As de outro motor:

- pistão MD com bronzina, anel e junta do M80 / M85 / M90, e o inverso
  (pelo "Agrale 4100");
- filtro de óleo do Agrale 4200 com motor MAN no meio das oito peças do
  M790 / M93, e o inverso (pelo "Agrale 4200");
- junta do M790 (2 cilindros) na página da junta do M93 (1 cilindro), e o
  inverso;
- virabrequim 4TNV88 XAT na página do virabrequim 4TNV88 comum, que diz
  "Não é compatível com o modelo 4TNV88-XAT", e nos filtros e anéis do
  4TNV88;
- filtro de combustível NS50 / NS75 / NS90 nas páginas de camisa, anel e
  pistão B9 / NB10, só porque os dois citam o microtrator TC10.

O resto era peça de microtrator (cabo da direção, cabo de embreagem, faca
da roçadeira TA73) e a sapata da VIO20 aparecendo como "peça do mesmo
motor".

**Regra nova da seção**: casa pela linha `Motores Compatíveis:` da
descrição, dos dois lados. A peça da página e a candidata precisam ter pelo
menos um motor escrito igual nessa linha. O metacampo continua fazendo o
primeiro corte, e só a candidata que passa nele tem a descrição lida. Sem
linha de motor, vale `Microtratores Compatíveis:` e o título vira "mesmo
microtrator". Sem nenhuma das duas, a seção não mostra peça. Linha que
começa com "Todos os modelos" (cabo do acelerador Tobatta) vale pela lista
do metacampo.

Conferido fora da loja, com o liquidjs rodando o arquivo novo contra as 118
peças: **zero sugestões erradas** e as mesmas listas da simulação em todas
as páginas. O título fica "mesmo motor" em 96 páginas e "mesmo microtrator"
em 8 (cabos, capa, decalques, lona, juntas da caixa, faca TA73), e 14
páginas ficam sem a seção porque nenhuma outra peça tem o mesmo motor. O
pistão MD é uma delas, porque a loja não tem outra peça de motor MD. Arquivo
gravado igual ao testado (md5 `bf3ec65f...`, 14.940 bytes; no ar é
`8914fd72...`). **Falta medir no preview.**

A coleção `pecas-agrale-m790-m93` tinha a mesma falha, nas regras "Agrale
4200" e "Agrale 4300", e mostrava o filtro do motor MAN. As duas regras
saíram (é loja, vale no ar na hora): 9 para 8 peças. Regra que fica:
**coleção "Peças para <motor>" só tem regra de motor**, nunca de trator.

### A linha Observação (24/09/2026, tema de trabalho `166112100400`)

Pedido do cliente, com print do pistão Agrale 4100: "a parte da observação
continua não formatada... preciso que se integre junto às outras". A linha
saía em `.atd-ficha__obs` com fio dourado de 2px à esquerda, recuo de 10px
e Inter 14px peso 400: a única linha da ficha com moldura própria e letra
menor que as outras.

Em `blocks/atd_produto_ficha.liquid`, item 10 do histórico:

- `.atd-ficha__obs` perdeu o fio e o recuo e herda o 15px e a tinta do
  `.atd-ficha__valor`, em **peso 500**. O tema só carrega Inter 400, 500,
  700 e 800; 600 cairia no 700 e pesaria como as pastilhas.
- **Uma frase por linha**: cada `<li>` do bloco Observações vira um
  `.atd-ficha__obs-item`. Para isso a descrição ganha uma quebra de linha
  depois de cada `</li>` antes do `strip_html` (a captura `atd_quebra`).
  Antes, "Filtro rosqueado, rosca M20 x 1,5." e "Diâmetro externo de cerca
  de 78 mm." saíam emendadas numa linha só, e numa descrição sem quebra no
  HTML (Cobertura do Radiador NS18) sairiam coladas, sem espaço.

Conferido fora da loja, porque a rede da sessão bloqueia o domínio: o
bloco foi renderizado com liquidjs contra as descrições reais (pistão Agrale
4100, filtro 2175107, cobertura NS18 com um segundo item de teste,
virabrequim 4TNV88 com `<br>` solto) e medido no Chromium com Inter
400/500/700/800. Todas as outras linhas saíram iguais ao antes, byte a byte.
Observação: 15px, peso 500, sem borda, começando no mesmo x das pastilhas
(116 no quadro de teste, igual às outras seis linhas). O arquivo gravado
bate com o testado (md5 `d803a77f...`). **Falta medir no preview**: com a
rede liberada, `?preview_theme_id=166112100400` no pistão Agrale 4100 e no
filtro 2175107, a 390, 990 e 1440.

### O localizador virou lista própria (23/09/2026)

`<select>` nativo não aceita folha na lista: quem desenha é o sistema
operacional. O campo do modelo virou `input` com painel próprio
(`role="listbox"`), com filtro por digitação sem acento e sem hífen, contagem
de peças por modelo e teclado (setas, Enter, Esc). A folha mora no
`{% style %}` do próprio snippet, porque é marcação nova sem regra
concorrente; cor, canto e altura de campo continuam vindo do bloco do banner.

"Mais procurados" deixou de ser lista fixa: são os modelos com mais peças no
catálogo, mais os que têm coleção própria. Marca com menos de 4 modelos fora
dos destaques sai em lista única, sem rótulo de grupo (a Tobatta tem 14).

No celular o painel abre pela borda direita do campo e cobre a linha inteira
(`width: calc(200% + 8px)`), porque o campo sozinho tem 175px e corta o nome
do modelo. **A marca é a coluna da esquerda e por isso abre pela borda
esquerda** (`left: 0; right: auto`): presa pela direita, como a do modelo,
ela nascia em x = -159 a 375px.

**A marca também virou lista própria, no fim de 23/09/2026**, a pedido do
cliente ("a lista que abre das marcas tem que ter o mesmo tamanho da outra").
É um `<button>` com o desenho do campo, a mesma seta e um painel da mesma
classe `.atd-loc__painel`, então herda teto, borda, sombra e o encaixe dentro
da imagem do banner. Cada marca traz a contagem de peças da coleção. Medido a
1440, com as duas abertas no mesmo instante: 245x205 cada, nascendo em 447 e
terminando em 652, 12px antes do fim da foto.

Duas coisas para não repetir:

- **O painel do modelo se acha por `combo.querySelector`, nunca por
  `form.querySelector('.atd-loc__painel')`.** Com dois painéis no mesmo
  formulário, o seletor solto devolve o da marca, que vem primeiro, e
  escolher a marca passa a escrever os modelos por cima dela.
- **O respiro entre linhas de uma lista mora no `gap` do pai**, não em
  `margin` do filho, quando existe uma regra de `li` com especificidade
  maior. Foi o que matou o `margin-bottom` da nota do Google no banner.

### A logo, resolvida em 21/09/2026

De **965 KB por página para 9,3 KB**, com o desenho do mesmo tamanho na
tela. O que havia:

- cabeçalho: `logo-atd_svg_...svg`, 321.746 bytes, pedido DUAS vezes (1x e
  2x). SVG a CDN não redimensiona, então o arquivo inteiro viajava nas duas;
- rodapé: `Logo_VL_sem_fundo_SVG_Correta.svg`, 321.768 bytes, mais uma vez.

O cliente exportou um `logo-atd-280.png` de 280x215 e achou que tinha
**ficado menor**. Tinha mesmo, e dá para provar: o PNG saiu da tela original
de 1275x981, que tem margem transparente em volta; o SVG do cabeçalho é a
mesma arte **já recortada**, 805x592. Como a régua manda `height: 60px`, o
desenho dentro do PNG ocupava 174 de 215 pixels de altura, ou seja **81%**.
Mesma caixa, desenho 19% menor.

O que está no tema agora:

- **`logo-atd-cabecalho.png`, 280x205, 7.057 bytes.** Recorte pela caixa
  alfa da arte original (bbox 102,100 a 1177,888) e redução para 280 de
  largura, paleta de 256 cores. Erro médio contra o RGBA cheio: 2 de 1020,
  invisível. Medido no cabeçalho: **82x60**, exatamente o que o SVG dava.
- **`logo-atd-rodape.png`, 240x185, 2.057 bytes.** Aqui vale um truque: o
  rodapé pinta a logo com `filter: brightness(0) invert(1)`, ou seja, só
  usa o CANAL ALFA e joga a cor fora. Então o arquivo é a silhueta branca da
  arte, no enquadramento original (sem recorte, para não mudar de tamanho).
  Medido: **52x40**, igual ao SVG.

A troca foi feita em `config/settings_data.json` (chave `logo`) e em
`sections/footer-group.json` (bloco `atd_rodape`, chave `logo`), no tema DEV.
**O tema publicado continua apontando para os SVG antigos**: o ganho só
chega ao site ao vivo quando o DEV for publicado.

Os SVG antigos **não foram apagados** de Conteúdo, Arquivos, porque o tema
publicado ainda os usa. Apagar depois, e só depois.

O tamanho na tela continua vindo de `atd-regua.css` (60px acima de 769,
42px abaixo), não da configuração do tema.

### O logo da loja pesa 238 KB (22/09/2026, resolvido acima)

`logo-atd_svg_3c6bbf01-f5b8-486d-8104-764ca5ac0faf.svg`, servido com
`?height=100`, chega ao navegador com **238.297 bytes ja comprimidos em
brotli** (321.746 crus). Ele aparece em **toda** pagina do site, no
cabecalho, exibido com **82px de largura**. Para comparar: as nove folhas
de estilo da loja somam 17 KB comprimidas.

A CDN da Shopify nao redimensiona SVG, entao `?height=100` nao muda nada:
o arquivo inteiro viaja sempre. Um SVG desse tamanho quase sempre tem
curva demais, ou uma imagem rasterizada embutida.

**Isto nao se conserta pelo tema.** A logo e intocavel como desenho (regra
do cliente), entao o conserto e reexportar o mesmo desenho: ou um SVG
otimizado, ou um PNG/WebP com 280px de largura, que e o dobro do que
aparece na tela. Os dois caminhos ficam abaixo de 10 KB sem mudar um pixel
do que o cliente ve. Trocar e no admin, em Personalizar > Cabecalho > Logo.

## 5b. Filtrar, uma gaveta só (18/09)

Quem desenha os filtros é `blocks/filters.liquid`, do tema. Ele monta **duas**
coisas ao mesmo tempo: uma fila horizontal de facetas, que aparecia só acima
de 750px, e uma gaveta (`#filters-drawer`), que aparecia só no celular. O
botão "Mais" da fila já abria a gaveta.

Em 18/09 a fila saiu do computador e ficou a gaveta nas duas larguras, a
pedido do cliente. Quatro defeitos que ele relatou eram da fila, não da
gaveta, e morreram juntos: "Preço" partido ao meio pelo `<overflow-list>`, o
painel de faceta caindo por cima do primeiro cartão da grade, o "Limpar tudo"
verde cheio virando o elemento mais forte da página e a fila reorganizando na
carga.

Tudo em `assets/atd-filtros.css`, a última folha nossa. Ela é componente, não
sistema: cor, fonte e controle continuam sendo decididos em `atd-sistema.css`.
Quase tudo nela é `!important`, porque o `styles.css` compilado dos blocos
carrega depois de todas as nossas folhas.

**Classificar é a primeira linha da gaveta**, acima dos grupos de filtro,
porque o cliente pediu. Os chips do que já está marcado ficam acima dele. A
área que rola virou coluna flex e a ordem é só de pintura, nada mudou de lugar
no HTML.

Três armadilhas, todas medidas:

1. A gaveta é `dialog-drawer--right`, mas o bloco escreve `margin: 0` nela e
   ela nasce **encostada na esquerda**, por cima da listagem. Com `inset: 0` e
   largura fixa, quem a joga para a direita é `margin-inline-start: auto`.
   Medido a 1440: de 1060 a 1440.
2. `sorting-filter-component` nasce com `display: none` acima de 750px, porque
   o Classificar era da fila horizontal.
3. Dentro dele existem **dois** controles, um `<select>` e um
   `accordion-custom`. Ligar o componente inteiro mostra "Classificar" duas
   vezes seguidas. Ficou o `<select>`, que serve nas duas larguras e abre o
   seletor do próprio aparelho no celular.

**A palavra cortada por baixo** tinha duas causas com o mesmo sintoma. O tema
trava o rótulo do valor em `height: 22px` com fonte de 18px, e o rabo do "q" e
da cedilha encostava no fio; virou altura automática, 15px com entrelinha 1,5.
E o último item era cortado ao meio pela borda da área que rola; uma máscara
esmaece os 24px finais, e o corte passa a se ler como "tem mais embaixo".
`mask` não cria contexto de empilhamento, ao contrário de opacidade.

**Cara da gaveta, segunda volta (18/09 noite)**: a primeira volta só trocou
cor e continuava uma lista de caixas de marcar sem hierarquia. Agora são
três degraus: título "Filtrar" em Barlow 26 com sobretítulo "Refine a busca"
(filete de ouro), nome de grupo em versalete 12px 700 com entreletra 0,12em,
e valores em pastilha de 38px, a mesma do "Por modelo" do mega menu. Marcado
muda fio, fundo e texto para o verde e ganha o visto; **o peso não muda**
(engrossar o marcado era lido como "negrito aleatório"). Classificar virou
versalete em cima de um botão de largura cheia. "Limpar tudo" é link
sublinhado. Detalhes e armadilhas no registro de 18/09 noite em
`comece-por-aqui.md`.

Registro da primeira volta: branco, filete de ouro de 3px no topo (o mesmo do painel
do mega menu), título em Barlow Condensed 24px, rótulo de grupo e valor em
Inter 15px tinta, caixa de marcar quadrada de 20px que fica verde quando
marcada, fios cinza-200. "Exibir mais" saiu do verde e virou cinza-600
sublinhado: verde cheio é comprar e confirmar escolha, e ele não é nem um nem
outro. No rodapé, "Ver N itens" verde e "Limpar tudo" vazado, com largura do
próprio texto porque em percentual ele quebrava em duas linhas a 390px.

**Efeito colateral aceito**: o alternador de uma ou duas colunas some do
computador junto com a fila. Se o cliente quiser de volta, é uma regra.

**No celular** "Fabricante da peça" continua escondido por `atd-sistema.css`.
"Tipo de Produto" voltou em 18/09 (o cliente sentiu falta) e aparece como
"Tipo de peça", nome trocado por `assets/atd-ordem.js`. No computador todos
aparecem.

### Rodada de 18/09 à tarde, tema 145546182704

- **Grade da página de produto vazava para o celular.** A regra
  `minmax(0, min(628px, 54%))` da seção 6 de `atd-filtros.css` não tinha media
  query: a 375 a coluna de compra ficava com 203px e o "Adicionar ao
  carrinho" encostava na borda. Agora só vale a partir de 990px. Entre 750 e
  989 fica o meio a meio do tema (339 e 339 a 768).
- **Celular: trilha e título em cima da foto** (seção 8 de `atd-filtros.css`).
  A grade vira coluna flex e as caixas da coluna de compra viram
  `display: contents`, então a ordem é só de pintura. Medido a 375: trilha
  196, título 243, foto 317 a 598, preço 622, quantidade e botão 702, tudo na
  régua de 16px. Armadilha: o seletor precisa ser de filho direto
  (`> .product-details > .group-block > .group-block-content > *`), senão
  pega o preço, que mora num grupo aninhado, e dá 16px a mais. Abaixo de
  400px o ícone sai do botão para o texto caber.
- **Preço que "se junta" ao carregar**: o selo do Judge.me nascia com "Sem
  avaliações" e só depois sumia. Fica escondido desde a primeira pintura
  quando `data-number-of-reviews='0'` (seção 9).
- **Cabeçalho do celular** (seção 10): o carrinho era traço branco (culpa de
  `body .button` do atd-custom). A conta saiu do cabeçalho do celular e virou
  "Minha conta" na gaveta (`atd-menu-celular`): logo a 96px do menu e do
  carrinho.
- **Filtrar na linha do título**, no celular e no computador
  (`blocks/atd_atalhos.liquid`). O botão novo aperta o original do tema, que
  fica escondido pela classe `atd-filtrar-no-topo` no body. O número conta o
  que está marcado na gaveta, não o endereço (parâmetro de filtro que a loja
  não tem fica na URL e não filtra). Primeiro cartão a 375 subiu para 434.
- **Classificar com a cara da loja**: `assets/atd-ordem.js` põe botão e lista
  próprios sobre o `<select>` (CSS na seção 2b). **Armadilha do tema:** o
  componente tem também os rádios `sort_by` da lista de computador, e o
  formulário lê os dois; mudar só o `<select>` não reordenava (o rádio velho
  ganhava). O script marca os dois. O mesmo script troca "A–Z" por "de A a
  Z", porque o texto vem da tradução da Shopify.
- **Mega menu mais rico** (seção 1b de `atd-catalogo.css`): topo com a marca em
  Barlow e "Ver tudo", tipos em pastilhas de 4 por linha, chips "Por modelo"
  (coleções `pecas-*`, lista `modelos` no snippet) e faixa de WhatsApp. Painel
  de 980x440, nenhuma das 8 marcas rola por dentro.
- **Selo do carrinho**: cadeado e caminhão em traço no lugar dos emoji
  (`snippets/cart-products.liquid`).

**Armadilha de medição**: com o painel do navegador escondido, a gaveta do
tema não abre nem com o clique no botão original (o `showDialog` depende de
quadro de animação). Para medir o conteúdo, `dialog.showModal()` direto.

---

## 6. SEO e busca com IA

- **BreadcrumbList** e **ItemList** em JSON-LD na página de listagem. A trilha
  dá o caminho no resultado do Google; a lista diz quais peças estão naquela
  prateleira sem o buscador interpretar o HTML.
- **AutoPartsStore** (LocalBusiness) na home, com endereço, telefone, horário,
  WhatsApp e marcas atendidas. É o que responde "onde compro peça de
  microtrator em Goiânia".
- **Meta title e description** nas 13 coleções de marca e tipo, que estavam
  vazias. Isso é conteúdo da loja, então vale também no ar. Só a meta. A
  descrição visível ficou de fora de propósito, porque apareceria na loja
  publicada sem aprovação.
- **Título das páginas de marca mais tipo.** O tema entregava
  `Yanmar - tagged "Juntas"`, em inglês, justamente nas URLs que o menu usa.
  Agora sai `Juntas Yanmar | A Trator Diesel` (`snippets/meta-tags.liquid`).
- **Página 404 traduzida**, e busca sem resultado com WhatsApp e atalhos no
  lugar da coleção inteira. Carrinho traduzido: "Cart" virou "Seu carrinho",
  "View all" virou "Ver todas as peças".
- H1 da home caiu de 2 para 1. Imagens sem alt na home, de 12 para 6. H1 da
  coleção deixou de ser fixo e passou a ser o nome real.
- **Descrição do produto no Google (15/09).** Sem descrição de SEO no
  produto, `snippets/meta-tags.liquid` monta "Nome. Serve nos motores X, Y.
  R$ 90,00, com envio para todo o Brasil e retirada em Goiânia em 24h." A
  compatibilidade sai da descrição, com os rótulos da ficha, cortada numa
  vírgula perto de 70 caracteres com "e outros". Esgotada troca o preço por
  "Consulte disponibilidade no WhatsApp". Campo de SEO preenchido ganha
  sempre. Vale também para `og:description`. Conferido em 20 peças.
- **Um h1 por página de texto (15/09).** Os modelos `page` e `page.contact`
  usam o bloco `atd_titulo_pagina`, que só imprime o h1 quando o conteúdo
  não tem um. As cinco páginas de hoje trazem o h1 na capa do `.atd-doc`,
  então ficam com esse só. A regra de `atd-paginas.css` que escondia o
  primeiro h1 ficou sem efeito.
- **Busca com h1 (15/09).** Com resultado, a linha "19 peças encontradas
  para junta" (`sections/atd-busca-resumo.liquid`) virou h1 sem mudar de
  desenho. Sem resultado, e em `/search` vazio, o h1 é o título de
  `atd-busca-vazia`, na escala de h2 que ele já tinha.
- **Foco da busca do cabeçalho (15/09).** `base.css` pintava oliva
  `rgb(107, 125, 42)`. Sobrescrito no bloco "Ajustes do cabeçalho"
  (`header-group.json`) por `#1e5b39` com anel de 3px a 14%. Medido a 1440.
- **Título e descrição da home (15/09).** A Admin API não grava o que fica em
  Loja virtual, Preferências, e `metafieldsSet` na loja não muda a home do
  tema publicado. Por isso os textos estão nos metafields da loja
  `global.title_tag` e `global.description_tag`, e `snippets/meta-tags.liquid`
  do DEV lê os dois quando `request.page_type == 'index'`. Para trocar, grave
  os metafields de novo. No tema publicado a home continua com "A Trator
  Diesel" e a descrição antiga (com Kubota) até o DEV ser publicado. Conferido
  no DEV: título de 60 e descrição de 151 caracteres.
- **Descrição das cinco páginas (15/09).** `global.description_tag` em cada
  página (contato, sobre-nos, politica-de-devolucao, ajuda-e-duvidas,
  politica-de-privacidade), de 131 a 151 caracteres. É conteúdo da loja,
  vale já no ar. Conferido por `curl` no publicado.
- **O tema publicado separa o título com travessão** ("Central de ajuda – A
  Trator Diesel"). O DEV usa " | ". Some quando o DEV for publicado.

---

## 7. Diferenças entre o tema DEV e o publicado

O preview `?preview_theme_id=145492672560` cai quando a sessão expira ou
quando o site abre numa aba nova, e volta o tema **ATUAL publicado**, com
todos os erros originais. Isso já custou uma rodada inteira, com o cliente
dizendo que nada tinha funcionado.

Confira de relance: no DEV a logo do cabeçalho começa na mesma coluna de
"Escolha a marca da sua máquina" (24px a partir de 1280px de largura); no
publicado ela está bem mais para dentro. Para confirmar por código, o comando
está em `comece-por-aqui.md`.

O publicado ainda tem, e o DEV já não tem: zoom de 0,85 na loja inteira,
cabeçalho de 162px fora da régua, chips de filtro e contagem na listagem,
fileira de marcas em meia página, botão de comprar branco vazado, setas de
galeria rosa, título repetido na página de produto e rodapé com recuo próprio.

---

## 8. Armadilhas do tema

Armadilha geral do projeto está em `comece-por-aqui.md`. Aqui ficam as que são
só de tema:

- Campos `range` do Shopify validam contra `min`, `max` e `step`. Valor fora
  do passo derruba o upsert inteiro com "must be a step in the range". Confira
  o `step` no schema do bloco antes de subir.
- Mudar `min`, `max` ou `step` de um `range` não revalida o valor já gravado
  no template, e o valor que sai da grade **trava o editor da página
  inteira**, porque ele grava o template todo de uma vez. Em 23/09 o
  `brand_height_mobile: 70` das marcas (schema `min 60, step 4`) impediu o
  cliente de trocar o texto do hero. Ao mudar um `range`, regrave o valor no
  template, já na grade nova, logo depois do schema.
- Blocos gerados pelo editor criam classe por instância
  (`ai-brands-item-<id>`) e imprimem o `{% style %}` no corpo da página. Os
  seletores precisam de `body` na frente e `[class*='prefixo-']`.
- `themeFilesDelete` está bloqueado. Arquivo aposentado é esvaziado, não
  apagado. O asset `assets/lavrale-logo.png` é uma dessas sobras.
- Ordem real das folhas, medida no navegador: `base`, `atd-custom`,
  `atd-catalogo`, `atd-vitrine`, `atd-home`, `atd-paginas`, `atd-regua`,
  `atd-botao-carrinho`, `atd-sistema`. **`atd-sistema` é a última da fila**,
  apesar de a régua ter a palavra final sobre largura de faixa e tamanho de
  logo.
- O cabeçalho usa uma coluna de 1300px, 10px mais larga de cada lado que a
  régua de 1280px. O recuo dele não sai do `.header__row--top`, vem da grade
  do `.header`.
- **Largura escrita no elemento, não em folha.** Quando uma medida não
  aparece em folha nenhuma e nem `!important` vence, procure
  `--size-style-width` (e irmãs) no `style` do próprio elemento, escrito
  pelo editor. Foi o caso da coluna de texto de 400px na página de produto.
- **Schema antes do template.** A Shopify normaliza o JSON do template
  contra o schema do bloco e **descarta em silêncio**, com `userErrors`
  vazio, qualquer chave que o schema ainda não declare. Grave o bloco
  primeiro, o template depois, e leia o arquivo de volta para conferir.
- **A fila horizontal de filtros pisca no carregamento (19/09).** Superada
  em 18/09: a fila não aparece mais em largura nenhuma, ver seção 5b. Fica
  registrado porque o `<overflow-list>` é do tema e volta a valer se a fila
  for religada. Relato:
  "os filtros aparecem inteiro e só depois se retraem e aparece o Mais". É o
  `<overflow-list>` do tema (`assets/overflow-list.js`): ele nasce com todos
  os filtros visíveis e o botão "Mais" com `hidden`, e só arruma a fila
  depois de subir, esperar a folha do shadow DOM, receber o aviso de um
  `IntersectionObserver` e passar por um `setTimeout(0)`. Entre a primeira
  pintura e esse momento a fila aparece inteira.

  Conserto em `assets/atd-catalogo.css`, seção 5: a fila fica
  `visibility: hidden` até o próprio componente escrever `--overflow-count`
  no estilo em linha, que é o sinal de que terminou de medir. `visibility`
  não tira do layout, então o `IntersectionObserver` continua enxergando, e
  **não cria contexto de empilhamento**, ao contrário de opacidade, que
  prenderia os painéis `position: fixed` dos filtros. Uma animação de 0s com
  meio segundo de atraso é a rede de segurança: se o JS do tema falhar, a
  fila aparece do mesmo jeito, só que sem arrumar.

  **Armadilha de medição:** com o painel do navegador escondido, o Chrome
  suspende `IntersectionObserver` e animação de CSS. O componente nunca
  arruma a fila e a rede de segurança nunca dispara, então essa correção
  **não pode ser conferida com a janela do navegador oculta**.
  `document.hidden` responde `true` nessa situação, e é o primeiro valor a
  ler antes de desconfiar do código.
