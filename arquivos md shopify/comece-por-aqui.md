# Comece por aqui (atualizado 24/09/2026)

> Datas: registros antigos marcados 16/09 e 17/09 foram feitos em 15/09/2026,
> pela data do sistema. A partir da rodada de 16/09 à tarde, a data é a real.

Documento de passagem. Sessão nova lê este primeiro.
**A lista de pendências deste documento é a única que vale.**

**Mudou em 24/09: o tema de trabalho foi publicado. Hoje não existe tema de
trabalho.** Conferido com `themes(first: 10)` em 24/09/2026.

- No ar: **DEV (mais recente)** (`gid://shopify/OnlineStoreTheme/166080315440`,
  cdn `/t/25/`). É a "Cópia de DEV - Filtros, carrinho e celular 18-09" de
  23/09, renomeada e publicada pelo cliente. A API bloqueia escrita nele.
- `145546182704` ("DEV - Filtros, carrinho e celular 18-09", `/t/24/`) e
  `145492672560` ("DEV - Ajustes visuais 27-08", `/t/23/`) estão
  despublicados e **defasados**: não têm o que foi feito no `/t/25/`. Não
  grave neles.
- **O próximo ajuste de tema começa por uma cópia nova do `166080315440`**,
  feita no admin (Loja virtual, Temas, Duplicar). Anote aqui o id e o cdn
  da cópia antes de gravar.
- Antes de gravar, confira sempre `themes(first: 10) { id name role }`.

O que muda no tema de trabalho **não** aparece no ar até o cliente publicar
de novo.

**Atenção ao que é tema e ao que é loja no ar.** Página de `/pages/`,
política de `/policies/`, produto, coleção e configuração da Yampi são
conteúdo da loja: mexeu, mudou no ar na hora, mesmo com o tema DEV
despublicado. Só arquivo de tema fica represado até a publicação.

**Use a skill `poupar-tokens-print-shopify` sempre que trabalhar aqui.**

**Padrão de produto, campo por campo**: `catalogo-e-busca.md`, seção 2.
Vale mesmo sem a skill `padronizar-produto-atd`, que não abre na nuvem.

\---

## Os documentos

|documento|quando abrir|
|-|-|
|`comece-por-aqui.md`|sempre, primeiro|
|`tema-e-design.md`|paleta, tipografia, régua, home, cabeçalho, mega menu, celular, página de produto, SEO, diferenças entre DEV e publicado|
|`catalogo-e-busca.md`|**padrão de produto campo por campo (seção 2)**, título, ficha, etiqueta, coleção, mega menu por marca e tipo, busca da Shopify, ERP Ensis|
|`yampi-checkout-e-catalogo.md`|cupom, order bump, upsell, carrinho abandonado, pagamento, frete, dados da Yampi|
|`paginas-institucionais.md`|políticas, fale conosco, faixa de fatos, acertos de interface do produto, faixa do vídeo|
|`registros.md`|o diário, dia a dia. Só quando a pergunta for "por que isso ficou assim"|
|`instrucoes-do-projeto.md`|o texto para colar no campo de instruções do projeto|

\---

## Como gastar menos tokens

1. Leia só este arquivo primeiro.
2. Busca no projeto antes de abrir documento inteiro.
3. Carregue todas as ferramentas numa chamada só.
4. Navegador só quando precisar olhar a loja ao vivo.
5. Para ler muitos registros de um painel, `browser\_batch` com pares de
`navigate` mais `javascript\_tool`.
6. Folha nossa de CSS só se edita por inteiro. Junte as mudanças.
7. Bloco novo carrega o próprio CSS num `{% style %}`, mais barato que
reescrever uma folha de 26KB.
8. Para varrer o site atrás de um texto, um `fetch` em série dentro de um
`javascript\_tool` só, com `?preview\_theme\_id=`. Treze páginas numa
chamada, sem print nenhum. Acima de umas 20 páginas o script estoura os
45s: divida em duas chamadas.
9. `/products.json?limit=250` devolve o catálogo publicado inteiro e dá
para auditar tudo dentro do navegador, sem trazer nada para o contexto.

\---

## Como o site está montado

Arquivos próprios do tema começam com `atd-`, e carregam nesta ordem:
`atd-custom.css` (variáveis), `atd-catalogo.css` (paleta e mega menu),
`atd-vitrine.css` (sistema da home), `atd-home.css` (listagem e página de
produto), `atd-paginas.css` (páginas institucionais) e `atd-regua.css`, que é
o último e tem a palavra final sobre largura das faixas da home, zoom da loja
e tamanho da logo.

JS próprio: `atd-catalogo.js` (mega menu), `atd-loja.js` (peça esgotada).

Blocos próprios: `atd\_produto\_ficha` (marca, código, motores, estoque,
entrega, WhatsApp), `atd\_breadcrumb`, `atd\_atalhos`, `ai\_gen\_block\_8f4d739`
(tarja do topo, 4 mensagens), `atd\_primeira\_compra` (faixa do desconto de
primeira compra) e `atd\_placa` (placa de identificação, faixa de confiança da
home).

Trechos próprios: `atd-404-resgate.liquid` (no `head`),
`atd-menu-produtos.liquid` (mega menu), `atd-busca-vazia.liquid`,
`sections/atd-busca-resumo.liquid`.

Paleta: verde `--atd-verde-700 #1e5b39` para botão e preço,
`--atd-verde-900 #14301f` para hover, tinta `#14181a` para título, cinza
`#6b7570`, ouro `#c08a2e` como acento único.

Régua: `--atd-recuo: max(24px, calc((100% - 1280px) / 2))`. Toda faixa da
home usa ela, da tarja de benefícios ao rodapé.

\---

## Armadilhas já medidas, não repita

* O tema só carrega Inter 400, 500, 700 e 800. Peso 600 vira 700 na tela.
* `--page-zoom` está com `!important` em `base.css`. Sobrescrever exige
`!important` também.
* O tema redesenha a seção do cabeçalho depois do `DOMContentLoaded`. JS que
depende dele precisa religar os ouvintes.
* Uma folha de estilo do Yampi, de outro domínio, ganha de seletor comum.
Onde for preciso, use `html body #header-group` com `!important`.
* **Botão que parece branco**: o botão está verde, quem pinta de branco é o
filho, `span.add-to-cart-text`, que herda `background-color #f7f7f7`.
Corrija no filho.
* O tema também pinta `linear-gradient(#f7f7f7, #f7f7f7)` por cima do fundo
de alguns botões. Trocar `background-color` não resolve, é preciso apagar a
`background-image`.
* `min-width 100%` do tema ganha de `max-width`. Para encolher a coluna da
foto, `min-width 0` mais largura explícita.
* A barra fixa de compra usa `transform` para centralizar e para animar.
Esconda por `opacity`, nunca por `transform`.
* A caixa de texto do bloco de vídeo também é absoluta e centrada por
`transform`. Ao esticá-la, tire o `translateX` e deixe só o `translateY`.
* Seletor por pedaço de classe pega vizinhos: `\[class\*='ai-brands-image-']`
casa também com `ai-brands-image-wrapper-`. Escreva `img` na frente quando
a regra for só da imagem.
* Blocos do editor imprimem o `style` no corpo da página, depois das folhas
do head. Por isso os seletores começam em `body`. E a regra do bloco pode
ter dois níveis de classe, que ganha de um nível só.
* O tema envolve cada bloco num `.shopify-block` que é item de um flex column
com `align-items center`, então ele encolhe até a largura do conteúdo.
Faixa que precisa ir de borda a borda pede
`body .shopify-block:has(> .minha-classe) { width: 100% }`.
* `themeFilesDelete`, escrita no tema publicado e `publishableUnpublish` são
bloqueados. Despublicar canal é no admin.
* `shopPolicyUpdate` exige `write\_legal\_policies`, que a conexão não tem. O
jeito que funciona é editar pelo iframe do admin.
* A busca nativa da Shopify ignora AND, OR e NOT. Só frase exata entre aspas
funciona, e sem casamento exato ela cai na busca aproximada, onde
`agritech` casa com `agrale`.
* Sinônimo de busca está suspenso pela Shopify. Apelido só funciona como
etiqueta.
* O mega menu lê `collection.all\_types`, com `all\_tags` de reserva. A URL
continua por etiqueta, então todo tipo precisa de uma etiqueta escrita
igual.
* No Search \& Discovery, "Produtos sem estoque" precisa ficar em **No final**.
* App do Search \& Discovery e editor de checkout rodam em quadro isolado de
outro domínio: só captura de tela e clique por coordenada, com
`preset desktop`.
* O painel da Yampi nega rotas de configuração com "Acesso restrito" quando a
janela é estreita. Redimensione para 1440x900 antes de abrir qualquer rota
de configuração. Os campos dele são Element UI, então
`querySelectorAll('select')` volta vazio: leia `input.el-input\_\_inner` e
clique por JavaScript, nunca por coordenada.
* `checkoutBranding` exige plano Plus. Contas de cliente novas são hospedadas
pela Shopify e não aceitam tema.
* `collection(handle: ...)` não existe na API, consulte por `id`.
* **Subir imagem para a loja**: desde 16/09 o staged upload funciona por
`curl` (ver registro de 16/09 noite). Registro antigo: a rede da sessão não
alcançava o `shopify-staged-uploads`. Suba como asset do tema por `themeFilesUpsert` em
base64 e depois chame `fileCreate` com a URL do asset em `originalSource`.
* **`curl` alcança `loja.atratordiesel.com.br` sim** (medido 15/09/2026, o
registro anterior dizia o contrário). Isso muda o jeito de auditar: dá para
varrer o site inteiro por script, sem navegador e sem print. O caminho que
funcionou foi Python com `urllib` em `ThreadPoolExecutor`, 156 páginas do
sitemap em uma chamada de Bash, e a análise toda em disco.
* **Para ler o tema DEV por `curl` não basta `?preview_theme_id=`.** A Shopify
responde com cookie e redirecionamento. Sem `-L -c -b` (ou `HTTPCookieProcessor`
no Python) você lê o tema publicado achando que leu o DEV. Confira sempre pelo
`/cdn/shop/t/<n>/`: desde 16/09, `23` é o DEV e `21` é o publicado.
* **`snippets/atd-404-resgate.liquid` salva a pessoa, não a posição.** Ele é
JavaScript rodando numa página que responde **HTTP 404**. Quem tem JS é levado
para a busca, e isso é ótimo. Mas o Google lê o 404, tira a URL do índice e a
autoridade do link se perde, e robô de IA que não roda JS não vê nada. Só
redirecionamento 301 no servidor preserva ranking. O resgate é rede de
segurança, nunca substituto do `urlRedirectCreate`.
* **Coleção nova nasce sem título e sem descrição de SEO.** `collectionUpdate`
com o campo `seo` resolve, e vale no ar na hora, mesmo com o tema DEV
despublicado.

\---

## As seis coisas que mais mudam o resultado

**1. A loja estava encolhida em 15%.** `base.css` trazia
`--page-zoom: 0.85 !important`. Corrigido em `assets/atd-regua.css`.

**2. Apelido de busca é etiqueta, não sinônimo.** A Shopify suspendeu
sinônimos. Precisa de mais apelidos? Grave como etiqueta.

**3. O mega menu lê `collection.all\_types`.** A URL continua por etiqueta, e
só funciona porque **toda peça tem uma etiqueta escrita igual ao seu tipo**.
Mexeu no tipo? Acerte a etiqueta junto.

**4. Endereço antigo não dá mais 404.** Seis redirecionamentos mais
`snippets/atd-404-resgate.liquid`. Falta a lista completa do Search Console.

**5. Peça esgotada aparece na busca**, em No final, com "Consulte
disponibilidade" no lugar do preço. **Por isso peça com estoque zero fica
ACTIVE, não arquivada**: arquivar tira do menu e cria prateleira vazia.

**6. Logo de marca é promessa de estoque.** Yanmar, Tobatta, Branco, Agrale,
Lavrale e Lombardini, todas com coleção própria.

A ordem das oito faixas da home está em `tema-e-design.md`.

\---

## Os dois telefones

* **(62) 3086-7211**, atendimento especializado: achar a peça certa,
compatibilidade, estoque, venda.
* **(62) 9839-8287**, e-commerce: como o site funciona, pedido, entrega,
troca, devolução, reembolso, dados pessoais.

Os dois estão publicados **sem o nono dígito**, exatamente como o cliente
escreveu. Conferido em 9 páginas: home do tema DEV, 4 páginas e 4 políticas.

Onde cada um está:

|3086-7211|9839-8287|
|-|-|
|ficha do produto, botão de dúvida|Política de troca e devolução, no site e em `/policies/refund-policy`|
|home, bloco de marcas e "Não sabe qual peça"|Central de ajuda, entrega, pedido e defeito|
|resgate da 404 e botão flutuante|Política de privacidade, no site e em `/policies/privacy-policy`|
|Contato, primeiro cartão|Contato, segundo cartão e acompanhar pedido|
|Central de ajuda, achar a peça e orçamento|Termos de serviço, cláusula de disputa|
|dados estruturados de vendas|checkout Yampi, cadastro da loja|
|e-mails de carrinho abandonado|rodapé e placa da home, segunda linha|

**Os links `wa.me` do site apontam para `556230867211`, menos um**: o botão
"Falar no WhatsApp" de `/pages/politica-de-devolucao` foi para `556298398287`
em 17/09, com OK do cliente. A política em `/policies/refund-policy` não tem
botão, só o número escrito.

\---

## O que ficou aberto, em ordem de valor

### 1. Search Console: verificar o domínio pelo DNS (16/09)

**A pendência mais cara da loja.** Sem ela não sai a lista de endereços
antigos (seção 2), e cada um é cliente batendo numa parede.

- O DNS de `atratordiesel.com.br` é da **KingHost** (`dns1` a
  `dns6.kinghost.com.br`). `loja.` é CNAME para `shops.myshopify.com`. O TXT
  da raiz hoje só tem o SPF.
- O cliente autorizou verificar pelo DNS. Em 16/09 as duas sessões estavam
  caídas no navegador da sessão: o Google pedia "Confirme que é você"
  (conta `televendas@atratordiesel.com.br`) e a KingHost estava na tela de
  login. **Senha não se digita**: o cliente entra nas duas abas.
- Com as duas logadas, o caminho: Search Console, Adicionar propriedade,
  **Domínio** `atratordiesel.com.br`, copiar o `google-site-verification=...`,
  KingHost, Domínios, `atratordiesel.com.br`, Editar DNS, novo registro TXT
  no host raiz (vazio ou `@`) com esse valor, **sem apagar o SPF**. Voltar ao
  Search Console e clicar Verificar (se falhar, tentar de novo em 1h).
  Conferir antes com `Resolve-DnsName atratordiesel.com.br -Type TXT`.
- Meta tag no tema não serve: o tema no ar é bloqueado para escrita pela API.

### 2. Lista de endereços antigos do Search Console

O Google ainda ranqueia a loja da plataforma anterior, no mesmo domínio, no
formato `/nome-da-peca/p`. Medido em 15/09/2026: continuam indexados e
**todos davam 404**. São centenas. Onze já foram resgatados (registro de
15/09 no fim deste documento). **O resto só sai do Search Console**, em
Indexação, Páginas, "Não encontrada (404)", botão Exportar.

Com a lista na mão, o caminho é `urlRedirectCreate`, em lote, por alias numa
mutation só. Casou com peça do catálogo, aponta para o produto; não casou,
aponta para a coleção mais próxima (marca ou tipo), nunca para a home.

**Cuidado com o CDN**: endereço que já respondeu 404 continua devolvendo 404
por alguns minutos depois do redirecionamento criado. Confira com
`?cb=$RANDOM` no fim da URL.

### 3. Esperando o cliente

- **Search Console** (seção 1): o cliente pediu em 16/09 para deixar por
  último.
- **Preço das peças fora da planilha**: B-205 0,50, B-204 1,00 e B-208 1,00
  (variantes de bronzina), NS18C.44821, TC14.62100, 10H1, 5431 e NS18.01336 P.
  Resolvidos em 17/09: 112776 fica em R$ 110 (já na planilha); 48385
  (129630.55731) e 3486 estão zerados e **continuam zerados**, sem aviso. O
  30508 saiu dessa lista em 24/09: o cliente disse que o estoque dele está
  certo.
- **Filtro "Modelo da máquina" nas coleções**: o dado está pronto
  (metafield `custom.modelos_compativeis` nas 109 peças com compatibilidade).
  Falta o cliente ligar no app Search & Discovery (o admin pede login no
  navegador da sessão). Registro de 17/09.
- **Carrinho**: com `skipToCheckout=1` cada "Adicionar" vai direto ao
  checkout, o que anula a faixa "Peças para o mesmo motor". Sugestão
  levada ao cliente em 17/09; decisão dele.
- Peças de plantadeira, balança e rolamento seguem sem linha de
  compatibilidade.

### 4. Entidade comercial, três campos na mão (o cliente faz no final)

`gid://shopify/BusinessEntity/29868687408`. Não existe mutation de entidade
comercial na Admin API, então é o cliente quem preenche em Configurações,
Geral, Informações da empresa, botão "Alterar entidade comercial" (é um web
component e não responde a clique sintético).

|campo|valor hoje|o que entra|
|-|-|-|
|`companyName`|vazio|VL COMÉRCIO DE MOTORES E PEÇAS LTDA|
|`address.address1`|vazio|Av. Bandeirantes, 948|
|`address.address2`|vazio|Qd.39 Lt.07, Vila Regina|
|cidade, estado, CEP, país|preenchidos|nada|

**Não bloqueia venda**: o pagamento é pela Yampi e pelo Mercado Pago. Dados de
sócios não são necessários (a seção Pessoas é do Shopify Payments).

### 5. Publicar o tema de trabalho (o cliente publica quando tudo acabar)

Em 22/09 o cliente publicou o `145546182704` (cdn `/t/24/`). Em 23/09 ele
o duplicou como `166080315440` (cdn `/t/25/`), que é o de trabalho e o
próximo a publicar. O que for feito lá só vai ao ar quando ele for publicado. Cuidado: mudança feita
direto no tema no ar **não entra sozinha** na cópia.

### 6. ~~Dois emoji no selo do carrinho~~ (fechado em 18/09, cadeado e caminhão em traço)

`snippets/cart-products.liquid` imprime `🔒 Compra segura` e `✅ Envio para
todo o Brasil` dentro de `.cart__trust-badge`. O resto do site usa ícone SVG,
e emoji não dá para trocar por folha de estilo. O selo já está na paleta
certa; falta só o desenho.

### 7. ~~Travessão no rótulo do Classificar~~ (fechado em 18/09 por `assets/atd-ordem.js`, vira "de A a Z")

Parcelamento no preço: fora, decisão do cliente em 18/09.

A opção "Ordem alfabética, A–Z" do Classificar tem um traço de meia-quadratina
vindo do arquivo de idioma do tema, e a regra da loja é não usar travessão em
texto do site. Conserto no `locales/pt-BR.json` do tema, ou pelo Translate &
Adapt.

### 8. ~~Políticas com rótulo colado no valor~~ (fechado em 18/09, no ar)

Ver registro de 18/09 (tarde), abaixo.

### 9. ~~"Inicio" sem acento no menu principal~~ (fechado em 18/09, no ar)

### 10. ~~Largura das páginas de texto~~ (fechado em 18/09, no tema de trabalho)

### 11. Arquivos sem uso no tema: o cliente apaga no editor de código

A exclusão pelo editor de código é bloqueada para o Claude (apagar é
definitivo), e `themeFilesDelete` é bloqueado na API. Conferido em 18/09:
apagar é seguro para estes seis, e os cinco primeiros têm cópia idêntica no
tema publicado (o `atd-rascunho.css` é só um comentário):
`assets/atd-busca.js`, `assets/atd-produto-foto.css`, `assets/lavrale-logo.png`,
`snippets/atd-menu-catalogo.liquid`, `blocks/atd_placa.liquid`,
`assets/atd-rascunho.css`. Mais os temporários destas rodadas, todos já
esvaziados e todos começando por `assets/atd-tmp-`: `-cart`, `-cartao`,
`-hero`, `-index`, `-price`, `-primeira`, `-trilha`, `-vitrine`,
`-atalhos`, `-idx`, `-marcas`, `-nav`, `-cat`, `-css`, `-loc`, `-menu`,
`-hero2`, `-tipos`, `-marcas2`, `-loc2`, `-regua`, `-mob`, `-schema`,
`-medida`, `-cab`, `-head`, `-hg`, `-sis`, `-vit`, `-reg`, `-conf`,
`-idx2`. Em Ativos, dá para ordenar por nome e apagar o bloco inteiro de
uma vez.

**`snippets/atd-regua-cabecalho.liquid` NÃO sai.** Uma marca temporária
dentro dele apareceu nas 20 páginas varridas: ainda é chamado por um render
(logo depois do script de `atd-marcas-medida`). Apagado, o site inteiro
mostraria "Liquid error". Só sai depois de tirar o render.

Como apagar: Loja virtual, Temas, tema de trabalho, Editar código, pasta,
clique direito no arquivo, "Delete Permanently". O zoom da janela desloca o
clique: confira o nome no diálogo de confirmação antes de aceitar.

### 12. Telefone da ficha do Google diferente do site (achado em 18/09)

A loja no Google Maps mostra (62) 3086-7200; o site usa (62) 3086-7211 para
peça certa e vendas. **O cliente confirmou em 18/09: o certo é 3086-7211.**
Falta trocar no Perfil da Empresa no Google (business.google.com, Editar
perfil, Contato). O Chrome desta máquina não é dono da ficha: quem
administra o perfil precisa fazer. A rotina diária (item 13) avisa enquanto
estiver errado.

### 13. Pix e nota do Google no site: rotina diária (desde 18/09 noite)

O site não guarda mais o percentual do Pix nem a nota do Google no código.
Lê três metacampos da loja (namespace `atd`): `pix_pct`, `google_nota`,
`google_avaliacoes`. Quem atualiza é a tarefa agendada do Claude
**"Sincronizar Pix e Google (A Trator Diesel)"**
(`~/.claude/scheduled-tasks/sincronizar-pix-e-google-atd/SKILL.md`),
segunda a sábado às 8h: lê o Pix na Yampi pelo Chrome e a ficha no Google
Maps, e grava só o que mudou. Avisa se o Pix passar de 7%, se o "acumular"
for ligado ou se o telefone da ficha seguir errado.

- Roda só com o app do Claude aberto; fechado, roda quando abrir.
- Na primeira vez o cliente clica "Executar agora" e aprova as ferramentas
  (Chrome e Shopify); ficam gravadas para as próximas. Deixei
  `google_avaliacoes` em 9 de propósito para essa primeira rodada gravar 10
  e já aprovar a escrita.
- Por que não roda "no servidor": a loja está no plano **Basic**, e no Flow
  o "Send HTTP request" é só Grow, Advanced ou Plus. A API da Yampi pede
  chave secreta (não pode ir no navegador do visitante) e o checkout da
  Yampi traz o desconto embutido na página, em outro domínio.
- Sem os metacampos, o site volta sozinho a 5% e ao texto do "Selo 2".
  `pix_pct` 0 esconde a linha do Pix. Nota abaixo de 4,5 mostra só o número
  de avaliações.

### 14. Catálogo: as quatro respostas do cliente (24/09), fechado

O cliente respondeu no mesmo dia e está gravado. Detalhe em
`catalogo-e-busca.md`, "Respostas do cliente, 24/09".

- ~~Estoque do 30508 e do 11352 contra a lista de zerados~~: **o estoque de
  hoje está certo** (14 e 3). Os dois saíram da lista de zerados.
- ~~Descrição do Conjunto do Pistão Agrale 4100~~: **vem com anéis, pino e
  travas**. O texto do ML saiu e a ficha voltou ao padrão.
- ~~Modelos fora dos Lombardini~~: o cliente mandou pôr só o que for
  certo. Entrou `Sileo 1000` e `Sileo 1400` no pistão 6501512 e na correia
  2440338. `linha 9LD` e `LGW` continuam fora do filtro de óleo 2175107.
- ~~`Original`~~: **todas as peças Lombardini são originais**; os oito
  títulos que faltavam ganharam a palavra.

**O que sobrou para conferir:**

- **Sileo no título do pistão 6501512?** A regra 2 diz que em pistão, anel
  e camisa todo modelo da ficha está no título. O Sileo 1000 / 1400 entrou
  na ficha e não no título. Ou entra no título, ou sai da ficha e do
  metacampo e fica só em etiqueta. Decisão do cliente.

- **O `12LD 475-2` do filtro de óleo 2175107.** Está no título desde o
  cadastro do cliente e continua lá. Mas os catálogos de revenda dão para o
  12LD 475-2 o filtro de 90 mm (2175131), e o 2175107 tem cerca de 78 mm.
  Vale o cliente conferir na plaqueta de um motor antes da próxima venda.
- **Faceta**, na próxima sessão com navegador:
  `/collections/lombardini?filter.p.m.custom.modelos_compativeis=LDW%201003`
  deve devolver 6 peças e `...=Sileo%201000` deve devolver 2 (pistão e
  correia), cada uma mais os 4 links de recomendação.

\---

## Registros, dia a dia

O diário mudou de arquivo em 23/09/2026: está inteiro em `registros.md`,
sem corte. Ele saiu daqui porque este arquivo é lido no começo de toda
tarefa e o diário era dois terços dele. Abra `registros.md` quando a
pergunta for "por que isso ficou assim"; para trabalhar, o que está acima
basta.

- Registro de 24/09/2026: os 9 Lombardini padronizados, SEO desatualizado e tema publicado
- Registro de 23/09/2026 (noite): cartao das marcas, hierarquia do banner, seta do localizador e o schema que some
- Registro de 23/09/2026 (tarde): botão, menu, lista de modelos, faixa de marcas e o diário
- Registro de 22/09/2026: busca por código, lista de modelos e a skill que faltava
- Registro de 21/09/2026: segunda volta com o print do cliente
- Registro de 23/09/2026: trilha, ordem da página de produto, localizador e plural
- Registro de 22/09/2026: linha do horizonte, busca e peso das imagens
- Registro de 21/09/2026 (noite): compatibilidade enxugada em 32 produtos
- Registro de 21/09/2026 (celular, peça esgotada, botões e localizador)
- Registro de 18/09/2026 (tarde): políticas, Pix, localizador e páginas em 1280
- Registro de 18/09/2026 (revisão geral)
- Registro de 18/09/2026 (noite): gaveta, Classificar, páginas e hierarquia
- Registro de 18/09/2026 (filtros, carrinho e celular)
- Registro de 19/09/2026
- Registro de 18/09/2026
- Registro de 17/09/2026 (noite)
- Registro de 17/09/2026 (tarde)
- Registro de 17/09/2026
- Registro de 16/09/2026 (noite)
- Registro de 16/09/2026 (tarde)
- Registro de 15 e 16/09: preços, ERP e estoque
- Registro de 15/09/2026, conferência de SEO e de descoberta por IA

## Conectores

Só o **Shopify** está conectado e ligado nesta conversa, e só ele precisa
ficar. O Supabase está autenticado mas desligado, e não serve a este projeto.
Canva, Google Drive e Notion ficaram pela metade e não conectam.

\---

## Como trabalhar aqui

**Confira em qual tema você está antes de medir.**
`document.documentElement.outerHTML.match(/\\/cdn\\/shop\\/t\\/(\\d+)\\//)\[1]`
devolve `23` no DEV e `21` no publicado (desde 16/09).

**Meça antes de tirar print.** O recorte de região do print não funciona no
painel desta sessão: ele devolve a tela inteira.

**Para confirmar que um CSS novo subiu, procure um seletor, nunca um
comentário.** A Shopify minifica o arquivo servido e remove os comentários.

**As três políticas se editam pelo admin, e dá para automatizar.** Com o
admin logado no navegador, o editor de
`/settings/legal/<refund|privacy|terms-of-service>` guarda o texto num iframe
contenteditable. O caminho que funcionou: percorrer os nós de texto do
`iframe.contentDocument`, trocar o que precisa, disparar
`new InputEvent('input',{bubbles:true})` no `body` e clicar em Salvar.
Confirme relendo a página pública depois.

**Página e política dizem a mesma coisa em dois lugares.**
`/pages/politica-de-devolucao` e `/policies/refund-policy` têm o mesmo texto,
e o mesmo vale para a privacidade. O rodapé aponta para a página, o checkout
aponta para a política. **Mudou uma, mude a outra.**

**`redirectNewHandle: true` no `productUpdate` cria o redirecionamento
sozinho.** Não precisa de `urlRedirectCreate`.


\---
