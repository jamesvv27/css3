# 16 - Valores de dimensiones

## Unidades de longitud relativas

Una _unidad de longitud relativa_ es aquella cuyo valor es relativo a otra propiedad.

En CSS2.1 las unidades relativas son `em`, que se calcula de la propiedad `font-size` de un elemento, y `ex`, que se calcula del x-height de la fuente de un elemento.

CSS3 añade más opciones a las unidades relativas, que por cierto, ya no son únicamente relativas al tamaño de fuente de un elemento.

### Unidades Root-Relative

`rem`, o _root em_ actúa como la unidad `em`, pero en lugar de ser relativa al valor `font-size` del elemento actual, es relativa al valor `font-size` del elemento raíz, osea, el elemento `<html>`.

```html
<ul>
	<li>Western gorilla
		<ul>
			<li>Western lowland gorilla</li>
			<li>Cross River gorilla</li>
		</ul>
	</li>
</ul>
```

Con `rem`, podemos hacer que los elementos `<li>` colocados en un nivel inferior al árbol del documento tomen como valor heredado el tamaño de fuente de la raíz del documento, en lugar de los elementos `<ul>`. Evitando así que el tamaño de fuente se vuelva a multiplicar:

```css
li { font-size: 2rem; }
```

### Unidades Viewport-Relative

Al usar porcentajes en varios elementos hijos, los calculos se pueden volver muy complejos si queremos que las diemensiones sean relativas a la raíz del documento y no a sus elementos padres.

Es por esto que podemos optar por usar las unidades Viewport-relative-- `vh` (alto) y `vw` (ancho)--. Cada unidad de valor representa un porcentaje de la ventana gráfica.

```css
E {
	height: 50vh;
	width: 75vw;
}
```

De este modo, no tenemos que hacer calculos complejos.

## Valores calculados

CSS3 permite que el navegador realice calculos con la función `calc()`, la cual podemos usar con cualquier unidad de valor. Esta función toma como argumento cualquier expresión matemática usando valores de unidad y los cuatro operadores aritméticos básicos.

Esta función es bastante útil al mezclar unidades.

```css
E {
	border: 10px;
	width: calc(75% - 2em);
}
```

En la adición y sustracción podemos utilizar cualquier tipo de unidad en ambas partes de la operación. Pero al utilizar la multiplicación al menos un argumento debe ser un número sin unidad, y en la división, el argumento después del operando debe de ser un número sin unidad.

```css
E {
	left: calc(5 * 10em);
	width: (80% / 4);
}

```

## Dimensionar elementos

Normalmente usamos las propiedades `width` y `height` para ajustar el tamaño de un elemento, pero CSS3 introduce nuevas propiedades y valores con el modelo box.

### Dimensiones del Box

Internet Explorer había implementado su modelo box distinto de la especificación del W3C. El modelo del W3C consistía en que el `width` era el ancho completo del contenido del box, y que cualquier padding o borde es adicional. En el modelo IE sucedía lo contrario, pues el valor `width` incluía cualquier borde o padding.

```css
E {
	border: 5px;
	padding: 10px;
	width: 100px;
}
```

En el modelo IE, el contenido del box tendría un ancho de 70px, mientras que en el modelo del W3C, tendría un ancho de 100px.

Ambas opciones pueden ser adecuadas dependiendo de la ocasión. En CSS3, si deseamoss usar el modelo IE, podemos usar la propiedad `box-sizing`:

```css
E { box-sizing: keyword; }
```

El valor por defecto es `content-box`, que aplica el `width` o el `height` como en el modelo del W3C, mientras que `border-box` aplica las dimensiones como en el modelo de IE.

### Dimensiones Intrínsecas y Extrínsecas

Contamos con el dimensionamiento _intrínseco_ y _extrínseco_. El dimensionamiento intrínseco se basa en los hijos de un elemento, mientras que el dimensionamiento extrínseco se basa en el tamaño de un elemento padre.

Estos modelos se aplican usando un valor de palabra clave en las propiedades `width` o `height`.

```css
E { width: keyword; }
```

#### `max-content` y `min-content`

Estos son valores intrínsecos que hacen a un elemento tan ancho o alto como el objeto de contenido (`max-content`) o más pequeño (`min-content`) que exista.

```html
<div>
	<img src="foo.png">
	<p>...</p>
</div>
```

En este marcado, el elemento `<p>` es más largo que el `<img>`. Si usamos el valor `min-content`, el tamaño del box será tan ancho como el elemento hijo más angosto-- en este caso, la imagen--, y el párrafo se envolvería ocupando otra línea.

#### `fit-content`

El siguiente valor por palabra clave puede ser más útil. Este dimensiona un elemento con tal de que sea lo suficientemente ancho para retener su contenido. Si se alcanza el ancho máximo del elemento, su contenido se envolverá por debajo.

#### `fill`

Este valor extrínseco hace a un elemento rellenar el espacio disponible dentro de la altura o anchura de su elemento padre contenedor.

```css
p { width: fill; }
```