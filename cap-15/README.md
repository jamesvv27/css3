# 15 - Disposiciones Flexibles

## Declarando el modelo Flexbox

Lo primero que hay que hacer es crear el _container flex_, el elemento padre que creará un nuevo contexto para sus contenidos. Para esto, usamos un nuevo valor para la propiedad `display`:

```css
E { display: flex; }
```

Esto crea un container flex block-leve, podemos también usar el valor `inline-flex` para una disposición inline.

Ahora podemos añadir _items flex_ al container. Un item flex es cualquier elemento hijo del container flex:

```html
<div id="container">
	<div id="a">...</div>
	<div id="b">...</div>
</div>
```

Por defecto, los items flex se colocan en la dirección del texto de documento, como por ejemplo, de izquierda a derecha en Español, y de derecha a izquierda en Árabe.

Para modificar la dirección predeterminada, podemos usar la propiedad `flex-direction` en el container. El valor predeterminado, `row`, hace que los elementos yazcan en una fila, mientras que el valor `column` los coloca de arriba a bajo en una columna.

```css
E {
	display: flex;
	flex-direction: column;
}
```

## Alineación de Flexbox

Flexbox utiliza dos axes para la alineación.
El _axis principal_ va en la dirección en que se colocan los elementos, ya sea de izquierda a derecha, o de arriba a abajo. Cuando el valor de `flex-direction` es `row`, el axis principal es horizontal, cuando es `column`, el axis principal es vertical. El _axis cruzado_ es la línea que va de forma perpendicular al axis principal: Es vertical cuando la dirección es `row`, y horizontal cuando es `column`.

Al usar los containers flex, es buena idea usar los puntos iniciales y finales de los axes, pues los axes flex pueden invertirse.

## Invertir el orden del contenido

Se puede cambiar rápidamente el orden en el que los elementos se muestran, sin importar su orden en el DOM.	Esto se logra con la propiedad `flex-direction`, usando el valor `row-reverse` para invertir de los elemento flex.

```css
E { flex-direction: row-reverse; }
```

## Reordenar el contenido por completo

Es posible crear patrones de orden personalizados con la propiedad `order`, que se aplica a los elementos flex (no al container). El valor de la propiedad es un número que crea un _grupo ordinal_ que junta elementos del mismo valor y los ordena por su grupo ordinal. Todos los elementos elementos van desde el menor hasta el mayor. Los elementos con el mismo número se agrupan en el orden en el que aparecen en el DOM.

A este marcado:

```html
<div id="container">
	<div id="a">...</div>
	<div id="b">...</div>
	<div id="c">...</div>
	<div id="d">...</div>
</div>
```

Le aplicaremos las siguientes reglas para reordanar los elementos:

```css
#a { order: 2; }
#b, #d { order: 3; }
#c { order: 1; }
```

El orden de los elementos entonces es el siguiente: `#c`, `#a`, `#b` y `#d`. Aunque su orden en el marcado no cambia.

## Añadir flexibilidad

Casi siempre encontraremos situaciones en donde las longitudes combinadas de elementos flex en el axis principal son mayores o menores que el ancho del container flex. Si esto ocurre, podemos aprovechar la parte "flexible" de Flexbox. Existen algunas propiedades que permiten que elemento flex se agranden o encojan para rellenar el container.

### Propiedad `flex-grow`

Si deseamos expander los elementos para que rellenen un espacio vacío en el container, podemos usar la propiedad `flex-grow`:

```css
.flex-item { flex-grow: 1; }
```

El valor de la propiedad es una relación usada para distribuir el espacio en blanco entre los elementos flex para que se expandan. Por lo que podemos brindar valores a elementos distintos para que algunos elementos sean más grandes que otros.

### Propiedad `flex-shrink`

`flex-shrink` se usa para encojer elementos. Esta viene bastante útil si los elementos son más grandes que el container.

```css
.flex-item { flex-shrink: 1; }
```

El valor, al igual que con `flex-grow` es una relación para reducir el tamaño de los elementos en una proporción determinada.

### Propiedad `flex-basis`

El ancho de elementos flex se puede ajustar por sus contenidos o explícitamente por un valor `width`. Para cambiar la forma en que un ajuste del ancho se calcula, podemos usar un la propiedad `flex-basis`, que toma como valor una unidad de longitud.

```css
.flex-item { flex-basis: 100px; }
```

Al aplicar esta propiedad cualquier valor `width` se ignora, y el valor que brindamos a `flex-basis` se usa para calcular el ajuste.

El ejemplo es:

```css
.child-item {
	flex-grow: 1;
	width: 150px;
}
#b {
	flex-basis: 100px;
	flex-grow: 3;
}
```

### Acortamiento para `flex`

La familia `flex-*` tiene su propiedad acortada `flex`, y los valores que toma en orden son: `flex-grow`, `flex-shrink`, y `flex-basis`.

Un ejemplo sería:

```css
E { flex: 1 2 150px; }
```

## Alineación dentro del container

Al tener elementos con dimensiones ajustadas dentro de un container flex, seguramente quedará algo de espacio vacío en uno o en ambos axes. Cuando este sea el caso, podemos alinear los elementos dentro del container para hacer un mejor uso del espacio disponible.

### Alineación horizontal con `justify-content`

Esta propiedad se aplica al container flex y acepta una serie de palabras clave como valores que se aplican dependiendo de la dirección del flex padre.

```css
.flex-container { justify-content: keyword; }
```

Los valores son `flex-start` (por defecto)--que alinea todos los elementos flex a la izquierda del elemento padre con el espacio sin usar ocupando el ancho restante a la derecha--, `flex-end`-- que alinea los elementos a la derecha del container--, `center`, que distribuye el espacio sin usar a los extremos, y `space-between` y `space-around`, los cuales añaden una cantidad equivalente de distancias entre cada elemento.

Aquí algunos ejemplos de comparación:

```css
.container-a { justify-content: flex-start; }
.container-b { justify-content: center; }
.container-c { justify-content: space-around; }
```

### Alineación vertical con `align-items`

Cuando la altura de los elementos flex es menor que la del container, podeoms usar `align-items` para ajustar los elementos dentro del container:

```css
.flex-container { align-items: keyword; }
```

Los principales valores son: `stretch`, `flex-start`, `flex-end`, y `center`, los cuales podemos ver en acción en la siguiente comparativa:

```css
.container-a { align-items: stretch; }
.container-b { align-items: flex-end; }
.container-c { align-items: center; }
```

### Alineación cruzada con `align-self`

Esta propiedad se aplica al elemento flex, no al container. Los valores son los mismos que para `align-items`, y surten los mismos en el elemento seleccionado. Los elementos hermanos no son afectados como podemos ver en el siguiente ejemplo:

```css
.container { align-items: flex-end; }
#c { align-self: flex-start; }
```

### Wrap and flow

Cuando hay demasiados elementos para que encajen dentro de una fila o columna de un container, los podemos dividir en varias líneas utilizando la propiedad `flex-wrap`. El valor por defecto (`nowrap`), resguarda a todos los elementos en la misma línea, mientras que `wrap` los divide sobre líneas extra.

```css
.flex-container { flex-wrap: wrap; }
```

Utilizando el valor `wrap-reverse`, podemos cambiar la dirección para que las nuevas líneas aparezcan por arriba.

### Acortamiento para `flex-flow`

Podemos combinar `flex-wrap` con `flex-direction` con la propiedad `flex-flow`. Por ejemplo:

```css
E { flex-flow: column wrap-reverse; }
```

### Alinear varias líneas con `align-content`

Cuando los elementos estén sobre varias líneas, podemos controlar su alineación con la propiedad `align-content`. Esta propiedad funciona como `justify-content`, solo que en el axis cruzado, y cuenta con los mismos valores posibles, `flex-start`, `flex-end`, `center`, `space-between`, `space-around`y también uno nuevo, `stretch`, que redminesiona los elementos para rellenar todo el espacio sin utilizar.