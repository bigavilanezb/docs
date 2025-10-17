# Guía Completa de Emmet - Atajos para HTML y CSS

Emmet es una herramienta que te permite escribir HTML y CSS más rápido usando abreviaciones. Aquí tienes todos los atajos organizados por categoría.

## 1. Multiplicación (*)

Crea múltiples elementos del mismo tipo.

**Sintaxis:** `elemento*número`

```html
<!-- ul*3 -->
<ul></ul>
<ul></ul>
<ul></ul>

<!-- li*5 -->
<li></li>
<li></li>
<li></li>
<li></li>
<li></li>

<!-- div*4 -->
<div></div>
<div></div>
<div></div>
<div></div>
```

## 2. Anidación de Hijos (>)

Crea elementos dentro de otros elementos.

**Sintaxis:** `padre>hijo`

```html
<!-- div>p -->
<div>
    <p></p>
</div>

<!-- ul>li -->
<ul>
    <li></li>
</ul>

<!-- nav>ul>li -->
<nav>
    <ul>
        <li></li>
    </ul>
</nav>

<!-- header>nav>ul>li*3 -->
<header>
    <nav>
        <ul>
            <li></li>
            <li></li>
            <li></li>
        </ul>
    </nav>
</header>
```

## 3. Elementos Hermanos (+)

Crea elementos al mismo nivel (hermanos).

**Sintaxis:** `elemento1+elemento2`

```html
<!-- div+p+span -->
<div></div>
<p></p>
<span></span>

<!-- header+main+footer -->
<header></header>
<main></main>
<footer></footer>

<!-- h1+p+ul>li*3 -->
<h1></h1>
<p></p>
<ul>
    <li></li>
    <li></li>
    <li></li>
</ul>
```

## 4. Subir Nivel (^)

Sube un nivel en la jerarquía.

**Sintaxis:** `elemento^elemento`

```html
<!-- div>p>span^div -->
<div>
    <p><span></span></p>
    <div></div>
</div>

<!-- ul>li>a^^p -->
<ul>
    <li><a href=""></a></li>
</ul>
<p></p>

<!-- div>section>article>p^^footer -->
<div>
    <section>
        <article>
            <p></p>
        </article>
    </section>
    <footer></footer>
</div>
```

## 5. Agrupación ()

Agrupa elementos para aplicarles operaciones.

**Sintaxis:** `(elementos)*número`

```html
<!-- (div>p)*3 -->
<div>
    <p></p>
</div>
<div>
    <p></p>
</div>
<div>
    <p></p>
</div>

<!-- (header>h1)+(main>p)+(footer>span) -->
<header>
    <h1></h1>
</header>
<main>
    <p></p>
</main>
<footer>
    <span></span>
</footer>

<!-- ul>(li>a)*5 -->
<ul>
    <li><a href=""></a></li>
    <li><a href=""></a></li>
    <li><a href=""></a></li>
    <li><a href=""></a></li>
    <li><a href=""></a></li>
</ul>
```

## 6. Clases (.)

Agrega clases a los elementos.

**Sintaxis:** `elemento.nombreClase`

```html
<!-- div.container -->
<div class="container"></div>

<!-- p.text.center -->
<p class="text center"></p>

<!-- ul.menu>li.item*3 -->
<ul class="menu">
    <li class="item"></li>
    <li class="item"></li>
    <li class="item"></li>
</ul>

<!-- .wrapper -->
<div class="wrapper"></div>
```

## 7. IDs (#)

Agrega IDs a los elementos.

**Sintaxis:** `elemento#nombreID`

```html
<!-- div#header -->
<div id="header"></div>

<!-- section#about -->
<section id="about"></section>

<!-- nav#main-nav>ul>li*3 -->
<nav id="main-nav">
    <ul>
        <li></li>
        <li></li>
        <li></li>
    </ul>
</nav>

<!-- #container -->
<div id="container"></div>
```

## 8. Atributos []

Agrega atributos personalizados.

**Sintaxis:** `elemento[atributo="valor"]`

```html
<!-- a[href="#" title="Enlace"] -->
<a href="#" title="Enlace"></a>

<!-- input[type="text" placeholder="Nombre"] -->
<input type="text" placeholder="Nombre">

<!-- img[src="logo.png" alt="Logo"] -->
<img src="logo.png" alt="Logo">

<!-- div[data-id="123" data-role="admin"] -->
<div data-id="123" data-role="admin"></div>
```

## 9. Texto {}

Agrega contenido de texto dentro de los elementos.

**Sintaxis:** `elemento{texto}`

```html
<!-- p{Hola Mundo} -->
<p>Hola Mundo</p>

<!-- a{Click aquí} -->
<a href="">Click aquí</a>

<!-- h1{Título Principal}+p{Descripción} -->
<h1>Título Principal</h1>
<p>Descripción</p>

<!-- ul>li{Item $}*3 -->
<ul>
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
</ul>
```

## 10. Numeración ($)

Genera números incrementales automáticamente.

**Sintaxis:** `elemento{texto $}*número`

```html
<!-- ul>li.item-$*3 -->
<ul>
    <li class="item-1"></li>
    <li class="item-2"></li>
    <li class="item-3"></li>
</ul>

<!-- div#box$*4 -->
<div id="box1"></div>
<div id="box2"></div>
<div id="box3"></div>
<div id="box4"></div>

<!-- img[src="image$.jpg"]*3 -->
<img src="image1.jpg" alt="">
<img src="image2.jpg" alt="">
<img src="image3.jpg" alt="">
```

### Numeración con Ceros ($$)

```html
<!-- img[src="img$$.jpg"]*3 -->
<img src="img01.jpg" alt="">
<img src="img02.jpg" alt="">
<img src="img03.jpg" alt="">

<!-- div.item-$$$*3 -->
<div class="item-001"></div>
<div class="item-002"></div>
<div class="item-003"></div>
```

### Numeración Inversa (@-)

```html
<!-- ul>li.item-$@-*3 -->
<ul>
    <li class="item-3"></li>
    <li class="item-2"></li>
    <li class="item-1"></li>
</ul>
```

### Numeración desde un número específico (@N)

```html
<!-- ul>li.item-$@5*3 -->
<ul>
    <li class="item-5"></li>
    <li class="item-6"></li>
    <li class="item-7"></li>
</ul>
```

## 11. Abreviaciones HTML Predefinidas

Emmet incluye atajos para estructuras comunes.

```html
<!-- ! o html:5 -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    
</body>
</html>

<!-- a:link -->
<a href="http://"></a>

<!-- link:css -->
<link rel="stylesheet" href="style.css">

<!-- script:src -->
<script src=""></script>

<!-- input:text -->
<input type="text" name="" id="">

<!-- input:email -->
<input type="email" name="" id="">

<!-- input:password -->
<input type="password" name="" id="">

<!-- btn -->
<button></button>

<!-- table+ -->
<table>
    <tr>
        <td></td>
    </tr>
</table>

<!-- select+ -->
<select name="" id="">
    <option value=""></option>
</select>

<!-- form:post -->
<form action="" method="post"></form>
```

## 12. Elementos Implícitos

Emmet detecta automáticamente ciertos elementos según el contexto.

```html
<!-- .container (dentro de div por defecto) -->
<div class="container"></div>

<!-- ul>.item*3 -->
<ul>
    <li class="item"></li>
    <li class="item"></li>
    <li class="item"></li>
</ul>

<!-- table>.row*2>.cell*3 -->
<table>
    <tr class="row">
        <td class="cell"></td>
        <td class="cell"></td>
        <td class="cell"></td>
    </tr>
    <tr class="row">
        <td class="cell"></td>
        <td class="cell"></td>
        <td class="cell"></td>
    </tr>
</table>

<!-- select>.option*3 -->
<select name="" id="">
    <option class="option" value=""></option>
    <option class="option" value=""></option>
    <option class="option" value=""></option>
</select>
```

## 13. Lorem Ipsum

Genera texto de relleno automáticamente.

**Sintaxis:** `lorem` o `lorem[número]`

```html
<!-- p>lorem -->
<p>Lorem ipsum dolor sit amet...</p>

<!-- p>lorem10 -->
<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Mollitia, minima.</p>

<!-- ul>li*3>lorem5 -->
<ul>
    <li>Lorem ipsum dolor sit amet.</li>
    <li>Expedita quaerat mollitia cum totam.</li>
    <li>Voluptatem nisi consequuntur quod quisquam.</li>
</ul>
```

## Ejemplos Prácticos Completos

### Estructura de Navegación Completa

```
nav#main-nav.navigation>ul.menu>li.menu-item*5>a[href="#"]{Página $}
```

Resultado:
```html
<nav id="main-nav" class="navigation">
    <ul class="menu">
        <li class="menu-item"><a href="#">Página 1</a></li>
        <li class="menu-item"><a href="#">Página 2</a></li>
        <li class="menu-item"><a href="#">Página 3</a></li>
        <li class="menu-item"><a href="#">Página 4</a></li>
        <li class="menu-item"><a href="#">Página 5</a></li>
    </ul>
</nav>
```

### Formulario de Contacto

```
form#contact.contact-form>(.form-group>label{Campo $}+input:text)*3+button{Enviar}
```

Resultado:
```html
<form id="contact" class="contact-form">
    <div class="form-group">
        <label for="">Campo 1</label>
        <input type="text" name="" id="">
    </div>
    <div class="form-group">
        <label for="">Campo 2</label>
        <input type="text" name="" id="">
    </div>
    <div class="form-group">
        <label for="">Campo 3</label>
        <input type="text" name="" id="">
    </div>
    <button>Enviar</button>
</form>
```

### Galería de Imágenes

```
.gallery>(figure.gallery-item>img[src="img$.jpg" alt="Imagen $"]+figcaption{Descripción $})*6
```

Resultado:
```html
<div class="gallery">
    <figure class="gallery-item">
        <img src="img1.jpg" alt="Imagen 1">
        <figcaption>Descripción 1</figcaption>
    </figure>
    <figure class="gallery-item">
        <img src="img2.jpg" alt="Imagen 2">
        <figcaption>Descripción 2</figcaption>
    </figure>
    <!-- ... hasta 6 -->
</div>
```

### Tabla de Datos

```
table.data-table>(thead>tr>th{Columna $}*4)+(tbody>tr*3>td{Dato}*4)
```

Resultado:
```html
<table class="data-table">
    <thead>
        <tr>
            <th>Columna 1</th>
            <th>Columna 2</th>
            <th>Columna 3</th>
            <th>Columna 4</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Dato</td>
            <td>Dato</td>
            <td>Dato</td>
            <td>Dato</td>
        </tr>
        <tr>
            <td>Dato</td>
            <td>Dato</td>
            <td>Dato</td>
            <td>Dato</td>
        </tr>
        <tr>
            <td>Dato</td>
            <td>Dato</td>
            <td>Dato</td>
            <td>Dato</td>
        </tr>
    </tbody>
</table>
```

## Emmet para CSS

Emmet también funciona en CSS con abreviaciones útiles.

```css
/* m10 */
margin: 10px;

/* p20 */
padding: 20px;

/* w100p */
width: 100%;

/* h50p */
height: 50%;

/* df */
display: flex;

/* jcc */
justify-content: center;

/* aic */
align-items: center;

/* fz16 */
font-size: 16px;

/* c#fff */
color: #fff;

/* bg#000 */
background: #000;

/* bd1-s-#ccc */
border: 1px solid #ccc;

/* tac */
text-align: center;

/* dib */
display: inline-block;

/* pos:a */
position: absolute;

/* t0+r0+b0+l0 */
top: 0;
right: 0;
bottom: 0;
left: 0;
```

## Consejos Finales

1. **Practica regularmente**: Emmet se vuelve natural con la práctica
2. **Combina operadores**: Usa múltiples operadores juntos para estructuras complejas
3. **Usa en tu editor**: La mayoría de editores (VS Code, Sublime, Atom) soportan Emmet por defecto
4. **Experimenta**: Prueba diferentes combinaciones para encontrar tu flujo de trabajo
5. **Atajo de expansión**: Generalmente es `Tab` o `Ctrl+E` según tu editor

¡Con Emmet puedes escribir HTML hasta 10 veces más rápido!