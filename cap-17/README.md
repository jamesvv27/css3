# 17 - Disposición de Grids

Los grids son una técnica de diseño fundamental.

## Terminología de los Grids

Los siguientes son términons clave para el Módulo de Grids:

* **Container de grid (Grid Container)**: El elemento container que define los límites y dimensiones del grid.
* **Líneas de grid (Grid lines)**: Las líneas divisorias entre filas y columnas.
* **Pistas de grid (Grid Tracks)**: Nombre acortado para las filas y columnas. A cada columna o fila de un grid se le conoce como _track_.
* **Celdas de grid (Grid cells)**: Cada intersección de una columna y una fila crea una _celda_.
*  **Áreas de grid (Grid areas)**: Una o varias celdas que marcan el espacio en el que un _espacio grid_ se colocará.
* **Espacios o items de grid (Grid items)**: Cada elemento hijo colocado en el grid.

Un grid se crea definiendo un número de líneas en el container grid para crear una serie de pistas. Los espacios del grid se posicionan en las pistas usando las líneas como coordenadas para crear áreas.

## Declarando y definiendo el Grid

El primer paso para crear un grid es declarar el _container del grid_. Las dimensiones del container grid son los límites del grid, y todas las propiedades del grid se le aplican al container. Para declarar el container grid, hacemos esto:

```css
E { display: grid; }
```

Lo siguiente es definir las pistas (las filas y las columnas). Podemos definir las pistas en un _grid explícito_ con un número preciso de filas y columnas, o en un _grid implícito_, que se crea relativo a su contenido. También es posible combinarlos.

### Crear grids explícitos definiendo el tamaño de las pistas

En un grid explícito, podemos definir un número específico de pistas ajustando su tamaño usando un par de propiedades: `grid-template-columns` y `grid-template-rows`. El valor para cada propiedad es una lista de longitudes separada por espacios, que ajusta el ancho de la columna o el alto de la fila.

```css
E { grid-template-columns: 20% 60% 20%; }
```

Podemos usar porcentajes o cualquier unidad de longitud así como _fracciones_ (_`fr`_), que es equivalente a una parte de una longitud sin asignar.

```css
E { grid-template-columnds: 100px 100px 200px 1fr; }
```

Del mismo modo, podemos añadir filas, si por ejemplo usamos el valor `auto`, la altura de la fila será igual a la altura de su contenido.

```css
E { grid-template-rows: 60px auto 5em; }
```

Al combinar estas propiedades podemos definir completamente el grid.

```css
E {
	display: grid;
	grid-template-columns: 1fr 3fr 1fr;
	grid-template-rows: 60px auto 5em;
}
```

### Colocar items en un grid explícito

Cualquier hijo inmediato de un container grid se convierte en un item de grid y debe de ser colocado dentro del grid. Para hacer esto, asignamos al item una coordenada de una celda usando una serie de propiedades de colocación. `grid-column-start` y `grid-row-start` nos permiten asignar las coordenadas tomando un número entero como valor, qeu se refiere a la línea al comienzo de una pista de grid. La combinación de ambas referencias crean la coordenada de una celda.

```css
F {
	grid-column-start: 2;
	grid-row-start: 2;
}
```

El valor predeterminado de ambas propiedades es 1, por lo que omitir alguno de los valores los coloca en la primer fila o columna.

Por defecto, el item encaja únicamente en la celda designada. Podemos hacer que un item tenga un área que abarque varias celdas usando las propiedades `grid-column-end` y `grid-row-end`.

```css
F {
	grid-row-start: 1;
	grid-row-end: 4;
}
```

También podemos usar la palabra clave `span` por si de momento no estaremos seguros sobre la línea en que un item de grid comenzará, pero también queremos siempre que abarquen el mismo número de columnas o filas.

```css
F { grid-row-end: span 3; }
```

### Propiedades acortadas de colocación de grids

Escribir cuatro propiedades individuales para colocar un elemento en un grid puede sesr algo tedioso, es por esto que contamos con las propiedades `grid-column` y `grid-row`, que abarcan de forma corta las propiedades `grid-column-start`, `grid-column-end`, `grid-row-start` y `grid-row-end` respectivamete.

De este modo, esto:

```css
F {
	grid-column-start: 2;
	grid-column-end: 3;
	grid-row-start: 1;
	grid-row-end: span 3;
}
```

Se acorta con esto:

```css
F {
	grid-column: 2 / 3;
	grid-row: 1 / span 3;
}
```

Y esto lo podemos acortar aún más con la regla acortada `grid-area`, que tiene esta sintaxis:

```css
F { grid-area: row-start / column-start / row-end / column-end; }
```

### Repetir líneas grid

Los grids más complejos nos dan mayor control sobre nuestro contenido.

Si tenemos un grid de 12 columnas y queremos evitarnos escribir repetitivamente las columnas individualmente, podemos usar la función `repeat()`. Esta función toma dos argumentos: un entero que define el número de repeticiones, seguido de una coma que lo separa del siguiente valor, que son los valores de las líneas grid a repetir.

```css
E { grid-template-columns: 1fr repeat(11, 10px 1fr); }
```

El ejemplo anterior repite un el patrón de `10px 1fr` 11 veces, y nos da el mismo resultado que escribir lo siguiente:

```css
E { grid-template-columns: 1fr 10px 1fr 10px 1fr 10px 1fr 10px 1fr 10px 1fr
10px 1fr 10px 1fr 10px 1fr 10px 1fr 10px 1fr 10px 1fr; }
```

### Nombrar áreas grid

Además de colocar items en un grid basándonos en coordenadas, también podemos colocar items en _áreas nombradas_ con la propiedad `grid-template-areas`. Con esta propiedad le podemos dar a áreas grid nombres específicos usando una serie de identificadores.

```css
E {
	display: grid;
	grid-template-areas: 'a b c';
	grid-template-columns: repeat(3, 1fr);
}
```

Creando tres columnas, la propiedad `grid-template-areas` le da nombre a cada una de las columnas con una cadena de carácteres separada por espacios.

Entonces, para colocar un item en un área nombrada, usamos el identificador del área como un valor en la propiedad `grid-area` del item.

```css
F { grid-area: b; }
```

Cada cadena de identificadores representa una fila, y si queremos agregar una nueva fila, tenemos que añadir una nueva cadena.

Si repetimos los identificadores en una misma cadena el área abarcará ese número de columnas, y si colocamos un mismo identificador en distintas cadenas pero en las mismas posiciones, el área abarcará ese determinado número de filas.

```css
E {
	display: grid;
	grid-template-areas:
	'nav head head'
	'nav main side';
	grid-template-columns: repeat(3, 1fr);
	grid-template-rows: 80px auto;
}
```

### Grids Implícitos

Los grids implícitos se definen por sus contenidos en vez de por una longitud especificada.

Podemos usar las propiedades `grid-auto-columns` y `grid-auto-rows` para que cada item tenga un lugar en el grid sin tener una cifra exacta de cúantas celdas deseamos tener.

```css
E {
	display: grid;
	grid-auto-columns: 1fr;
	grid-auto-rows: 80px;
}
```

Cada propiedad toma un solo valor para esspecificar el ancho de la fila o de la columna. Es entonces que cualquier item con un valor `grid-column` o `grid-row` se colocará en el grid, y el grid automaticamente ajustará su tamaño para retener los items.

### Items de grid sin un lugar declarado

Si los hijos de un container grid no tienen declarado un lugar en el espacio, sus valores `grid-column` y `grid-row` tendrán su valor predeterminado de 1, por lo que varios items se apilarán en la misma celda.

Esto lo podemos alterar con la propiedad `grid-auto-flow`, que hace que cualquier item sin un lugar asignado se inserte en algun espacio disponible en el grid.

```css
E { grid-auto-flow: keyword; }
```

El valor de palabra clave puede ser `column` o `row`. Al usar `column`, los items llenarán las celdas vacías en el orden de las columnas. Lo mismo sucede si usamos `row`, pues los items empezarán a apilarse entre las filas vacías.

## Combinar grids explícitos e implícitos

Al crear grids explícitos, puede que nos encontremos con situaciones en las que nuestros contenidos tengan que sobrepasar una o varias pistas más.

```css
E {
	grid-template-columns: repeat(3, 1fr);
	grid-template-rows: repeat(2, 80px);
	grid-auto-columns: 1fr;
	grid-auto-rows: 80px;
}
```

Este código crea 3 columnas con 2 filas explícitas, y permite que a cualquier item que exceda los límites del grid explícito se le asigne un lugar en 1 celda implícita.

### Propiedad acortada `grid`

La sintaxis para abarcar las propiedades de la familia de grids es la siguiente:

```css
E { grid: grid-auto-flow grid-auto-columns / grid-auto-rows; }
```

## Orden de apilamiento de items grid

Si los items en un mismo grid se cruzan entre sí, podemos ajustar su orden de apilamiento con la propiedad `z-index`. Los items con el mayor valor de esta propiedad se apilarán por encima de todos los demás.

```css
.item-one {
	grid-column: 2 / 4;
	grid-row: 2;
}
.item-two {
	grid-column: 1 / 3;
	grid-row: 1 / 3;
	z-index: 2;
}
```