# 5 - Fuentes Web

Una de las características que regresó a CSS3 fue la posibilidad de especificar fuentes que no existen en el sistema del usuario--utilizando el método `@font-face`.

## La regla `@font-face`

Para mostrar fuentes web en páginas, primero es necesario definirlas usando la regla `@font-face`. Esta regla deja en claro el nombre y tipo de la fuente y le brinda al navegador la ubicación del archivo. La sintaxis básica es:

```css
@font-face {
	font-family: FontName;
	src: local('fontname'), url('/path/filename.otf') format('opentype');
}
```

La propiedad `src` le indica al navegador la ubicación del archivo de fuente. Esta propiedad puede tener algunos valores distintos, estos son: `local`, que usa el nombre del archivo de fuente para revisar si la fuente ya se encuentra instalada en la computadora del usuario; y `url` provee una ruta de la fuente si no se encuentra disponible localmente. También podemos utiliazr `format` para especificar el tipo de fuente.

Para usar la fuente definida, solo hay que llamar su nombre en la pila de fuentes:

```css
E { font-family: FontName; }
```

Vamos a ver un ejemplo a un elemento `<h1>`:

```css
@font-face {
	font-family: ChunkFive;
	src: local('ChunkFive'), url('ChunknFive.woff') format ('woff');
}

h1.webfont { 
	font-family: ChunkFive, sans-serif; 
}
```

Primero le damos un nombre a la fuente, a la cual llamamos `ChunkFive`. Después le damos valores a la propiedad `src` para verificar primero si se encuentra disponible la fuente en el sistema del usuario, de lo contrario usamos una ruta al archivo de la fuenta. Por último, asignamos como `woff` el valor del `format`.

Al momento de usar la regla, en la última línea, la ajustamos para que se aplique a todos los elementos `<h1>` con clase `webfont`.

### Definiendo Tipos de fuente distintas

La sintaxis `@font-face` define solo un tipo de fuente--una sola permutación de tamaño, peso, etc. Si deseamos usar un tipo de fuente, como una con mayor peso, o cursivas, tenemos que definir cada tipo de fuente individualmente. Para hacer esto, debemos reutilizar el mismo nombre y añadir descriptores extra a la regla `@font-face`:

```css
@font-face {
	font-family: 'Gentium Basic';
	src: url('GenBasR.woff') format('woff');
}
@font-face {
	font-family: 'Gentium Basic';
	font-style: italic;
	src: url('yGenBasI.woff') format('woff');
}
h1 { 
	font-family: 'Gentium Basic', sans-serif;
}
```

Este estilo se le aplica al siguiente marcado:

```html
<h1>
	<em>I knew him, Horatio</em>
</h1>
```

### Tipos de Fuente de Adevis y de A mentis

Algo a considerar a la hora de usar fuentes web es que se debe proporcionar un enlace a un archivo apropiada para cada tipo de fuente distinto que deseemos usar. De lo contrario, los navegadores intentarán recrear el tipo de fuente artificialmente, y esto a menudo sale mal:

```css
@font-face {
	font-family: 'Gentium Basic';
	src: url('GenBasR.woff') format('woff');
}
h1 {
	font-family: 'Gentium Basic', sans-serif;
	font-style: italic;
}
```

En el ejemplo anterior, se proporcionó únicamente el tipo de fuente normal, y al momento de aplicarlo al elemento `<h1>` se usó el estilo de fuente en cursiva. Esto provoca que el navegador muestre automáticamente de forma distorsionada un estilo en cursiva.

## Sintaxis `@font-face` "a prueba de errores".

Debido a los posibles errores, es necesario contar con soluciones alternativas para asegurarse que el `@font-face` funcione correctamente en todos los navegadores.

Veremos algunos de los errores que soluciona.

### Usando Fuentes locales

El valor `local()` de la propiedad `src` se usa para revisar si un  usuario ya cuenta con la fuente definida instalada en su sistema--en caso de que sí, la copia local se puede usar en lugar de descargar una nueva copia.

La pega es que `local()` no es soportado en versiones de Internet Explorer anteriores a la 9.

### Formatos de Fuente

Este problema se relaciona con el formato de propiedad _Embedded OpenType_ (EOT) de Microsoft, pues es la única fuente soportada en Internet Explorer 8 y versiones anteriores. Y en IE9 la regla `@font-face` falla cuando el navegador está ajustado en modo de compatibilidad.

### Ahora sí, la sintaxis "A prueba de errores"

Para que la fuente de elección se muestre en todos los navegadores, en todas las plataformas, usaremos el código en este formato:

```css
@font-face {
	font-family: 'Gentium Basic';
	src: url('GenBkBasR.eot');
	src: url('GenBasR.eot?#iefix') format('embedded-opentype'),
	url('GenBkBasR.woff') format('woff'),
	url('GenBkBasR.ttf') format('truetype');
}
```

La primer fuente especificada es la EOT para Internet Explorer 8 y versiones anteriores. La siguiente regla contiene el hint opcional `format()`. La fuente EOT necesita incluirse nuevamenente para el problema de compatibilidad de IE9.
<br>
Después, el formato WOFF se define para la gran mayoría de navegadores, seguido por el formato TTF para navegadores antiguos.

## Autoridad de licencia de Fuentes para uso Web

Varios propieterios de fuentes prohíben que sus fuentes sean implementadas en páginas web utilizando `@font-face`. Esto es debido a que las fuentes OpenType o TrueType son fáciles de encontrar y descargar y pueden ser usadas de forma ilegal en aplicaciones web online y offline.

La mejor práctica es revisar que la fuente a utilizar tenga una licencia que permita explícitamente su uso en implementación web.

## Un ejemplo de la vida real

Vamos a ver un ejemplo con tres familias de fuente distintas con formato de fuente WOFF:

```css
@font-face {
	font-family: 'CartoonistHand';
	src: url('CartoonistHand.woff') format('woff');
}
@font-face {
	font-family: 'CartoonistHand';
	font-style: italic;
	src: url('CartoonistHand-Italic.woff') format('woff');
}
@font-face {
	font-family: 'CartoonistHand';
	font-weight: bold;
	src: url('CartoonistHand-Bold.woff') format('woff');
}
@font-face {
	font-family: 'ChunkFiveRegular';
	src: url('Chunkfive.woff') format('woff');
}
@font-face {
	font-family: 'AirstreamRegular';
	src: url('Airstream.woff') format('woff');
}
.font-face h1 { font-family: ChunkFiveRegular, sans-serif; }
.font-face h2 { font-family: AirstreamRegular, cursive; }
.font-face p { font-family: CartoonistHand, sans-serif; }
```

El marcado utilizado es el siguiente:

```html
<h1>Great Expectations</h1>
<h2>By Charles Dickens</h2>
<p>
	My father's family name being <em>Pirrip</em>, and my Christian name
	<em>Philip</em>, my infant tongue could make of both names nothing longer or
	more explicit than <strong>Pip</strong>. So, I called myself <strong>Pip
	</strong>, and came to be called <strong>Pip</strong>.
</p>
```

## Control de la carga de Fuentes

Las fuentes web se cargan como activos externos y se deben descargar por el navegador antes de que sean mostrados. Antes de que el archivo se cargue, ninguna fuente será visible en los elementos a los que se aplique la fuente.

Varios proveedores FaaS ofrecen formas para solventar este problema utilizando archivos de configuración, si usamos nuestas propias fuentes, podemos usar el Web Font Loader Library _`(https://github.com/typekit/webfontloader/)`_, que ofrece un evento de sistema que permite controlar la apariencia de la página de forma dinámica mientras las fuentes se cargan.

## Más propiedades de Fuente

El módulo Web Fonts de CSS3 también trajo dos propiedades extra que fueron propuestas para CSS2.
<br>

### `font-size-adjust`

La pega de usar pilas de fuentes en CSS es que las fuentes pueden variar bastante en tamaño, y puede que distintas fuentes luzcan más grandes o pequeñas en un mismo tamaño ajustado. Para prevenir esto, la propiedad `font-size-adjust` permite alterar dinámicamente la propiedad `font-size` para tener una apariencia consistente sin importar qué fuentes se utilicen de la pila.

```css
E { font-size-adjust: number; }
```

El valor `number` es la proporción de la altura que ocupa una _x_ minúscula.
<br>
Si una fuente tiene como altura 16px, y la altura de su _x_ minúscula es la mitad de eso (8px), su relación de altura es de 0.5 (8 dividido entre 16):

```css
p { font-size-adjust: 0.5; }
```

Así nos aseguramos que sin importar la fuente mostrada, la altura del carácter _x_ siempre sea la misma.

### `font-stretch`

Algunas familias de fuentes contienen variantes, y la propiedad `font-stretch` da un acceso a estas. Su sintaxis es la siguiente:

```css
E { font-stretch: keyword; }
```

El valor `keyword` puede ser cualquiera de los siguientes: `normal`, `ultra-condensed`, `extra-condensed`, `condensed`, `semi-condensed`, `semi-expanded`, `expanded`, `extra-expanded`, y `ultra-expanded`. Cada keyword se relaciona a una variante de fuente dentro de una familia.

## Features OpenType

Los formatos de fuente OpenType tienen un rango de variaciones.

### Habilitando las Font Features

Varios navegadores han implementado una propiedad que permite explorar las features extra proporcionadas por OpenType y otros formatos similares. La nueva propiedad se llama `font-feature-settings` y su sintaxis es:

```css
E { font-feature-settings: "parameters"; }
```

El valor _`parameters`_ es una serie de cadenas que contienen códigos para cada feature, además de un valor binario opcional para habilitar o desactivar la feature.

```css
E { font-feature-settings: "dlig" on; }
```

Para deshabilitar una feature, se usa el valor binario alternativo `off`.

```css
E { font-feature-settings: "dlig" off; }
```

Es posible colocar más de un parámetro con una lista separada por comas.

```css
E { font-feature-settings: "liga", "tnum" off; }
```

### Propiedades Font Feature

Las features individuales habilitadas o deshabilitadas por `font-feature-settings` también están especificadas para ser implementadas como propiedades individuales, conocidas como las propiedades `font-variant-*`. Por ejemplo:

```css
E { font-variant-ligatures: no-discretionary-ligatures; }
```

Otra propiedad relacionada es `font-kerning` que controla el kerning de una fuente. Con calores como `normal`, `none` y `auto`.

```css
E { font-kerning: auto; }
```

## Soporte en navegadores para los Web Fonts:

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
			@font-face
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
	</tr>
	<tr>
		<td>
			font-size-adjust
		</td>
		<td>
			✗
		</td>
		<td>
			✓
		</td>
		<td>
			✗
		</td>
		<td>
			✗
		</td>
	</tr>
	<tr>
		<td>
			font-stretch
		</td>
		<td>
			✗
		</td>
		<td>
			✓
		</td>
		<td>
			✗
		</td>
		<td>
			✓
		</td>
	</tr>
		<tr>
		<td>
			font-feature-settings
		</td>
		<td>
			✓
		</td>
		<td>
			✓
		</td>
		<td>
			✗
		</td>
		<td>
			IE10
		</td>
	</tr>
		<tr>
		<td>
			font-variant-*
		</td>
		<td>
			✓
		</td>
		<td>
			✗
		</td>
		<td>
			✓
		</td>
		<td>
			✗
		</td>
	</tr>
</table>