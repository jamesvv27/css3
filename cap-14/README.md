# 14 - Transiciones y animaciones

La principal diferencia entre las transiciones y las animaciones es que unas son _implícitas_ y las otras son _declaradas_. Esto significa que las transiciones únicamente toman efecto cuando las propiedades a las que se aplican cambian de valor, mientras que las animaciones se ejecutan explícitamente cuando se aplican a un elemento.

## Transiciones

Las transiciones son una animación implícita, pues solo actúan cuando una propiedad CSS tiene un nuevo valor. Para que una transición ocurra, debe de haber: un valor inicial, un valor final, la transición, y algo que la active.

El siguiente es un ejemplo de estas cuatro condiciones en una transición:

```css
div {
	background-color: black;
	transition: background-color 2s;
}
div:hover { background-color: silver; }
```

Primero tenemos el valor inicial (`background-color: black`), y la transición (`background-color 2s`). Lo que lo activa es la pseudo-clase `:hover`, la cual ajusta el valor final (`silver`) para la propiedad `background-color`.

### `transition-property`

Esta propiedad especifica la propiedad de un elemento que será animada:

```css
E { transition-property: keyword; }
```

La palabra clave que podemos que pasar como valor es `all`, (por defecto) `none`, o una propiedad CSS válida.

```css
h1 {
	font-size: 150%;
	transition-property: font-size;
}
```

Esta propiedad define que `font-size` será transicionado.

### `transition-duration`

Esta ajusta el tiempo que toma una transición para completarse.

```css
E { transition-duration: time; }
```

`time` es un número con una unidad de _ms_ (_milisegundos_) o _s_ (_segundos_).
Es posible que una transición surta efecto si declaramos `transition-duration` sin la propiedad `transition-property`--que ahora tendrá como valor `all`--.

```css
h1 {
	font-size: 150%;
	transition-property: font-size;
	transition-duration: 2s;
}
```

### `transition-timing-function`

Para controlar la forma en que un elemento transiciona, podemos usar esta propiedad, que permite variaciones en velocidad dentro de la duración de la transición. Esta propiedad tiene tres valores diferentes, una palabra clave, la función `cubic-bezier()` o la función `steps()`

#### Palabras clave

La sintaxis para palabras clave es la siguiente:

```css
E { transition-timing-function: keyword; }
```

Los valores posibles son `ease` (por defecto), `linear`, `ease-in`, `ease-out`, y `ease-in-out`.

Un pequeño ejemplo:

```css
h1 {
	font-size: 150%;
	transition-property: font-size;
	transition-duration: 2s;
	transition-timing-function: ease-out;
}
```

#### Curva Cúbica de Bézier

Podemos usar la función `cubic-bezier()` para mayor control de la transición.

```css
E { transition-timing-function: cubic-bezier(x1, y1, x2, y2); }
```

Una curva cúbica de Bézier es una curva continua que pasa por cuatro puntos definidos en una cuadrícula definida desde el 0 al 1 en ambos axes. sus puntos son _P₀_, _P₁_, _P₂_, y _P₃_.

_P₀_ siempre se encuentra en la coordenada (0,0) y _P₃_ siempre se encuentra en la posición (1,1), es entonces que en la función definimos las posiciones de los puntos _P₁_ y _P₂_ [(_x₁_, _y₁_) y (_x₂_, _y₂_)] para formar la curva.

```css
E { transition-timing-function: cubic-bezier(0.6, 0.1, 0.15, 0.7); }
```

La animación entonces progresará desde el punto inicial hasta el punto final siguiendo la forma de la curva en la duración ajustada.

#### Función `steps()`

Esta corre la animación en una serie de intervalos escalonados.

```css
E { transition-timing-function: steps(count, direction); }
```

El valor `count` es un entero que define por cuántos intervalos debería pasar la animación, y el valor opcional `direction` es una de dos palabras clave, `start` o `end` (predeterminado), que ajusta el punto en el que sucede el cambio en cada intervalo.

Aquí un ejemplo:

```css
E { transition-timing-function: steps(4, end); }
```

### `transition-delay`

Esta ajusta el tiempo en el que la transición comienza.

```css
E { transitio-delay: time; }
```

Si usamos valores negativos, la transición iniciará inmediatamente y se saltará el tiempo que ajustamos.

### Propiedad `transition` acortada

Al igual que otras propiedades CSS que forman parte de una "familia", la de `transition-*` tiene un acortamiento con la siguiente sintaxis:

```css
E { transition: property duration timing-function delay; }
```

Los valores de tiempo, `transition-duration` y `transition-delay`, deben de ser declarados en ese orden. Si solo uno se declara, se asume que es `transition-duration`.

### Ejemplo

```css
h1 {
	font-size: 150%;
	transition: font-size 2s ease-out 250ms;
}
h1:hover { 
	font-size: 600%;
}
```

### Varias transiciones

Se pueden añadir varias transiciones a un elemento al brindar una lista de valores separados por comas a las propeidades. Y dicho esto, los siguientes ejemplos son válidos:

```css
E {
	transition-property: border-width, height, padding;
	transition-duration: 4s, 500ms, 4s;
}
E { 
	transition: border-width 4s, height 500ms, padding 4s; 
}
```

Si una propiedad tiene menos valores que las demás, esa lista de valores se repetirá, por lo que el ejemplo anterior lo podemos escribir de la siguiente manera:

```css
E {
	transition-property: border-width, height, padding;
	transition-duration: 4s, 500ms;
}
```

Otro ejemplo práctico es el siguiente:

```css
.widget {
	background-color: black;
	left: 10%;
	top: 60%;
	transition: background-color 4s linear, left 2s ease-in-out, top 2s ease-in-out;
}
div:hover .widget {
	background-color: silver;
	left: 75%;
	top: 10%;
}
```

## Animaciones

La limitante de las transiciones es que solo se aplican cuando el valor de una propiedad cambia. Y el módulo de Animaciones de CSS3 permite que las animaciones se apliquen directamente con una sintaxis que permite mayor control.

Para crear animaciones, es neceario definir las propiedades y los tiempos, y después se añaden los controles de animación a los elementos que serán animados.

### Keyframes

Podemos ver a las animaciones como una serie de transiciones concatenadas. Primero hay que definir los _keyframes_, que son los puntos que definen el inicio y fin de una transición. Una animación simple tiene dos keyframes, uno de comienzo y uno de fin.

Los keygrames se declaran con la regla `@keyframes`, que tiene la siguiente sintaxis:

```css
@keyframes name{
	selector { property : value; }
}
```

El primer valor de esta regla es `name`, un identificador único para darle nombre a la animación.

`selector` ajusta la posición dentro de la duración de la animación del keyframe. Si queremos que el keygrame ocurra a la mitad de la animación, usamos un valor de `50%`. Y también es posible usar una de dos palabras clave, `from` o `to`.

La siguiente animación cuenta con tres keyframes:

```css
@keyframes expand{
	from {
		border-width: 4px;
	}
	50%{
		border-width: 12px;
	}
	to{
		border-width: 4px;
		height: 100%;
		width: 100%;
	}
}
```

Los selectors de keyframe se pueden concatenar al igual que otros selectors CSS. Por lo que podemos escribir el ejemplo anterior de la siguiente manera:

```css
@keyframes expand{
	from {
		border-width: 4px;
	}
	50%{
		border-width: 12px;
	}
	to{
		height: 100%;
		width: 100%;
	}
}
```

### `animation-name`

La propiedad `animation-name` se refiere a una animación que ha sido definida con la regla `@keyframes`, y su sintaxis es la siguiente:

```css
E { animation-name: name; }
```

### `animation-duration`

La duración de la animación se ajusta con la propiedad `animation-duration`, que funciona de la misma forma que `transition-duration`

```css
E { animation-duration: time; }
```

### `animation-timing-function`

Esta también es funcionalmente idéntica a la función `transition-timing-function`:

```css
E { animation-timing-function: value; }
```

Los valores permitidos son los de palabras clave (`ease`, `linear`, `ease-in`, `ease-out` y `ease-in-out`), la función `cubic-bezier()` y la función `steps()`.

### `animation-delay`

De igual forma, esta propiedad es funcionalmente idéntica a su contraparte de transiciones:

```css
E { animation-delay: time; }
```

### `animation-iteration-count`

A diferencia de una transición, una animación puede repetirse cualquier número de veces. El número de repeticiones se ajusta con la propiedad `animation-iteration-count`, que tiene esta sintaxis:

```css
E { animation-iteration-count: count; }
```

El valor `count` puede ser un número entero, para ajustar la cantidad de veces que se repetirá la animación, o la palabra clave `infinite`.
Por defecto la propiedad tiene el valor de `1`, y al brindar el valor de `0` o cualquier número negativo, la animación no se reproducirá.

### `animation-direction`

Las animaciones se reproducen de inicio a fin, pero también pueden reproducirse en reversa.

Se puede definir si una animación siempre correrá en una dirección o alternará entre el orden natural o en reversa. Para esto usamos la propiedad `animation-direction`: 

```css
E { animation-direction: keyword; }
```

Tiene dos opciones: `normal` (predeterminado) o `alternate`. Si usamos el valor `alternate`, la animación correra de inicio a fin y después se reproducirá en reversa antes de comenzar de nuevo.

### `animation-fill-mode`

Si la animación no se repite un número infinito de veces, es posible usar esta propiedad para ajustar cómo aparecerá el elemento fuera del ciclo de la animación.

```css
E { animation-fill-mode: keyword; }
```

Las palabras clave permitidas son `none` (por defecto), `backwards`, `forwards` y `both`. Al usar `backwards`, las declaraciones especificadas en el keyframe `0%` o `from` se aplicarán antes de que la animación comience, si usamos `forwards`, las declaraciones en el keyframe `100%` o `to` se aplicarán cuando la animación termine. Utilizando `both`, las declaraciones del `0%` se aplicarán antes de la animación, y las del `100%` después de la animación.

### `animation-play-state`

Esto define si una animación se encuentra activa. Su sintaxis es:

```css
E { animation-play-state: keyword; }
```

El valor de palabra clave tiene dos opciones: `running`, que significa que la animación está corriendo, y `paused`, cuando se encuentra en pausa. Podemos usar esta propiedad para una acción de reproducir/pausar:

```css
E:hover { animation-pay-state: paused; }
```

### Acortamiento para `animation`

Al igual que con las transiciones y otras propiedades, podemos usar la propiedad acortada `animation` que tiene la siguiente sintaxis:

```css
E { animation: name duration timing-function delay iteration-count direction fill-mode play-state; }
```

### Ejemplo

El ejemplo real es este:

```css
@keyframes expand {
	0% { border-width: 4px; }
	50% { border-width: 12px; }
	100% {
		border-width: 4px;
		height: 100%;
		width: 100%;
	}
}
div {
	... 
	animation: expand 6s ease 0 infinite alternate;
}
```

### Varias animaciones

Podemos añadir varias animaciones a un elemento utilizando una lista separada por comas con cualquiera de ambas sintaxis:

```css
E {
	animation-name: first-anim, second-anim;
	animation-duration: 6s, 1.25ms;
	animation-delay: 0, 750ms;
}
E { animation: first-anim 6s, second-anim 1.25ms 750ms; }
```

## Soporte en navegadores para transiciones y animaciones

<table>
	<tr>
		<td></td>
		<td>Chrome</td>
		<td>Firefox</td>
		<td>Safari</td>
		<td>IE</td>
	</tr>
	<tr>
		<td>Transiciones</td>
		<td>✓</td>
		<td>✓</td>
		<td>✓</td>
		<td>IE10</td>
	</tr>
	<tr>
		<td>Animaciones</td>
		<td>✓</td>
		<td>✓</td>
		<td>✓</td>
		<td>IE10</td>
	</tr>
</table>