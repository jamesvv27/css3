# 3 - Selectors

Los Selectors son el núcleo de CSS desde CSS3.

Los selectors pueden ser separados en dos categorías. La primera abarcando a aquellos que actúan directamente en elementos definidos en el árbol del documento (como los elementos `p` o `href`); esta categoría contiene los selectors `class`, `type` y `attribute`. A estos los llamaremos _DOM selectors_
<br>
La segunda categoría contiene a los `pseudo-selectors`, que actúan en elementos o información que se encuentra fuera del árbol del documento (como la primer letra de un párrafo o el último elemento hijo de un elemento padre).

CSS3 nos provee con tres nuevos selectors de atributos y un _combinator_, que consiste en un selector que une a otros selectors.

## Selectors de atributos

Los selectors de atributos fueron introducidos en CSS2, y permiten colocar reglas que coincidan con elementos basándose en sus atributos --como `href` o `title`-- y los valores de esos atributos.
Los cuatro selectors definidos en CSS2 son:

```css
E[attr] {...} /* Selector de Atributos Simple */
E[attr='value'] {...} /* Selector de Atributos por Valor Exacto */
E[attr ~='value'] {...} /* Selector de Atributos por Valor Parcial */
E[attr|='value'] {...} /* Selector de Atributos por Lenguaje */
```

El _Selector de Atributos Simple_ aplica las reglas a los elementos que tengan el atributo especificado definido, sin importar el valor del mismo atributo.

```css
a[rel] {
	color: #ff0000;
	}
```

Si deseamos ser más específicos, podemos usar el _Selector de Atributos por Valor Exacto_ para seleccionar únicamente los elementos que tengan exactamente el mismo valor definido:

```css
a[rel='friend'] {
		color: #ff0000;
		}
```

Para seleccionar elementos que tengan un valor especificado como parte de una lista, usaremos el _Selector de Atributos por Valor Parcial_.

```css
a[rel~='friend'] { 
		color: #ff0000;
		}
```

El _Selector de Atributos por Lenguaje_ aplica las reglas a elementos que tengan un atributo que coincida con el primer argumento en el selector. Por ejemplo, si tenemos dos elementos `<a>` que tienen un atributo `lang`, en el cual el valor en un elemento es (`es-ES`) y en el otro es (`es-MX`) y queremos seleccionar ambos, podemos usar el siguiente código:

```css
a[lang|='es'] {
		color: #ff0000;
		}
```

## Nuevos Selectors de Atributos en CSS3

Los nuevos selectors de CSS3 pueden ser bastante útiles para documentos XML con su funcionalidad para buscar coincidencias en sub-cadenas dentro del valor de un atributo.

### Beginning Substring Attribute Value Selector

Mejor conocido como el _Beginning selector_, este encuentra elementos cuyo atributo elegido comience con la cadena de carácteres proporcionada. La sintaxis completa de este selector es la siguiente:

```css
E[attr^='value'] {...}
```

Veamos un ejemplo de este selector:

```css
a[title^='image'] {...}
```

Las reglas se aplicarán a cualquier elemento `<a>` cuyo atributo `title` **comience** con la palabra _image_.

Un ejemplo aplicado en una página web puede ser el siguiente:

```html
<p>
	This is a
	<a href="http://example.com/">
		hyperlink
	</a>
	.
</p>
```

Al visualizar este enlace es difícil saber si se trata de un redireccionamiento a una página del mismo sitio web o a un URL externo. Con el Beginning Selector, podemos identificar el protocolo del enlace (_http_) y añadir un ícono de URL externo a todos los enlaces que comiencen con el protocolo _http_:

```css
a[href^='http'] {
		background: url('link.svg') center left no-repeat;
		display: inline-block;
		padding-left: 20px;
		}
```

### Ending Substring Attribute Value Selector

También conocido como el _Ending Selector_, funciona del mismo modo que el Beginning Selector, solo que buscará coincidencias con la última palabra del valor del atributo proporcionado. Su sintaxis es la siguiente:

```css
E[attr$='value'] {...}
```

Aplicado en una página, podemos usar este selector para mayor claridad a enlaces, solo que esta vez por las terminaciones de un archivo:

```css
a[href$='.pdf'] {
		background-image: url('pdf.svg') 
		}
```

### Arbitrary Substring Attribute Value Selector

A este lo podremos llamar como _Arbitrary Selector_, este selector funciona de la misma forma que los dos anteriores, solo que busca las coincidencias en **cualquier** lugar del valor del atributo. La sintaxis de este selector es la siguiente:

```css
E[attr*='value'] {...}
```

La gran diferencia entre este, y el Selector de Valor Parcial de CSS2, es que en el Arbitrary Selector se buscan coincidencias mediante sub-cadenas de carácteres, mientras que en el anterior, las coincidencias se encuentran buscando entre una lista de valores separada por espacios.

### Varios Selectors de Atributos

Se pueden concatenar varios selectors juntos, esto permite que seamos realmente específicos con nuestras búsquedas.

```html
<p>
	<a href="http://example.com/folder1/file.pdf">
		Example
	</a>
</p>
<p>
	<a href="http://example.com/folder2/file.pdf">
		Example
	</a>
</p>
```

Si deseamos aplicar reglas únicamente al segundo elemento `<p>`, podemos concatenar selectors de la siguiente forma:

```css
a[href^='http://'][href*='/folder2/'][href$='.pdf'] {...}
```

## El General Sibling Combinator

Este nuevo selector introducido en CSS3 es una extensión del _Adjacent Sibling Combinator_ de CSS2, y sus sintaxis se diferencían por un carácter:

```css
E + F {...} /*Adjacent Sibling Combinator*/
E ~ F {...} /*General Sibling Combinator*/
```

El Adjacent Sibling selecciona únicamente a un elemento _`F`_ que haya sido inmediatamente precedido por un elemento hermano _`E`_, mientras que el General Sibling selecciona a todos los elementos _`F`_ que sucedan al elemento _`E`_ (que de igual forma, debe ser un elemento hermano).

## Soporte en navegadores para Selectors:

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
			New attribute selectors
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
			General sibling Combinator
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
