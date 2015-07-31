---
layout: post
title: Cambios de color suaves
date: 2015-07-31 13:12:00
disqus: y
---

<style>
.link {
	color: red;
	-webkit-transition: all 0.5s ease;
    -moz-transition: all 0.5s ease;
    -o-transition: all 0.5s ease;
    -ms-transition: all 0.5s ease;
    transition: all 0.5s ease;
}

.link:hover, .no-link:hover{
	color: green;
}

.no-link {
	color: red;
}
</style>

Buenos días, hoy os traigo un trozo de CSS bastante útil que vale, sobretodo, para cambiar de color los <i>links</i>. Como ya sabeis muchos (y los que no seguid leyendo) en los enlaces de nuestra web, los que se crean con la etiqueta a, tienen varios selectores CSS exclusivos que facilitan los cambios de color cuando un usuario pasa el ratón por encima, o ya han sido visitados por ejemplo. Esto es tan fácil como poner los siguientes selectores después de la etiqueta en nuestro archivo .css.

```CSS
a:link {
	/* Aqui se aplica a cualquier link en su estado original sin haber sido visitado */
}

a:visited {
	/* Este estilo se aplica solo a aquellos que han sido visitados anteriormente */
}

a:active {
	/* Este estilo se aplica mientras haces click con el ratón */
}

a:hover {
	/* Este se aplica si el puntero del ratón está sobre el link */
}
```

Aquí os dejo la web oficial del [W3Schools (inglés)](http://www.w3schools.com/css/css_link.asp) donde se explica mejor que hace cada uno.

Vamos ahora con la parte "histórica": hasta hace unos años, cuando CSS3 no existía, si queríamos hacer un efecto como este: <span class="link">EFECTO CHULO</span> teníamos que usar casi obligatoriamente la librería jquery y su método .animate(). Si no la usábamos obteníamos el siguiente efecto <span class="no-link">EFECTO NO TAN CHULO</span>.

Hoy en día, además de que CSS3 es mucho más ligero, también es más fácil y organizado ya que lo tendremos todo en el mismo archivo sin necesidad de importar librerías ni crear trozos de script por toda nuestra página.

---

Después de la teoría y la historia os voy a enseñar como hacerlo. En CSS3 tenemos las transiciones (ya las explicaré más en profundidad) y con ellas se pueden hacer esas cosas de manera muuy sencilla con un par de líneas de código.

Primero tenemos que poner que dos colores queremos que se vean:

```CSS
a {
	color: red; /* Color principal */	
}

a:hover {
	color: green; /* Color al pasar el ratón por encima */
}
```

Después añadimos las transiciones: 

```CSS
a {
	color: red; /* Color principal */
    transition: all 0.5s ease; /* El tiempo se puede cambiar al que se quiera (1s, 2s, 0.8s, 0.1s ...). */
}

a:hover {
	color: green; /* Color al pasar el ratón por encima */
}
```

Esto debería funcionar en todos los navegadores pero como cada uno va a su aire añadimos las extensiones para todos y así nadie se queja:

```CSS
a {
	color: red; /* Color principal */
    transition: all 0.5s ease; /* El tiempo se puede cambiar al que se quiera (1s, 2s, 0.8s, 0.1s ...). */
    -webkit-transition: all 0.5s ease;
    -moz-transition: all 0.5s ease;
    -o-transition: all 0.5s ease;
    -ms-transition: all 0.5s ease;
}

a:hover {
	color: green; /* Color al pasar el ratón por encima */
}
```

Y con esto ya tendríamos funcionando nuestros links de manera más suave y bonita. 

Esto no se aplica solo a los links ya que el selector :hover se puede poner a casi todas las etiquetas de HTML. De hecho el ejemplo anterior no era un link sino un SPAN. De todas formas ya traeré más cosillas con esto para que veais todo el potencial que tiene.

Espero que os haya gustado y, sobretodo, os haya resultado útil. Nos vemos en el siguiente post <i class="fa fa-smile-o"></i>.