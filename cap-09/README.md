# 9 - Efectos de borde y box

La siguientes características de los módulos de Backgrounds y Borders nos dan nuevos métodos para decorar los elementos sin marcado redundante.

## Esquinas redondas a los bordes

Aquí a cada esquina se le trata como un cuarto de elipse, el cual se define por una curva dibujada entre un punto del _axis x_ y un punto del _axis y_.

Un cuarto de elipse puede ser _regular_, en el cual la distancia entre ambos axes es igual, o _irregular_, en el que sucede lo contrario.

Con la propiedad `border-radius` podemos definir el radio del cuarto de elipse usando la siguiente sintaxis:

```css
E { border-v-h-radius x y; }
```

En este caso, _`v`_ es una palabra clave con valor de `top` o `bottom`; _`h`_ es una palabra clave con valor de `left` o `right` y los valores de _`x`_ y _`y`_ son distancias entre los axes que definen la curva del cuarto de elipse.

Veámoslo en práctica:

```css
div { border-top-right-radius: 20px 20px; }
```

Esta es una curva regular ubicada en la esquina superior derecha con un radio de 20px en ambos axes.
<br>
Para curvas regulares, podemos omitir escribir el valor de un axis una vez más:

```css
div {
	border-top-left-radius: 20px;
	border-top-right-radius: 20px;
	border-bottom-right-radius: 20px;
	border-bottom-left-radius: 20px;
}
```

### Acortamiendo para `border-radius`

Escribir una propiedad para cada esquina puede ser algo repetitivo. Por lo que aquí tenemos una sintaxis para emplear solo una propiedad para todas las esquinas (regulares):

```css
E { border-radius: [top-left] [top-right] [bottom-right] [bottom-left]; }
E { border-radius: [top-left] [top-right & bottom-left] [bottom-right]; }
E { border-radius: [top-left & bottom-right] [top-right & bottom-left]; }
E { border-radius: [top-left & top-right & bottom-right & bottom-left]; }
```

Veamos un ejemplo aplicado:

```css
.radius-1 { 
	border-radius: 
	0 20px;
}
.radius-2 { 
	border-radius:
	0 10px 20px;
}
.radius-3 { 
	border-radius:
	0 0 20px 20px; 
}
```

Si queremos la sintaxis acortada para curvas irregulares, podemos listar los valores separados por una diagonal (`/`):

```css
border-radius: { horizontal-radius / vertical-radius; }
```

Ambas partes (`horizontal-radius` y `vertical-radius`) pueden contener desde uno a cuatro valores, y emplean la misma sintaxis para elegir a qué esquina se le va a aplicar el radio.

```css
.radius-4 { 
	border-radius: 
	20px / 10px;
}
.radius-5 { 
	border-radius: 
	20px / 10px 20px; 
}
.radius-6 { 
	border-radius: 
	10px 20px 20px / 20px 10px; 
}
```

### Valores de porcentaje

También es posible definir el `border-radius` utilizando un valor de porcentaje, el cual se referirá al porcentaje de la longitud del lado del elemento al que se aplicará.

```css
div {
	border-radius: 50%;
	height: 100px;
}
.ellipse {
	width: 200px;
}
.circle { 
	width: 100px; 
}
```

Estas reglas se aplicarán a dos elementos, el primero tiene un ancho más largo, y el segundo tiene un alto y ancho equivalentes.

## Imágenes para bordes

CSS3 introduce una serie de propiedades que brindan una sintaxis simple para aplicar bordes decorativos con imágenes.

### `border-image-sources`

Esta define la fuente de la imagen que se empleará para el borde. Su sintaxis es:

```css
E { border-image-source: url('foo.png'); }
```

### `border-image-slice`

Una vez que tengamos la fuente de la imagen para el borde, es necesario recortarla. La propiedad `border-image-slice` permite colocar desde uno a cuatro valores, que se van a cada lado del elemento. Estos valores se usan para definir una distancia desde cada borde de la imagen.

```css
E { border-image-slice: 34; }
```

No se usan unidades de medida en el valor brindado, pues para imágenes bitmap las unidades son valores de pixeles, pero para imágenes de vectores, son valores de coordenadas. También es posible usar valores de porcentaje con esta propiedad.

```css
E {
	border: 34px 10px;
	border-image-slice: 34;
	border-image-source: url('foo.png');
}
```

A este elemento le estamos aplicando un borde de 34px en la parte superior e inferior y de 10px en la parte izquierda y derecha.

Lo que sucederá entonces, es que en la parte izquierda y derecha la imagen se distorsionará para que pueda encajar dentro de los 10px que definimos.

A la propiedad `border-image-slice` también se le puede meter un valor opcional de `fill`. Si se incluye la palabra clave ``fill, el área de la imagen dentro de os recortes se aplicará sobre el fondo del elemento.

```css
E { border-image-slice: value fill; }
```

### `border-image-width`

Los recortes de las imágenes de fondo se estiran o se achatan para encajar en el ancho del elemento. Esto se puede controlar con la propiedad `border-image-width`:

```css
E { border-image-width: value; }
```

_`value`_ puede tener de uno a cuatro valores para coincider con los lados del elemento.

_`value`_ crea un borde "virtual" sobre el elemento, pues no cambia la disposición de la página a diferencia de `border-width`.

```css
E { border-width: 34px; }
F {
	border-width: 1px;
	border-image-width: 34px;
}
E, F {
	border-image-slice: 34;
	border-image-source: url('foo.png');
}
```

El contenido del elemento _`E`_ estará contenido dentro de los límites de `border-width` (34px), mientras que con _`F`_, a pesar de que se se aplican los recortes de la imagen, su contenido se verá sobre los bordes "virtuales".

Si usamos un número sin unidad de medida, actuará como un multiplicador del valor `border-width`. En el siguiente ejemplo, `border-image-width` sería equivalente a `20px`.

```css
E {
	border-width: 10px;
	border-image-width: 2;
}
```

### `border-image-repeat`

Esta propiedad controla la manera en la que la imagen encajará en la longitud de cada lado entre las esquinas:

```css
E { border-image-repeat: keyword; }
```

Este acepta dos de tres valores de palabras clave: `stretch` (por defecto), `repeat` y `round`. Al usar `repeat`, la imagen se recorta a su longitud normal, y se repite hasta que rellene todo el recorte definido. `round` actúa como `repeat`, solo que escala el recorte para que encaje de la mejor forma en el borde.

Si por ejemplo, deseamos estirar el elemnto en el borde superior y en el inferior, y redondearlo en el lado izquierdo y en el derecho, podemos usar lo siguiente:

```css
E { border-image-repeat: stretch round;s }
```

### Propiedad `border-image` recotada

Esta es la sintaxis recortada para usar `border-image`:

```css
E { border-image: source / slice / width /outset repeat;s }
```

Aquí un ejemplo de esto en uso:

```css
F { border-image: url('foo.png') 25 10 fill / 25px 10px / 5px round; }
```

## Sombras por fuera

Es posible añadir sombras a elementos box. Para esto, usamos la propiedad `box-shadow`. Su sintaxis es similar a `text-shadow`:

```css
E { box-shadow: inset horizontal vertical blur-radius spread color; }
```

`inset` es una palabra clave opcional que define si la sombra se colocará dentro o fuera del elemento (por defecto se colocará fuera). `horizontal` y `vertical` ajustan la distancia de la sombra desde el box.

`blur-radius` es un valor de longitud que funciona de la misma forma como con `text-shadow`. `spread` ajusta la distancia en la que se dispersa la sombra. Un valor positivo hará la sombra más grande que su elemento, y un valor negativo la hará más pequeña.

`color` es un valor opcional en el que definimos el color, por defecto será el color heredado.

```css
.shadow-one { 
	box-shadow:
	inset 
	4px 4px;
}
.shadow-two { 
	box-shadow: 
	4px 4px 3px;
}
.shadow-three {
	 box-shadow: 
	 inset
	 12px 12px 2px -6px;
}
.shadow-four {
	 box-shadow: 
	 inset
	 #999 4px -4px 2px 0; 
}
.shadow-five { 
	box-shadow:
	#999 4px -4px 2px 0,
	-4px 4px 2px;
}
```

## Soporte en navegadores para efectos de borde y de box


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
			border-radius
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
			border-image
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
			IE11
		</td>
	</tr>
		</tr>
		<tr>
		<td>
			box-shadow
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