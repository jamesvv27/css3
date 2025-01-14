# 2 - Media Queries

Anteriormente la World Wide Web solía ser accesada únicamente mediante navegadores de escritorio hasta ahora, donde han surgido nuevos dispositivos en los cuales se puede acceder a la Web, como celulares, tabletas, y consolas. Ahora, al realizar páginas web, es necesario considerar que pueden ser visualizadas desde un monitor o desde una pantalla portátil.
<br>
CSS ha tenido una forma para ofrecer diseños a distintos tipos de medios por un tiempo, esto se lograba usando el atributo `media` del elemento `link`:

```html
<link 
	href="style.css"
	media="screen"
	rel="stylesheet"
>
```

Aunque este enfoque tiene algunos errores, pues la lista de tipos es bastante amplia, y los dispositivos a los que van enfocados no los soportan.
La solución de CSS3 a este problema es utilizar media queries, definidas en el _[Modulo de Media Queries](http://www.w3.org/TR/css3-mediaqueries/)_. (Media Queries Module).
Estos queries extienden los media types proporcionando una sintaxis de consulta que permite utilizar estilos mucho más específicos para el dispositivo del usuario.

Los media queries dan la libertad de crear sitios web que sean independientes de dispositivos, dando así a los usuarios la mejor experiencia posible sin importar en dónde escojan visitar el sitio.

Esta característica se encuentra en estado de Recommendation del W3C, por lo que es considerado un estándar. Y ha sido implementado en navegadores principales desde Internet Explorer 9.

## Ventajas de los Media queries

Los media queries pueden detectar dispositivos basandose en sus atributos, por lo que ya no se requiren de scripts para este primer paso.

También permiten que hojas de estilo estén enfocadas directamente en un dispositivo; si un dispositivo con una pantalla pequeña se detecta, se aplicarán reglas CSS de acuerdo a ese tamaño de pantalla, saltandose elementos redundantes, usando tamaños de imagen disminuidos y haciendo el texto más claro.

## Sintaxis

Una consulta de medios asigna un parámetro (o serie de parámetros) que habilita reglas de estilo asociadas si el dispositivo utilizado para ver la página tiene propiedades que coincidan con ese parámetro. Es posible usar consultas de medios de 3 formas.

La primera es llamar a una hoja de estilos externa usando el elemento `link`:

```html
<link href="file" rel="stylesheet" media="logic media and (expression)">
```

La segunda forma es llamar a una hoja de estilos externa usando la directive `@import`

```css
@import url('file') logic media and (expression);
```

La tercera es usar media queries en un elemento de estilo implementado o en la misma hoja de estilos con la regla extendida  `@media`:

```css
@media logic media and (expression) { rules }
```

Adentrándonos un poco más en la sintaxis, tenemos al atributo `media`, que declara los media types a los cuales se les aplican los estilos, en la etiqueta `link` en HTML lo podemos ver de la siguiente manera:

```html
<link href="style.css" rel="stylesheet" media="screen">
```

Los valores más usuales para los media types son `screen` y `print`, y con esta sintaxis, podemos hacer una lista separada por comas para elegir varios media queries. Si se omite asignar un valor, el valor del media type será el predeterminado, el cual es `all`.<br>
Entonces, es por esto que, los siguientes ejemplos sun funcionalmente idénticos:

```css
@media all and (expression) { rules }
@media (expression) { rules }
```

El primer atributo nuevo para la regla `@media` es _`logic`_, esta palabra clave opcional puede tener como valor `only` o `not`:

```css
@media only media and (expression) { rules }
@media not media and (expression) { rules }
```

El valor `only` es útil por si queremos ocultar la regla para navegadores antiguos que **no** soporten la sintaxis, los navegadores que **sí** soporten la sintaxis ignorarán el valor `only`.<br>
El valor `not` es usado para negar la consulta, este se utiliza para que los estilos se apliquen si los parámetros que definimos **no** se cumplen.

Si usamos _`logic`_ o _`media`_ en nuestros queries, también tendremos que utilizar el operador `and` para combinarlos con el atributo obligatorio `expression`. Este atributo se usa para definir parámetros que ofrecen funcionalidades más allá del media type. A estos parámetros se les conoce como _media features_, y son indispensables para los media queries.

## Media Features

Los _media features_ son información sobre el dispositivo que se está usando para mostrar la página web: sus dimensiones, resolución, y demás. Esta información se usa para evaluar una _`expression`_, el resultado de esto determina las reglas de estilo que se aplicarán. Para ejemplificar, una _`expression`_ se puede interpretar como "aplicar ciertos estilos únicamente para los dispositivos con una resolución mayor a 480p".

En media queries, la mayoría de expresiones de los media features necesitan que se les pase un valor:

```cs
@media (feature: value) { rules }
```

Este valor se necesita para construir expresiones como la del ejemplo anterior. En algunas contadas excepciones, se puede omitir el valor del feature.

```css
@media (feature) { rules }
```

### Ancho y Alto

El media feature `width` describe el ancho del navegador (en el que se incluye la barra de scroll) para sistemas de escritorio.

```css
@media (width: 600px) { rules }
```

En este caso las reglas de estilo se aplican únicamente a navegadores que tengan como ancho exactamente 600px. A este feature le podemos agregar los prefijos `max-` y `min-`, que nos permiten probar con una anchura máxima o mínima.

```css
@media (max-width: 480px) { rules }
@media (min-width: 640px) { rules }
```

La primer consulta aplica las reglas a los navegadores que no tengan más de 480px de ancho, y la segunda indica que las reglas se aplicarán en navegadores que tengan por lo menos 640px de ancho.

En un ejemplo más práctico, colocaremos un encabezado decorativo para navegadores con ventanas más anchas:

```css
@media (min-width: 400px) {
	h1 { background: url('landscape.jpg') }
}
```

Esta consulta de medios comprueba que la ventana gráfica tenga una anchura de al menos 400px y le aplica una imagen de fondo al elemento `h1` en caso de que lo anterior se cumpla.

El media feature `height` funciona de la misma manera, solo que este se dirige a navegadores basándose en su altura en lugar de su anchura. La sintaxis es la misma que con `width` y también permite usar los prefijos `max-` y `min-`:

```css
@media (height: value) { rules }
@media (max-height: value) { rules }
@media (min-height: value) { rules }
```

### Pixel Ratio

A grandes rasgos, una unidad de pixel (px) de CSS es una medida de un pixel individual en la pantalla de la computadora- si la ventana gráfica del navegador tiene como ancho 1024 pixeles y a un elemento le damos un ancho de 1024px, esperaríamos que el elemento cubra toda la longitud horizontal de la ventana. Muchos dispositivos actuales cuentan con resoluciones que harían que un elemento con un ancho de 1024 pixeles luzca pequeño y difícil de leer.

Para esto, los dispositivos cuentan con un pixel virtual CSS distinto a los pixeles físicos del dispositivos, esto con el fin de que dispositivos como smartphones y tablets puedan hacer zoom a los contenidos de las páginas web.<br>
A la relación de pixeles físicos a pixeles CSS se le conoce como _device pixel ratio - DPR_ (relación de pixeles del dispositivo).

Por ejemplo, si un dispositivo tiene un DPR de 2, esto significa que un pixel de CSS será equivalente a 4 pixeles físicos- 2 verticales y 2 horizontales.<br>
Un dispositivo con una resolución física de 640x1136 y un DPR de 2, tendráuna resolución CSS de 320x568.

En CSS podemos usar el media feature llamado `resolution` que nos permite dirigirnos a dispositivos basándonos en su DPR:

```css
@media media and (resolution: value) { rules }
```

El valor de `resolution` debe ser un número ocon una unidad de resolución: _dots per inch (DPI)_, _dots per centimeter (DPCM)_, o _dots per pixel (DPPX)_. Si queremos aplicar una regla a dispositivos que tengan un DPR de 1.5, usamos esto:

```css
@media (resolution: 1.5dppx) { rules }
```

También podemos detectar relaciones de pixel mínimas y máximas:

```css
@media (max-resolution: number) { rules }
@media (min-resolution: number) { rules }
```

Esto hace que colocar imagenes de fondo de alta resolución a navegdores con mayor densidad de pixeles sea más sencillo.

```css
E { background-image: url('image-lores.png'); }
@media (min-resolution: 1.5dppx) {
	background-image: url('image-hires.png');
	background-size: 100% 100%;
}
```

La primer regla (_`E`_) indica que los navegadores con relación de pixeles "estándar" o de baja resolución usarán la imagen `image-lores.png`, mientras que los dispositivos con un DPR de al menos 1.5 usarán la imagen `image-hires.png`.

### Ancho y Alto del Dispositivo

Los media features `width` y `height` se refieren a las dimensiones de la ventana gráfica del navegador, pero no al tamaño de la pantalla del dispositivo. Para dirigirse al tamaño de la pantalla física, podemos usar las propiedades `device-width` y `device-height` con sus prefijos `min-` y `max-`. Para poner en perspectiva porqué usaremos estas propiedades, el media feature `width` se mide en pixeles CSS, mientras que `device-width` se mide en pixeles físicos.<br>
Para hacer el contenido legible en pantallas pequeñas, ambas dimensiones deben de coincider, esto se puede hacer añadiendo la etiqueta _meta viewport_ en la cabeza del documento de esta forma:

```html
<meta 
	name="viewport" 
	content="width=device-width"
>
```

Cuando esta etiqueta con estos valores está presente en el `head` de una página, los navegadores móviles entran en un "modo móvil", en el que la ventana gráfica se ajusta a las dimensiones adecuadas para ese dispositivo.

La ventana gráfica de un navegador en un dispositivo móvil suele ser del mismo tamaño de la pantalla, por lo que ambas dimensiones son equivalentes. En navegadores de escritorio lo más óptimo será ajustar los contenidos al tamaño de la ventana gráfica en vez de al tamaño de la pantalla.

### Orientación

Para optimizar las páginas para visualización tanto horizontal como vertical, el media feature adecuado es el de `orientation`:

```css
@media (orientation: value) { rules }
```

_`value`_ puede ser una de dos opciones: `landscape` o `portrait`. El valor `landscape` se aplica cuando el ancho del navegador es mayor a la altura, y el valor `portrait` se aplica cuando el ancho es menor a la altura.<br>
Así pues, `orientation` puede ser bastante útil para dispositivos móviles que el usuario pueda rotar como teléfonos y tabletas.

Por ejemplo, podemos usar `orientation` para mostrar un menú de navegación horizontalmente o verticalmente, dependiendo de la orientación del navegador del usuario:

```css
ul { overflow: hidden; }
li { float: left; }
@media (orientation: portrait) {
	li { float: none; }
}
```

Por defecto, el valor `float` de los elementos `li` es de `left`, haciendo así que se apilen de manera horizontal. Si la página se visualiza en orientación `portrait`, el valor `float` se elimina, y los elementos se apilan de forma vertical.

### Relación de aspectos

Se pueden crear queries que se aplican cuando alguna relación de ancho a alto se cumple. Se puede usar `aspect-ratio` para comprobar la relación de aspecto del navegador, o `device-aspect-ratio` para ver la relación de aspecto del dispositivo:

```css
@media (aspect-ratio: horizontal/vertical) { rules }
@media (device-aspect-ratio: horizontal/vertical) { rules }
```

Los valores _`horizontal`_ y _`vertical`_ son enteros positivos que representan la relación del ancho y el alto de la pantalla del dispositivo respectivamente.

También podemos usar las variaciones `min-` y `max-` con `aspect-ratio` y `device-aspect-ratio`. En el siguiente ejemplo de código las reglas de la consulta se aplican a cualquier elemento que tenga una relación de aspecto mayor a 16:9:

```css
@media (min-device-aspect-ratio: 16/9) {...}
```

## Varios Media Features

Se pueden concatenar varios queries juntas en el mismo media type añadiendo expresiones con el operador `and`:

```css
@media logic media and (expression) and (expression) { rules }
```

Esta sintaxis comprueba que ambas expresiones se cumplan antes de aplicar las reglas seleccionadas. Por ejemplo, para verificar una pantalla angosta en un dispositivo con una relación de aspecto no mayor a 15:10, se usa la siguiente consulta:

```css
@media (max-device-aspect-ratio: 15/10) and (max-width: 800px) {...}
```

También se puede usar una expresión condicional añadiendo queries extra en una lista separada por comas:

```css
@media logic media and (expression), logic media and (expression) { rules }
```

En esta sintaxis, las reglas se aplican cuando cualquiera de los casos sea verdadero.

## Desarrollo Web Mobile-First

La mejor práctica para construir sitios web emplea un método conocido como _mobile-first development_, en el que empezamos desarrollando para pantallas más pequeñas antes de añadir los elementos más grandes y complejos.<br>
El motivo por el cual este método se adoptó fue por la manera en la que algunos navegadores cargan elementos de las páginas web, como las imágenes, que se incluyen en las hojas de estilo.

El método mobile-first para crear páginas web comienza por crear una hoja de estilos básica, que se aplica a todos los navegadores, incluyendo los móviles, y después añadir progresivamente elementos y características para usuarios con pantallas más grandes, usando una consulta de medios con el feature `min-width`:

```css
@media (min-width: 600px){
	E { background-image: url('huge-image.jpg'); }
}
```

En este caso, la imagen de fondo nunca se carga en dispositivos con pantallas más pequeñas, esto se puede extrapolar cargando hojas de estilo diferentes:

```html
<link 
	href="basic.css" 
	rel="stylesheet"
>
<link 
	href="desktop.css" 
	rel="stylesheet" 
	media="(min-width: 600px)"
>
```

## Soporte de navegadores para Media Queries:

<table>
	<tr>
		<td>
		</td>
		<td>
			Chrome
		</td>
		<td>
			Firefox
		</td>
		<td>
			Safari
		</td>
		<td>
			IE
		</td>
	</tr>
		<tr>
		<td>
			Media queries
		</td>
		<td>
			✓
		</td>
		<td>
			✓
		</td>
		<td>
			✓
		</td>
		<td>
			✓
		</td>
	</tr>
</table>
