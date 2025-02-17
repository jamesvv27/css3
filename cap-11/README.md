# 11 - Gradientes

## Gradientes lineales

Un _gradiente lineal_ es aquel que gradualmente transicione entre colores sobre una longitud o una línea recta que conecta dos puntos.

La sintaxis más simple para un gradiente lineal en la propiedad `background-image` es la siguiente:

```css
E { background-image: linear-gradient(black, white); }
```

Los gradientes requieren de al menos dos fuentes de color, un inicio y un fin.

### Ajustando la dirección del gradiente

El axis entre las fuentes de color se conoce como la _línea del gradiente_. Para cambiar la línea, primero especificamos un lado o esquina del box al darle un nuevo primer argumento a la función. Este argumeno es una cadena de palabras clave, empezando por `to`, seguido de la dirección.

```css
E { background-image: linear-gradient(to top, black, white); }
```

En el ejemplo anterior la línea del gradiente se dibuja desde la esquina superior izquierda hacia la esquina inferior derecha.

Para mayor control sobre la dirección, podemos pasar el valor de un ángulo en lugar de palabras clave.

Podemos hacer que la línea del gradiente tenga la misma dirección del ejemplo anterior con ángulos:

```css
E { background-image: linear-gradient(135deg, black, white); }
```

### Añadir más fuentes de color

Es posible usar más, y cada color que agreguemos se declara simplemente añadiendo un nuevo color en la lista separada por comas:

```css
E { background-image: linear-gradient(black, white, black); }
```

Aquí las fuentes de color se distribuyen equitativamente sobre la longitud del gradiente. Esta distribución se puede modificar añadiendo una longitud o valor de porcentaje después de cada fuente de color.

```css
E { background-image: linear-gradient(black,white 75%, black); }
```

Para modificar esto también podemos usar unidades de longitud:

```css
div { background-image: linear-gradient(to right, black, white 75%); }
div { background-image: linear-gradient(to right, black 50%, white); }
div { background-image: linear-gradient(to right, black, white 50%, black 1px); }
```

### Repetir gradientes lineales

Es posible crear el mismo gradiente hasta que el elemento se rellene utilizando la función `repeating-linear-gradient()`. Esta función acepta la misma serie de valores que `linear-gradient`, solo que se requiere un último valor de longitud para la última fuente de color.

```css
E { background-image: repeating-linear-gradient(white, black 25%); }
```

El valor de la última fuente de color define el punto en el que el gradiente se detiene y comienza a repetirse.

Veamos algunos otros ejemplos:

```css
.gradient-1 {
	background-image: repeating-linear-gradient(to left, black, white, black 25%);
}
.gradient-2 {
	background-image: repeating-linear-gradient(45deg, black, white 2px, black 10px);
}
.gradient-3 {
	background-image: repeating-linear-gradient(315deg, black, black 2px, white 2px, white 4px);
}
```

## Gradientes radiales

Un _gradiente radial_ es una transición gradual entre colores que se mueve desde un punto central hacia todas las direcciones. Estos se definen con la funcion `radial-gradient()`:

```css
E { background-image: radial-gradient(white, black); }
```

### Usando gradientes radiales

Es posible ajustar la forma de un gradiente radial añadiendo una palabra clave antes de las fuentes de color. Por defecto es `ellipse`, pero se puede usar, por ejemplo, `circle`:

```css
E { background-image: radial-gradient(circle, white, black); }
```

Por defecto el centro de un gradiente radial se encuentra en el centro del elemento al que se le aplica. Y es posible cambiar este punto añadiendo un argumento de posición a la función `radial-gradient()`, con valores de ya sea longitud, porcentaje, o palabras clave.

```css
E { background-image: radial-gradient(circle at 100% 50%, white, black); }
```

También es posible definir hasta qué punto termina un gradiente con el argumento `extent`, y se coloca justo después de la palabra clave de la forma:

```css
E { background-image: radial-gradient(circle 50px, black, white); }
```

Las cuatro palabras clave posibles que se pueden colocar son `closest-corner`, `closest-side`, `farthest-corner` (predeterminado), y `farthest-side`.

### Usar varias fuentes de color

Los gradientes radiales también pueden aceptar múltiples fuentes de color y valores de longitud o porcentaje para posicionarlas.

Veamos algunos ejemplos:

```css
.gradient-1 { 
	background-image: radial-gradient(farthest-side circle, black, white, black); 
}
.gradient-2 { 
	background-image: radial-gradient(farthest-side circle, black, white 25%, black); 
}
.gradient-3 { 
	background-image: radial-gradient(farthest-side circle at left, white,
black 25%, white 75%, black); 
}
.gradient-4 { 
	background-image: radial-gradient(circle closest-side circle at 40% 50%,
white, white 25%, black 50%, white 75%, black); 
}
```

### Repetir gradientes radiales

Se puede usar la función `repeating-radial-gradient()` para repetir los argumentos brindados hasta que se alcance el límite especificado en la última fuente de color.

```css
E { background-image: repeating-radial-gradient(circle, black, white 20%); }
```

## Varios gradientes

Dado que los gradientes se aplican con la propiedad de `background-image`, es posible usar la sintaxis de varios valores para aplicar varios gradientes en un elemento utilizando valores separados por comas.

Veamos dos ejemplos, uno con gradientes lineales y otro con gradientes radiales:

```css
.linears {
	background-image:
	linear-gradient(to right bottom, black, white 50%, transparent 50%),
	linear-gradient(to left bottom, black, white 50%, black 50%);
}
.radials {
	background-image:
	radial-gradient(closest-side circle at 20% 50%, white, black 95%, transparent),
	radial-gradient(closest-side circle at 50% 50%, white, black 95%, transparent),
	radial-gradient(closest-side circle at 80% 50%, white, black 95%, transparent);
}
```

## Soporte en navegadores para gradientes

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
			Gradientes lineales
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
			Gradientes lineales repetidos
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
			Gradientes radiales
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
			Gradientes radiales repetidos
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
