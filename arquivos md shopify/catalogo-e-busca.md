# Catálogo e busca

Funde `busca-e-dados-da-loja.md`, `estoque-erp-shopify.md` e
`auditoria-e-reforma-02-09.md`.

**Isto tudo é conteúdo da loja, não do tema.** Mexeu, mudou no ar na hora,
mesmo com o tema DEV despublicado. Título de produto e dado de catálogo só se
gravam com planilha na mesa e OK do cliente.

---

## 1. Padrão de título e de ficha, definido pelo cliente em 02/09

**Título**: peça, mais a marca da **máquina** em que ela serve, mais os
modelos separados por " / ", mais a medida.

- Códigos de motor em caixa alta: NS11, TC14, 3TNV88, B4T.
- Medida logo depois dos modelos: STD, 0,25, 0,50.
- `Original <Marca>` só onde já era verdade.
- **Nunca travessão.** Vírgula, ponto ou parênteses.
- Exceção: as 8 lâminas de enxada rotativa levam o fabricante no fim do
  título, senão Fardin e Balbinot ficariam idênticas.

**Marca** (campo Fornecedor): o fabricante **real** da peça. Aparece na ficha
e **nunca** no título. Sem fabricante conhecido, a marca é `1ª Linha`.

**Ordem da ficha**: marca, código, motores (ou microtratores), estoque.

**Nomes já unificados**: bronzina manda sobre casquilho e sobre mancal de
biela. `Faca para Rotativa` cobre lâmina de enxada e lâmina faca rotativa, e
**não** se confunde com faca para roçadeira, que é peça diferente.

**Equivalência de fabricante nunca é texto visível, só etiqueta.** Decisão do
cliente em 09/09: o número facilita achar a mesma peça fora da loja.

SKU `NS18.01336 P`: o "P" faz parte do código real.

---

## 2. Cadastro de produto novo

A tabela de campo por campo é a skill `padronizar-produto-atd`, escrita em
22/09/2026 a partir de três peças já certas do catálogo (camisa NS11, camisa
AR160 e elemento de filtro 4TNV88). Invoque com o código interno, endereço ou
título da peça. Fica aqui só o que não é tabela de skill:

- **Erro silencioso.** Sem etiqueta igual ao tipo, `/collections/marca/tipo`
  não dá prateleira vazia: devolve a coleção da marca inteira. Parece que
  funcionou e não funcionou.
- **Coleção automática recalcula com atraso.** Ver a peça na coleção agora não
  prova que ela vai continuar lá depois que o título mudar. Confie no título
  gravado, não na tela.
- **Coleção de tipo precisa ser automática, nunca manual.** Válvulas era
  manual e cada peça nova entrava à mão. Virou `TYPE EQUALS`.
- **A Shopify junta etiquetas ignorando acento e caixa** (`valvula`, `Válvula`
  e `VÁLVULA` são uma etiqueta só). Não gaste etiqueta em variação de acento,
  gaste em variação de palavra.
- **Peça com estoque zero fica ACTIVE, não arquivada.** Arquivar tira do menu
  e cria prateleira vazia. Esgotada aparece na busca, em No final, com
  "Consulte disponibilidade" no lugar do preço. Na listagem ela **só entra na
  tela depois que a última página da coleção carrega** (19/09). Antes ficava
  no fim da página e recuava a cada lote novo do rolar infinito, porque o
  `order: 1` do CSS só ordena dentro do que já está na grade. Quem decide
  agora é `assets/atd-loja.js`, lendo `data-last-page` da grade e `data-page`
  de cada card. Coleção de uma página só mostra a esgotada na hora.
- **`redirectNewHandle: true` no `productUpdate`** cria o redirecionamento
  sozinho. Não precisa de `urlRedirectCreate`.

**Marca nova precisa de três coisas, e só dessas três:**

1. Coleção automática por `TITLE CONTAINS <marca>`.
2. **Publicar a coleção** nos canais Loja virtual e Google & YouTube. Coleção
   criada pela API nasce sem canal e dá 404.
3. O handle escrito em `marcas_handles`, em
   `snippets/atd-menu-produtos.liquid`, o único lugar que decide quais marcas
   aparecem no menu Produtos.

Foi assim que a Lombardini entrou em 08/09. Depois disso, marca ou tipo novo
também entra nas três listas de handles descritas em `tema-e-design.md`.

Em 15/09 entraram **Tramontini** (por título, filtro 71364, fabricante Jet
Fil) e **Agritech**, que é a exceção: coleção por `TAG EQUALS agritech`,
porque os microtratores TC são vendidos como Yanmar e como Agritech e o
título diz Yanmar. As 13 peças TC têm as etiquetas `yanmar` e `agritech` e
aparecem nas duas marcas. Peça TC nova precisa da etiqueta `agritech`.

---

## 3. Coleções e mega menu

O catálogo tem **127 produtos**, todos com etiqueta igual ao campo "Tipo de
produto", o que liga a URL nativa `/collections/marca/tipo` sem app nenhum.

13 coleções automáticas criadas e publicadas: Yanmar 75, Tobatta 14, Branco
12, Agrale 10, Lavrale 6, Anéis 21, Juntas 17, Filtros 13, Bronzinas 11,
Pistões 7, Camisas 4, Virabrequins 3, Mancais 3. Mais Lombardini, criada em
08/09.

**O mega menu lê `collection.all_types`**, com `all_tags` de reserva. A URL
continua por etiqueta, então **todo tipo precisa de uma etiqueta escrita
igual**. Mexeu no tipo, acerte a etiqueta junto.

Coleções internas que não aparecem para o cliente: `produtos-vindo-do-ml`,
`produtos-exclusivos-ecommerce`, `vehicles-and-parts-example-products`. Elas
estão na lista de coleções puladas na trilha. Para garantia total, despublique
do canal Loja Virtual (despublicar canal é no admin, `publishableUnpublish`
está bloqueado).

Auditoria do catálogo publicado: 117 produtos, zero títulos duplicados, zero
sem imagem, sem tipo, sem SKU, sem marca ou com preço zero. Os 40 links de
tipo do mega menu devolvem produto.

### Padronização de 16/09

132 produtos auditados contra a skill `padronizar-produto-atd` e cruzados
com três exportações do Ensis (13.615 linhas; 125 SKUs casam pelo código
interno, 7 seguem sem par, os mesmos de antes). Backup do que mudou em
`backup-produtos-16-09.json`. Gravado, sem `userErrors`:

- **Facas de rotativa (8)**: o fabricante no fim do título saiu do
  travessão para parênteses, `... Tobatta / Yanmar (Fardin)`. As quatro Tipo
  C ganharam a linha `Compatibilidade:`, e as Balbinot passaram de "Yanmar e
  Tobatta" para "Yanmar / Tobatta", uma pastilha por marca.
- **Parafuso Lavrale**: saiu "- Balbinot" (não há outro parafuso para
  colidir) e entrou a medida do ERP, `12 x 35 mm`.
- **Sapata VIO20**: "De" e "p/" corrigidos, descrição no formato da ficha,
  etiquetas do zero (tinha nenhuma, nem a do tipo).
- **Anéis Tobatta TR9**: "Motores Compatíveis" sem dois-pontos, a ficha não
  mostrava a linha. AR80, que já estava na descrição, entrou no título.
- **Conjunto do Pistão Agrale**: descrição reescrita no formato da ficha (a
  aplicação estava em linhas soltas e nenhuma linha aparecia), título com
  " / " e STD.
- **Filtro 4TNV88**: "4TNV84T4TNV88" colado virou dois modelos.
- **Etiquetas**: discos e anéis de plantadeira ganharam a cor do ERP
  (`disco vermelho`, `anel roxo`), que é como o balcão identifica. Etiquetas
  quebradas por vírgula (`5`, `disco 14`, `rebaixo 0`, `25`, `6`) saíram.
  Anéis NS18 e caixa do ventilador NS75 ganharam os modelos.

Depois, com a resposta do balcão:

- **Parafuso Lavrale** (SKU 41685, IDENTIFICAÇÃO `2070` sem P): é original,
  título ganhou `Original`. Marca continua Balbinot.
- **Rotor da bomba de óleo Tobatta** (10H1): não é original, `Original` saiu
  do título. Marca `1ª Linha` estava certa.
- **Escala do Regulador Yanmar NS50 / NS75 / NS90 / NS11** (3486): era
  cadastrada como Acelerador, o ERP diz `ESCALA DO REGULADOR, CONJUNTO`.
  Título, tipo (`Regulador`, o mesmo do Conjunto do Regulador NS50),
  etiquetas e endereço trocados; o endereço antigo redireciona. O tipo
  Acelerador deixou de existir.

**Estoque conferido em 16/09** contra as três exportações de 14/09: as 135
variantes com par batem com o ESTOQUE TOTAL do ERP. As exportações repetem o
código em mais de um endereço, e a soma do ESTOQUE LOJA de todos os endereços
é o total. Única exceção: 118057 (filtro de ar principal 3TNV88 / 4TNV88),
13 no total e só 1 no endereço de loja. Pendentes no ERP: 4870 e 4280, duas
unidades cada.

### Estoque zerado até segunda ordem (decisão do cliente, 16/09/2026)

Zerado no site e **mantido em zero** até o cliente mandar voltar, mesmo que
o ERP mostre saldo. Backup das quantidades em
`backup-compatibilidade-15-09.json`, chave `estoque_zerado_15_09`.

- **Por pedido direto**: Escala do Regulador NS50 / NS75 / NS90 / NS11
  (3486, tinha 1), bronzina de biela NS18 1,50 (4280, 1), bronzinas de biela
  NS50 0,50 e 0,75 (4298, 13; 4299, 75), Conjunto do Regulador NS50 (7159,
  12), disco de milho 11 mm (106292, 1).
- **Pela regra da Amotor**: item que aparece na exportação da Amotor Diesel
  (`amotor.csv`, 4.524 códigos, casados pelo código interno) com ESTOQUE
  LOJA igual ao ESTOQUE TOTAL fica zerado no site. Em 16/09 casaram cinco:
  7159 (12 de 12), 11352 conjunto do pistão Agrale (4 de 4), 30508 filtro
  Lombardini (6 de 6), 2370 cobertura do radiador NS18 (3 de 3) e 38782
  bronzina 3TNV70 (3 de 3). Os outros 15 SKUs do site que aparecem na Amotor
  têm loja menor que total e não mudaram.
- **Atenção na próxima atualização de estoque pelo ERP**: pule estes SKUs, e
  refaça o cruzamento com a Amotor, porque a regra vale para item novo que
  cair nela. Isto é exceção à regra geral de "estoque é o total do ERP".

### Compatibilidade padronizada (16/09/2026)

Padrão da ficha: `Motores Compatíveis: MODELO, MODELO` (ou `Microtratores`,
`Tratores`, `Motogeradores`, `Geradores`, `Mini Escavadeiras`, `Câmbios`
com o mesmo `Compatíveis:`), só o código do motor, sem a marca na frente,
sem "Motor" dentro do valor, vírgula entre modelos. A ficha quebra em
pastilha por vírgula e por barra, e com `Compatibilidade:` em prosa ela cortava
errado: o carretel B4T saía como `Branco B4T 5`, `5 e 6`, `5 HP`.

25 descrições corrigidas, sem `userErrors`, texto antigo em
`backup-compatibilidade-15-09.json`: carretel 75044 (`B4T 5.5 HP, B4T 6.5
HP`), cachorrete 55118, cachimbo 8135, coxim 66098, molas 37422, filtros
Branco 15991, 15201, 54647, carcaça 33457, bloco 14234, bronzinas 5307,
5309, 38782, 78058, 727, juntas 4636, anéis 66697, retentor 38812, mancal
52830, filtros Yanmar 66727, 111057 (`3TNV80F3TNM74F` colado e `3TNNM74F`
repetido), pistão 68300, filtro Agrale 11326 (prosa virou Tratores, Motores e
Câmbios), cabo 1669 (`TC14s`) e cobertura 2370, que não tinha linha nenhuma.

Divergências de título e compatibilidade: **resolvidas em 16/09** com o
cliente (10127, 595, 727, 5431, 68099, carretel). Na mesma rodada, o padrão de
rótulos ficou fechado: Microtratores só para os TC, Tratores para trator de
verdade, e `Compatibilidade:` saiu do catálogo. Regra completa na skill
`padronizar-produto-atd`; registro em `comece-por-aqui.md`, 16/09 (tarde).

Peso zerado ou impossível na Shopify (a Yampi calcula frete com ele):
74794 virabrequim 4TNV88 XAT (0 g), 52791 virabrequim 4TNV88 (15 g), 6352
pistão Agrale M790 (1 g), 64820 faca de roçadeira Lavrale (0 g).

A equivalência visível do filtro Agrale 4200 já não existia: está só nas
etiquetas. Conferido depois: fichas com uma pastilha por modelo,
`/collections/yanmar/sapata` devolve 1 peça, `/collections/lavrale/faca-para-rotativa`
4, e a auditoria roda limpa nas 132.

---

### Marca não é modelo de máquina (18/09/2026)

O filtro "Modelo da máquina" lê `custom.modelos_compativeis`. Em 18/09 ele
trazia **Lombardini** e **Ruggerini** como se fossem modelos: são marcas de
motor. Um produto só carregava as duas, `Conjunto do Pistão Agrale 4100 / 4118
/ 4120 STD` (id 8082827444272). Saíram do metacampo. As duas já existiam como
etiqueta no mesmo produto, então a equivalência de fabricante continua
achável pela busca, que é onde ela deve morar.

Regra que fica: nesse metacampo entra **modelo de máquina ou de motor**, nunca
o nome do fabricante. "Agrale 4100 HSE" e "Valmet 110 TA" estão certos, porque
o modelo inclui a marca; "Lombardini" sozinho, não.

**Como achar quem tem um valor de faceta**: pela URL da loja, não pela busca
do Admin. `products(query: "metafields.custom.x:y")` **não** filtra metacampo,
devolve o catálogo inteiro. Já
`/collections/all?filter.p.m.custom.modelos_compativeis=<valor>` devolve
exatamente quem tem aquele valor; leia os `product-card a[href]` da resposta.

### Motor não é marca, e medida de cilindro não se mistura (21/09/2026)

Achado a pedido do cliente, na ficha do `Conjunto do Pistão Agrale 4100 /
4118 / 4120 STD` (8082827444272): o campo MOTORES trazia
`Ruggerini, Lombardini (1 cilindro)`. São **marcas**, não modelos de motor, e
o "(1 cilindro)" ainda estava errado, porque os Ruggerini da série MD são
bicilíndricos. A Lombardini é dona da Ruggerini desde os anos 90, então as
duas na mesma linha também se repetem.

**Os motores certos, com a conta que sustenta cada um.** A peça é pistão de
**85 mm**, e pistão e anel de segmento só servem no motor de mesmo diâmetro:

- **Agrale M85: 85 mm** (curso 100, 567 cm³, 1 cilindro). É o único da linha
  M com 85. O M80 tem 80, o M90 tem 90 (curso 105, 668 cm³), o M93 tem os
  mesmos 668 cm³ do M90 e o M790 tem 90 mm em 2 cilindros. **Corrigido na
  mesma noite**: mesmo diâmetro não basta, o M85 saiu da lista, porque o SKU
  da peça é da família de 2 cilindros. Ver a regra 8 mais abaixo.
- **Ruggerini MD170, MD171, MD190, MD191: 85 mm**, pelo manual de oficina da
  série MD2 (a tabela dá `Bore mm 80 85 85 85` para MD150/151, MD170/171,
  MD190/191 e MD190E/191E). O **MD150 e o MD151 têm 80 mm** e por isso ficam
  de fora.
- Que a linha 4100 leva Ruggerini está no nome do catálogo oficial de peças
  da própria Agrale: "Trator Agrale 4120 Motor Ruggerini".
- Os dados do site batem com isso por outro caminho: `Jogo de Anéis Agrale
  M90 STD` e `Bronzina de Biela Agrale M80 / M85 / M90` dizem os dois
  "Tratores Compatíveis: Agrale 4100".

Gravado: `Motores Compatíveis: M85, MD170, MD171, MD190, MD191`. Texto antigo
em `backup-compatibilidade-21-09.json`. Entraram também as etiquetas `m85`,
`md170`, `md171`, `md190`, `md191` e `agrale m85`, porque equivalência de
fabricante nesta loja mora em etiqueta, e `ruggerini` e `lombardini`
continuam lá.

**O que é "MD"** (pergunta do cliente em 21/09, à noite): é a família de
motor **Ruggerini** que a Agrale montou nessa linha de tratores. MD170,
MD171, MD190 e MD191 são modelos de motor, do mesmo jeito que M85 e M90 são
modelos de motor Agrale; a diferença é que os MD são **Ruggerini de 2
cilindros**, e os M são Agrale de 1 cilindro. O nome não aparece na
plaqueta do trator, aparece na do motor.

Confirmado no catálogo oficial de peças da Agrale para
`4100.4 HSE / 4100 HSE / 4100 SEI / 4100 E HSE / 4120 HSE / 4120 SEI /
4118.4`: é **um catálogo só para os sete tratores**, e dentro dele
convivem três motores, cada um com sua família de código. O SKU da peça,
`7072.004.007.00.3`, cai na família 7072, que é a de 2 cilindros. Por isso
a lista de quatro MD está certa como conjunto.

**O que falta confirmar**: qual MD equipa cada trator, um a um. O casamento
por potência (4118 com MD170/171, 4120 com MD190/191) é inferência, não
catálogo, e como a peça é a mesma para os sete isso não muda o que está
escrito na ficha.

**Regra que fica**: em peça que depende do diâmetro do cilindro (pistão,
anel, camisa), a lista de motores só pode ter motores de mesmo diâmetro.
Bronzina de biela e de mancal podem cruzar diâmetros, porque dependem do
virabrequim e não do cilindro.

### Regra da compatibilidade, fechada com o cliente em 21/09/2026 (noite)

Isto é o que decide se uma linha de compatibilidade pode existir. Vale no
cadastro de peça nova e em qualquer revisão. Quando uma linha não passa por
estas regras, ela **sai**: o cliente foi explícito, "não podemos induzir o
cliente ao erro", e peça a menos se resolve no telefone, peça errada não.

**1. Diâmetro manda em pistão, anel e camisa.** Essas três só podem listar
motores do **mesmo diâmetro de cilindro**. Bronzina de biela e de mancal
podem cruzar diâmetros, porque dependem do virabrequim. Junta, filtro,
cabo, rotor de bomba, silencioso e regulador não dependem do diâmetro e
podem ter lista larga.

Diâmetros Agrale confirmados no folheto da linha M (Agrale, setembro de
2010, o mesmo que a Amotor distribui): M80 80 x 100 mm; M85 85 x 100 mm,
567 cm³; M90 ID 90 x 105 mm, 668 cm³; M93 ID 90 x 105 mm, 668 cm³; M790
90 x 100 mm, 2 cilindros, 1.272 cm³. Um jogo de anéis não serve em M90,
M85 e M80 ao mesmo tempo.

**2. Modelo que não está no título não entra na lista**, a menos que a peça
seja independente do diâmetro. Foi assim que saíram BS95 do jogo TR10 e
BS180 do pistão AR140.

**3. Marca não é modelo.** Ruggerini, Lombardini, Scania e Komatsu são
fabricantes. Vão para **etiqueta**, que é onde a equivalência mora nesta
loja, e nunca para a linha de compatibilidade nem para
`custom.modelos_compativeis`.

**4. Sem extensão de aplicação.** O código de aplicação que vem depois do
modelo não entra: `4TNV98-DSA`, `3TNM72-ASA3T`, `4TNV88 XAT`, `3TNE68-AK`,
`3TNV76-CSA` e `BD 5.0 XS` viram `4TNV98`, `3TNM72`, `4TNV88`, `3TNE68`,
`3TNV76` e `BD 5.0`. O mesmo para o sufixo de acabamento da linha NS da
Yanmar: `NSB90R` e `NSB90RE` viram `NSB90`, `NSB18R` e `NSB18RE` viram
`NSB18`, `NS75R` vira `NS75`. Só é seguro colapsar porque o código base já
está na mesma lista; se não estiver, coloque o base.

**Fica quem é outro motor de verdade**: o T de turbo e o L (`4TNV98T`,
`4TNV106T`, `4TNV84T`, `4TNV94L`), e o modelo que a fábrica vende com a
letra colada (`3TNV82A`, `3TNE78A`). Fica também o nome de **máquina**
que o cliente lê na plaqueta, como TC14S, porque isso é microtrator e não
acabamento de motor.

**4b. NSB e NS sao o mesmo motor** (cliente, 22/09/2026). O B do meio e
nomenclatura, nao modelo. `NSB11` vira `NS11`, `NSB18` vira `NS18`, e assim
para toda a linha NS. Saiu de 22 produtos, do titulo, da ficha e do
metacampo, e ficou como **etiqueta**, para quem digita NSB continuar
achando. Numa peca so isso tirou metade da lista: a escala do regulador
tinha 18 motores e ficou com 10.

**5. Nada de "todos os modelos"**, com uma excecao confirmada pelo cliente
em 22/09: o `Cabo do Acelerador Tobatta` serve mesmo em todo modelo Tobatta
e a linha fica como esta. Saiu "Scania turbinados (todos os
modelos)" do filtro de óleo Agrale 4200. Promessa larga em peça que se
confere pela rosca e pela vedação é devolução na certa.

**6. Sem parêntese explicativo dentro do valor.** `3D76 (Komatsu)` vira
`3D76`, `3YM30 (marítimo)` vira `3YM30`, `BD 13.0 (linhas G2 e XS)` vira
`BD 13.0`. A ficha quebra o valor em pastilha e o parêntese entra junto.
Explicação, se precisar, vai na linha `Observações:`.

**7. Peças do mesmo conjunto dizem a mesma coisa.** Pistão, anel e camisa
do mesmo motor têm que ter listas idênticas. Divergência entre elas é erro
em uma das três, não compatibilidade diferente.

**8. O SKU diz a família, e o SKU não mente.** No código Agrale, 7006,
7007 e 7010 são o motor M93 a ar; 7009 é o M95W a água; **7071 e 7072 são
o Ruggerini de 2 cilindros**. Código Tobatta é outro mundo (`7CC010`,
`14CC03`, `16CC04`) e nunca carrega motor Agrale. Antes de aceitar uma
lista de motores, veja de qual família é o SKU.

**9. Gravou em lote, toque e confira.** Depois de mexer no metacampo pela
API, `tagsAdd` e `tagsRemove` de uma etiqueta temporária em cada produto, e
confira a faceta por
`/collections/all?filter.p.m.custom.modelos_compativeis=<valor>`, contando
os `href="/products/` distintos. **Toda página traz 4 links de
recomendação** (os anéis de milho), então 4 quer dizer zero resultado.

### O que foi gravado em 21/09/2026 (noite), com OK do cliente

32 produtos, sem `userErrors`, texto e etiquetas antigos em
`backup-compatibilidade-21-09-noite.json`.

Por pedido direto do cliente:

- `Jogo de Anéis Agrale M90 STD`: de M90, M85, M80 para **M90**. Os três
  têm diâmetros diferentes.
- `Jogo de Anéis Yanmar B10 / NB13`: saiu o NB10. Regra que o cliente
  passou: **o que serve no B9 serve no NB10** (menos o virabrequim), e **o
  que serve no B10 serve no NB13**. São dois pares, não um grupo de quatro.
- `Jogo de Anéis Tobatta TR9 / AR80 / AS80 / M90 STD`: o M90 é motor
  Agrale e saiu do título, da ficha, do metacampo e da etiqueta. SKU
  `7CC010`, Tobatta.
- `Jogo de Anéis Tobatta AR160 STD`: de seis modelos para **AR160**. A
  camisa AR160 já era só AR160.
- NSB90RE fora da camisa e do anel NS90, e o resto do conjunto NS90
  alinhado em NS90, NSB90, NSB95.

Achados na mesma rodada, pela regra acima:

- `Conjunto do Pistão Agrale 4100 / 4118 / 4120 STD`: **saiu o M85**. O SKU
  é `7072.004.007.00.3` e o 7072 é a família de **2 cilindros (Ruggerini)**
  no catálogo oficial da Agrale para esses mesmos sete tratores. O M85 é
  Agrale de **1 cilindro**: mesmo diâmetro, outra peça. Ficou
  `MD170, MD171, MD190, MD191`.
- Filtro de óleo Agrale 4200: saiu a linha do Scania.
- `Pistão Tobatta AR140 / AS140 / BS180`: saiu o BS180, título incluído.
- `Jogo de Anéis Tobatta TR10 / AR70 / AR90 / AR120`: saiu o BS95.
- Família NS11: camisa, anel e bronzina passaram a dizer as mesmas cinco
  (NS11, NSB11, NS12, NSB12, BM11). A camisa não tinha NS12 e o anel não
  tinha BM11; a bronzina, que tinha as cinco, ainda repetia NSB11.
- Extensões de aplicação e sufixos R/RE tirados de 18 produtos, entre eles
  o pistão 3TNM72, que sozinho listava **40 variações** do mesmo motor.

### As pendencias de 21/09, respondidas pelo cliente em 22/09/2026

Gravado em 27 produtos, sem `userErrors`, texto e etiquetas antigos em
`backup-compatibilidade-22-09.json`. A faceta foi reindexada e conferida
pela URL: `NSB11`, `NSB18`, `NSB90`, `T12` e `AR120` devolvem zero;
`NS11` devolve 13, `NS12` 8, `AS140` 2.

- **NS e NSB sao o mesmo motor.** Regra 4b acima.
- **Tobatta AR100**: o anel serve em `AR100, AR110, AS100, AS110`. T12 e
  TR12 sairam. O titulo virou `Jogo de Anéis Tobatta AR100 / AR110 /
  AS100 / AS110 STD`, e o SKU `110CC010` confirma a familia 110.
- **Tobatta TR10** (codigo interno 534): serve em `TR10, AR70, AR90`. O
  AR120 saiu do titulo e da ficha.
- **Tobatta AR140**: o anel tambem serve no AS140, entao anel e pistao
  agora dizem a mesma coisa e o conjunto fecha.
- **Agrale 4100**: as sete versoes (`4100 HSE`, `4100 SEI`, `4100 SEI GÁS`,
  `4100.4 HSE`, `4118.4`, `4120 SEI`, `4120 HSE`) viraram tres, `Agrale
  4100, Agrale 4118, Agrale 4120`. O cliente pediu o caminho mais simples,
  e com isso o `4100 SEI GÁS`, que era o unico ponto duvidoso contra o
  catalogo oficial, deixou de existir sem precisar de decisao.
- **Filtro de oleo Agrale**: `Agrale 4200 (motor MAN)` virou `Agrale 4200`,
  e o MAN foi para a linha `Observações:`, pela regra 6.

**Conferencia de 22/09**, rodada depois de gravar, cruzando o catalogo com
ele mesmo: **uma unica sobra**, a frase "Todos os modelos Tobatta" do cabo
do acelerador, que o cliente confirmou estar certa. Zero NSB, zero extensao
de aplicacao, zero sufixo R ou RE, zero parentese dentro de valor, e **zero
conjuntos de pistao, anel e camisa em desacordo**.

### A busca deixou de misturar (22/09/2026)

Relato: "pesquisando filtro de ar branco ele me retorna um filtro de ar,
logo depois dois filtros de combustivel da Branco e filtros de ar de outras
marcas". Medido: aquela busca devolvia **16 pecas de 132**, e "junta
yanmar" devolvia **69**. E o que ja estava escrito na secao 4 deste
arquivo: a busca nativa completa o resultado com casamento parcial e
operador booleano nao funciona.

A separacao passou a ser feita **depois** da busca, em
`sections/search-results.liquid`. Uma peca fica na lista de cima so se
titulo, tipo, marca, etiquetas ou modelos compativeis contem **todas** as
palavras da pergunta. O resto continua na pagina, atras de um botao "Ver
também N peças parecidas", porque numa loja de 132 pecas dar zero resultado
custa mais caro que dar demais. Se nenhuma peca casa com tudo, nada e
escondido.

Tres detalhes que a medicao obrigou a incluir:

- **acento nao conta**: "pistao" tem que achar "Pistão", senao a busca do
  balcao, que digita sem acento, dava zero;
- **palavra de 4 letras ou mais casa por comeco**: "junta" tem que achar
  "juntas", senao "junta yanmar" achava 1 peca em vez de 12;
- **palavra de ate 3 letras exige palavra inteira**: o "ar" de "filtro de
  ar" nao pode casar dentro de "arruela".

Medido depois: "filtro de ar branco" mostra **1**, "junta yanmar" **12**,
"ns11" **12**, "camisa yanmar ns90" **1**, "bomba" **3** e nada escondido,
"xyzabc" cai na tela de busca vazia de sempre.

### A trilha passou a dizer marca E tipo (21/09/2026)

Relato: "na bomba de óleo lubrificante NS11 aparece Início / Agritech ou
Início / Yanmar, mas tinha que ser Início / Yanmar / Bomba".

A trilha dizia a marca e nunca dizia que peça é. Em `blocks/atd_breadcrumb.liquid`:

- **marca**: lista na configuração do bloco, lida NA ORDEM escrita
  (`yanmar,agrale,tobatta,branco,lavrale,lombardini,tramontini,agritech`).
  Quem cai em duas sai com a primeira. A coleção de chegada deixou de mandar
  aqui, de propósito: a trilha é o lugar da peça no catálogo, não o caminho
  que a pessoa fez, e o mesmo texto vai para o JSON-LD.
- **tipo**: o campo "tipo de produto". Link para a marca já filtrada,
  `/collections/yanmar?filter.p.product_type=Bomba`. Coleção própria de tipo
  existe para alguns (Camisas, Juntas, Bronzinas, Filtros, Pistões, Anéis,
  Válvulas, Virabrequins) e não para outros (Bomba, Rotor, Cabo, Regulador).
  O filtro existe para todos, então a trilha usa o filtro: um caminho só.

Peça sem marca conhecida cai na regra antiga (coleção de chegada, senão a
primeira coleção útil). O JSON-LD ficou com quatro degraus e as posições
são contadas, não fixas, porque um degrau pode faltar.

### Letra dobrada na busca (21/09/2026)

Medido: **"tobata" devolvia 14 peças e ZERO casamentos exatos.** O catálogo
escreve "Tobatta", a loja etiqueta as duas formas, e quem digita não sabe
qual é a da loja. A Shopify achava as 14 por semelhança; o recorte de
casamento exato dizia "nenhuma peça responde exatamente", que é pior do que
não dizer nada.

Regra nova, simétrica e sem lista de sinônimos: a palavra perguntada ganha
uma forma com as consoantes dobradas encolhidas (**tt, rr, ss, ll, nn, mm,
cc**) e o palheiro ganha a mesma redução. "tobata" acha "Tobatta" e
"tobatta" acha a etiqueta "tobata". De quebra vale como tolerância a erro de
digitação ("masa" acha "massa").

Medido depois: "tobata" 14 e todas exatas, "tobatta" 14 e todas exatas, e as
onze medidas anteriores **iguais**.

### O plural irregular, fechado em 23/09/2026

O que 22/09 deixou aberto era isto: "anel ar160" dava **zero** casamentos
exatos, porque o título diz "Anéis" e o casamento por começo de palavra
(" anel" contra " aneis") não fecha. Ficou registrado na época como problema
de etiqueta. Não era: etiqueta resolveria um caso, e o buraco valia para
toda palavra que muda de letra no plural.

Agora cada palavra da pergunta vale por ela mesma **e pela outra forma de
número**, montada por regra de português sobre a palavra já sem acento:

- termina em **eis**, vira **el**: aneis, anel
- termina em **oes** ou **aes**, vira **ao**: pistoes, pistao
- termina em **ns**, vira **m**: bons, bom
- termina em **es**, perde o final: motores, motor
- termina em **s**, perde o s: juntas, junta
- termina em **l**, vira **is**: anel, aneis
- termina em **ao**, vira **oes**: pistao, pistoes
- termina em **m**, vira **ns**: bom, bons

Palavra de até 3 letras continua exigindo palavra inteira, e forma derivada
que encolhe para 3 letras ou menos volta a exigir palavra inteira também,
senão o "ar" de "ares" casaria dentro de "arruela".

Medido depois: **"anel ar160" passou de 0 para 1 exata**, "aneis" dá 22,
"pistao" dá 8, "camisas" dá 4. E as medidas de 22/09 continuam iguais:
"filtro de ar branco" 1, "junta yanmar" 12, "ns11" 12, "camisa yanmar ns90"
1.

**Zero exatas passou a ser dito em voz alta.** A regra de 22/09 (nada é
escondido quando nada casa com tudo) está certa, mas a página ficava
mentindo por omissão: mostrava as parecidas como se fossem o resultado.
Agora sai uma linha, "Nenhuma peça responde exatamente a X, estas são as
mais parecidas que temos".

### O cartao sem metacampo (22/09/2026)

Relato: "o cabo do acelerador Tobatta, quando pesquisamos por ele, nao
mostra a compatibilidade antes de apertar no produto". Causa: o cartao
(`snippets/atd-card-info.liquid`) le `custom.modelos_compativeis`, e essa
peca nao tem lista de modelos para gravar, porque serve em todos. Agora,
**so quando o metacampo falta**, o cartao le a linha de compatibilidade da
propria descricao. O cabo passou a mostrar "Serve em Todos os modelos
Tobatta". Quem tem metacampo nao paga nada por isso.

### O cabo do acelerador entrou no filtro e na busca (23/09/2026)

Pedido do cliente: "o cabo do acelerador que serve em todos os tobattas tem
que ter etiquetas de todos os tobattas para que apareça na pesquisa ou nos
tipos". Ele tinha 5 etiquetas e nenhum metacampo de modelo, então quem
filtrasse Tobatta por AR100 não via a peça que serve na máquina dele.

Gravado: as **14 etiquetas de modelo** que a Tobatta tem no catálogo (ar70,
ar80, ar90, ar100, ar110, ar140, ar160, ar220, as80, as100, as110, as140,
tr9, tr10), mais `tobatta` e `tobata`, e o metacampo
`custom.modelos_compativeis` com os mesmos 14 modelos. Reindexado com
`tagsAdd` e `tagsRemove` depois da gravação do metacampo, pela regra da
seção acima.

Medido depois: `/collections/tobatta?filter...=AR100` devolve **3 peças**, com
o cabo entre elas.

**O cartão continua dizendo a verdade curta.** Com metacampo, o cartão
passaria a dizer "Serve em AR100, AR110, AR140 e mais 11", que é pior do que
"Todos os modelos Tobatta". Então `atd-card-info.liquid` ganhou uma regra: a
linha de compatibilidade da descrição **ganha do metacampo quando começa em
"Todos"**. Só essa; qualquer outra prosa continua perdendo, porque lista de
modelo é sempre mais precisa.

**Aviso medido, e reconferido em 21/09:** `product.tags` na página de
RESULTADO DE BUSCA continua devolvendo a lista ANTIGA deste produto, quatro
horas depois da gravação. A prova é limpa: etiqueta velha ("f7041") dá
casamento exato, etiqueta nova ("ar100", "tr9", "tobata") não. O metacampo,
que está no mesmo palheiro desde 22/09, também não chegou: o objeto inteiro
da peça está velho nesse contexto, não só as etiquetas.

**O que foi tentado e NÃO resolve:** `productUpdate` com o mesmo título (a
Shopify ignora valor igual e nem mexe no `updatedAt`); `tagsAdd` seguido de
`tagsRemove`, que é o empurrão que funciona para a faceta (ver a seção de
reindexação), mas não para este cache; cache-buster na URL da busca.

**O que NÃO se deve fazer:** mexer no catálogo (título, publicação) para
forçar a mão. O prejuízo é pequeno e de um lado seguro: a peça APARECE na
busca, só entra como parecida em vez de exata. Errar para menos é melhor do
que errar para mais. É cache da Shopify e vira sozinho.

**Modelo Tobatta que a loja atende e que não está nestes 14** (T12 e TR12
foram citados em 22/09) **não entrou**, porque criaria valor de filtro com
uma peça só e seria inventar verdade de catálogo. Entra quando o cliente
disser.

### "Você quis dizer" na busca vazia (22/09/2026)

Relato do cliente: "estou pesquisando 4tnv84 e ele não retorna o 4tnv84t,
seria como se faltasse uma letra". A causa é a regra medida na seção 4: a
Shopify completa palavra pelo começo só no título, e 4TNV84T mora apenas na
compatibilidade.

**O T é significativo e não entra na regra de simplificar.** T é turbo e
turbo é outro motor. A prova está no próprio catálogo: o
`elemento-filtro-combustivel-yanmar-4tnv88` serve em 4TNV98 e **não** em
4TNV98T, enquanto o `elemento-do-filtro-separador-de-combustivel` serve nos
dois. Vale o mesmo para o L. A regra 4 da compatibilidade continua como
está.

O conserto foi na busca, não no catálogo. Quando a busca devolve zero,
`sections/search-results.liquid` varre `custom.modelos_compativeis` de todas
as peças e oferece os modelos que **começam** pelo que foi digitado (ou o
contrário: digitou o modelo e sobrou letra). O link vai para a faceta da
marca, que é exata. Medido: `4tnv84` oferece 4TNV84T com 2 peças, `4tnv10`
oferece 4TNV106T e 4TNV106, `nsb1` e `zzzznaoexiste` não oferecem nada.
Quando a sugestão é o termo mais um T, sai também a linha explicando que
turbo é outro motor.

Três detalhes que precisam continuar juntos:

- a conta mora na **seção**, e não no `snippets/atd-busca-vazia.liquid`,
  porque precisa de `{% paginate collections.all.products by 250 %}` para
  enxergar além de 50 produtos, e o snippet roda dentro do paginate da
  busca, onde a Shopify proíbe aninhar outro. Sem o paginate a varredura
  via 50 produtos e 73 modelos, e o 4TNV84T ficava de fora;
- a conta só roda com `search.results_count == 0`: busca que deu certo não
  paga nada;
- o snippet recebe tudo por parâmetro (`sugestoes`, `nota_turbo`), então
  continua funcionando onde ninguém passa nada.

As onze medidas de sempre não mudaram: "anel ar160" 1 exata, "aneis" 22,
"pistao" 8 todas exatas, "camisas" 4, "filtro de ar branco" 1, "junta
yanmar" 12, "ns11" 12, "camisa yanmar ns90" 1, "tobata" e "tobatta" 14 cada
e todas exatas, "4tnv88" 6 todas exatas.

### Filtro desatualizado depois de gravação em lote (18/09/2026, noite)

Relato: "algumas buscas do Qual é a sua máquina não encontram, mesmo com a
peça cadastrada". Medido: das 210 opções do localizador, **80 voltavam
vazias** (3TNV70, NS50, BTD22, YT18, VIO17...). O metacampo estava certo nas
109 peças; o **índice do filtro** da loja conhecia só 28 modelos na Yanmar e
70 no catálogo todo. Causa: a gravação em lote pela API em 17/09 (12:13 a
12:16) não reindexou o filtro. Peça editada depois por outro motivo tinha
entrado; as outras não.

Conserto: tocar cada produto. `tagsAdd` de uma etiqueta temporária e
`tagsRemove` logo depois, 54 por chamada (custo 10 cada, teto 1000), nas 109
peças com metacampo. Depois disso as 210 opções devolvem pelo menos uma peça.
Isso também completou o filtro "Modelo da máquina" das coleções, que mostrava
menos da metade dos modelos.

**Regra:** gravou metacampo de filtro em lote pela API, toque os produtos
em seguida e confira uma faceta pela URL. Edição pelo admin, produto a
produto, reindexa sozinha.

### Modelos em botões no topo da coleção (21/09/2026)

A página da marca abria com 76 peças de todos os modelos, e dizer o modelo
custava abrir a gaveta "Filtrar". Agora, logo abaixo do título, existe uma
fila de botões com os modelos, em `snippets/atd-modelos-chips.liquid`,
chamado pelo bloco `atd_atalhos` (o cabeçalho da coleção). Um toque recorta
a página; o botão marcado fica verde e traz o X para desmarcar.

A lista sai de `collection.filters`, **o mesmo filtro "Modelo da máquina" da
gaveta**, já calculado pela Shopify para aquela página. Consequências que
valem lembrar:

- não existe lista escrita à mão nem varredura do catálogo, e não há
  consulta nova: peça nova com `custom.modelos_compativeis` entra sozinha;
- a fila acompanha o recorte. Em Yanmar são 82 modelos; na coleção Juntas,
  só os modelos que têm junta;
- **se o índice do filtro estiver velho, a fila fica curta pelo mesmo
  motivo da seção acima.** Modelo cadastrado que não aparece nem aqui nem na
  gaveta quer dizer produto por tocar.

Ordem, que é o que decide se a fila serve para alguma coisa: os 12 primeiros
são os modelos com **mais peças**, não os primeiros do alfabeto. Medido em
Yanmar: por ordem alfabética a dobra mostraria 2TNV70, 3D68E e 3D76, códigos
de motor que quase ninguém procura, e esconderia TC11, NS18 e NS11, que são
os três com mais peças. Do 13º em diante volta a ordem da Shopify,
alfabética, que é como se procura um modelo específico numa lista grande.

Passando de 12, o resto fica atrás de "Ver todos os N modelos". Sem
JavaScript aparecem todos e o botão não aparece: nada fica escondido sem
jeito de abrir. No celular a fila corre para o lado, sem dobra, com o rótulo
em caixa alta igual ao das filas de marca e de tipo que vêm logo abaixo.

---

## 4. A busca da Shopify e seus limites

- **Operadores não funcionam.** Medido: `yanmar AND zzznaoexiste` devolve os
  mesmos 43 de `yanmar`. Só frase exata entre aspas funciona. O script que
  tentava contornar isso foi desligado em vez de entregue, com a medição
  escrita em `assets/atd-busca.js`.
- **Busca com poucos casamentos exatos completa com aproximados.** Foi assim
  que `agritech` devolvia Agrale e `válvula` devolvia virabrequim. Etiquetar
  bem encolhe a cauda; ela some de vez só quando o catálogo daquele tipo
  cresce.
- **Sinônimo está suspenso pela Shopify.** Apelido de busca só funciona como
  **etiqueta**. Precisa de mais apelidos? Grave como etiqueta.
- **Completar palavra pelo começo só acontece no TÍTULO** (medido em
  22/09/2026). Etiqueta e metacampo exigem a palavra inteira. Contagem de
  itens da grade: `4tnv10` zero e `4tnv106` uma; `4tnv9` zero e `4tnv94`
  uma; `nsb1` zero e `nsb11` oito. Já `camis`, `bronz`, `pist` e `virabr`,
  que são começo de título, devolvem a lista toda. É a explicação do relato
  "`4tnv84` não retorna o `4tnv84t`": 4TNV84T só existe na compatibilidade.
- **O curinga `*` não é prefixo, é aproximação.** `4tnv84*` devolve seis
  peças, e quatro delas são de 4TNV88 e 4TNV86, que são outros motores. Não
  serve para consertar busca de código.
- No app **Search & Discovery**, "Produtos sem estoque" precisa ficar em **No
  final**. O app roda em quadro isolado de outro domínio: só captura de tela e
  clique por coordenada, com `preset desktop`.
- Busca sem resultado usa `snippets/atd-busca-vazia.liquid` e
  `sections/atd-busca-resumo.liquid`, com WhatsApp e atalhos, no lugar de
  despejar a coleção inteira.
- Endereço antigo não dá mais 404: seis redirecionamentos mais
  `snippets/atd-404-resgate.liquid`. Falta a lista completa do Search Console.

---

## 5. ERP Ensis

Regras completas na skill `estoque-ensis-ecommerce`. Local de estoque:
`gid://shopify/Location/75530534960`.

### Como o arquivo chega

- CSV latin-1 com separador `;`, números no formato brasileiro.
- A chave é a coluna IDENTIFICAÇÃO contra o SKU da Shopify, normalizada
  tirando espaço, ponto, barra e traço. **Comparação exata**: o ` P` separa
  paralela de original, e casar por aproximação troca o fabricante da peça.
- Erros de digitação comuns: P solto, grudado ou ausente; `PI` no lugar de
  `P`; `I` maiúsculo lido como `l` ou `1`.
- **A coluna LINHA não é marca limpa.** `DIVERSOS`, `PEÇAS PARARELAS`,
  `MAM PECAS`, `IMPORTADAS//PEÇAS`, `CONSUMO` e `BASE` querem dizer que o ERP
  não sabe: mantenha a marca do site.
- **ESTOQUE TOTAL inclui depósito. ESTOQUE LOJA é a prateleira.** Para a
  promessa de retirada em 24h, o total pode prometer peça que não está lá.

### O que a sugestão do ERP erra em marca

SKF, FAG, NSK e NTN são **compatibilidade**, não fabricante. LINTEC é linha
interna. O ERP chega a propor trocar Bosch e Lombardini por Lintec, e Yanmar
por Buffalo numa peça cujo título diz Original. Confira uma a uma antes de
levar ao cliente.

### Gravações já feitas

**01/09**: 139 variantes conferidas contra os dois inventários (6.375 mais
2.726 linhas, 8.747 códigos distintos). Estoque das 139, SKU de 125 trocado do
código externo para o interno (`003948-9` vira `3948`, sem zeros à esquerda,
sem travessão e sem o dígito), marca de 23 pela coluna LINHA. Nenhum SKU
repetido, nenhuma colisão.

**14/09**: estoque de 54 variantes, soma de 2945 para 2791,
`inventorySetQuantities` sem `userErrors`, amostra de 5 SKU conferida de volta.

### As 14 que ficaram em zero por falta de par

NS18.01336 P, TC14.62100, NS18RG.44830, 10H1, NS18C.44821, B-208 1,00,
B-205 0,50, B-204 1,00, 2070 P, 14000422, NS50.51402, 7031221, 129630.55731,
119515.23601.

Quatro delas existem no ERP com o sufixo P diferente (NS18.01336, 2070,
NS50.51402 P, 119515.23601 PI). O cliente optou por zerar em vez de forçar o
par, porque o P separa peça original de paralela.

O NS18C.44821 tem par no ERP (`NS18C.44821 P`), mas esse item já está casado
com o conjunto da Moldemaq. Um item do ERP não vira dois produtos.

### Correções de código confirmadas pelo cliente

- `38222` no site é a IDENTIFICAÇÃO `365200172 P`, código interno `038222-1`.
- `B8.B.502 P` no site, `B8.B.502` no ERP, sem o P.
- `NS90.01111 l` no site, `NS90.01111 I` no ERP, com i maiúsculo.

### Aviso registrado

Trocar o SKU quebra qualquer integração que casa produto por código: Yampi,
Mercado Livre, planilhas de importação. O cliente foi avisado antes da
gravação de 01/09.
