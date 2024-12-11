# 1 - Introduciendo CSS3

## Qué es CSS3 y cómo se convirtió en lo que es ahora

### Breve historia sobre CSS3

La última versión principal de CSS fue CSS2.1, una revisión de CSS2 que había sido lanzada en 1997, y el primer navegador que dio soporte completo a esta especificación fue Internet Explorer 8, lanzado en 2009.
<br>
El desarrollo de CSS3 inició en 1998, pero debido a que la implementación de CSS2 en los navegadores de la época era demasiado inconsistente, el W3C suspendió el desarrollo de la nueva versión y se enfocó en continuar trabajando con CSS2.1. Para 2005 se continuó con el trabajo de los módulos de CSS3.
<br>
Internet Explorer dominaba el mercado de los navegadores, y debido a que se rehusaba a implementar CSS3, una oleada de navegadores surgió para competir por usuarios, teniendo como principal objetivo ofrecer a desarrolladores y usuarios nuevas tecnologías. Y qué mejor forma de traer nuevos añadidos que implementando soporte para la espeficación CSS3.
<br>
Actualmente la espeficación CSS3 se encuentra bajo desarrollo constante y usado por una gran variedad de navegadores.

### CSS3 es modular

El W3C, consciente que estandarizar un nuevo lenguaje de estilos tomaría bastante tiempo, decidió dividir a CSS3 en varios módulos. Cada uno de estos módulos podría ser trabajado por distintos autores a distintos ritmos, y el proceso de implementación sería escalonado.
<br>
Es por esto que en lugar de un solo documento de espeficación para CSS3, existe el Módulo de Interfaz Básica de Usuario de CSS3 (_CSS3 Basic User Interface Module_), los Selectores Nivel 3 (_Selectors Level 3_), Consultas de Medios (_Media Queries_), etc.

### No existe tal cosa como CSS3

Dado que CSS se ha convertido en algo modular, a cada módulo se le asigna un número de nivel para marcar por cuántas revisiones ha pasado. Algunos módulos se encuentran en Nivel 4 (como los Selectores), otros están en Nivel 3, mientras que los módulos nuevos están apenas en Nivel 1.
Esto quiere decir que CSS es un estándar en  constante cambio, cada módulo se estará desarrollando a su propio ritmo, y los nuevos módulos se añadirán mientras se hallan nuevas características.
<br>
Cuando decimos CSS3, nos referimos meramente a "Características de CSS agregadas desde CSS2.1." CSS3 es un estándar, y nunca veremos algo como CSS4.

## Estado de los módulos y el Proceso de Recomendación

El Estado de un módulo se asigna por el W3C, e indica el prgreso del módulo a través del proceso de recomendación. A pesar de esto, el estado de un módulo no es necesariamente un indicador de qué tan implementado se encuentra el módulo en los navegadores.

Cuando un documento propuesto se acepta como parte de CSS3, a su estado se le denomina _Working Draft_ (Borrador en progreso). Este estado significa que el documento ha sido publicado y se encuentra listo para ser revisado por la comunidad.

Antes de que un documento pueda progresar de un Working Draft, su estado cambia a _Last Call_ (Última llamada), lo que quiere decir que el período de revisión está por cerrarse, y que el documento está listo para avanzar al siguiente nivel.
<br>
El siguiente nivel es _Candidate Recommendation_ (Recomendación Candidata), y significa que el documento es aceptable para el W3C, y a este punto los desarrolladores de navegadores empezarán a implementar las propiedades en el documento para recabar feedback.
<br>
Cuando dos o más navegadores han implementado las propiedades de la misma forma mientras no hayan problemas técnicos, el documento progresa a un _Proposed Recommendation_ (Recomendación Propuesta), este estado significa que la propuesta está implementada y lista para ser aprobada por el Comité Asesor del W3C, una vez que haya sido aprobada, la propuesta se convierte en _Recommendation_ (Recomendación).

## Introducción a la sintaxis

```css
E { property: value; }
```

En este ejemplo el selector se representa con _`E`_. Posteriormente, tenemos la propiedad, en este caso, llamada `property`, seguido de esta, contamos con el valor de la propiedad, al que hemos llamado `value`.
<br>

## Prefijos de los Vendors

Debido a los constantes cambios y el hecho de que los navegadores necesitan implementar características. Es posible que las características sean implementadas de forma inconsistente entre navegadores, por lo que los vendors de cada navegador incluyen su propio prefijo al inicio de propiedades experimentales.
<br>
Supongamos que tenemos una propiedad llamada `monkeys` que ha sido recientemente definida en una especificación, y que varios navegadores principales la hayan decidido implementar, en ese caso, es necesario utilizar el siguiente código:

```css
E {
-moz-monkeys: value; /* Firefox */
-ms-monkeys: value; /* Internet Explorer */
-webkit-monkeys: value; /* Chrome/Safari */
}
```

Aunque esto puede llevar a problemas para los vendors, por ejemplo, los desarrolladores podrían haber usado las nuevas propiedades en sus páginas web, pero no eliminaron los prefijos de los vendors cuando la implementación de las propiedades haya cambiado en los navegadores. Esto ha llevado a que los vendors de los navegadores se vean en la necesidad de continuar el soporte para características experimentales para siempre para evitar errores en páginas web que los usen.