# 4 - Pseudo-clases y Pseudo-elementos

Las pseudo-clases y pseudo-elementos son selectors que actúan de acuerdo a la información de los elementos que recae fuera del árbol del documento.

En CSS3 podemos seleccionar elementos hijos sin que estos tengan clases innecesarias o atributos redundantes; al siguiente ejemplo le podemos aplicar reglas de estilo:

```html
<ul>
	<li>Lorem ipsum</li>
	<li>Lorem ipsum</li>
	<li>Lorem ipsum</li>
	<li>Lorem ipsum</li>
</ul>
```

La ventaja de los nuevos selectors es que si se añaden nuevos elementos al marcado, los nombres de las clases no se tienen que actualizar para mantener el orden.

## Pseudo-clases estructurales

Una pseudo-clase nos da una forma de seleccionar un elemento basado en información no especificada en el árbol del documento. Existen varios subtipos, y el más común es el de Pseudo-clase estructural (_structural pseudo-class_).

En el siguiente marcado:

```html
<div>
	<p>Lorem ipsum.</p>
	<p>Lorem ipsum.</p>
</div>
```

El primer elemento `<p>` es el primer hijo del elemento `<div>` , además de eso, no hay ninguna otra forma de información que permita aplicar una regla solo a ese elemento. Es por esto que CSS2 introdujo la pseudo-clase `:first-child`:

```css
E:first-child {...}
```

Esta pseudo-clase nos permite hacer una selección basada en información que existe pero que no está visible como un atributo del elemento.
<br>
CSS3 extiende las posibilidades de las pseudo-clases con la introducción de 11 pseudo-clases estructurales nuevas.

### Pseudo-clases `:nth-*`

Cuatro de las nuevas pseudo-clases se basan en un valor iterativo o contado para encontrar la posición de un elemento en el árbol del documento.

La sintaxis es `:nth-*`, y la sintaxis básica de las pseudo-clases `:nth-*` es algo simple.
Por defecto, `n` representa un número que inicia en 0 y se incrementa en 1. Otro entero se le puede pasar como un multiplicador.
<br>
Por ejemplo, al colocar `2n` contaremos a múltiplos de 2 (2, 4, 6...), con `3n` contaremos múltiplos de 3 (3, 6, 9...):

```css
E:nth-*(n) {...}
E:nth-*(2n) {...}
E:nth-*(3n) {...}
```

En el primer ejemplo, todos los elementos de tipo _`E`_ se seleccionarán, en el segundo, se seleccionarán todos los **segundos** elementos _`E`_, y el último ejemplo seleccionará cualquier **tercer** elemento de tipo _`E`_.

Además de esto, se pueden utilizar operadores matemáticos (+), y (-). De este modo, `2n+1` seleccionaría todos los múltiplos de 2 más 1 (1, 3, 5...), y `3n-1` selecciona todos los múltiplos de 3 menos 1 (2, 5, 8...).
Si colocamos `n+1`, se seleccionarán todos los elementos a excepción del primero (2, 3, 4, 5...):

```css
E:nth-*(n+1) {...}
E:nth-*(2n+1) {...}
E:nth-*(3n-1) {...}
```

También podemos usar valores por palabra, `even` y `odd`, y podemos usar estos para seleccionar los elementos de orden par o impar respectivamente:

```css
E:nth-*(even) {...}
E:nth-*(odd) {...}
```

También se puede utilizar `0n` como valor. Este puede ser bastante útil si se usa junto a un operador matemático, de este modo, ambos de los siguientes ejemplos darían el mismo resultado; seleccionar únicamente el tercer elemento de la lista:

```css
E:nth-*(0n+3) {...}
E:nth-*(3) {...}
```

### `nth-child()` y `nth-of-type()`

Las pseudo-clases estructurales permiten seleccionar elementos basados en su posición en el árbol del documento en relación a su elemento padre (`-child`), o su clasificación (`of-type`).

Los ejemplos más simples de estas pseudo-clases son `:nth-child()` y `:nth-of-type()`. El primero, `:nth-child()`, selecciona un elemento basado en su posición en un conteo de el número total de hijos en su elemento padre; `:nth-of-type()` basa su conteo no en el número total de hijos,  sino en el de el tipo de elemento específicado.

```css
E:nth-child(n) {...} /* 1 */
E:nth-of-type(n) {...} /* 2 */
E:nth-child(2n) {...} /* 3 */
E:nth-of-type(2n) {...} /* 4 */
```

En este ejemplo, las reglas 1 y 2 son equivalentes porque el valor de conteo (`n`) es el predeterminado; ambos seleccionarán todos los elementos hijos de tipo _`E`_.
<br>
La diferencia recae en los siguientes ejemplos. En el 3, `nth-child(2n)` selecciona todos los elementos de tipo _`E`_ de un conteo que incluye a todos los elementos hermanos, pero solo en donde los elementos tengan numeración par. En el 4, `nth-of-type(2n)` selecciona a todos los elementos de tipo _`E`_ con numeración par de un conteo que incluya solo a esos números.

Usaremos el siguiente ejemplo para demostrar la diferencia entre estas pseudo-clases.

```html
<div>
	<h2>The Picture of Dorian Gray</h2>
	<p>The artist is the creator...</p>
	<p>To reveal art and conceal the artist...</p>
	<p>The critic is he who can translate...</p>
</div>
```

En el ejemplo usaremos la siguiente hoja de estilos:

```css
p:nth-child(2n) { 
		font-weight: bolder ;
	 	}
	 	
p:nth-of-type(2n) { 
		font-weight: bolder; 
		}
```

En el marcado de ejemplo, el elemento `<div>` tiene un total de cuatro elementos hijos, un `<h2>` y tres `<p>`. El selector `:nth-child(2n)` en la primer línea aplica negritas a cada segundo elemento hijo (en este caso, al primer y al tercer elemento `<p>`).
<br>
Por otro lado, el selector `:nth-of-type(2n)` ignora el `<h2>` y aplica negritas a cada segunda instancia de los tres elementos `<p>`, y en el marcado lo aplicaría únicamente al segundo párrafo.

### `nth-last-child()` y `nth-last-of-type()`

Estas pseudo-clases aceptan los mismos argumentos que `:nth-child()` y `nth-of-type()`, solo que se cuentan desde el último elemento hacia el primero.

### `first-of-type`, `last-child` y `:last-of-type`

`first-of-type` aplica las reglas únicamente al elemento que es el primer hijo del nombre del tipo de su padre.
<br>
Por otro lado, `:last-child` y `last-of-type`, seleccionan el último elemento hijo, o el último elemento hijo del tipo del padre, respectivamente.

Veamos el siguiente marcado:

```html
<div>
	<h2>Wuthering Heights</h2>
	<p>I have just returned...</p>
	<p>This is certainly...</p>
	<p>In all England...</p>
	<h3>By Emily Bronte</h3>
</div>
```

Aquí usaremos `:first-child` y `:last-child`:

```css
:first-child { 
	text-decoration: underline;
	 }

:last-child { 
	font-style: italic;
	 }
```

Lo que ocurrirá es que al elemento `<h2>` se le aplicará un subrayado, pues es el primer hijo del `<div>`. Y el último hijo del `<div>` es el elemento `<h3>`.

Si por el contrario, aplicamos el estilo con  los selectors `:first-of-type` y `last-of-type`:

```css
:first-of-type { 
	text-decoration: underline;
	 }
	 
:last-of-type { 
	font-style: italic;
	 }
```

Los elementos `<h2>`, `<h3>` y el primer `<p>` estarán subrayados. Esto es porque son la primer instancia de ese tipo de elemento. Y de igual forma, estarán en cursiva porque así como son el primer elemento de su tipo, también son el último, por lo que se aplican ambas reglas.

### `:only-child` y `only-of-type`

Estas dos pseudo-clases son usadas para seleccionar elementos en el árbol del documento que tengan un padre, pero sin elementos hermanos (`:only-child`) o sin hermanos del mismo tipo (`:only-of-type`).

En el siguiente ejemplo, usaremos las siguientes reglas de estilo:

```css
p:only-of-type { 
	font-style: italic;
	 }
	 
p:only-child { 
	text-decoration: underline;
	 }
```

y las aplicaremos a este marcado:

```html
<h2>On Intelligence</h2>
<p>Arthur C. Clarke once said:</p>
<blockquote>
	<p>It has yet to be proven that intelligence has any survival value.</p>
</blockquote>
```

Ambos elementos `<p>` son los únicos elementos de su tipo en su nivel en el árbol del documento, por lo que la regla `:only-of-type` selecciona a ambos y les aplica letra cursiva.
Por otra parte, el elemento `<p>` dentro del `<blockquote>`, también es el único hijo en su nivel, y también está sujeto a la regla `only-child` que le aplica el subrayado.

## Otras Pseudo-clases

CSS3 introduce un número de pseudo-clasess que permiten seleccionar elementos basándose en otros criterios. Como elementos de UI, o un selector inverso que actúe en función de lo que un elemento **no** sea.

### `:target`

Los sitios no solamente se enlazan entre páginas, también brindan enlaces internos hacia elementos específicos. Una URI puede contener una referencia a un ID único, o un anchor nombrado.
<br>
La pseudo-clase `:target` permite aplicar estilos al elemento cuando el URI de referencia se haya visitado.

### `:empty`

La pseudo-clase `:empty` selecciona un elemento que no tenga hijos, ni nodos de texto. Tomando en cuenta este marcado:

```html
<tr>
	<td></td>
	<td>Lorem ipsum</td>
	<td>
		<span></span>
	</td>
</tr>
```

Al aplicarle esta regla:

```css
td:empty { 
	background-color: rgb(255, 0, 0); 
	}
```

Esta solo se aplicará al primer elemento `<td>`, pues los otros dos contienen un nodo de texto y un elemento hijo, respectivamente.

### `:root`

La psuedo-clase `:root` selecciona el primer elemento en un árbol de documento, lo cual es bastante útil si vamos a añadir una hoja de estilos a documentos XML.  Hay que considerar que, en HTML, por otro lado, el elemento raíz siempre será el `<html>`.

### `:not()`

La pseudo-clase de negación `:not()` selecciona todos los elementos a excepción de los que se les pasa como valor:

```css
E :not(F) {...}
```

Esta regla selecciona a todos los hijos del elemento _`E`_ a excepción de los de tipo _`F`_. Por ejemplo, para darle color a todos los elementos hijos inmediatos de un `<div>`, excluyendo a los elementos `<p>`, usamos lo siguiente:

```css
div > :not(p) { color: rgb(255, 0, 0); }
```

Veamos el siguiente marcado de ejemplo:

```html
<div>
	<p>Lorem ipsum dolor sit amet...</p>
	<p>Nunc consectetur tempor justo...</p>
	<p>Nunc porttitor malesuada cursus...</p>
</div>
```

Si, por ejemplo, queremos escribir en cursiva a todos los elementos hijos `<p>` a excepción del primero, podemos usar la siguiente regla:

```css
p:not(:first-child) { 
		font-style: italic; 
		}
```

El valor que se le pase a `:not()` debe ser un selector simple. Combinators como + y >, y los pseudo-elementos no son valores válidos.

### Estado de Elementos UI

Los elementos relacionados a formularios y entradas de usuario pueden tener varios estados; pueden estar desactivados o palomeados, por ejemplo, al ajustar los siguientes atributos:

```html
<textarea 
	disabled="disabled"
></textarea>
<input 
	checked="checked" 
	type="checkbox"
>
```

En CSS3 podemos aplicar reglas a estos elementos basándonos en su estado actual:

```css
:checked {...}
:disabled {...}
:enabled {...}
```

### Pseudo-clases de Constraint Validation

HTML5 introdujo un nuevo API para la validación de formularios, conocido como el _API constraint validation_, que puede ser utilizado para determinar si ciertos requerimientos son cumplidos antes de que los contenidos del formulario se envíen al servidor. Este API trae con esta funcionalidad un nuevo grupo de pseudo-clases.

Con el constraint validation, un campo de un formulario puede hacerse obligatorio con el uso del atributo `required`:

```html
<input 
	required
	type="text" 
	>
```

Se peuden estilizar elementos dependiendo de si son requeridos u opcionales utilizando las pseudo-clases del mismo nombre de los atributos:

```css
:required {...}
:optional {...}
```

Cada campo de un formulario puede estar en uno de dos estados de validación: ya sea `valid` o `invalid`, y cada estado viene con una pseudo-clase. Hay que considerar que si no se especifica, un campo de un formulario, es válido por defecto:

```css
:valid {...}
:invalid {...}
```

Algunos elementos HTML5 pueden tener un rango permitido de valores en función de los atributos `min` y `max`. Se pueden estilizar estos elementos dependiendo de si el valor actual está dentro o fuera del rango establecido con las siguientes pseudo-clases:

```css
:in-range {...}
:out-of-range {...}
```

## Pseudo-elementos

Al igual que las pseudo-clases, los pseudo-elementos brindan información que no está especificada en el árbol del documento. Mientras que las pseudo-clases utilizan condiciones "invisibles", los pseudo-elementos van más allá y permiten aplicar estilos a elementos que no existen en el árbol.

En CSS2, los cuatro pseudo-elementos son `:first-line` y `:first-letter`, que seleccionan sub-elementos en nodos de texto, y `:after` y `:before`, que permiten aplicar estilos al principio, y al final de elementos existentes. CSS3 no introduce nuevos pseudo-elementos aunque si provee de una nueva sintaxis para diferenciarlos de las pseudo-clases. En CSS3, los pseudo-elementos cuentan con un prefijo `::`, del siguiente modo:

```css
::first-line {...}
::first-letter {...}
::after {...}
::before {...}
```

### El pseudo-elemento `::selection`

Las primeras versiones del modulo de Selectors de CSS3 incluían la definición de un pseudo-elemento `::selection`. Este pseudo-elemento se usa para aplicar reglas a un elemento que el usuario ha seleccionado en el navegador, como por ejemplo, una porción de un nodo de texto:

```css
::selection {...}
```

Solo un número limitado de propiedades se pueden aplicar con `::selection`, las cuales son: `color`, `background-color` y `background`. Al utilizar `::selection` podemos hacer algo como lo siguiente:

```css
p::selection {
	background-color: rgb(0, 0, 0);
	color: rgb(255, 255, 255);
}
```

Al seleccionar con el cursor el texto del párrafo, los colores serán blanco y negro en lugar de blanco y azul.

## Soporte en navegadores para Selectors de DOM y de Atributos:

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
			Pseudo-clases estructurales
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
			:target
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
	<tr>
		<td>
			:empty
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
	<tr>
		<td>
			:root
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
	<tr>
		<td>
			:not()
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
	<tr>
		<td>
			Pseudo-elementos
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
	<tr>
		<td>
			Estados de elementos de UI
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
	<tr>
		<td>
			Constraint validation
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
			IE10*
		</td>
	</tr>
	<tr>
		<td>
			::selection
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