# 6 - Efectos de texto y estilos tipográficos

El contenido del texto ha sido una característica elemental de la Web desde su creación, y CSS3 ha expandido las funciones del texto con el _Text Module_.

Las nuevas funcionalidades del módulo tienen bastantes elementos implementados, que aumentan las opciones a la hora de añadir efectos a los textos.

## Axis y Coordenadas

Un concepto nuevo a CSS3 es el de los axis. En el que se emplea el sistema de coordenadas del plano cartesiano. Y que consiste en dos líneas, la horizontal siendo el _axis x_ y la vertical el _axis y_. El punto en donde las dos líneas de cruzan es el origen.

Para elementos en pantalla, podemos medir las longitudes de los axis en pixeles, que también cuentan con etiquetas positivas y negativas.

## Efectos dimensionales: `text-shadow`

La posición de la sombra se ajusta utilizando las coordenadas _x_ y _y_. _x_ se usa para ajustar la distancia horizontal de la sombra al texto, e _y_ para la distancia vertical (el _offset-y_):

```css
E{ text-shadow x y; }
```

Veamos un ejemplo de una sombra gris debajo de un `<h1>`:

```css
h1 { 
	text-shadow: 3px 3px #BBB
	 }
```

Para estas sombras también podemos usar valores negativos:

```css
.one {
	text-shadow: -3px -3px #BBB;
}
.two {
	text-shadow: -5px 3px #BBB;
}
.three {
	text-shadow: -5px 0 #BBB;
}
```

Esta propiedad cuenta con una cuarta opción: _`blur-radius`_. Esta opción da un efecto de difuminado a la sombra:

```css
E { text-shadow: x y blur radius color; }
```

El valor del radio del blur debe ser un entero con una unidad de medida. Mientras más alto sea el valor, el difuminado será más claro, y abarcará más espacio.

```css
.one {
	text-shadow: 3px 3px 3px ###BBB;
}
.two {
	text-shadow: 0 0 3px #000;
}
```

### Varias sombras

La sintaxis de `text-shadow` permite añadir varias sombras a un nodo de texto. Para esto, solo hay que brindarle valores extra a la propiedad usando comas para separarlos:

```css
E { text-shadow: value, value, value; }
```

Las sombras se aplican en el orden que se introduzcan los valores. Aquí un ejemplo:

```css
.one {
	text-shadow:
	0 -2px 3px #FFF,
	0 -4px 3px #AAA,
	0 -6px 6px #666,
	0 -8px 9px #000;
}
.two {
	color: #FFF;
	text-shadow:
	0 2px rgba(0,0,0,0.4),
	0 4px rgba(0,0,0,0.4),
	0 6px rgba(0,0,0,0.4),
	0 8px 0 rgba(0,0,0,0.4);
}
```

## Restringiendo el overflow

En algunas situaciones, como cuando el espacio de las pantallas es algo limitado, tal vez sea necesario restringir el texto a una sola línea y un anchoen específico.

Una nueva propiedad llamada `text-overflow` está disponible en CSS3 para estas circunstancias. Su sintaxis es:

```css
E { text-overflow: keyword; }
```

Los valores que se pueden utilizar son `clip` y `elipsis`. El valor por defecto es `clip`, el cual hace que el texto se muestre incluso por fuera del container. Por otro lado, el valor `elipsis` remplaza el último carácter por los puntos suspensivos (...) si este se sale del container.
<br>
Veamos un ejemplo:

```css
p {
	overflow: hidden;
	text-overflow: elipsis;
	white-space: nowrap;
}
```

Ajustando el valor de `overflow` a hidden, evitamos que el contenido se muestre fuera del borde. El valor de la propiedad `white-space` (`nowrap`) evita que el texto se muestre en varias líneas.

## Alineando texto

CSS3 añade dos nuevos valores a la propiedad `text-align`: `start` y `end`, que resultan útiles en sitios que utilicen texto que se lea de derecha a izquierda.

La propiedad `text-align-last` permite ajustar la alineación de la última (o única) línea de un texto en un bloque justificado. Esta propiedad acepta los mismos valores que `text-align`:

```css
E { text-align-last: keyword; }
```

Si queremos justificar el bloque de un texto, y también alinear la última línea a la derecha, podemos usar lo siguiente:

```css
p {
	text-align: justify;
	text-align-last: right;
}
```

## Controlando la contención de líneas

Un problema al usar texto dínamico es el de las líneas conteniendose en donde no deben. CSS3 nos da más control sobre estos tipos de problemas con algunas propiedades que nos permiten definir de forma más claro como queremos que el contenido de texto esté envuelto.

### Cortar palabras

La primer propiedad es `word-wrap` que especifica si el navegaor puede cortar palabras largas para que estas quepan dentro del elemento padre. Su sintaxis es:

```css
E { word-wrap: keyword; }
```

Los valores posibles son `normal` y `break-word`. El primero hace que las líneas puedan cortarse únicamente entre palabras, y el segundo permite que las mismas palabras puedan cortarse para evitar el overflow hacia el elemento padre.

Si por ejemplo queremos que las palabras largas sean contenidas en lugar de pasarse de su container, podemos usar lo siguiente:

```css
p.break {
	word-wrap: break-word;
}
```

### Palabras separadas por sílabas

Una opción extra para cortar palabras en varias líneas de texto, es usando la separación de sílabas, que es mucho más adecuado.

En CSS3 podemos usar la propiedad `hyphens` para esto:

```css
E { hyphens: keyword; }
```

`hyphens` tiene tres posibles valores: `manual`, `auto` y `none`. El valor `auto` es el más útil, pues no es ncesario hacer ninguna sugerencia de separación en el marcado.s

## Redimensionar elementos

Una propiedad nueva que es útil para elementos cuyos contenidos son más anchos que su container es la propiedad `resize`. Esta propiedad tiene la siguiente sintaxis:

```css
E { resize: keyword; }
```

El valor de la propiedad define en qué dirección se puede arrastrar el elemento, ya sea `horizontal` o `vertical`. También puede ser `both`, para hacerlo en ambas direcciones o `none`. 

```css
p {
	overflow: hidden;
	resize: both;
}
```

## Soporte en navegadores para estilos tipográficos y estilos de texto

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
			text-shadow
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
			text-overflow
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
			text-align
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
			✗
		</td>
	</tr>
		<tr>
		<td>
			text-align-last
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
			✓
		</td>
	</tr>
		<tr>
		<td>
			overflow-wrap
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
			hyphens
		</td>
		<td>
			✗
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
			resize
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
			✗
		</td>
	</tr>
</table>