##Grid

Um guia simples para design responsivo.<br>
webfatorial.github.io/grid/

####Por que se importar com responsivo?
Queremos que nossos sites sejam usáveis em todos os dispositivos, respondendo ao comportamento e tamanho e orientação de tela do visitante.

####Um mundo fragmentado
Desde 2013 existem milhares de diferentes dispositivos e tamanhos de tela que acessam a internet, tornando impossível projetar layouts para todos. Ao invés disso, precisamos adotar uma abordagem mais fluida ao design.

####Mobile First
O termo "mobile first" (móvel primeiro) tem aparecido bastante ultimamente. O que isso realmente significa é começar com os estilos para mobile e ir avançando em estilos otimizados para telas maiores apenas quando necessário. Em outras palavras, seus estilos para dispositivos móveis se tornam o padrão e você não os precisa mais sobrescrever depois. é muito mais simples!

> Assumindo um layout flexível, mas simples, por padrão, você pode melhor se resguardar contra navegadores — com viewports pequenas e grandes — que não são totalmente capazes em relação a layout responsivo. Então, quando falamos sobre layout, "mobile first" realmente significa "progressive enhancement" (melhoramento progressivo).

##Media queries com min-width
Introduza regras específicas ao layout somente quando precisar delas. Use `min-width` para lidar com complexidade à medida em que a viewport se torna maior. É mais fácil ter todas as media queries próximas ao invés de no final da folha de estilos ou em documento separado.

```css
/* Small screens (default) */
html { font-size: 100%; }

/* Medium screens (640px) */
@media (min-width: 40rem) {
  html { font-size: 112%; }
}

/* Large screens (1024px) */
@media (min-width: 64rem) {
  html { font-size: 120%; }
}
```

##Passos

####1. Nem todos os navegadores são iguais
Navegadores irão renderizar seu CSS de maneira diferente. Para evitar isso, é uma boa ideia usar uma alternativa moderna ao reset, como [Normalize.css](http://necolas.github.io/normalize.css/), que irá renderizar seus elementos mais consistentemente entre os navegadores (cross-browser). Lembre-se de incluí-lo antes de sua folha de estilos.

```html
<link rel="stylesheet" href="/css/normalize.css">
<link rel="stylesheet" href="/css/grid.css">
```

####2. Adicione a meta tag Viewport
Coloque na `<head>` de seu HTML. Isso habilita o uso de media queries para layouts cross-device.

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

####3. Use box-sizing: border-box
Coloque no início de seu arquivo CSS. O `*` vai afetar todos os elementos na página.

```css
*, *:before, *:after {
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
}
```

####4. Crie um contêiner
Um contêiner detém todos os elementos e controla a largura máxima da página. Usando um contêiner você faz de projetos de design responsivo mais fáceis!

```css
.container {
  margin: 0 auto;
  max-width: 48rem;
  width: 90%;
}
```

```html
<div class="container">
  <!-- Your Content -->
</div>
```

####5. Crie uma coluna
Com mobile first, colunas são nível de bloco (`block`), por padrão tomando a largura total disponível. Nenhum estilo adicional é necessário!

```html
<div class="container">
  <div class="column">
    <!-- Your Content -->
  </div>
</div>
```

####6. Crie tamanhos de colunas
Em telas grandes, colunas obtêm `float: left` a fim de "empilhar" (stack) o conteúdo horizontalmente. Colunas agora usam padding para espaçamento, então você não precisa mais se preocupar em remover margens.

```html
<div class="container">
  <div class="row">
    <div class="column half">
      <!-- Your Content -->
    </div>
    <div class="column half">
      <!-- Your Content -->
    </div>
  </div>
</div>
```

```css
@media (min-width: 40rem) {
  .column {
    float: left;
    padding-left: 1rem;
    padding-right: 1rem;
  }

  .column.full { width: 100%; }
  .column.two-thirds { width: 66.7%; }
  .column.half { width: 50%; }
  .column.third { width: 33.3%; }
  .column.fourth { width: 24.95%; }
  .column.flow-opposite { float: right; }
}
```

####7. Crie linhas
Colunas são envoltas em linhas para evitar que outros elementos fiquem "empilhados" (stacking) próximo a elas, isso também conhecido como "questões de limpeza" (clearing issues). Linhas recebem clear usando o popular `clearfix`, criado por [Nicolas Gallagher](http://nicolasgallagher.com/micro-clearfix-hack/).

```html
<div class="container">
  <div class="row clearfix">
    <div class="column half">
      <!-- Your Content -->
    </div>
    <div class="column half">
      <!-- Your Content -->
    </div>
  </div>

  <div class="row clearfix">
    <div class="column half">
      <!-- Your Content -->
    </div>
    <div class="column half">
      <!-- Your Content -->
    </div>
  </div>
</div>
```

```css
.clearfix:before,
.clearfix:after {
  content: " ";
  display: table;
}

.clearfix:after {
  clear: both;
}

.clearfix {
  *zoom: 1;
}
```

#### Fluxo oposto
Adicione a classe `.flow-opposite` em colunas nas quais você quer o conteúdo apareça primeiro em mobile, mas apareçam à direita em telas maiores.

```html
<div class="container">
  <div class="row clearfix">
    <div class="column half flow-opposite">
      <!-- Your Content -->
    </div>
    <div class="column half">
      <!-- Your Content -->
    </div>
  </div>
</div>
```

```css
@media (min-width: 40rem) {
  .column.flow-opposite { float: right; }
}
```

####Leitura Complementar
* [A Book Apart: Mobile First](http://www.abookapart.com/products/mobile-first)
* [A Book Apart: Responsive Web Design](http://www.abookapart.com/products/responsive-web-design)
* [Beginner’s Guide to Responsive Web Design](http://blog.teamtreehouse.com/beginners-guide-to-responsive-web-design)
* [Box-sizing: Border-box FTW](http://www.paulirish.com/2012/box-sizing-border-box-ftw/)
* [Don't Forget the Viewport Meta Tag](http://dev.tutsplus.com/articles/quick-tip-dont-forget-the-viewport-meta-tag--webdesign-5972)
* [The Many Faces of ‘Mobile First’](http://bradfrostweb.com/blog/mobile/the-many-faces-of-mobile-first/)
* [Understanding the Humble Clearfix](http://fuseinteractive.ca/blog/understanding-humble-clearfix)

####Referências
* [Android Fragmentation Visualized](http://opensignal.com/reports/fragmentation-2013/)
* [Animate.css](http://daneden.github.io/animate.css/)
* [Box Model](http://developer.mozilla.org/en-US/docs/Web/CSS/box_model)
* [Chrome Developer Tools](http://developers.google.com/chrome-developer-tools/)
* [Code samples by GitHub Gist](https://gist.github.com/aekaplan)
* [Internet Explorer Box Model](http://en.wikipedia.org/wiki/Internet_Explorer_box_model_bug)
* [Progressive Enhancement](http://coding.smashingmagazine.com/2009/04/22/progressive-enhancement-what-it-is-and-how-to-use-it/)
