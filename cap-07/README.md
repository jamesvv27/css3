# 7 - Columnas múltiples

## Métodos de disposición de columnas

Es posible dividir los contenidos de una páginas en columnas utilizando dos métodos, ya sea ajustando un número de columnas específico, o haciendo que de forma dinámica, ajustando el ancho de las columnas, se calcule el número de columnas que pueden encajar en el navegador.

### `column-count`

La forma más simple de dividir los contenidos en columnas equitativamente distribuidas es usando la propiedad `column-count`:

```css
E { column-count: columns; }
```

El elemento _`E`_ es el padre del contenido que deseamos dividir, y el valor de _`columns`_ es un entero que define el número de columnas.

El siguiente es un ejemplo en el que dos párrafos que contienen el mismo texto se dividen en un número distinto de columnas:

```css
div[class*='-2'] {
	column-count: 2;
}
div[class*='-3'] {
	column-count: 3;
}
```

Estas reglas de estilo se aplicaron al siguiente marcado:

```html
<div class="columns-2">
	<p>A young man...</p>
</div>
<div class="columns-3">
	<p>A young man...</p>
</div>
```

### Columnas dinámicas: `column-width`

El segundo método para dividir columnas es bastante adecuado para diseños flexibles. Podemos usar la peopiedad `column-width` para especificar el ancho de cada columna, y el navegador llenará al elemento padre con la mayor cantidad de columnas posible. Su sintaxis es:

```css
E { column-width: length; }
```

Al igual que con `column-count`, _`E`_ es el elemento padre del elemento que queremos dividir en columnas. Solo que el valor `length` se trata de una unidad de longitud, ya sea _px_, _em_ o un porcentaje. Veamos el siguiente ejemplo:

```css
div {
	column-width: 150px;
}
```

```css
.columns {
	column-width: 150px;
	width: 710px;
}
```

El navegador crea cuatro columnas para llenar al elemento padre. Las columnas se redimensionan ligeramente para que rellenen mejor a este elemento. Usan como dimensión _mínima_ el valor de 150px.

### Distribución de contenido variable entre columnas

Por defecto, el contenido que se divide en varias columnas se balanceará de forma equitativa entre ellas. En caso de que el navegador no pueda acomodar el contenido para que haya un número equivalente de líneas en cada columna, la última columna será la más corta.

Para cambiar este comportamiendo predeterminado, podemos hacerlo con la propiedad `column-fill`:

```css
E { column-fill: keyword; }
```

Esta propiedad cuenta con dos valores posibles, el primero siendo `balance`, que intenta hacer que todas las columnas tengan una longitud equivalente, y el segundo es `auto`, que rellena a las columnas en orden sucesivo.
<br>
El valor `auto` solo funciona cuando el elemento padre tiene una altura fija. El contenido se apilará a la primera columna hasta alcanzar esa altura, y se seguirá de esta forma con las siguientes columnas.

### Combinar `column-count` y `column-width`

Se pueden utilizar estas dos propiedades en un elemento, en caso de que esto ocurra, el valor `column-count` actúa como un valor máximo.

```css
.columns {
	column-count: 3;
	column-width: 150px;
}
```

Lo que el ejemplo anterior hace es dividir el texto en columnas de 150px siempre y cuando no creen 3 o más columnas, en caso de que sí, creará 3 columnas con un ancho mínimo de 150px.

Para usar ambas propiedades juntas, podemos usar la siguiente sintaxis:

```css
E { columns: column-width column-count; }
```

## Espacios entre columnas y reglas.

Al usar una disposición preceptiva de varias columnas, el navegador colocaría un espacio de _1em_ entre cada columna. Aunque podemos alterar ese valor predeterminado y especificar otra distancia con las propiedades `column-gap` y `column-rule`.

La primer propiedad tiene la siguiente sintaxis para definir el espacio entre columnas:

```css
E { column-gap: length; }
```

_`length`_ es cualquier número con una unidad de medida CSS estándar.

La propiedad `column-rule` dibuja una línea de forma equidistante entre las columnas. La sintaxis para `column-rule` consta de tres subpropiedades:

```css
E{
	column-rule-width: length;
	column-rule-style; border-style;
	column-rule-color: color;
	column-rule: length border-style color;
}
```

Veamos entonces el siguiente ejemplo:

```css
.columns {
	column-count: 3;
	column-gap: 2em;
	column-rule: 0.3em double silver;
}
```

En este ejemplo los hijos del elemento se dividen en tres columnas, cada una con un espacio de 2em entre sí y una regla de 0.3em. Como podemos ver en el código, las subpropiedades de `column-rule` las podemos ajustar usando únicamente esta propiedad.

## Elementos que abarcan varias columnass

Si deseamos que ciertos elementos abarquen varias columnas, podemos usar `column-span`, que tiene la siguiente sintaxis:

```css
E { column-span: value; }
```

_`value`_ puede ser uno de dos valores: `all` o `none`, este último siendo el valor por defecto, el cual mantiene al elemento en el flujo de la columna. Mientras que `all` rompe con el flujo, haciendo que todo contenido que anteceda y preceda al elemento se distribuya en columnas, pero el elemento en cuestión no.

```css
h2 {
	column-span: all;
}
```

## Soporte en navegadores para Múltiples Columnas

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
			column-count
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
			IE10
		</td>
	</tr>
	</tr>
	<tr>
		<td>
			column-width
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
			IE10
		</td>
	</tr>
	<tr>
		<td>
			columns
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
			IE10
		</td>
	</tr>
	<tr>
		<td>
			column-fill
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
			IE10
		</td>
	</tr>
	<tr>
		<td>
			column-gap
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
			IE10
		</td>
	</tr>
	<tr>
		<td>
			column-rule
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
			IE10
		</td>
	</tr>
	<tr>
		<td>
			column-span
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
			IE10
		</td>
	</tr>
</table>