# 10 - Color y opacidad

El módulo de Color CSS introduce el canal _Alpha_ y la propiedad de _opacidad_ para el uso de colores y facilidad de su implementación.

## La propiedad de Opacidad

La opacidad es la cantidad de luz que un objeto permite que pase sobre él. Es decir, entre menos opaco sea un objeto, más transparente será.

En CSS la opacidad se mide con la propiedad `opacity` y tiene la siguiente sintaxis:

```css
E { opacity: number; }
```

El valor de _`number`_ es una fracción decimal-- un número entre 0.0 y 1.0--.

En el siguiente ejemplo, tendremos una serie de varios elementos con parentesco entre sí:

```html
<div class="parent">
	<div class="child">
		<p>...</p>
	</div>
</div>
```

Vamos entonces a aplicar algunas reglas de opacidad a estos elementos:

```css
.parent { 
	background-color: black; 
}
.child { 
	background-color: white; 
}
.child.semi-opaque-1 { 
	opacity: 0.66; 
}
.child.semi-opaque-2 { 
	opacity: 0.33; 
}
```

Cuando no especificamos un valor de opacidad, se predeterminará a 1.0.

Algo a notar es que la opacidad afecta a todos los elementos hijos de un elemento. Si un elemento tiene un 0.5 de valor de `opacity`, sus elementos hijos no tendrán una opacidad mayor a esa.

Para esta limitación podemos emplear el canal Alpha.

## Valores de color extendidos

En CSS2.1 se pueden emplear tres métodos para valores de color. Ya sea por palabras clave, valores _HEX_, o _RGB_. En CSS3 el rango de esto se expande con un nuevo método.

### El canal Alpha

Este canal es la medida de la opacidad de un **color**, lo que diferencía a esto del valor de `opacity`, es que este último es la medida de la opacidad de un **elemento**.

CSS3 introduce el valor Alpha como un valor en el modelo _RGBA_ (_Red, Green, Blue, Alpha_) y se aplica con la función `rgba()`. La sintaxis es la siguiente:

```css
E { color: rgba(red, green, blue, alpha); }
```

El valor del argumento `alpha` es el mismo que el del valor brindado para la opacidad, una fracción decimal que va desde 0.0 hasta 1.0.

```css
E{
	color: rgba(0,0,0,0.5);
}
```

El ejemplo anterior le da una opacidad al color negro de 50%.

Dado que `rgba()` es un valor de color, no se puede usasr para cambiar la opacidad de un elemento. Y aunque el valor de `rgba()` puede ser heredado, los elementos hijos pueden sobrescribir esto con su propio valor `rgba()`.

Para ver la diferencia entre el canal Alpha y el valor de la opacidad probaremos estas reglas en dos ejemplos que tienen el mismo marcado:

```html
<div class="box">
	<div class="text">
		<h1>...</h1>
	</div>
</div>
```

A uno le ajustaremos la opacidad y al otro le daremos un valor `rgba()`:

```css
.box { 
	background-image: url('monkey.svg'); 
}
.text { 
	background-color: white;
}
.opacity { 
	opacity: 0.5;
}
.rgba { 
	background-color: rgba(255,255,255,0.5); 
}
```

Lo que sucede aquí es que el primer box el valor de `opacity` se hereda al hijo `<p>`, lo cual hace al texto semitransparente. En el segundo box, el valor `rgba()` se aplica solamente al color de fondo de `.text`, por lo que el texto está completamente opaco.

#### Degradado RGBA

Los navegadores que no soporten valores RGBA ignorarán las reglas que se les aplique y tendrán el color predeterminado de lo que sea que haya sido heredado.

Para que esto no ocurra, simplemente debemos especificar el color dos veces-- una con el canal Alpha y otra sin él--.

```css
p {
	color: #F00;
	color: rgba(255,0,0,0.75);
}
```

### Hue, Saturation, Lightness (Matiz, saturación y luminosidad)

CSS3 introduce un nuevo sistema de color conocido como HSL, y se utiliza con la siguiente sintaxis:

```css
E { color: hsl(hue,saturation,lightness); }
```

### HSLA

Se puede utilizar el canal Alpha con HSL con la función de color `hsla()`, que simplemente extiende el método ya existente con un argumento adicional:

```css
E { color: hsl(hue,saturation,lightness,alpha); }
```

### Variable de color: `currentColor`

CSS3 también introduce una nueva palabra clave para `color`: `currentColor`. Esta palabra clave actúa como una variable para el color actual.

Digamos que un elemento tiene un valor de `color` de `red`, es entonces que la variable `currentColor` también será `red`, y la podemos usar para ajustar el mismo color a otro elemento sin tener que especificar ese color nuevamente.

```css
h2 {
	color: black;
}
.ccolor {
	background-color: black;
	color: white;
}
h2 abbr { 
	border-bottom: 6px double currentColor; 
}
```
## Soporte en navegadores para Color y opacidad

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
			opacity
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
			Valores RGBA
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
			Valores HSL
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
			Valores HSLA
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
			Valor currentColor
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