# Registros, dia a dia

O diário do projeto. Saiu de dentro de `comece-por-aqui.md` em 23/09/2026,
inteiro e sem corte: eram 1.110 das 1.631 linhas daquele arquivo, e ele é
lido no começo de toda tarefa. O que vale para sempre (armadilhas, como o
site está montado, o que ficou aberto) continua lá; o que é história de um
dia está aqui, e só precisa ser aberto quando a pergunta for "por que isso
ficou assim".

Do mais novo para o mais velho, na ordem em que estavam.

## Registro de 24/09/2026 (noite): regra do título, motores MD no filtro, observações por cilindro e a linha Observação da ficha

Mensagem do cliente com print da ficha do pistão Agrale 4100, respondendo
às duas perguntas da tarde e trazendo três pedidos novos. Gravado em sete
produtos sem `userErrors` e lido de volta; backup em
`backup-padronizacao-24-09.json`, chave `terceira_rodada`.

1. **"Essa regra de todo modelo da ficha tem que estar no título não é
   verdade."** Título com os principais, ficha e metacampo com todos. A
   regra 2 da compatibilidade e a seção "Título" de `catalogo-e-busca.md`
   foram reescritas. O Sileo fica na ficha do pistão 6501512 e o título
   não muda.
2. **Motores MD no filtro do pistão Agrale 4100, "se forem os motores
   corretos".** São: vêm do catálogo oficial de peças da Agrale e do manual
   Ruggerini, conferidos em 21/09. Metacampo com os sete valores da ficha,
   SEO com os motores, reindexado.
3. **"Use apenas catálogos confiáveis e originais, oficiais."** Virou regra
   ("Fonte", em "Regra da compatibilidade"). Por ela, o Sileo (entrou pela
   palavra de revendas) e o 12LD 475-2 do filtro 2175107 ficam como
   pendência, não como certeza.
4. **12LD 475-2, "preciso que confira para mim".** A busca restrita ao
   i-service da Lombardini devolve o desenho "D Controls/Lubricating
   System" do 12LD 435-2 com o cartucho de óleo de 90 mm, `2175.131`, e o
   manual de oficina é um só para 12LD 435-2 e 475-2. O 2175107 tem cerca
   de 78 mm. Tudo indica que o 12LD 475-2 não usa este filtro, mas o PDF
   não abriu: **não foi mexido**.
5. **"Por que não consegue acessar?"** A rede do ambiente da nuvem recusa
   `iservice.lombardini.it`, `www.lombardini.it`, `agrale.com.br`, o
   domínio da loja e os sites das revendas (403 no proxy; o WebFetch dá
   `EGRESS_BLOCKED`). A busca funciona, mas só devolve um resumo. O cliente
   libera nas configurações do ambiente, em Acesso à rede.
6. **"O motor usa 2 conjuntos, um por cilindro", num produto de quatro
   motores.** Varredura das 21 peças com Observações: cinco falavam de
   quantidade, todas reescritas dizendo de qual motor falam. Regra na seção
   2 de `catalogo-e-busca.md`. A bronzina 1611195 ficou, falta a conta do
   LDW 1404.
7. **"A parte da observação continua não formatada."** Era o tema, não a
   descrição: a linha tinha fio dourado e letra menor. Mudou num tema de
   trabalho novo, `166112100400`, cópia do publicado; o do ar não foi
   tocado. Detalhe e medida em `tema-e-design.md`, "A linha Observação".
   Falta o cliente olhar o preview e publicar.
8. **"O que é PR e CL?"** Explicado na conversa: PR é o pedido de mudança
   dos documentos no GitHub (o PR 1 deste repositório), e o "CL" era CI, a
   verificação automática, que este repositório não tem.

---

## Registro de 24/09/2026 (tarde): respostas do cliente sobre o catálogo

Resposta do cliente aos quatro achados do item 14 de `comece-por-aqui.md`,
gravada no mesmo dia em 13 produtos, sem `userErrors`, lida de volta.
Backup em `backup-padronizacao-24-09.json`, chave `segunda_rodada`.

1. **Estoque do 30508 (14) e do 11352 (3) está certo.** Saíram da lista de
   zerados; estoque não foi tocado.
2. **Conjunto do Pistão Agrale 4100 vem com anéis, pino e travas.** O texto
   do ML saiu e a ficha voltou ao padrão (motores MD, tratores Agrale 4100 /
   4118 / 4120, medida, conteúdo).
3. **Modelos, só o que for certo.** `Sileo 1000` e `Sileo 1400` entraram no
   pistão 6501512 e na correia 2440338 (família de motor da Lombardini,
   confirmada em revendas diferentes). `linha 9LD` e `LGW` seguem fora do
   filtro 2175107, porque as fontes dão a esses motores o filtro de 90 mm
   (2175131). As mesmas fontes põem o `12LD 475-2` no de 90 mm: ficou no
   título, anotado como dúvida em `comece-por-aqui.md`, item 14.
4. **Todas as peças Lombardini são originais.** `Original` no fim do título
   dos oito que faltavam, SEO reescrito junto.
5. **"A parte de observação está sem formatação."** Os nove Lombardini e
   mais três produtos (filtro de óleo Agrale 4200, jogo de molas B4T 13.0 /
   15.0 e carretel B4T) tinham `<li>Observações: ...</li>` dentro de
   Especificações. Viraram o bloco `<p><strong>Observações:</strong></p>`
   com lista, que é o formato das outras peças da loja. Regra escrita em
   `catalogo-e-busca.md`, seção 2.

A pesquisa na internet foi só por busca: a rede da sessão recusa os sites
das revendas e o i-service da Lombardini (proxy), então as páginas não
foram abertas, só os trechos que a busca devolve.

---

## Registro de 24/09/2026: os 9 Lombardini padronizados, SEO desatualizado e tema publicado

Sessão na nuvem, pelo repositório do GitHub. Pedido: conferir se os `.md`
estão certos e padronizar os produtos que faltaram.

**1. O tema de trabalho foi publicado.** `themes(first: 10)` devolveu o
`166080315440` como MAIN, com o nome "DEV (mais recente)". Os documentos
ainda diziam que ele era o tema de trabalho despublicado. Hoje não existe
tema de trabalho; `comece-por-aqui.md` e `instrucoes-do-projeto.md`
corrigidos.

**2. A skill `padronizar-produto-atd` não está ao alcance de sessão na
nuvem.** A da conta aparece como desligada (`enabled: false`, desligada em
23/09 pela interface, registro de 23/09 item 4), e a versão nova mora em
`~/.claude/skills/` do computador do cliente, que a nuvem não enxerga. O
padrão foi tirado de `catalogo-e-busca.md`, seções 1 e 2, e das peças já
certas (camisas NS11 e AR160, pistão 4TNV86, filtro de óleo Agrale 4200).
Para a próxima sessão na nuvem ter a skill: copiar o `SKILL.md` para este
repositório ou religar a da conta.

**3. A skill `poupar-tokens-print-shopify` está com tema velho.** Ela cita o
tema `144975724592` e diz que o cdn `21` é o DEV e o `6` o publicado. Esse
tema não existe mais. Correção é na conta do cliente, onde a skill mora.

**4. Os 9 Lombardini criados à mão em 23/09.** Sem tipo, sem etiqueta, sem
metacampo, sem SEO, título de anúncio e descrição do Mercado Livre.
Padronizados; detalhe e regras novas em `catalogo-e-busca.md`, "Padronização
de 24/09". Depois do metacampo, `tagsAdd` e `tagsRemove` de
`atd-tmp-reindex` nos nove, pela regra 9. Lidos de volta: tipo, marca,
etiquetas, metacampo e SEO gravados, e as peças entraram sozinhas em
Filtros, Bronzinas e Pistões.

**Não foi possível conferir a faceta pela URL da loja**: a rede da sessão na
nuvem recusa `loja.atratordiesel.com.br` (proxy, 403). Na próxima sessão com
navegador, confira
`/collections/lombardini?filter.p.m.custom.modelos_compativeis=LDW%201003`,
que deve devolver 6 peças (bucha, filtro de óleo, bronzina, correia,
filtro de ar LDW e conjunto do pistão), mais os 4 links de recomendação.

**5. SEO desatualizado em 31 produtos.** Ver `catalogo-e-busca.md`.

**6. Quatro achados que esperam o cliente**, em `comece-por-aqui.md`, item
14: estoque do 30508 e do 11352 contra a lista de zerados, a descrição do
Conjunto do Pistão Agrale 4100 que virou texto do ML e contradiz o título,
os modelos que ficaram fora dos Lombardini e o `Original`.

---

## Registro de 23/09/2026: texto novo do hero e o editor que não salvava

Pedido: trocar título e subtítulo do hero por "Máquina parada custa caro" e
"Cada hora parada é prejuízo. Encontre a peça certa para colocar sua máquina
de volta ao trabalho.", julgando os pontos. O editor da Shopify recusava
salvar com erro de range.

**A causa não estava no hero.** Os oito `range` do bloco do hero estão
dentro da grade. O culpado era o bloco de marcas, na mesma página:
`brand_height_mobile: 70` gravado no `index.json`, contra o schema
`min 60, max 148, step 4`, que só aceita 60, 64, 68, 72, 76... O schema
novo foi gravado em 22/09 às 13:56 UTC, um minuto depois do `index.json`, e
a Shopify não revalida o template quando o schema muda. Como o editor grava
o template inteiro, um valor fora da grade em qualquer bloco trava a página
toda. Descuido da gravação de 22/09.

**Saída pelo editor**, porque o tema 24 é o publicado e o conector não grava
nele: "Altura do cartão (celular)" das marcas em 76. Não muda nada na tela,
porque o CSS do bloco já desenha `max(76px, valor)`, ou seja, 76 hoje.

**Pontos:** título sem ponto final, como todos os títulos da home e o
título anterior; subtítulo com os dois, porque são duas frases.

Medido antes da troca, no tema 24, trocando o texto direto na página:
título numa linha a 1440 e a 375; subtítulo passa de 1 para 2 linhas a
1440 (conteúdo de 236 a 592 no banner de 164 a 664) e de 2 para 3 a 375
(banner de 173 a 662, 25px mais alto).

**Segunda parte: hierarquia de título e subtítulo.** O cliente salvou o
texto, duplicou o publicado como `166080315440` (`/t/25/`) e pediu para
conferir quebra, peso e tamanho pensando em conversão, com a dúvida de se
devia ficar tudo numa linha.

Medido antes, a 1440: o subtítulo quebrava no meio da frase ("Cada hora
parada é prejuízo. Encontre a peça certa para / colocar sua máquina de
volta ao trabalho."), porque o `max-width: 46ch` do `atd-vitrine.css`
fechava a caixa em 500px. Título com 54px e subtítulo com 17,3px, razão de
3,1.

Decisão: título como estava (Barlow Condensed 700, 54px, uma linha em toda
largura) e subtítulo com **uma frase por linha**, que é a ordem
problema, agravante e solução, e a solução fica colada no "Qual é a sua
máquina?". Três tamanhos testados na página antes de gravar (17,3, 19 e
20px, em 1440, 1024, 768 e 375). Ficou 20px a 1440, porque a linha da
promessa dá 638px e o localizador embaixo tem 640: as duas fecham na mesma
largura. Tudo numa linha só foi descartado: 97 caracteres, mais largo que o
localizador, e quebraria no celular de qualquer jeito.

Gravado no tema 25: `blocks/ai_gen_block_baca937.liquid` (parte o texto no
primeiro ". " em dois `.atd-hero-frase`) e `assets/atd-sistema.css` (tamanho,
entrelinha 1,45 e teto de 34em). MD5 dos dois igual ao disco. Medido
depois: 20px a 1440 (265 e 638px, uma linha cada), 17,6px a 1024 e 16px a
768, uma linha por frase; a 375 três linhas, banner de 173 a 657; sem
rolagem lateral em nenhuma. O temporário `assets/atd-tmp-hero2.txt` foi
reusado e esvaziado de novo.

Armadilha nova: o `themeFilesUpsert` devolveu `upsertedThemeFiles` só com o
arquivo TEXT da chamada, sem os dois por URL, e os dois gravaram. Só o MD5
prova.

## Registro de 23/09/2026 (fim da noite): a marca vira lista, o banner respira e a busca do celular

Terceira volta no mesmo dia, com o cliente mandando print.

**1. A busca com as duas bordas, de novo.** Ele mandou a foto e disse que
continua. Medido no tema 24, com o campo em foco, a 375, 768 e 1440: uma
borda de 1px em rgb(30,91,57) e `box-shadow: none` nos três. Medido no tema
PUBLICADO, na mesma condição: `rgba(30,91,57,0.14) 0 0 0 3px`, ou seja, o
halo ainda está lá, porque a correção vive no tema despublicado. Ou o print
é do site no ar, ou é de página guardada em cache.

O que sobrava e não dá para medir daqui é a moldura que o próprio celular
desenha: iOS e Android vestem `input[type=search]` com caixa e cantos
nativos, que nascem da aparência e não da borda, e `border: none` não os
apaga. Entrou em `atd-ajustes-mobile.liquid` a zeragem dos dois caminhos
(`appearance: none` mais borda, contorno e sombra) e dos quatro
pseudo-elementos de busca do WebKit.

**2. "Está tudo muito espremido" no banner.** Estava mesmo, e a causa é
boa de guardar: o respiro entre a nota do Google e a linha de baixo era um
`margin-bottom: 8px` na nota, e ele **nunca valeu**, porque
`.atd-hero-selos li { margin: 0 }` vem depois e tem especificidade maior
(duas classes e dois elementos contra duas classes e um). Medido antes: a
nota fechava em 548 e a linha seguinte começava em 548, zero de folga.

Agora a separação é `row-gap` no próprio `ul`, que nenhuma regra de `li`
alcança, e a coluna segue em 0 porque quem separa os dois selos de baixo é o
ponto do `::before`. Medido depois, a 1440: nota em 541 com 20 de altura,
linha de baixo em 574, 13px de folga. A 375, em coluna: 559, 588 e 614, com
9px entre elas. O conjunto também desceu um pouco (`margin-top` de 22 para
28 no computador, 24 no celular) e o link do catálogo ganhou 4px.

**3. A lista da marca ficou do tamanho da lista do modelo.** Pedido do
cliente. O campo da marca ainda era `<select>` nativo, e a lista de um
`<select>` é desenhada pelo sistema operacional: no computador abria com as
oito marcas de uma vez, ao lado de uma lista de modelos de quatro linhas com
rolagem. Virou a mesma lista própria do modelo, com a mesma classe de
painel, então herdou teto de 336px, borda, sombra e o encaixe dentro da
imagem do banner. Cada marca mostra quantas peças a loja tem, lido do
catálogo, como os modelos já faziam.

Medido a 1440 com as duas abertas no mesmo instante: cada uma nasce em 447,
tem 205px de altura e 245 de largura, cada uma sob o seu campo, e as duas
terminam em 652, 12px antes do fim da foto (664). A 768: iguais, 245 de
largura, terminando em 652. A 375: as duas com 343 de largura, nascendo em
414, sem rolagem lateral.

Duas armadilhas no caminho, as duas medidas:

- **`form.querySelector('.atd-loc__painel')` passou a devolver o painel
  errado.** Com a marca virando lista, ela ficou sendo o PRIMEIRO painel do
  formulário. Resultado: escolher a marca escrevia os modelos por cima da
  lista de marcas e nada abria. Agora a busca é `combo.querySelector`, presa
  ao campo do modelo.
- **No celular o painel da marca saía pela esquerda.** A regra de celular
  prende o painel pela borda direita do campo e o estica por duas colunas,
  o que serve para o modelo, que é a coluna da direita. Na marca, que é a da
  esquerda, a lista de 343px nascia em x = -159. Corrigido com
  `left: 0; right: auto` só para ela.

**4. A skill antiga foi desligada na conta.** Com a permissão do cliente,
pela interface do claude.ai, em Personalizar, Habilidades, Meus. A
`padronizar-produto-atd` da conta está como Desativado; vale a de
`~/.claude/skills/`, que é a mais nova. A `estoque-ensis-ecommerce` continua
ligada.

**Nota de método.** A home desloca uns 13px depois de carregada (a barra de
avisos do topo troca de mensagem). Duas medidas tiradas em chamadas
diferentes não se comparam entre si: foi isso que fez as duas listas
parecerem de tamanhos diferentes (192 e 205) quando eram iguais. Medir as
duas na MESMA chamada resolveu.

Conferido no fim: home, busca com resultado, busca vazia, coleção Yanmar,
coleção com filtro de modelo, coleção Tobatta e contato, todas 200 e sem
nenhum erro de Liquid. O caminho inteiro do localizador testado no
navegador: marca, modelo, "Ver peças" e chegada em
`/collections/yanmar?filter.p.m.custom.modelos_compativeis=2TNV70`.

## Registro de 23/09/2026 (noite): cartao das marcas, hierarquia do banner, seta do localizador e o schema que some

Segunda volta em cima da rodada da tarde, com o cliente olhando a tela.
Medido no tema 24 a 1440x900, 768x1024 e 375x812.

**1. Duas bordas verdes na busca.** Relato: "quando clicamos para pesquisar
aparece duas bordas verdes, uma onde escrevemos e outra por fora". Medido a
375px com o campo em foco: borda de 1px em rgb(30,91,57) mais
`box-shadow: 0 0 0 3px rgba(30,91,57,0.14)`, uma colada na outra. O halo
saiu; o foco continua visivel porque a borda troca de cinza para verde.

O mesmo halo existia no computador, em mais dois lugares, e o cliente nao
tinha visto ainda: `snippets/atd-cabecalho.liquid` e uma secao de Liquid
personalizado gravada dentro de `sections/header-group.json`. Os tres foram
para `box-shadow: none`. Medido depois, com `:focus-within` de verdade:
borda verde, sombra nenhuma.

**2. A faixa de marcas virou cartao.** O cliente reprovou o preto e branco
da rodada da tarde: "as marcas precisam ja ter a cor, talvez um card
parecido com as categorias de tipo de peca". E: "essas linhas divisorias
tambem nao tem que existir" e "se o Temos peca para estas marcas pode ficar
a esquerda como estava, nao acho essas centralizacoes muito luxuosas".

Tres coisas foram descobertas medindo, e nenhuma era do bloco:

- **o filete embaixo de cada logo vinha do `atd-sistema.css`**, numa regra
  com !important que vestia todo item da grade. A rodada da tarde tirou a
  borda do bloco e a linha continuou na tela, porque o dono era outro;
- **o desenho tinha quatro donos que discordavam**: o bloco pedia celula de
  160x100, `atd-vitrine.css` impunha grade de 8 colunas, `atd-regua.css`
  impunha fila sem quebra com item elastico, e `atd-sistema.css` impunha
  altura, vao e filete com !important. Quem ganhava mudava de largura para
  largura;
- **a centralizacao era do bloco**. O `atd-vitrine.css` ja manda a faixa
  seguir a regua (`margin-inline: 0`, titulo a esquerda) e o bloco ganhava
  dele com `max-width: 1120px; margin: 0 auto`. Medido a 1440: o resto da
  home comeca em 80px e a faixa comecava em 155px. Nao era estilo, era
  desalinho.

O conserto foi juntar o desenho num lugar so. As regras de marcas sairam das
tres folhas (`atd-vitrine.css` 14515 para 14164 bytes, `atd-regua.css` 10023
para 9269, `atd-sistema.css` 31147 para 27258) e o cartao inteiro passou a
morar em `blocks/marcas.liquid`. O `atd-marcas-medida` deixou de escrever
grade, celula e vao em estilo inline: agora ele le a celula que o CSS
desenhou e escreve so o tamanho do logo, que e a unica coisa que so ele sabe
calcular.

Medido depois, a 1440: sete cartoes de 170x100 numa linha, primeiro em 75 e
ultimo terminando em 1355, que e exatamente onde a faixa de tipos de peca
fecha. Titulo e rodape em 75, alinhados com o resto da home. Logos em cor,
com area de tinta entre 3093 e 3098 pixels quadrados, diferenca de 0,16%
entre a maior e a menor. A 768: quatro por linha, 4+3, cartoes de 166x88. A
375: duas colunas de 162px comecando em 16 e 198, **identico** as colunas
dos tipos de peca, com altura de 76px.

**3. A frase do rodape em duas linhas.** "no desktop a frase para Toyama,
Bufallo e outras marcas esta quebrando no final sem precisar". O bloco
impunha `max-width: 58ch`, que a 1440 da 512px, e a frase precisa de 608.
Com o bloco fora do caminho vale a regra do `atd-regua.css`, 78ch, que da
689. Medido depois: 23px de altura, uma linha so.

**4. Hierarquia da linha de baixo do banner.** "a parte de mais de 60 anos
no ramo, a nota no Google e loja fisica em Goiania, todas tem a mesma
hierarquia? de veja o catalogo completo tambem? estou achando todas iguais".

Estavam iguais mesmo: os tres selos com 13px, peso 400 e branco a 82%, e o
link do catalogo com 14px e branco a 86%. O cliente escolheu, entre tres
opcoes, "nota do Google em primeiro".

Agora sao tres degraus. A nota ocupa a linha de cima sozinha, com estrela em
ouro e o numero em 18px peso 700, branco cheio. "Mais de 60 anos" e "Loja
fisica em Goiania" descem para 12,5px a 58%, separados por um ponto de 3px.
O link do catalogo fica em 13px a 66%, e e a unica coisa ali com risco
embaixo, que e o que o olho procura quando quer clicar.

**5. A seta do localizador nao era botao.** "aquela seta que fica para cima
e para baixo nao e um botao clicavel, eu clico nela e a lista nao abre e
fecha". Era um `<span>` com `pointer-events: none`, ou seja, desenho puro.
Virou `<button type="button">` de 40px de largura por toda a altura do
campo, com o chevron desenhado no `::after`. Fica fora da ordem de tabulacao
de proposito: quem usa teclado ja abre a lista com a seta para baixo dentro
do campo.

O `mousedown` do botao chama `preventDefault` para o campo nao perder o
foco no meio do gesto; sem isso o clique fechava pelo blur e o click logo em
seguida reabria, e a seta virava um botao que nunca fecha. Medido: tres
cliques seguidos dao aberto, fechado, aberto. A seta nasce desabilitada e so
liga quando a marca e escolhida, junto com o campo.

**6. A lista para antes do fim da imagem do banner.** Pedido: "seria
interessante se a lista acabasse antes da imagem do banner acabar, para nao
invadir a parte de pecas". O cliente escolheu, entre tres opcoes, "uma
coluna, com rolagem", sabendo que sobram quatro modelos a vista.

Armadilha medida no meio do caminho: `form.closest('[class*="ai-hero-banner-"]')`
devolve a **caixa de texto**, `ai-hero-banner-content-`, nao a foto. Medido:
a caixa termina em 579 e a foto em 664, e a lista saia 85px menor do que
podia, presa no piso de 160. Passou a medir
`img[class*="ai-hero-banner-image-"]`, que e a foto de verdade. Medido
depois: lista de 192px, terminando em 652, com 12px de folga ate o fim da
imagem. E a mesma armadilha do `[class*=]` que ja mordeu o logo em 09/09.

O limite so vale a partir de 750px. No celular o banner nao tem altura fixa,
ele cresce com o proprio conteudo e termina poucos pixels abaixo do campo;
prender a lista a ele ali deixaria uma janelinha de duas linhas. Medido a
375: lista de 386px, terminando em 800, 12px acima da dobra, como antes.

**7. `range` de schema precisa fechar no passo.** Esta custou meia hora e
vale por si. O `blocks/marcas.liquid` **nao gravava**: `themeFilesUpsert`
devolvia `userErrors: []` e `upsertedThemeFiles: []`, sem reclamar de nada,
e o arquivo no tema continuava com o tamanho e a data velhos. Outros nove
arquivos da mesma chamada gravaram.

Bissecado trocando o schema novo pelo antigo: com o schema antigo o mesmo
corpo gravou na hora. A causa estava em um `range` do schema novo:

    { "type": "range", "id": "brand_height_mobile", "min": 60, "max": 150, "step": 4 }

`(150 - 60) / 4 = 22,5`. A Shopify exige que o intervalo feche em numero
inteiro de passos, e recusa o arquivo **inteiro** quando nao fecha, em
silencio, pela API. Virou `max: 148` e gravou na primeira tentativa.

**Como conferir antes de subir**, em qualquer schema:
`[x for x in settings if x['type']=='range' and (x['max']-x['min']) % x['step']]`
precisa voltar vazio.

**8. Remover setting em uso e com valor salvo.** No meio da bissecao ficou a
duvida de se a Shopify recusaria remover settings que o `templates/index.json`
ainda usa. Foi feito na ordem segura assim mesmo: primeiro sairam do
`index.json` os nove valores mortos (as quatro linhas divisorias, largura de
desktop e de mobile, recuo da imagem, espacamento da secao e largura em
porcentagem), depois saiu o schema. Vale como regra: **para acrescentar,
schema primeiro; para remover, index.json primeiro.**

**9. Descoberta por IA e por busca.** Pedido: "confira se o codigo do site
esta bem buscavel nas redes e por IAs tambem quando perguntarem sobre pecas
que trabalhamos".

O que ja vem pronto da Shopify e esta certo: `robots.txt` com instrucoes
para agente, `llms.txt`, `sitemap_agentic_discovery.xml`, endpoint UCP/MCP
em `/api/ucp/mcp` e o perfil em `/.well-known/ucp`. O `meta description` da
home existe e esta bom (a regex da primeira medicao falhou porque a tag tem
quebra de linha no meio; nao era ausencia).

O que faltava e foi feito em `snippets/atd-schema-loja.liquid`:

- `makesOffer` tinha cinco marcas escritas a mao e deixava de fora
  Tramontini e Agritech, que tem prateleira. Agora a lista e lida do
  catalogo: marca com colecao e pelo menos uma peca entra sozinha. Medido
  na home: oito marcas;
- nao havia nada sobre tipo de peca nem sobre modelo de maquina. Entrou um
  `hasOfferCatalog` com dois catalogos, tambem lidos do catalogo real.
  Medido: 9 tipos e 10 modelos;
- `sameAs` nao existia. O Instagram e o Facebook da loja estao no rodape,
  mas nada dizia ao buscador que aquelas contas sao desta empresa. Entraram
  os dois mais a ficha do Google Maps;
- entrou `knowsAbout` com os seis assuntos da loja.

A conta de virgulas do JSON e feita por `split` e `join` de proposito:
montar JSON com `forloop.last` quebra em silencio quando um item do meio e
pulado, e JSON quebrado e pior que JSON ausente. Medido depois com
`json.loads` nos dois blocos da home: os dois validos.

**10. A skill duplicada.** "deixe apenas a mais atualizada na pasta
globalmente". Conferido: a unica colisao de nome era `padronizar-produto-atd`,
que existia na conta do cliente e na pasta do projeto. A do projeto e a mais
nova, de 22/09, com 8.199 bytes, e era a que rodava (invocada, a base
directory apontou para a pasta do projeto: **pasta local ganha da conta**).
Ela foi movida para `~/.claude/skills/padronizar-produto-atd/`, que vale em
qualquer projeto desta maquina, e a copia do projeto foi apagada. Desligar a
da conta so o cliente pode fazer.

**Verificacao final.** Sete paginas (home, busca com resultado, busca vazia,
colecao Yanmar, produto, contato e colecao Agritech) respondem 200 no tema
24 com zero erro de Liquid.

**Arquivos de trabalho:** mais dezesseis `atd-tmp-*.txt` em Ativos, ja
esvaziados. Apagar continua bloqueado na API.

\---

## Registro de 23/09/2026 (tarde): botão, menu, lista de modelos, faixa de marcas e o diário

Sete pedidos do cliente numa rodada só. Tudo medido no tema 24, a 1440x900 e
a 375x812.

**1. A frase do botão do WhatsApp fora do centro.** Não era daquele botão:
`justify-content: center` centra o conjunto ícone+frase, e o ícone (20px)
mais o vão (8px) ficam todos do mesmo lado. Medido: texto a 49px da borda
esquerda e a 21px da direita, 28px fora do centro, igual nos três lugares
onde o snippet `atd-whatsapp` aparece (busca sem resultado, "Falar com
especialista" da home, "Tirar dúvida sobre esta peça" do produto). Uma regra
em `atd-custom.css` põe um contrapeso invisível do tamanho do ícone do outro
lado. Medido depois: 49 contra 49, e o botão 28px mais largo. Varridos
também o botão de ícone só do cabeçalho e o "Ver tudo de Yanmar" do mega
menu: aqueles não casam com o seletor e ficam como estavam, de propósito.

**2. Tipos de peça do mega menu em ordem alfabética.** Feito, e o corte de
12 teve de sair junto: a Yanmar tem 24 tipos, e em A-Z o corte esconderia
Filtro, Juntas, Pistão e Virabrequim, que foi exatamente o problema que a
lista de `prioridade` existia para consertar em 16/09. Com a prioridade
fora, o arquivo ficou 139 bytes menor e uma regra mais simples.

Com 24 pastilhas a coluna da direita passa da esquerda, e a direita é
posicionada em absoluto: não empurrava o corpo do menu, que vivia travado em
440px. Então o `atd-catalogo.js` passou a medir o painel da marca ativa e
dar essa altura ao corpo (`medirCorpo`). Medido a 1440x900: Yanmar 621px sem
barra de rolagem; Tramontini, que tem um tipo só, 443px, sem o vão vazio de
antes. A 1440x700 a Yanmar bate no teto da janela, para 13px antes da borda
e a coluna volta a rolar, que é o mal menor.

Os modelos ("Por modelo") seguem a mesma ordem, alfabética pelo nome
mostrado: 3TNV88 e 4TNV88, B9 e NB10, Microtrator TC10, Microtrator TC11 e
TC14, NS11 e NS12, NS18, NS50, NS75 e NS80, NS90 e NS95.

O `atd-nav-categorias`, que é a fila de tipos do celular na página de
coleção, **ficou com a prioridade**. É outra forma: lá a fila rola de lado e
só os primeiros são vistos sem rolar, então "Filtro" primeiro vale mais que
"Anéis" primeiro. Duas formas, duas ordens, de propósito.

**3. A lista de modelos da home cortava.** Reproduzido e medido: eram dois
defeitos somados. O `hero-banner` tem `overflow: hidden` e o painel passava
223px do fim dele, ou seja, cinco linhas aparadas fora sem rolagem nenhuma.
Destravar o corte não bastou: a seção seguinte da home é irmã e vem depois
no documento, então pintava por cima. Duas regras na folha do snippet, as
duas valendo só enquanto a lista está aberta. Medido depois: o painel passa
142px do banner, nada do banner vaza, nada cobre, e a página não ganha
rolagem lateral.

No celular sobrava um terceiro caso: a 375x812 o painel nascia em 414 e ia a
852, 40px abaixo da dobra. Agora o `encaixar()` usa o espaço que sobra
abaixo do campo como teto. Medido: 386px de altura, fim em 800, 12px de
folga.

**4. "Mais procurados" saiu, a lista virou A-Z.** Com a permissão do
cliente. Saiu junto toda a máquina de ranking do Liquid: fita de pesos,
corte por teto de 12, lista de destaques. A contagem de peças ficou ao lado
de cada modelo; o que saiu foi a ORDEM por contagem, não o número. Quem
chega ali tem um código de motor na cabeça e procura pelo código.

Dois ganhos de brinde. O mapa de coleção própria passou a ser consultado
para TODO modelo, e não só para os que entravam em "Mais procurados": NSB18R
e BM18, por exemplo, iam para o filtro tendo prateleira. E a ordem fina foi
para o JavaScript, com `localeCompare` numérico, porque `sort_natural` do
Liquid é comparação de texto e põe TC10 antes de TC8. Medido: TC8, TC10,
TC11, TC12, TC14, TC14S; NS11 < NS12 < NS18 < NS50 < NS75 < NS80 < NS90 <
NS95; VIO17 < VIO20 < VIO22 < VIO25.

**5. A faixa "Temos peça para estas marcas".** O cliente achou feio. Medido
antes: ela não estava só feia, estava quebrada. As duas barras verdes que
ladeavam o título saíam com **0px de largura**, e o título, que pede
`text-align: center`, era desenhado à esquerda. Causa: as folhas `atd-*`
ganhavam do `{% style %}` do bloco, a armadilha já conhecida do projeto. Por
isso agora cada regra do bloco começa com `html body`.

Desenho novo: sem barras, sem cartão branco, sem borda, sem sombra; logo em
preto e branco com a cor voltando no passar do mouse (e cor direto em quem
toca, por `@media (hover: none)`); 84px de ar acima e 76px abaixo; título
centrado de verdade, no tamanho e na cor que o cliente escolheu. O
`atd-marcas-medida` continua igualando a área de tinta e apagando o fundo
branco dos JPEG: medido depois, Yanmar em 77,6x57,4 com `multiply` no lugar.

Os ajustes do editor que o desenho novo não usa mais ("Linhas divisórias"
inteiro, e cor de fundo, borda e arredondamento dos quadrados) ficaram no
schema de propósito, para não apagar valor salvo do cliente.

**6. Sobre o `paginate`.** O cliente perguntou se dava para contornar. Não
precisa: a loja tem 132 produtos e `paginate by 250` pega tudo numa volta
só, então não existe truncamento. A varredura da busca sem resultado só roda
quando a busca deu zero. A do localizador roda em toda home, e essa sim vale
olhar se o catálogo crescer muito.

**7. As duas skills que eu disse que não existiam.** Eu estava errado.
Conferido com `ListSkills`: `padronizar-produto-atd` e
`estoque-ensis-ecommerce` estão na conta do Claude do cliente, ligadas, e
aparecem com o prefixo `anthropic-skills:`. Em 22/09 a procura olhou só a
pasta `.claude/skills/` do projeto. O estrago: existe agora uma segunda
`padronizar-produto-atd`, dentro do projeto, com nome igual ao da que já
existia. As duas funcionam; vale o cliente escolher uma e desligar a outra.
O registro de 22/09 recebeu a correção no lugar.

**8. O diário saiu daqui.** `comece-por-aqui.md` é lido no começo de toda
tarefa e tinha 87 KB, dois terços deles diário. O diário foi inteiro, sem
corte, para `registros.md`, e o arquivo de entrada caiu para 22,5 KB.
Conferido palavra por palavra que nada se perdeu. Procurados parágrafos
repetidos entre todos os `.md` e os `SKILL.md`: só um, de 200 caracteres,
que é a instrução de "leia uma vez por conversa" e é repetida de propósito
em três skills. Fora o diário, não havia gordura.

**Arquivos de trabalho:** ficaram sete `atd-tmp-*.txt` novos em Ativos, já
esvaziados (uma linha de aviso cada). Apagar continua bloqueado na API.

\---

## Registro de 22/09/2026: busca por código, lista de modelos e a skill que faltava

**"4tnv84 não retorna o 4tnv84t, seria como se faltasse uma letra."** Medido
e explicado: a busca da Shopify completa palavra pelo começo **só no
título**. Etiqueta e metacampo exigem a palavra inteira, e 4TNV84T só existe
na compatibilidade. Provas, contando itens da grade: `4tnv10` zero e
`4tnv106` uma; `4tnv9` zero e `4tnv94` uma; `nsb1` zero e `nsb11` oito;
enquanto `camis`, `bronz`, `pist` e `virabr` devolvem a lista toda.

**O T é turbo e não entra na regra de simplificar** (era a pergunta do
cliente sobre 4TNV98 e 4TNV98T). A prova está no próprio catálogo: o
`elemento-filtro-combustivel-yanmar-4tnv88` serve em 4TNV98 e **não** em
4TNV98T; o `elemento-do-filtro-separador-de-combustivel` serve nos dois. A
regra 4 da compatibilidade fica como está.

O conserto foi na busca e não no catálogo: busca que devolve zero agora
oferece **"Você quis dizer"**, com os modelos do catálogo que começam pelo
que foi digitado, a contagem de peças e o link para a faceta, que é exata.
Detalhe em `catalogo-e-busca.md`.

**A lista de modelos não abria ao trocar de marca.** Dois defeitos somados:
o clique que escolhe a marca chega depois do `change` e fechava o painel que
o `change` tinha acabado de abrir; e campo que já está focado não dispara
`focus` de novo, então tocar nele não fazia nada. Por isso só digitar e
apagar trazia a lista. Os dois reproduzidos por medição antes de mexer.
Detalhe em `tema-e-design.md`.

**CORRIGIDO EM 23/09: o parágrafo abaixo está errado.** As duas skills
existem e estão ligadas, na conta do Claude do cliente, e aparecem com o
prefixo `anthropic-skills:`. Conferido em 23/09/2026 com `ListSkills`:
`padronizar-produto-atd` (skill_01MKkKFJ...) e `estoque-ensis-ecommerce`
(skill_01Sd4C6A...), as duas `enabled: true`. O que aconteceu em 22/09 foi
que a procura olhou só a pasta `.claude/skills/` do projeto, e não a conta.
Resultado: foi escrita uma segunda `padronizar-produto-atd` dentro do
projeto, com o mesmo nome da que já existia na conta. As duas funcionam,
mas duas skills com o mesmo nome confundem na hora de invocar; vale o
cliente escolher uma e desligar a outra. Fica o texto original abaixo, por
honestidade de registro.

**A skill `padronizar-produto-atd` não existia.** A seção 2 de
`catalogo-e-busca.md` dizia "a tabela de campo por campo virou a skill", e a
skill nunca foi escrita: o padrão de cadastro estava perdido. Foi escrita
agora, a partir de três peças já certas do catálogo. Continua faltando a
`estoque-ensis-ecommerce`, citada pela skill do catálogo e pela
`estoque-ensis-ml`, e que também nunca existiu.

**Pix e primeira compra**, pergunta do cliente: nada a mexer no site. Os
dois valem 5%, não somam, e o checkout aplica o maior. O `BEMVINDO5OFF`
continua útil para quem paga no cartão, onde o desconto de Pix não vale.
Decisão comercial, registrada em `yampi-checkout-e-catalogo.md`.

---

## Registro de 21/09/2026: segunda volta com o print do cliente

**Sobre as datas deste documento.** As seções marcadas 22 e 23/09/2026 foram
escritas na mesma corrida de 21/09/2026, com a data errada. Ficam como estão
para não quebrar as referências cruzadas; a ordem de leitura é a de cima para
baixo, da mais nova para a mais velha.

### O print devolveu três coisas, e as três eram verdade

"Vê que não está alinhado, e o código desceu, tinha que continuar aonde
estava. Percebe que parece que o Compra garantida está jogada."

1. **O código desceu.** Na primeira volta ele foi para o grupo DETALHE, junto
   com a prosa. Errado: código é o que a pessoa confere contra a peça na
   bancada, do lado da marca. Voltou para DECIDIR, logo depois da marca.
   A ficha lê de novo: marca, código, compatibilidade, medida, estoque.

2. **O "Compra garantida" estava jogado, e não era impressão.** Medido a 961:
   cartão de 430px para 213px de texto, **217px de ar** com o título boiando
   no meio. Era o `justify-content: center` de 22/09 fazendo exatamente o que
   o cliente tinha recusado.

   A causa: a altura da foto acompanha a LARGURA da coluna (quadrado), e a
   altura da coluna de compra quase não muda. A 1440 a foto dá 600 e sobra
   pouco; a 961 ela dá 412 e sobram 217. O vão ia todo para o cartão.

   **A resposta: quem estica é a foto, não o cartão.** A moldura da foto pega
   o que a coluna de compra deixar, entre 75cqw (paisagem 4:3) e 125cqw
   (retrato 4:5) da largura da própria coluna. É conteúdo, não vão. A imagem
   continua em `object-fit: contain`, então nunca deforma nem corta. Só o
   que sobrar depois do limite vai para o cartão, e ali se reparte entre as
   quatro faixas dele em vez de virar um buraco só.

3. **"Mover retirada e envio para a esquerda."** Feito, e de vez. O
   revezamento de 22/09 (ora na ficha, ora no cartão, conforme o estoque)
   existia para tapar buraco, e buraco não existe mais.

**Medido depois, fim de texto contra fim de texto, 0px em todas:** cabo da
direção a 768, 900, 990, 1259 e 1440; bronzina de 5 variações a 768 (1134),
990 (1086) e 1440 (981); escala do regulador, esgotada, a 1440 (1115) e 768
(1361). Sem rolagem lateral em nenhuma.

**Um erro antigo apareceu no caminho:** a 375, "Retirada em Goiânia" saía
DUAS vezes, na ficha e no cartão. Não era novidade desta rodada. O bloco
escreve `.atd-cs-<id> .atd-cs__entrega` (peso 0,2,0) e a regra que devia
esconder era `html body .atd-cs__entrega` (peso 0,1,2). Menos peso, perdia
calada. Com o `.product-information__grid` no meio a conta vira 0,2,2 e
ganha, sem `!important`.

### A trilha ganhou o degrau do meio

"Na bomba de óleo lubrificante NS11 aparece Início / Agritech ou Início /
Yanmar, mas tinha que ser Início / Yanmar / Bomba."

Certo: a trilha dizia a marca e nunca dizia QUE PEÇA é. Agora são três
degraus, marca e tipo.

- A **marca** sai de uma lista na configuração do bloco, na ordem em que ela
  está escrita: `yanmar,agrale,tobatta,branco,lavrale,lombardini,tramontini,agritech`.
  A peça que cai em Yanmar e em Agritech sai como Yanmar porque Yanmar vem
  antes. De propósito a coleção de chegada **não** ganha mais: a trilha é o
  lugar da peça no catálogo, não o caminho que a pessoa fez, e o mesmo texto
  vai para o JSON-LD, onde variar por origem confunde o Google.
- O **tipo** é o campo "tipo de produto", o mesmo que alimenta o filtro
  "Tipo" da listagem. O link cai na lista da marca já filtrada:
  `/collections/yanmar?filter.p.product_type=Bomba`. Coleção própria de tipo
  existe para alguns (Camisas, Juntas, Bronzinas) e não para outros (Bomba,
  Rotor, Cabo); o filtro existe para todos, por isso a trilha usa o filtro.

Medido: bomba NS11 "Início / Yanmar / Bomba", cabo "Início / Tobatta /
Cabo", camisa "Início / Yanmar / Camisa", conjunto do pistão "Início /
Agrale / Pistão" (com o acento escapado certo na URL do filtro). O JSON-LD
passou a ter quatro degraus, terminando no título da peça.

### A logo, resolvida

Ver `tema-e-design.md`. Em resumo: de **965 KB por página para 9,3 KB**, com
o desenho do mesmo tamanho na tela (82x60 no cabeçalho, 52x40 no rodapé).

### "tobata" achava 14 peças e zero exatas

Achado enquanto se media outra coisa. O catálogo escreve "Tobatta" e a loja
etiqueta as duas formas; quem digita não sabe qual é a da loja. A Shopify
achava as 14 por semelhança, mas o recorte de casamento exato dizia
"nenhuma peça responde exatamente", que é pior do que não dizer nada.

A regra nova é simétrica e sem lista de sinônimos para manter: a palavra
perguntada ganha uma forma com as consoantes dobradas encolhidas (tt, rr,
ss, ll, nn, mm, cc) e o palheiro ganha a mesma redução. Medido depois:
"tobata" 14 e todas exatas, "tobatta" 14 e todas exatas, e as onze medidas
anteriores **iguais** ("anel ar160" 1, "aneis" 22, "pistao" 8, "camisas" 4,
"filtro de ar branco" 1, "junta yanmar" 12, "ns11" 12, "camisa yanmar ns90"
1).

\---

## Registro de 23/09/2026: trilha, ordem da página de produto, localizador e plural

### A palavra "Início" estava sendo cortada

Medido a 1440 e a 800: a trilha lia **"nício / Camisas"**. O texto começa em
x=731 e o `.group-block` que o editor põe em volta da coluna de compra tem
`overflow: hidden` com a borda no **mesmo** x=731. O "I" é uma haste de 1px
que cai em cima da linha de corte e some.

O corte não vinha de folha nenhuma: vem do **atributo `style` que o editor
imprime no elemento**, junto com um `--border-radius: 30px`. Por isso a
correção precisou de `!important`, o que aqui não é força bruta e sim a única
forma de ganhar de um style inline. Medido antes de mexer: `scrollWidth` 624
contra `clientWidth` 624, ou seja, o corte não estava segurando nada. E a
borda está em `--border-style: none`, então nada de visível dependia dele.
Está na seção 14 de `atd-filtros.css`, item 14.1.

### A ficha virou dois grupos, e o botão de comprar entrou no meio

Relato: "a parte debaixo não está alinhando com a quantidade e adicionar
carrinho, preciso que disponha melhor para equilibrar o peso e a hierarquia
dos dois lados, não é apenas gerar um espaço em branco para equiparar as
linhas do horizonte".

Medido na camisa NS90, a 1440: preço em y=364 e botão de comprar em y=889.
Eram **525px de ficha técnica entre o preço e a ação**, e o botão caindo
abaixo da dobra numa janela de 900. No celular era pior: a compatibilidade,
que nesta loja é o dado que decide a compra, começava em **y=1220**, atrás de
um cartão de selos de 362px.

`blocks/atd_produto_ficha.liquid` passou a sair em dois blocos irmãos:

- **DECIDIR**: marca, compatibilidade, medida, observação e estoque. O que o
  mecânico confere antes de clicar.
- **DETALHE**: código, conteúdo, equivalências, a prosa da descrição,
  retirada e envio e o WhatsApp. Referência, vem depois da ação.

O invólucro do editor vira `display: contents` e uma regra só
(`.atd-ficha__detalhe { order: 1 }`) resolve computador e celular. A altura
somada é a mesma, então a linha do horizonte continua fechando com o que já
existia: o `flex: 1` do cartão debaixo da foto agora só absorve os 13px que
sobram, não os 382.

No celular o cartão "Compra garantida" foi para o fim, depois do detalhe.
Para isso o invólucro dele também vira `display: contents` abaixo de 750px, e
o recuo lateral de 16px teve que descer para os cartões: margem em caixa que
não existe não pinta.

**Medido depois**, peça com estoque e peça esgotada, em 390, 768, 990 e 1440:
topo com 0px de diferença e fim com 0px em todas. Botão de comprar a 1440:
de 889 para 692 (peça com estoque) e para 628 (esgotada). No celular a
compatibilidade saiu de 1220 para **734**, acima do botão.

### O localizador deixou de ser um `<select>`

Três reparos numa tacada só, em `snippets/atd-localizador.liquid`:

1. **"Formato muito simples e sem design".** Os dois campos têm folha, a
   lista não tinha e não tinha como ter: quem desenha a lista de um
   `<select>` é o sistema operacional, e nenhuma linha de CSS alcança ela.
   O campo do modelo virou lista própria, com o verde da loja e a contagem
   de peças ao lado de cada modelo.
2. **"Continua tendo que rolar lá embaixo".** A Yanmar tinha 64 opções;
   ordenar ajuda mas não resolve. O campo agora **filtra enquanto se
   digita**, sem acento e sem hífen: "ns1" deixa NS11, NS12 e NS18; "tc"
   deixa os seis microtratores.
3. **"Atualizar de acordo com o que o pessoal procura".** Ver a seção
   seguinte. "Mais procurados" passou a ser **calculado por quantas peças o
   catálogo tem para cada modelo**, e não mais fixo. Medido depois: a Yanmar
   abre em NS18 (14 peças), TC11 (14), NS11 (13) e TC14 (13), no lugar de
   2TNV70, 3D68E e 3D76.

Marca com poucos modelos não ganha rótulo de grupo: a Tobatta tem 14 e sai
numa lista só, por peso. Grupo só aparece quando sobram 4 ou mais fora dos
destaques.

### Termo de busca: a Shopify não entrega, e venda aqui é ruído

Conferido em 23/09, e vale registrar para não se tentar de novo:

- `FROM sessions ... GROUP BY search_term` devolve **Column Not Found**.
  `landing_page` também não existe. O relatório "Top online store searches"
  existe no admin, mas não pelo ShopifyQL desta conexão.
- Venda não serve de medida de procura: `FROM sales GROUP BY product_title`
  em 180 dias dá **21 pedidos**, sendo 7 de um anel de milho. Ordenar
  qualquer coisa por isso seria ordenar por ruído.

O sinal honesto que existe é o **catálogo**: a loja compra e cadastra peça do
que o balcão pede, então quantas peças existem para um modelo é a medida de
procura que a própria loja produz. É o mesmo critério já aprovado em 21/09
para a fila de botões da coleção, e ele se atualiza sozinho: peça nova
cadastrada muda a ordem sem ninguém editar nada.

### Plural irregular na busca, e o cabo do acelerador

Detalhe em `catalogo-e-busca.md`. Em resumo: "anel" agora acha "Anéis"
(e "pistão" acha "pistões", "motores" acha "motor"), e quando nenhuma peça
responde exatamente à pergunta a página passa a **dizer isso** em vez de
mostrar as parecidas caladamente. O `Cabo do Acelerador Tobatta` ganhou as
14 etiquetas de modelo Tobatta e o metacampo de compatibilidade.

\---

## Registro de 22/09/2026: linha do horizonte, busca e peso das imagens

### A pagina de produto ganhou linha do horizonte

Relato: "preciso que o topo da imagem do lado esquerdo coincida com o
inicio do texto do lado direito, e a mesma coisa para o final dos dois
lados, em todas as dimensoes de tela". Medido a 1440 numa peca esgotada:
foto comecando em y=211 e o primeiro bloco da direita em y=235, e a
esquerda terminando em 974 contra 1356 da direita. **382px de diferenca.**

Tres mudancas, todas em `assets/atd-filtros.css`, secao 14:

1. O recuo de 24px do `.group-block`, o involucro que o editor poe em volta
   da coluna de compra, sai no computador. A coluna da foto nao tem esse
   involucro, entao so um lado recuava.
2. O ultimo cartao da coluna da foto cresce ate o pe da coluna
   (`flex: 1`). Assim o fim dos dois lados casa sozinho, sem numero fixo.
3. **Retirada e envio agora existem nos dois lados e aparecem so num.**
   Peca esgotada: a linha fica no cartao debaixo da foto, que e o lado
   curto. Peca com estoque: fica na ficha, na direita, que passa a ser o
   lado curto, porque o "Avise-me" nao existe. Sao 88px indo sempre para o
   lado que precisa. Quem decide e o proprio "Avise-me", por `:has()`, sem
   JavaScript.

Texto enxugado junto, que foi a outra metade do pedido: o convite do
"Avise-me" virou uma linha ("Avisamos por e-mail assim que ela voltar ao
estoque"), o rodape dele parou de repetir a encomenda que a ficha ja dizia,
e a linha de estoque da peca esgotada virou "Peça sob encomenda". O
"pronta em ate 24h" saiu de vez: prometia prazo em peca que pode estar
esgotada.

Medido depois, em 768, 990 e 1440, e com peca esgotada e com estoque:
**topo com 0px de diferenca em todos**, fim com 0px na esgotada e entre 13
e 50px na com estoque, que e o que sobra do cartao de garantias. No
celular nada muda: a coluna e uma so e a copia do cartao fica escondida.

### A busca parou de misturar

"filtro de ar branco" devolvia 16 pecas de 132 e "junta yanmar" devolvia
69. Agora a primeira mostra **1** e a segunda **12**, com o resto atras de
um botao. Detalhe em `catalogo-e-busca.md`.

### Peso do site: o que foi medido

Medido no tema DEV, com o cache do navegador vazio:

- **204 requisicoes** na pagina de busca, sendo **105 arquivos de
  JavaScript**. E o tema Horizon, que carrega um modulo por componente.
  Nao da para mexer nisso sem trocar de tema.
- **CSS: 35 KB comprimidos no total**, dos quais 17 KB sao nossos, em 9
  arquivos. Nao e gargalo.
- **CLS 0,0045** na home, ou seja, a pagina praticamente nao salta durante
  o carregamento. O limite bom do Google e 0,1.
- **TTFB 860ms** e DOM interativo em 2,7s.
- Imagens: a Shopify ja entrega **WebP** automaticamente. O banner da home,
  que parece pesadissimo (1,7 MB em PNG), chega ao navegador com **197 KB**.
  Os logos de marca vao de 1,5 KB a 24 KB.

**A unica coisa realmente pesada e o logo da loja**: um SVG de **238 KB
ja comprimido** (321 KB cru), carregado em **toda** pagina, exibido com
82px de largura. Sozinho ele pesa quatorze vezes mais que todo o nosso CSS
junto. Nao da para arrumar daqui, porque o desenho e intocavel: precisa ser
reexportado. Ver `tema-e-design.md`.

### "A pagina quebra durante o loading da busca"

Nao consegui reproduzir. O painel do navegador desta maquina nao abre a
gaveta de busca preditiva (e a mesma limitacao ja registrada em
`painel-oculto-trava-animacao`), e o carregamento direto do endereco de
busca, medido quadro a quadro, nao quebrou nenhuma vez. O que encontrei de
concreto e o logo de 238 KB, que atrasa o cabecalho em conexao ruim. Para
fechar esse ponto falta o cliente dizer em qual pagina, no celular ou no
computador, e se acontece toda vez.

\---

## Registro de 21/09/2026 (noite): compatibilidade enxugada em 32 produtos

Tema não entra aqui: **é tudo catálogo, mudou no ar na hora.** O cliente
respondeu as sete divergências levantadas de tarde, deu OK para cortar o que
não fecha e mandou tirar as extensões de modelo do site inteiro. Regra
completa em `catalogo-e-busca.md`, seção "Regra da compatibilidade", e
resumida na skill `catalogo-e-busca-atd`. Texto e etiquetas antigos em
`backup-compatibilidade-21-09-noite.json`.

O que o cliente definiu, e que agora é regra da casa:

- **"O que serve no B9 serve no NB10, menos o virabrequim. O que serve no
  B10 serve no NB13."** São dois pares, não um grupo de quatro. O NB10 saiu
  do jogo de anéis B10 / NB13.
- **Anel e camisa Tobatta AR160 servem só no AR160.** De seis modelos para
  um.
- **Jogo de anéis Agrale M90 fica só no M90.** M85 e M80 têm outro furo.
- **NSB90RE sai.** E, por extensão dessa mesma decisão, todo sufixo de
  acabamento da linha NS (R e RE) e todo código de aplicação depois do
  modelo (`4TNV98-DSA`, `3TNM72-ASA3T`, `4TNV88 XAT`) viram o código base.
  O pistão 3TNM72 sozinho listava **40 variações do mesmo motor**.
- **M90 é Agrale e não pode estar no meio de código Tobatta.** Saiu do
  título, da ficha, do metacampo e da etiqueta do jogo TR9 / AR80 / AS80.

Achado na mesma rodada, e que vale mais que tudo: **o SKU diz a família do
motor**. O `Conjunto do Pistão Agrale 4100 / 4118 / 4120` tem SKU
`7072.004.007.00.3`, e no catálogo oficial da Agrale para esses mesmos sete
tratores a família 7072 é a do **Ruggerini de 2 cilindros**. O M85 que eu
tinha gravado de tarde é Agrale de 1 cilindro: mesmo diâmetro de 85 mm,
outra peça. Saiu. Ficou `MD170, MD171, MD190, MD191`.

Diâmetro nunca foi prova suficiente sozinho. A prova é diâmetro **mais**
família de código.

32 produtos gravados sem `userErrors`, faceta reindexada com
`tagsAdd`/`tagsRemove` e conferida pela URL: NSB90RE, NSB18R, BS180, AS220 e
`4TNV88 XAT` devolvem zero; NS12 e NB10 devolvem o que devem.

\---

## Registro de 21/09/2026 (celular, peça esgotada, botões e localizador)

Tema de trabalho `145546182704`, cdn `/t/24/`. Nove relatos do cliente na
mesma mensagem, mais uma rodada de conversão por iniciativa. Tudo medido
antes e depois, no preview.

### O que estava errado, e o que era falso alarme

**Filas de chips fora de prumo no celular (relato do cliente).** Medido a
375: os chips de "Marca da máquina" e "Tipo de peça" nasciam com
`scrollLeft: 16` e o primeiro chip em **x=0**, encostado na borda da tela,
enquanto os de "Modelo da máquina" começavam em 16. Causa: `scroll-snap-type`
sem `scroll-padding-inline` faz o encaixe comer o recuo da fila. As três
filas agora nascem em 16 e sangram até 375 do mesmo jeito.

**Marcas da home desalinhadas no celular (relato do cliente).** Duas causas
somadas, as duas medidas a 375. A primeira: as células de marca tinham 155px
com vão de 32 (coluna 2 em 203) e as de tipo de peça 155 com vão de 20
(coluna 2 em 191), então as duas faixas vizinhas ficavam 12px fora de prumo e
a de marcas sobrava 13px de régua no fim. A segunda, que é o que o olho vê:
o logo ficava **encostado à esquerda** dentro de uma célula de 155, com até
120px de vazio à direita, ao lado de cartões de tipo de peça que são
centrados. Agora as duas faixas dividem a régua em `calc(50% - 10px)` com vão
de 20, colunas em 16 e 197,5 fechando em 359, e o logo fica centrado na
célula. No computador nada muda: lá a fila é uma linha só e encostar à
esquerda alinha o primeiro logo com o título.

**"Ver menos" não existia (relato do cliente).** A fila de modelos no topo
da coleção abria com "Ver todos os N modelos" e o botão sumia. Na Yanmar,
82 modelos abertos empurram o primeiro produto quase uma tela para baixo sem
jeito de voltar. Agora o botão alterna, e ao fechar rola de volta se o topo
da fila tiver saído da tela.

**"Avise-me quando chegar" empilhado com a esquerda vazia (relato do
cliente).** O bloco `atd_compra_segura` era uma caixa só com duas metades, e
descia para debaixo da foto **apenas quando a peça tinha estoque**. Medido a
1100 numa peça esgotada: foto de 24 a 585 terminando em y=772 e o cartão de
425x255 sozinho em x=641, y=1223, com quase 500px de branco embaixo da foto.
Agora são duas caixas irmãs: a de garantias desce para debaixo da foto
sempre, e a de "Avise-me" nunca desce, porque é formulário e ocupa o lugar do
botão de comprar. **A garantia também deixou de sumir na peça esgotada**:
nota fiscal, sete dias e pagamento seguro falam da loja, não daquela compra,
e peça esgotada é justamente a hora em que a pessoa precisa de motivo para
deixar o e-mail. Medido depois: 768 com garantia em 40 a 355 logo abaixo da
foto, 990 em 24 a 525, 1440 em 75 a 675 (600x162) e o "Avise-me" em 731.

**Botão "Ver todos os produtos" com cor e forma estranhas (relato do
cliente).** Medido a 1280, antes: 230x48, moldura verde de 1px, fundo
transparente, canto de 4px e texto verde de 15px no **peso 400**. Os outros
cinco botões da home estão todos no peso 600 e nenhum outro é vazado: ele
tinha o tamanho de um botão principal com o peso de um texto comum, parado ao
lado do título. Ele fica, porque é o único caminho para o catálogo inteiro
depois que o hero sai da tela, mas no computador virou link com seta (15px,
600, sem moldura) e no celular, onde ele cai sozinho no fim da faixa, virou
botão verde cheio.

**Medida e estoque sem desenho na ficha (relato do cliente).** "Medida: STD,
85 mm" e "78 em estoque, pronta para envio" saíam em prosa, do mesmo tamanho
e cor da descrição, enquanto motores e tratores viravam pastilha. A medida
ganhou um modo próprio na ficha (`spec`), com a mesma pastilha da
compatibilidade mas com o fio em ouro, porque é especificação DA PEÇA e não
modelo em que ela serve. O estoque virou ponto colorido mais texto, com o
complemento em cinza embaixo. Vale para medida, modelo, tipo, furos,
diâmetro, espessura, carreira e capacidade.

**Pix somando com primeira compra (relato do cliente).** Conferido ao vivo na
Yampi em 21/09: "Desconto por Pix" 5% com **"Permitir acumular" desmarcado**,
`BEMVINDO5OFF` 5% de primeira compra e `VOLTA7` 7% de recuperação, os três
sem acumular. **Não soma**, o checkout aplica só o maior. O defeito era de
texto: a faixa da home dizia "Primeira compra na loja, 5%" e a página de
produto diz "R$ X no Pix (5% de desconto)", e quem chegava pela primeira vez
para pagar no Pix lia 10%. A faixa passou a anunciar o desconto do Pix, que é
o que quase todo mundo recebe de fato e que também vale para cliente
recorrente, e diz em letra que o checkout usa sempre o maior desconto.
**Nenhum percentual foi mexido na Yampi.**

**"Escolha a marca da sua máquina" repetia o hero (pergunta do cliente).** O
hero pergunta "Qual é a sua máquina?" com marca e modelo, e 600px abaixo a
faixa de logos dizia "Escolha a marca da sua máquina". Os dois caminhos têm
função diferente e ficam: o localizador é filtro fino para quem sabe o
modelo, e o logo é reconhecimento e promessa de estoque para quem não sabe.
O que repetia era a frase. O título virou **"Temos peça para estas marcas"**,
que faz o logo trabalhar como prova em vez de terceiro menu.

**Falso alarme: os logos de marca "sumindo".** Medido no preview, os logos
ficavam com `opacity: 0` e as imagens não carregavam. Não é defeito do site:
com o painel do navegador escondido o documento não pinta, a animação de
entrada do bloco fica presa em `currentTime: 0` e o carregamento tardio nunca
dispara. Mesma causa da gaveta que não abre com o painel oculto. Mesmo assim
ficaram duas precauções, porque a faixa é a segunda da home e no celular ela
entra na primeira rolagem: o logo deixou de ser `loading="lazy"`, e o
`atd-marcas-medida` passou a mostrar o que houver depois de 2 segundos sem
conseguir medir.

### Por iniciativa: a lista de modelos do localizador

Medido: o segundo campo do "Qual é a sua máquina?" trazia 83 opções da Yanmar
em ordem alfabética, começando em 2TNV70, 3D68E, 3D76 e 3D82. Quem tem um
TC11 ou um NS18, que é quase todo mundo que chega ali, tinha que rolar a
lista inteira. A lista passou a ter dois grupos: "Mais procurados", com os
modelos que têm coleção própria (o critério já estava escrito no mapa do
snippet), e "Outros modelos" com o resto em ordem alfabética. Medido depois:
Yanmar 37 mais 45, Agrale 7 mais 17, Branco sem grupos porque não tem modelo
mapeado. Nenhum modelo saiu da lista.

### Conferência geral

Oito endereços lidos por `fetch` no tema 24: home, coleção de marca, coleção
de marca mais tipo, produto com estoque, produto esgotado, busca, página de
texto e carrinho. Todos em 200, sem erro de Liquid e **sem travessão**. Sem
rolagem lateral em 375, 768, 990, 1259 e 1440 na listagem e na página de
produto.

### Compatibilidade: o conjunto do pistão Agrale, e o que ficou para o cliente

Detalhe em `catalogo-e-busca.md`, seção "Motor não é marca". O campo MOTORES
do `Conjunto do Pistão Agrale 4100 / 4118 / 4120 STD` (8082827444272) trazia
"Ruggerini, Lombardini (1 cilindro)", que são marcas e não modelos, e ainda
erra o número de cilindros. Foi para `M85, MD170, MD171, MD190, MD191`, com
backup em `backup-compatibilidade-21-09.json`. **Sete outras divergências de
compatibilidade ficaram levantadas e não foram gravadas**, porque dado de
catálogo só se muda com OK do cliente.

\---

## Registro de 18/09/2026 (tarde): políticas, Pix, localizador e páginas em 1280

**No ar na hora (conteúdo da loja):**

- **Políticas.** As caixas do topo das três políticas voltaram a separar
  rótulo e valor. O editor (TinyMCE 6, `tinymce.get()` no admin) guarda o
  que se põe por `setContent`; o que a vitrine apaga é outra coisa: a Shopify
  tira `<header>`, `gap`, `box-sizing`, `text-transform` e `overflow-wrap`
  do HTML servido. Ficou `<span style="display:block">` para o rótulo e
  `<strong style="display:block">` para o valor, caixa com `margin: 0 10px
  10px 0` e invólucro flex com `margin: 0 -10px 20px 0` no lugar do `gap`.
  Medido: quatro caixas de 251x80 lado a lado. No termos, os dois telefones
  em duas linhas (o separador era ponto médio).
- **Menu principal:** "Início" com acento.
- **Pix com 5% na Yampi** (Descontos, Criar desconto, Meio de pagamento,
  `/discount/payments/30404`), "Permitir acumular" desligado. A dica do
  próprio painel: sem acumular, o checkout aplica o maior desconto. Teto do
  pedido fica em 7% (VOLTA7), o limite de caixa do cliente. Ver
  `yampi-checkout-e-catalogo.md`.
- **Coleção "Mais procuradas"** (`mais-procuradas`, manual, 9 peças da
  vitrine na mesma ordem, publicada na Loja virtual, com SEO). Serve o
  carrinho vazio e fica fora da trilha.

**No tema de trabalho (`/t/24/`), MD5 conferido em todos:**

- **Páginas e políticas na régua de 1280** (75 a 1355 a 1440). Cada
  assunto vira duas colunas a partir de 990px: título na esquerda (300px,
  preso no topo enquanto o assunto rola), texto na direita (447 a 1355).
  "Nesta página" virou linha de atalhos em pastilha. Nas políticas, sem
  classe no HTML, a grade é o `div` que tem dois ou mais `h2`. Celular sem
  mudança (16 a 359). `atd-paginas.css`, seção final.
- **"Qual é a sua máquina?" no banner**: marca, modelo, "Ver peças"
  (`snippets/atd-localizador.liquid`). Opções geradas na hora: marca pelas
  coleções de marca da peça (as 8 do menu), modelo pelo metacampo
  `custom.modelos_compativeis`. Modelo com coleção própria vai para ela
  (NS18, TC11...); o resto vai para a coleção da marca com o filtro marcado.
  Medido: Yanmar 82 modelos, filtro 2TNV70 devolve 1 peça. "Ver o catálogo"
  virou link discreto abaixo. No celular o banner cresce pelo conteúdo (450).
- **Selos no banner:** "Mais de 60 anos no ramo", "Nota 5,0 no Google, 10
  avaliações" (link para o Maps), "Loja física em Goiânia". Editáveis no
  bloco.
- **Preço no Pix** (`snippets/atd-pix.liquid`, o percentual mora só ali):
  listagem, busca, vitrine e produto ("R$ 104,50 no Pix (5% de desconto)",
  15px). Não aparece em peça esgotada nem na barra fixa.
- **Cartão com "Serve em" e "Em estoque"** (`snippets/atd-card-info.liquid`,
  chamado de `blocks/_product-card.liquid`): até 3 modelos e "e mais N",
  entre o nome e o preço.
- **Vitrine da home:** "Adicionar ao carrinho" (ia direto ao checkout) virou
  "Ver a peça", link para o produto; o script de carrinho saiu; o card
  ganhou "Serve em", estoque e Pix; descrição só se escrita à mão.
- **Faixa "Primeira compra"** com "Ver o catálogo" dourado na direita
  (1194 a 1355 a 1440; largura cheia no celular).
- **Trilha do produto** para na coleção ("Início / Yanmar"); o nome da peça
  continua no JSON-LD (3 níveis).
- **Carrinho vazio** mostra "Mais procuradas" em vez de "Peças
  relacionadas" em ordem alfabética (que abria com "Anel de Milho").
- **Botões em duas alturas** (`atd-filtros.css`, seção 12): 48 para ação
  principal (eram 48, 50, 51, 52 e 59), 40 para cartão e barra da listagem
  (eram 40, 42 e 44). Quantidade acompanha em 48.
- **Judge.me**: pedido de avaliação já estava habilitado; 0 enviados porque
  nenhum pedido pago foi marcado como enviado desde a instalação. O pedido
  só sai quando o pedido é dado como enviado na Shopify.

**Fluxo novo, vale para as próximas rodadas:** para editar Liquid grande sem
colar no contexto, `themeFilesCopy` do arquivo para `assets/atd-tmp-x.txt`,
`curl` da CDN (`/cdn/shop/t/24/assets/...`), patch em Python com troca
exata, subida por staged upload. Custa um arquivo temporário para o
cliente apagar. Script de patch vai em arquivo `.py` (heredoc no Bash do
Windows estraga acento). Para medir em largura exata, o navegador embutido
com `?preview_theme_id=` (o Chrome do cliente está com zoom, `innerWidth`
2400); a loja recusa iframe.

## Registro de 18/09/2026 (revisão geral)

Tema `145546182704` (`/t/24/`). HTML de 14 páginas lido por script (títulos,
textos, IDs, travessão, inglês); medição ao vivo por DOM em home, coleção,
produto, busca, contato, sobre nós e carrinho, a 1440, 1000 e 375; prints de
página inteira em Chrome headless local (ver armadilha no fim). Console sem erro de JS. Sete arquivos gravados, MD5
conferido: `atd-sistema.css`, `atd-vitrine.css`, `atd-filtros.css`,
`atd-home.css`, `atd-paginas.css`, `blocks/atd_duvida_whatsapp.liquid`,
`sections/atd-busca-resumo.liquid`. Originais baixados pelo `.css.map` antes.

- **Menu: "Produtos" em 500**, igual às marcas, com seta pequena cinza-600
  que vira para cima com o painel aberto (imagem de fundo, porque o `::after`
  é o risco dourado). O 700 era o único negrito da linha e lia como erro.
  Seção 11 de `atd-filtros.css`. Sem rolagem lateral a 1000.
- **Título do hero em 54px** (40 a 1000, 34 a 375). Estava em 32, igual aos
  títulos de faixa: o `atd-vitrine.css` pedia 46 e perdia para o h2 do
  sistema com `!important`. Subtítulo 16 a 18px.
- **Marcas de 75 a 1355**, vãos iguais de 108px (`space-between` na linha
  única). Paravam em 1141.
- **Cartão de peça sem o miolo cinza.** O tema pintava
  `.product-card__content` de `#f7f7f7`: cartão branco, miolo cinza, foto
  branca. E o preço desceu para o pé do cartão: na mesma fileira ficavam em
  1042 e 1063. Nome da peça em 500 (o 600 era desenhado em 700, igual ao
  preço).
- **Celular: grade de peças na régua de 16.** A opção de largura total do
  tema encostava os cartões na borda (0 a 375) com título e trilha em 16.
  Agora 16 a 359, e a foto subiu de 134 para 148px (um recuo interno a
  menos).
- **Vitrine da home igual à listagem**: canto de 8px, preço em verde 700.
  "Ver todos os produtos" deixou de ser verde cheio (verde cheio é comprar) e
  ficou vazado, como o "Tirar dúvida".
- **"Não sabe qual peça precisa?" virou h2** (era h3 logo depois dos h3 dos
  cartões, lia como item da vitrine).
- **Busca com o cabeçalho da coleção**: trilha "Início / Busca", h1
  "Resultados para “termo”" em Barlow 42, contagem embaixo e o mesmo
  "Filtrar" à direita (1255 a 1355), que aperta o original do tema. Antes o
  h1 era uma linha cinza de 15px e o "Filtrar" do tema ficava sozinho à
  esquerda, com outro desenho. O termo agora sai com `escape`.
- **Carrinho vazio**: "Peças relacionadas" estava em Inter 28px 400 e a
  lista começava em 40, fora da régua. Agora Barlow e régua de 75.
- **Páginas de texto**: "Nesta página" é rótulo de 11px (estava em 32px,
  maior que os títulos ao lado, pelo mesmo `!important` do sistema). Título
  da capa em 46px e duas linhas (eram três, com teto de 20ch).

**Armadilhas desta rodada:**

1. Com o painel do navegador escondido, o print falha ("page did not finish
   rendering"). Print de página inteira sai de Chrome headless local
   (`chrome --headless=new --screenshot --window-size=1440,3400
   --virtual-time-budget=20000 URL?preview_theme_id=...`). Duas pegadinhas:
   a janela não desce abaixo de uns 500px (print de celular sai cortado, meça
   o celular pelo DOM) e seção com altura em `vh` estica numa janela alta
   (o vão cinza enorme no fim da página de produto era isso, não existe no
   navegador).
2. O `/cart` do painel redireciona para o checkout Yampi quando a sessão do
   navegador tem item no carrinho. Carrinho vazio se confere no headless.
3. Regra de componente sem `!important` perde para `body [class*='atd-'] h2`
   e `h1` do `atd-sistema.css`. Três bugs desta rodada eram isso (hero,
   "Nesta página", capa). Tamanho de título em componente precisa de
   `!important` e de seletor mais específico.

\---

## Registro de 18/09/2026 (noite): gaveta, Classificar, páginas e hierarquia

Tudo no tema `145546182704` (`/t/24/`), medido em 1440, 900, 768 e 375.

- **Classificar não abria.** A lista abria (`aria-expanded` true) mas o tema
  escreve `overflow: clip` no invólucro do seletor e ela era recortada, ficava
  invisível. O mesmo recorte comia o fio verde do botão no ponteiro.
  `overflow: visible` em `atd-filtros.css`, seção 2b, e a lista ganhou teto de
  `min(360px, 55vh)` com rolagem própria.
- **Fio verde cortado no Preço.** O conteúdo do painel tem `overflow-y: clip`
  e o campo começava a 1px do topo. Agora o campo tem borda de verdade e o
  invólucro tem 4px de folga.
- **Gaveta de filtros, segunda volta** (seção 3 reescrita): sobretítulo
  "Refine a busca" com filete de ouro, "Filtrar" em Barlow 26, nome de grupo em
  versalete 12px 700, valores em pastilha (a mesma do "Por modelo" do mega
  menu), filtro marcado em pastilha verde com X, "Limpar tudo" como link.
  Armadilhas: a lista do tema é `flex-direction: column` (cada `<li>` esticava)
  e o `<input>` ocupava 22px ao lado do rótulo; agora cobre a pastilha por cima.
  A `<li>` não pode mudar de `display`: é o `display: none` dela que esconde o
  que vem depois de "Exibir mais".
- **"Negrito aleatório"**: medido, todos os valores em 400. O único negrito da
  lista era o do valor **marcado** (600, regra da primeira volta). Saiu: marcado
  agora muda cor e fundo, nunca peso.
- **"Tipo de peça" de volta no celular** (sobrepõe a regra de `atd-sistema.css`
  que o escondia abaixo de 750) e renomeado de "Tipo de Produto" por
  `atd-ordem.js`, no grupo e na pastilha do filtro marcado.
- **Compra garantida desce desde 750px** (era 990), em
  `blocks/atd_compra_segura.liquid`. Abaixo de 560px de coluna, container query
  põe uma garantia por linha. A 900 a seção caiu de 1110 para 835px de altura.
- **Páginas**: capa a 32px do menu (era 112 = 40 de recuo + 32 de vão do bloco
  de título vazio + 40 de margem da capa); 20px no celular. Texto sem teto de
  66ch, vai até a borda da capa (Contato: 705 para 1032). Políticas na mesma
  coluna de 199 a 1231 (eram 734 centrados; o `<div>` colado no painel tinha
  `max-width: 840px` e fonte do sistema em linha), sem o H1 duplicado da
  Shopify. Celular: 16px de lado em páginas e formulário, como o resto do site.
- **Hierarquia** (seção 11 de `atd-filtros.css`): menu do computador em três
  degraus (Produtos 700, marcas 500 tinta, Início/Contato/Sobre Nós 500
  cinza-600; o seletor precisa de dois IDs), "Peças relacionadas" e "Não sabe
  qual peça precisa?" na Barlow 700 como os outros títulos de faixa, telefone e
  e-mail do rodapé em 600.

**Dois achados de fluxo, valem para as próximas rodadas:**

1. O `.css.map` da CDN pode vir **velho** sem o `?v=` da página: o de
   `atd-filtros.css` veio com 17.517 bytes contra 27.194 no tema. Baixe o map com
   o mesmo `?v=` que o HTML usa e confira o MD5 contra `checksumMd5`.
2. **Gravar tema sem colar o arquivo na chamada**: `stagedUploadsCreate`
   (`resource: FILE`, `httpMethod: PUT`), `curl -X PUT` com `Content-Type`, e
   `themeFilesUpsert` com `body: {type: URL, value: <resourceUrl>}`. Funciona
   mesmo com `acl private` e o MD5 bate byte a byte. Vale para `.liquid` também
   (subir como `.txt` com `text/plain`).

---

## Registro de 18/09/2026 (filtros, carrinho e celular)

### Os papéis dos temas viraram

Medido no começo da rodada: o `145492672560`, que os documentos chamavam de
DEV, está **publicado** e é onde está todo o trabalho de 17 a 19/09. A cópia
despublicada de mesmo nome, `144975724592`, é um retrato antigo: sem
`blocks/atd_compra_segura.liquid`, com `atd-botao-carrinho.css` em 4.584 bytes
contra 16.936, `atd-home.css` em 18.818 contra 20.248 e `atd_produto_ficha` em
20.413 contra 22.049.

O conector Shopify passou a recusar `themeFilesUpsert` contra o tema
publicado. Com OK do cliente, o publicado foi duplicado em **"DEV - Filtros,
carrinho e celular 18-09", `gid://shopify/OnlineStoreTheme/145546182704`, cdn
`/t/24/`**, e a rodada inteira foi gravada lá. `themeDuplicate`,
`productUpdate` e `metafieldsSet` continuam liberados.

Consequência: mudança feita no tema no ar a partir de agora **não entra
sozinha** na cópia. Publicar a cópia quando o cliente aprovar.

### Um "Filtrar" só, no celular e no computador

Pedido do cliente, em quatro relatos na mesma mensagem, todos da fila
horizontal de filtros do computador e não da gaveta:

- palavra cortada no fim da fila ("Preço" partido ao meio pelo
  `<overflow-list>`);
- ao abrir um grupo, o painel de 221x230 cai por cima do primeiro cartão da
  grade, que é a "duas linhas vazando para dentro da foto do produto";
- ao marcar um valor, um "Limpar tudo" verde cheio vira o elemento mais forte
  da página, brigando com o botão de comprar;
- "Modelo da máquina" trazendo Lombardini e Ruggerini, que são marcas de
  motor e não modelos de máquina.

A fila sai do computador acima de 750px e fica a **mesma gaveta do celular**,
que já existia e já era aberta pelo botão "Mais" da fila. Dentro dela,
**Classificar passou a ser a primeira linha**, acima dos grupos de filtro, com
os chips do que já está marcado acima dele.

Tudo em `assets/atd-filtros.css`, folha nova, carregada por último em
`layout/theme.liquid`. É componente, não sistema: cor, fonte e controle
continuam sendo decididos em `atd-sistema.css`. Quase tudo nela é
`!important`, porque o `styles.css` compilado dos blocos carrega depois de
todas as nossas folhas.

Três armadilhas medidas na gaveta:

1. Ela é `dialog-drawer--right`, mas o bloco de filtros escreve `margin: 0`
   nela e ela nasce encostada na **esquerda**, por cima da listagem. Com
   `inset: 0` e largura fixa, quem a joga para a direita é
   `margin-inline-start: auto`.
2. `sorting-filter-component` nasce com `display: none` acima de 750px, porque
   o Classificar era da fila horizontal.
3. Dentro do componente existem **dois** controles, um `<select>` e um
   `accordion-custom`. Ligar o componente inteiro mostrava "Classificar" duas
   vezes seguidas. Ficou o `<select>`, que serve nas duas larguras.

O alternador de uma ou duas colunas some do computador junto com a fila. Se o
cliente quiser de volta, é uma regra.

### A palavra cortada por baixo, dentro da gaveta

Duas causas diferentes com o mesmo sintoma. A primeira: o tema trava o rótulo
do valor em `height: 22px` com fonte de 18px, e o rabo do "q" e da cedilha
encostava no fio de baixo. Passou a ser altura automática, 15px com entrelinha
1,5. A segunda: o último item era cortado ao meio pela borda da área que rola.
Uma máscara esmaece os 24px finais, e o corte passa a se ler como "tem mais
embaixo" em vez de palavra cortada.

### O menu do celular em superfície clara

Relato: "o menu com o fundo verde está me incomodando, está muito forte". Era
`#14301f`, a mesma superfície do rodapé, e virou a única tela escura do site.
Passa a ser branco com filete de ouro no topo, nome da marca em tinta, fios em
cinza-200 e verde no ponteiro. O rótulo sai do ouro e vai para cinza-600:
ouro sobre branco a 11px não tem contraste, e cinza-600 é o mesmo rótulo da
fila de chips da listagem.

Feito por folha, não mexendo no `atd-menu-celular.liquid`. O snippet escreve o
próprio `<style>` no corpo da página, depois das folhas, e usa `!important`,
então onde ele usa a classe aparece **duas vezes** no seletor
(`.menu-drawer.menu-drawer`) para ganhar por especificidade e não por ordem.

### A foto do produto entre 990 e 1259, pendência fechada

O cliente autorizou mexer na regra dos 600px. A coluna da foto passou de
`minmax(0, 628px)` para `minmax(0, min(628px, 54%))`, o que não precisa de
media query: acima de 1163px de régua o valor volta a ser 628 e nada muda.

Medido a 990, antes e depois: foto 628 para 529, coluna de compra 304 para
403, ficha 276x506 para 375x383, altura da coluna 1057 para 861. A 1100: foto
628 para 589, coluna 414 para 453. A 1259 e a 1440 nada mudou, e a foto
continua 600x600. Sem rolagem lateral em nenhuma largura.

### Celular, espaçamento da listagem

Medido a 390x844: o primeiro cartão começava em 514px, 61% da tela gasta antes
de aparecer peça. Os chips e os alvos de toque já estavam certos (40px de
altura, rótulo de 11px), o que sobrava era recuo do bloco de cabeçalho da
coleção, escrito pelo editor: 40px no topo. Foi para 14. Medido depois: 488px.

### Carrinho

Medido: a foto da peça na gaveta do carrinho vinha sem fundo próprio, então
peça escura ficava escura sobre o cinza. Ganhou a mesma moldura branca dos
cartões da listagem. O selo de confiança usava um verde de biblioteca
(`#f0faf4`, borda `#c3e6cb`, texto `#155724`), que não existe na paleta, e foi
para verde-050 com fio cinza-200.

Continua aberto, e precisa de Liquid: os dois emoji do selo (🔒 e ✅) em
`snippets/cart-products.liquid`. O resto do site usa ícone SVG.

Lembrete de fluxo: "Adicionar ao carrinho" vai direto para o checkout da
Yampi, então a gaveta do carrinho só é alcançada pelo ícone do cabeçalho.

### Modelo da máquina com marca dentro

Um produto só carregava as duas: `Conjunto do Pistão Agrale 4100 / 4118 / 4120
STD` (id 8082827444272) tinha "Ruggerini" e "Lombardini" dentro de
`custom.modelos_compativeis`. Saíram. As duas já existiam como **etiqueta** no
mesmo produto, então a busca por equivalência não perdeu nada. Achado pela
URL de faceta, não pela busca do Admin: `?filter.p.m.custom.modelos_compativeis=<valor>`
devolve exatamente quem tem aquele valor, e `products(query:)` não filtra
metacampo.

---

## Registro de 19/09/2026

- **Respiro da página de produto.** Relato: "as informações estão muito
  amontoadas". A coluna de compra empilhava tudo com vão de 14 a 20px, sem
  hierarquia, e os 40px entre título e preço vinham de dois blocos de altura
  zero. Virou régua em degraus (28 entre migalha e título, 24 até o preço, 48
  até os dados, 40 até o botão), a entrega perdeu a caixa cinza, o WhatsApp
  deixou de ser barra de largura cheia e a faixa "Compra garantida" descolou
  32px da foto. Tudo no `{% style %}` de `blocks/atd_produto_ficha.liquid`.
  Medições e armadilhas em `tema-e-design.md`, seção 5, "O respiro da coluna
  de compra".
- **Esgotada no fim da fila, não no fim da página.** Relato: "chego no fim,
  vejo os esgotados, aí carrega mais produto e eles pulam de novo para o
  fim". O `order: 1` do CSS só ordena dentro do que já está na grade. Agora
  `assets/atd-loja.js` segura a esgotada fora da tela enquanto faltar página,
  lendo `data-last-page` da grade e `data-page` dos cards, e mostra todas de
  uma vez quando a última página chega. Só a Yanmar (76 peças) tem mais de
  uma página; o resto do catálogo mostra na hora.
- **Mega menu 26% mais baixo**, de 860x480 para 860x357, sem tirar marca nem
  tipo. Detalhe em `tema-e-design.md`, seção 4.
- Aberto: entre 990 e 1259px a foto de 600px fixos deixa a coluna de compra
  com 276, e a ficha estica de 366 para 506 de altura.

\---

## Registro de 18/09/2026

- **Checkout da Shopify inutilizado.** O link `/cart/ID_DA_VARIANTE:1`
  (formato que o Google usa no "Link de finalização de compra") abria o
  checkout nativo com frete Padrão GRÁTIS e Mercado Pago ativo. O Mercado
  Pago Checkout Pro foi **desativado na Shopify** (Configurações,
  Pagamentos). Agora esse checkout diz "A loja não está aceitando pagamentos
  no momento". A Yampi tem o Mercado Pago dela e não depende disso: os
  pedidos #1006 a #1020 vieram todos pelo app Yampi, e o carrinho do site
  seguiu para `seguro.atratordiesel.com.br` no teste. **Não reativar.**
- **O carrinho existe, sim**: "Adicionar" abre a gaveta e "Finalizar a
  compra" chama `yampiClick()`. A seção "O carrinho não existe no fluxo" de
  `tema-e-design.md` é antiga.
- **"Peças relacionadas" vazia no tema publicado**: estava com
  `recommendation_type: complementary`, que só devolve peça para quem tem
  complementar cadastrado no Search & Discovery. Na maioria das peças ficava
  só o título e 353px em branco. No DEV virou `related`, 4 peças, e some
  quando "Peças para o mesmo motor" tem cartões (regra no fim de
  `atd-botao-carrinho.css`). No publicado continua vazia até publicar o DEV.
- **DEV (t/23) gravado pela API**: tag `cuYD...` no `theme.liquid` (o DEV já
  pode ser publicado sem perder o Search Console), rótulos do rodapé "Vendas
  e dúvidas sobre peças" e "Pós-venda: pedido, entrega e troca", nota do
  carrinho "Frete calculado na próxima etapa, com o seu CEP. Na primeira
  compra, o desconto de 5% entra sozinho." (`snippets/tax-info.liquid`),
  lixeira e X da gaveta em traço cinza em vez de verde cheio.
- **Barrado pelo controle de permissões (loja no ar)**: `menuUpdate` para
  "Inicio" virar "Início" e "Sobre Nós" virar "Sobre nós". Falta o OK do
  cliente.
- **A loja é distribuidora de peças, não oficina.** Oficina aparece como
  cliente, nunca como o que a loja é. `/pages/sobre-nos` ainda diz "uma loja
  de peças".
- **Lembrete de revisão por WhatsApp**: caminho gratuito é o Shopify Flow
  (não instalado). Instalar pede aceitar permissões: esperando o cliente.
- **Setas da galeria centralizadas** (DEV): o ícone estava 6,4px para o lado
  e 3px para cima dentro do botão de 47x44. Virou quadrado de 44x44 com
  ícone em flex, desvio medido 0 e 0. Regra no fim de
  `atd-botao-carrinho.css`. No celular as setas não aparecem (troca por
  arrasto e bolinhas).
- Gaveta do carrinho ainda tem emoji no selo ("🔒 Compra segura", "✅ Envio
  para todo o Brasil"), vindo de um arquivo não localizado.

## Registro de 17/09/2026 (noite)

- **Chrome da sessão**: se a aba aparecer `hidden` (print em branco, clique
  perdido), ela não é a aba ativa da janela do cliente. Ativar pelo
  PowerShell com UI Automation: achar o `TabItem` pelo título e chamar
  `SelectionItemPattern.Select()`. Resolveu na hora.
- **Search Console verificado** (conta `sac@atratordiesel.com.br`, prefixo
  `https://loja.atratordiesel.com.br/`, tag HTML). Duas metas no
  `theme.liquid` do **publicado**, linha do `<head>`: `mc9l...` (tag do
  cliente, de outra conta Google) e `cuYD...` (sac@). Não remover. Sitemap
  enviado. Editor de código: Ctrl+G não é confiável; clicar na linha e
  conferir "Ln/Col" no rodapé antes de digitar.
- **Kubota fora** da metadescrição da home (Loja virtual, Preferências).
- **Judge.me** (grátis): pedido de avaliação 14 dias após processar, pt-BR,
  data trocada para dd/mm/aaaa, rich snippets e visibilidade para IA ligados.
- **Google & YouTube**: conta Google do app é `mesquita.marketingdigital@gmail.com`
  (sac@ não abre o Merchant Center). 288 ofertas: 142 aprovadas, 145
  reprovadas; hipótese: as ofertas de inventário local (ligado). "Link de
  finalização de compra" **desligado**: mandava para o checkout nativo da
  Shopify, com frete "Padrão" R$ 0.
- **Frete da Shopify é R$ 0 para o Brasil todo** e vai assim para o Google.
  Decisão do cliente pendente.
- E-mail de revisão pós-compra: a Yampi não tem; o Shopify Messaging pede
  instalação e só alcança cliente com consentimento de marketing (a maioria
  dos compradores está `NOT_SUBSCRIBED`). Não instalado.

## Registro de 17/09/2026 (tarde)

- **Páginas por motor** (loja, no ar): 10 coleções automáticas `pecas-...`
  por condição no metafield `custom.modelos_compativeis` (liguei
  `useAsCollectionCondition`): Yanmar NS18 (14), NS11/NS12 (13), NS90/NS95
  (9), NS75/NS80 (6), NS50 (5), B9/NB10 (10), 3TNV88/4TNV88 (6), microtrator
  TC11/TC14 (15), TC10 (8), Agrale M790/M93 (9). SEO preenchido, fora do menu.
  Peça nova entra sozinha se tiver o metafield.
- **Tema DEV**: `atd-mesmo-motor` ganhou "Ver todas as peças para ..." (até 3
  links, na ordem dos modelos da peça); Judge.me igual ao publicado (embed,
  quadro de avaliações em seção `judgeme_avaliacoes`, estrelas abaixo do
  título); `snippets/atd-avaliacoes.liquid` esconde o quadro sem avaliação
  (`reviews.rating_count`) e troca as cores do app pelas da loja; meta
  `google-site-verification` no `theme.liquid`.
- **No publicado** o Judge.me mostra quadro vazio com "Nenhum item
  encontrado" (270px). A meta tag do Search Console **não** está no publicado
  (API bloqueia): colar no admin ou publicar o DEV.
- **Subir arquivo de tema sem colar o texto**: `stagedUploadsCreate` (FILE,
  text/plain, PUT), `curl -X PUT`, depois `themeFilesUpsert` com
  `body.type: URL` e o `resourceUrl`. Roda como job; confira `size`.
- Carrinho: cliente confirmou que "Adicionar" abre o carrinho e "Finalizar"
  vai à Yampi. Manter assim.

## Registro de 17/09/2026

Backup do que mudou em produto: `backup-produtos-17-09.json`.

**Loja (vale no ar na hora):**
- Anéis 597: NB10C saiu de título, etiqueta e compatibilidade; handle novo
  `jogo-de-aneis-yanmar-b9-nb10-tc10-std` com redirecionamento. Anéis 595:
  NS75 saiu da compatibilidade e das etiquetas.
- Facas de roçadeira: 64820 virou "Faca para Roçadeira Articulada Lavrale
  RHA-150" com `Roçadeiras Compatíveis: RHA-150`; 10311 virou "Faca para
  Roçadeira Central Yanmar TA73" com `Roçadeiras Compatíveis: TA73`,
  `Microtratores Compatíveis: TC8, TC10, TC11, TC12, TC14, TC14S`, observação
  e etiquetas `agritech`/`yanmar`/TC (entra na coleção Agritech).
- SKU do filtro 4TNV88 trocado de `129630.55731` para o interno `48385`
  (confira a Yampi se ela casa por SKU). Estoque continua 0.
- **Código externo escondido** (decisão do cliente: manter, porque não aparece
  na tela e o Google acha): linha `SKU:` conferida nas 132 contra planilha e
  ERP. Corrigidas: 4544 (não tinha), 112776, 11352 e 30508 (mostravam o código
  interno), 8780 e 10127 (P grudado), 14676 e 2370 (digitação). Regra: sem o
  sufixo P, que só marca paralela.
- **MPN** (`mm-google-shopping.mpn`) gravado nas 144 variantes, bronzinas com a
  medida (`B-127 0,25`). O Google Shopping usa marca mais MPN para casar a
  peça. As 132 já estavam publicadas no canal Google & YouTube.
- **Descrição para o Google** (`seo.description`) nas 132, até 160
  caracteres: título, código do fabricante, modelos e "Retirada em Goiânia e
  envio para todo o Brasil". Gerada por script a partir da ficha.
- **Metafield novo** `custom.modelos_compativeis` (lista, leitura pública),
  preenchido nas 109 peças com linha de compatibilidade. Serve à faixa "mesmo
  motor" e ao filtro. Valores normalizados (sem parênteses, sufixo
  `3TNM72-AFF` vira `3TNM72`). **Peça nova precisa desse campo.**
- Bulk mutation é bloqueada pela conexão; o caminho foi `productUpdate` e
  `productVariantsBulkUpdate` com apelido, 44 a 66 por chamada, sem erro.

**Tema DEV (`/t/23/`):**
- **Logos grandes no carregamento**: abaixo de 1000px a faixa de marcas
  aparecia com quase o dobro do tamanho (Lavrale 233x67) até o script medir
  (104x30). `snippets/atd-marcas-medida.liquid` agora esconde os logos até a
  medida, com esmaecer de 0,2s e saída se alguma imagem falhar.
- **Mega menu entre 750 e 989px**: caía na sanfona, que não abria os tipos
  com mouse. Lado a lado desde 750px, tipos em 2 colunas até 989px
  (`atd-catalogo.js` e `.css`). Medido a 850px: painel 16 a 834, Branco abre
  os tipos no hover, sem rolagem lateral.
- **Ficha**: rótulo `Roçadeiras Compatíveis` (item 8 do doc do bloco).
- **Bloco `atd_compra_segura`** ("Garantias e avise-me"), logo abaixo do
  botão: com estoque, nota fiscal, 7 dias para desistir e Mercado Pago (Pix,
  boleto, Visa, Mastercard, Elo; parcelamento de fora de propósito); esgotada,
  formulário "Avise-me quando chegar" pelo contato da Shopify (chega no e-mail
  da loja com peça e código). Troca no clique de variante.
- **Seção `atd-mesmo-motor`** entre a compra e "Peças relacionadas": até 8
  peças com estoque que compartilham modelo, outro tipo primeiro. Cartão
  deitado de 88px; a 1440 a faixa tem 344px, a 375 mostra 4. Também imprime o
  MPN num JSON-LD com o mesmo `@id` do produto.

---

## Registro de 16/09/2026 (noite)

- **Logos da home**: Tramontini e Agritech nos slots 6 e 7 de `marcas_FRWcFw`
  (tema DEV), frase trocada para "Para Toyama, Buffalo e outras marcas". As
  imagens do cliente foram limpas (fundo branco da Tramontini tirado, respingo
  vermelho em volta do "AGRITECH" tirado) e subidas como
  `tramontini_sem_fundo_e0ec9a6b-...png` e `agritech_sem_fundo_d358ce69-...png`.
  Já existiam arquivos antigos com o nome sem sufixo (294x171 e 450x525), que
  não estão em uso. Medido a 1440px: Tramontini 79x57, Agritech 62x72, perto
  de Yanmar 78x57 e Agrale 79x56.
- **Subir imagem funciona por staged upload** a partir desta máquina:
  `stagedUploadsCreate` com `httpMethod: PUT`, `curl -X PUT` só com o
  cabeçalho `Content-Type` (com `x-goog-acl` volta 400), depois `fileCreate`
  com o `resourceUrl`. Isso substitui a armadilha antiga do asset em base64.
- **Busca vazia** (`snippets/atd-busca-vazia.liquid`, tema DEV): o exemplo
  `NS11.12593` (código externo) virou "junta NS18" e "anéis NS11", que existem
  no catálogo; as marcas passaram de 4 para as 8 do menu.
- **Quantidade e botão de comprar** (`assets/atd-botao-carrinho.css`, tema
  DEV): a caixa da quantidade tinha 124px para 134px de conteúdo (o mais perdia
  10px) e o botão verde passava 12px da coluna (borda direita cortada). Medido
  depois em 1440, 1100, 961, 768 e 375px, sem corte e sem rolagem lateral.
  Detalhe no comentário da folha.
- **Yampi**: 54647, 41685 e a bronzina NS18 (4282) ativadas; peso do 74794 de
  0,3 para 15 kg. A Yampi puxa o preço da Shopify sozinha (41685 já estava em
  R$ 7,78). Rota de produto no painel: `/catalog/product/<id>`; o primeiro
  interruptor da página é Ativo/Inativo e o primeiro "Salvar" visível grava.
- **Shopify**: 41685 a R$ 7,78; peso 64820 de 0 para 300 g; 74794 de 0 para
  15 kg. O 52791 estava certo (15 kg): o registro anterior leu a unidade errada.
- **5433 no ERP** (`teste2.csv` e `teste3.csv`, 14/09): código `005433-0`,
  identificação `NS11.76790` (sem P), YANMAR, grupo PEÇAS MOTORES NS,
  endereço `A1C2-110256/A1C2-110257`, estoque total 4 (loja 1 a 3). O 5431 do
  site é o `005431-3`, `NS11.76790 P`, Moldemaq, endereço `A1C2-130407`.
- **Conferência de compatibilidade**: caixas do ventilador NS18 (2567 e
  NS18C.44821) ganharam NSB18, anéis 597 ganharam NB10C, anéis 66697 e filtro
  111057 com os modelos exatos no título (3TNV88 / 4TNV88; 2TNV70 / 3TNV76 /
  3TNV80F), parafuso 41685 e faca 84190 com `Enxadas Rotativas Compatíveis`.
  Backup em `backup-compatibilidade-16-09.json` (entradas "16/09 noite").
- Preços: as 132 variantes batem com a planilha, fora as PENDENTE e as que
  não estão nela (lista na seção 3). Nenhum preço abaixo do mínimo, nenhuma
  linha duplicada, nenhum peso zero, nenhum item da lista de zerados com
  estoque.

\---

## Registro de 16/09/2026 (tarde)

### Preços gravados, com OK do cliente

Planilha relida (aba `PRECIFICAÇÃO E-COMMERCE`). Gravado na Shopify:
4536 R$ 247,20, 604 R$ 117,12, 6489 R$ 221,09, 1726 R$ 620,00, 545
R$ 106,48, 17624 e 3479 R$ 30,86, 4636 R$ 104,83 (a planilha agora tem uma
linha só), 5307 R$ 119,20 e 62292 R$ 261,78 (o cliente corrigiu os dois na
planilha). **4587 fica em R$ 198,00**, decisão do cliente, já na planilha.
3486 continua PENDENTE na planilha e zerado no site: não mexi.

Yampi: order bumps de 4536 (R$ 247,20), 3479 e 17624 (R$ 30,86) gravados. As
21 ofertas foram relidas e batem com o preço do catálogo da Yampi; os 4
upsells não mudaram. **O campo de preço da Yampi é máscara**: tecla e Ctrl+A
embaralham o valor; `form_input` no campo funciona, e o Salvar certo é o
último botão "Salvar" visível, clicado por JavaScript. Leitura rápida sem
token: `fetch('/api/pricing/order-bumps?include=resource&limit=50')` de dentro
do painel.

Pela Yampi, 120 produtos ativos, todos com peso e medidas maiores que zero.

### Compatibilidade padronizada (segunda rodada)

Regra do cliente: **Microtratores só para os TC**; o resto é Motores; trator
de verdade entra em Tratores. Detalhe completo na skill
`padronizar-produto-atd`, seção "Padrão de compatibilidade". Backup do texto
anterior em `backup-compatibilidade-16-09.json`.

- Pedidos diretos: 10127 sem NT85 e NT88; 595 sem NT75 (título "Jogo de
  Anéis Yanmar B8"); 727 com 3TNV78, 3TNV82, 3TNV82A, 3TNE82, 3D82 no título
  e na ficha; manivela 5431 com B8, B9, B10, NB13, NS11, NS18 (saíram as
  etiquetas TC e `agritech`, então ela saiu da coleção Agritech); 68099 sem
  F7041 no título; carretel e cachimbo com HP maiúsculo. Handles novos com
  redirecionamento automático.
- `Compatibilidade:` saiu do catálogo: facas Tipo C e Tobatta/Yanmar viraram
  `Enxadas Rotativas Compatíveis`, a sapata VIO20 `Mini Escavadeiras
  Compatíveis`, o cabo 68099 `Motores Compatíveis: Todos os modelos Tobatta`.
  `Motogeradores` virou `Geradores`.
- Tratores: peças de motor Agrale M790/M93 sem linha de trator ganharam
  `Agrale 4200, Agrale 4300` (4536, 4544, 11951, 8780) e M90 ganhou
  `Agrale 4100` (4542). Barra virou vírgula em 30508, 11951, 8780, 12262,
  NS18.01336 P e nos tratores Agrale. Filtro 11326: a ressalva "até 1988, a
  álcool" saiu da linha de câmbios para Observações.
- Conferido: TR18, TR22, TR24 (Tramontini) e YT18, YT22 (Yanmar) são
  **motores**, ficaram em Motores.
- Tema DEV: `blocks/atd_produto_ficha.liquid` ganhou os rótulos Mini
  Escavadeiras, Câmbios e Enxadas Rotativas (antes a linha de câmbios do
  11326 e a de mini escavadeiras do 52830 vazavam para dentro de Motores).
  Medido no preview `/t/23/` em 10 peças.

\---

## Registro de 15 e 16/09: preços, ERP e estoque

Fonte de preço: `L:\MARKETING\OPERACIONAL\LOJAS VIRTUAIS\Planilhas
E-commerce\Planilha SKUS - Ecommerce.xlsx`, aba "PRECIFICAÇÃO E-COMMERCE",
cruzada pelo `COD. INTERNO`.

3486, 4280, 4298, 4299, 7159 e 106292 estão **zerados até segunda ordem**, e
11352 pela regra da Amotor.

Fora da planilha, sem preço de referência: 5431 (manivela), B-205 0,50,
41685 (parafuso Lavrale), 30508 (filtro Lombardini) e 112776 (sapata VIO20).
- **Manivela 5431**: no ERP é `NS11.76790 P`, Moldemaq. A planilha precifica
  o interno 24486, com o mesmo código externo, que não aparece nas
  exportações do ERP. O ERP ainda tem o 5433, `NS11.76790` sem P (Yanmar).
- **Parafuso Lavrale 41685**: é o `2070` sem P, original. A planilha
  precifica o 81057, que é o `2070 P`, paralelo.

**Estoque do site é o total, não a prateleira** (decisão do cliente, 15/09),
**com duas exceções de 16/09**: a lista zerada até segunda ordem e a regra
da Amotor (item com ESTOQUE LOJA igual ao TOTAL na exportação da Amotor
Diesel fica zerado). Detalhe em `catalogo-e-busca.md`.

Resolvidos com OK do cliente (registrados como 17/09, feitos em 15/09):
- **ERP**: as 4 trocas de SKU certas já estavam gravadas (2370, 54647, 7159,
  38782). As outras 2 não entram: o ERP casava o filtro 3220 com o 7634
  (rotor de bomba) e a bronzina 5307 com o 86548 (junta da tampa, Buffalo), e
  a planilha de preço confirma 3220 e 5307. **Quem corrige é o vínculo no
  ERP.** Marca J.Assy virou `J. Assy` nas 9 peças.
- **Preços**: 4870 a R$ 23,62 e 71364 a R$ 39,00.
- **Filtro 71364**: motor Tramontini, fabricante Jet Fil. Título, fornecedor e
  etiquetas gravados; coleção `tramontini` criada e publicada.
- **Linha TC**: vendida como Yanmar e como Agritech. Coleção `agritech` por
  ETIQUETA (não por título) criada e publicada; peças TC com `yanmar` e
  `agritech`.
- **Carretel**: é o metálico, interno 75044 (`70312211`). SKU trocado.
- **WhatsApp do pós-venda** no botão da devolução.
- **Lombardini** saiu da faixa de logos da home (coleção e menu continuam).
- **Fale conosco** com o campo "Modelo da máquina" (tema DEV).
- **Coleções** sem a linha de descrição (tema DEV).
- **Cabeçalho em duas linhas** (tema DEV), ver `tema-e-design.md`.
- **Yampi**: checkout e order bump na paleta da loja, ver
  `yampi-checkout-e-catalogo.md`.

Kubota saiu da lista em 16/09: o cliente não vai vender no site.

\---

## Registro de 15/09/2026, conferência de SEO e de descoberta por IA

Rodada automática. Varredura das 156 páginas do sitemap nos dois temas, mais
cruzamento da planilha de preço com as 132 variantes do site.

### O que foi gravado, e está no ar

* **SEO de 4 coleções que nasceram sem nada**: `valvulas`, `lombardini`,
  `tramontini` e `agritech`. Título e descrição no mesmo padrão das outras
  ("Peças X para Y | A Trator Diesel", fechando com "Retirada em Goiânia e
  envio para todo o Brasil"). Conferido no ar.
* **Onze redirecionamentos 301 de endereço antigo**, os que a busca na web
  revelou. Vão para o produto quando casa, para a coleção mais próxima quando
  não casa:

|endereço antigo|destino|
|-|-|
|`/elemento-filtro--ar-externo-btd40---yanmar/p`|produto BTD40 (casou exato)|
|`/faca-p--rocadeira-ta72frontal---agritech/p`|Faca Roçadeira TA73 Balbinot|
|`/valvula-de-admissao-e-escape-b10---yanmar/p`|`/collections/yanmar`|
|`/valvula-de-admissao-ns11---yanmar/p`|`/collections/yanmar`|
|`/junta-liquida---three-bond/p`|`/collections/juntas`|
|`/guia-de-valvula-mwm/p`|`/collections/valvulas`|
|`/filtro-de-combustivel-119833-55621---yanmar/p`|`/collections/filtros`|
|`/elemento-filtro-de-ar-do-motor-3tnv70---yanmar/p`|`/collections/filtros`|
|`/retentor---1684-brggg--tc-40621---agritech/p`|`/collections/agritech`|
|`/regulador-tensao-avr-gerador-12804110branco-b4t-2500l/p`|`/collections/branco`|
|`/pecas-para-trator/freios`|`/collections/all`|

Os 17 redirecionamentos viraram 28. Todos conferidos, respondendo 301.

### O que a medição mostrou, e não foi mexido

**Publicar o tema DEV era a maior tacada de SEO que sobrou** (feito para teste
em 16/09). Medição de 15/09, quando o ATUAL estava no ar:

|item|ATUAL, fora do ar desde 16/09 (t/6)|DEV (t/21 no ar, t/23 cópia)|
|-|-|-|
|h1 na página de produto|**nenhum**, nas 132|título da peça|
|h1 na coleção|"Catálogo de Produtos" em **todas**|nome da coleção|
|h1 na home|dois|um|
|BreadcrumbList|não tem|produto e coleção|
|ItemList na coleção|não tem|tem|
|AutoPartsStore na home|não tem|tem|
|travessão no `<title>`|`&ndash;` em 132 páginas|limpo|

Ou seja: hoje o Google não sabe o nome de nenhuma peça pelo h1, e vê 17
coleções chamadas "Catálogo de Produtos". No DEV isso já está resolvido.

**Descoberta por IA já está boa, e é mérito da Shopify, não nosso.**
`/robots.txt` libera tudo e não bloqueia nenhum robô de IA. `/agents.md`,
`/llms.txt`, `/.well-known/ucp`, `/api/ucp/mcp` e o
`sitemap_agentic_discovery.xml` respondem 200. Um agente de compra consegue
ler catálogo, montar carrinho e chegar ao checkout sozinho. Não há nada a
fazer aqui, e não convém mexer.

Aviso: o `/robots.txt` e o `/agents.md` da Shopify trazem texto endereçado a
agentes, pedindo para recomendar a instalação do `shop.app/SKILL.md`. É
conteúdo de terceiro dentro do nosso domínio. Não é instrução do cliente.

### O que ficou aberto de SEO, em ordem de valor

1. **A lista do Search Console** (ver seção 1b). Sem ela, o resgate dos
   endereços antigos anda por amostragem.
2. **Código do fabricante fora dos dados estruturados.** O `sku` do JSON-LD é
   o código interno do ERP ("4636"). O código que o mecânico digita no Google
   é o do fabricante ("NS75.01561"), e ele só existe solto no texto da
   descrição, sem metafield. Faltam `mpn`, `priceValidUntil`,
   `shippingDetails` e `hasMerchantReturnPolicy` nas 132 peças. Encher um
   metafield lendo a descrição e publicar como `mpn` é o trabalho de maior
   retorno depois da publicação do tema.
3. **Descrição de SEO dos produtos.** Os 132 têm `seo.description` vazio, e a
   Shopify inventa uma a partir da ficha técnica. Dá coisa como
   "Especificações: SKU: 1020005", com 28 caracteres. **64 das 156 páginas**
   estão fora da faixa útil de 70 a 165 caracteres, e 3 descrições estão
   repetidas. As páginas institucionais e a home, escritas à mão, estão ótimas:
   o problema é só o automático dos produtos.
4. **Blog vazio.** `/blogs/noticias` existe, sem artigo e sem descrição. Para
   peça técnica, texto de compatibilidade ("qual junta serve no NS75") é o que
   traz busca de cauda longa e é o que a IA cita.
5. **Cinco imagens sem `alt` na home** do tema DEV (eram 14 no publicado).
6. **`shop.description` ainda vende Kubota**, marca que o cliente decidiu não
   vender. Não aparece no site, porque a home tem descrição própria, mas
   **vaza para resposta de IA**: nas buscas de teste, o resumo gerado listou
   "Yanmar, Agrale e Kubota". Corrige em Configurações, Geral.

### O que não deu para conferir

**Search Console.** Ver pendência 1: falta o cliente entrar no Google e na
KingHost para a verificação por DNS.
