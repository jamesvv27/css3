# 8 - Imágenes de fondo

## Cambios a las propiedades de fondo existentes

Los módulos de _Backgrounds_ y _Borders_ extienden las propiedades para que sean mucho más útiles y complementen a algunas propiedades ya existentes de CSS2.1

### `background-position`

Esta propiedad puede contener uno de dos valores, ya sea una palabra clave para cada lado de la caja: `top`, `right`, `left`, `bottom`. O valores de longitud que ajustan a una posición relativa hacia la esquina superior izquierda del elemento al que se le aplica.

Ahora en CSS3, esta propiedad acepta hasta cuatro valores. Se pueden utilizar palabras clave para especificar un lado y después valores de longitud o porcentajes para la distancia relativa desde ese lado. Lo podemos ver en el siguiente ejemplo:

```css
.foo {
	background-position: right 10em bottom 50%;
}
```

La imágen de fondo en el elemento `.foo` se posicionará 10em desde la derecha y 50% desde el fondo.

### `background-attachment`

La forma en que una imagen de fondo se desplaza se determina por la propiedad `background-attachment`. Los valores posibles en CSS2.1 son `scroll`, el cual hace que la imagen no se desplace hacia abajo junto al elemento pero si lo haga con la ventana gráfica, y `fixed`, el cual hace que la imagen tampoco se desplace junto a la ventana gráfica.

El nuevo valor, `local`, añadido en CSS3, permite que una imagen de desplace junto al elemento y la ventana gráfica.

### `background-repeat`

En CSS2.1, la propiedad `background-repeat` acepta uno de cuatro valores posibles: `no-repeat`, `repeat`, `repeat-x`, y `repeat-y`. Con  estos valores, se pueden poner mosaicos a las imágenes de forma vertical, horizontal, o ambas sobre un elemento.
<br>
Y en CSS3, la utilidad de esta característica se expande con la nueva propiedad `space`, que hace que la imagen de fondo se repita sobre su elemento contenedor tantas veces como sea posible (sin que la imagen se desborde de los límites).
<br>
La segunda nueva propiedad es `round`, que hace que la imagen de fondo que se repite se escale para que un determinado número de imágenes rellenen al elemento.

```css
.space { 
	background-repeat: space;
}
.round { 
	background-repeat: round;
}
```

## Varias imágenes de fondo

En CSS3, casi todas las propiedades `background-*` aceptan varios valores, y de este modo podemos añadir varias imágenes de fondo a un elemento.

Para hacer esto, solamente hay listar los valores separados por comas:

```css
E { background-image: value, value }
```

Para cada capa que creemos, se pueden añadir valores de las propiedades `background-*` relacionadas:

```css
h2 {
	background-image: url('monkey.svg'), url('landscape.jpg');
	background-position: 95% 85%, 50% 50%;
	background: no-repeat;
}
```

## Imágenes de fondo escaladas dinámicamente

Una nueva propiedad de CSS3 es `background-size`. Esta propiedad, permite ajustar el tamaño de las imágenes de fondo.

```css
E { background-size: value; }
```

El valor de esta propiedad puede ser una longitud, un porcentaje, un par de ambos, o una palabra clave.

```css
E { background-size: width height; }
```

La longitud puede ser de cualquier unidad de medida. Si utilizamos porcentajes, la dimensión se basará en el elemento contenedor.

Si solo se especifica un valor, ese valor se considerará el ancho, y la altura entonces tendrá el valor de `auto`.

Veamos un ejemplo, ahora con la propiedad `background-position`:

```css
h2 {
	background:
	url('monkey.svg') no-repeat 95% 85%,
	url('monkey.svg') no-repeat 50% 80%,
	url('monkey.svg') no-repeat 10% 100%,
	url('landscape.jpg') no-repeat 50% 50%;
	background-size: auto 80%, auto 15%, auto 50%, auto;
}

```

Con `background-size`, podemos usar dos palabras clave: `contain` y `cover`.
<br>
`contain` escala la imagen de forma proporcional lo más grande que se pueda sin exceder el alto o el ancho del elemento contenedor.
`cover` escala la imagen al tamaño de la altura o el ancho del tamaño contenedor, el que sea el mayor de los dos.

```css
.monkey-1, .monkey-2 {
	background-image: url('monkey.svg');
	background-position: 50% 50%;
}
.monkey-1 { 
	background-size: contain;
}
.monkey-2 { 
	background-size: cover;
}
```

## Background Clip y Origin

En CSS2, la posición de una imagen de fondo es relatiiva al límite exterior del relleno de su elemento contenedor, y cualquier "desborde" o "fuga" se extiende por debajo de su borde. CSS3 introduce dos nuevas propiedades que brindan más control sobre su posición.

La primer propiedad es `background-clip`, que define la sección del box que se convertirá en el límite en el cual se mostrará el fondo. Su sintaxis es la siguiente:

```css
E { background-clip: box; }
```

El valor `box` puede ser uno de tres palabras clave: `border-box` (valor por defecto), `content-box` o `padding-box`.
<br>
`border-box` muestra el fondo detrás del borde, y es posible ver esto si usamos un borde transparente o con opacidad. El valor de `padding-box` muestra el fondo solo cuando está por encima del borde, y no por detrás. Y `content-box` hace que no haya nada de fondo después del borde.

```css
h2 {
	background: url('landscape.jpg') no-repeat 50% 50% #EFEFEF;
	border-width: 20px;
	padding: 20px;
}
h2.brdr {
	background-clip: border-box; 
}
h2.pddng { 
	background-clip: padding-box; 
}
h2.cntnt { 
	background-clip: content-box; 
}
```

La siguiente propiedad es `background-origin`. Usando esta propiedad podemos ajustar el punto en el que el fondo iniciará.

```css
E { background-origin: box; }
```

El valor de `box` acepta las mismas palabras clave que `background-clip`: `border-box`, `content-box` y `padding-box`.

```css
h2 { 
	background: url('monkey.svg') no-repeat 0 100%;
}
h2.brdr { 
	background-origin: border-box; 
}
h2.cntnt { 
	background-origin: content-box; 
}
h2.pddng {
	background-origin: padding-box;
}
```

## Shortcuts para la sintaxis

El shortcut de la propiedad `background` ha sido actualizado para incluir valores para las propiedades `background-size`, `background-clip` y `background-origin` en una misma línea.

Los valores de `background-size` deben de ir después de los de `background-position`, y deben de ser separados por una diagonal:

```css
E { background: url('bar.png') no-repeat 50% 50% / 50% auto;s }
```

## Soporte en navegadores para imágenes de fondo

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
			background-position
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
			background-attachment
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
			background-repeat (nuevo)
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
		<td>
			✓
		</td>
	</tr>
		<tr>
		<td>
			background-repeat
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
			Varias imágenes de fondo
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
			background-size
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
			Propiedad background con shortcuts
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
			background-clip
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
			background-origin
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