---
layout: post
title: Enlaces a puntos de ancla suaves
date: 2015-07-31 14:36:00
disqus: y
---

<style>
</style>

Hola de nuevo, hoy vengo con un pequeño script que hace que el movimiento que generan los enlaces a la misma página, o puntos de ancla (<i>anchor</i> en inglés), sea suave y no instantáneo. Voy a empezar nombrando algunas características más de los puntos de ancla y cómo se crean para que los conozcáis un poco más y luego pasaré a explicar el pequeño código que uso para hacer el movimiento suave.

Como he dicho antes, un punto de ancla es un enlace a un punto dentro de nuestro archivo HTML. Imaginaos que tenemos un archivo con varias secciones y un menú al principio. Lo que tendríamos que hacer para que el menú nos llevase a cada una de esas partes es lo siguiente.

```HTML
<a href="#nombredelaseccion">Ir a Seccion 1</a>
```

Donde #nombredelaseccion es el atributo name del a donde vamos a desplazarnos.

```HTML
<a name="#nombredelaseccion"><h2>Seccion 1</h2></a>
```

Y así sucesivamente con todas las secciones. Cabe destacar que podemos crear un link a un punto de ancla de otro archivo, de modo que no solo cargue el archivo sino que nos lleve a un punto determinado del mismo.

```HTML
<a href="nombredelarchivo.html#nombredelaseccion">Ir al segundo archivo, seccion 1</a>
```

Si queréis comprobar como funcionaría esto, os dejo un ejemplo en vivo para que podáis verlo por vosotros mismos <a href="https://jsfiddle.net/s4o4feug/" target="_blank">aquí</a>. Si habéis entrado observaréis que el cambio es inmediato y muy brusco, tal como ocurría con <a href="http://legomolina.github.io/2015/07/31/smooth-links/" target="_blank">el cambio de color de los links</a>.

Para solucionar esto os voy a enseñar un pequeño script con jquery para que estos enlaces sean suaves. Os dejo el ejemplo <a href="https://jsfiddle.net/5z8365oq/1/" target="_blank">aquí</a>.

Lo primero que tenemos que hacer es, obviamente, importar la librería jquery a nuestro archivo. Una vez hecho eso escribiremos el siguiente código:

```javascript
window.onload() {
	$(".menu-button").click(function(e) { //asignamos una funcion anónima a todos los <a> que queremos que tengan la propiedad de moverse con suavidad

	});
};
```

Donde .menu-button es el selector que usaremos para seleccionar todos los enlaces ```<a>``` que queramos. Yo he usado el atributo class por la comodidad de seleccionar todos a la vez pero podéis emplear el que queráis. Una vez seleccionados todos los botones les asignamos una función anónima cuando se llame al evento onclick del link.

```javascript
window.onload() {
	$(".menu-button").click(function(e) { //asignamos una funcion anónima a todos los <a> que queremos que tengan la propiedad de moverse con suavidad
		e.preventDefault(); //con esto evitamos que hagan cualquier movimiento extraño antes de la animación
		var puntero = $(this).data('zone'); //cojemos el target del movimiento (a donde se va a mover la página)
		var distancia = $('div[id^="' + puntero + '"]').offset(); //capturamos la distancia que hay desde arriba del documento hasta nuestro target
	});
};
```

```HTML
<a href="#" class="menu-button" data-zone="seccion1">Ir a sección 1</a>
```
```HTML
<div id="seccion1">Seccion 1</div>
```

Bien, llegados a este punto tenemos que definir las zonas o secciones y lo haremos con divs y una id. Si recordáis, antes hemos empleado el atributo name de la etiqueta a para crear los puntos de ancla pero esta vez optaremos por divs con una id única. Si por algún motivo no queremos que sean divs en la línea: 

```javascript
var distancia = $('div[id^="' + puntero + '"]').offset(); //capturamos la distancia que hay desde arriba del documento hasta nuestro target
```

Cambiamos div por la etiqueta elegida e id por el atributo que queremos que sea el nombre. Esto es útil si en vez de divs usamos encabezados ```<h>``` y queremos que sean estos los delimitadores de secciones. Para hacer esto cambiaríamos el código por el siguiente:

```javascript
var distancia = $('h1[id^="' + puntero + '"]').offset(); //capturamos la distancia que hay desde arriba del documento hasta nuestro target
```

Por otra parte tenemos que configurar los enlaces para que sepan a dónde tienen que dirigirnos. Para eso usaremos el atributo data- de HTML5 junto con el nombre que queramos para ir a la zona deseada. Si queremos que en vez de zone sea data-go en el script tendremos que cambiar .data('zone') por .data('go') donde aparezca.

```javascript
window.onload() {
	$(".menu-button").click(function(e) { //asignamos una funcion anónima a todos los <a> que queremos que tengan la propiedad de moverse con suavidad
		e.preventDefault(); //con esto evitamos que hagan cualquier movimiento extraño antes de la animación
		var puntero = $(this).data('zone'); //cojemos el target del movimiento (a donde se va a mover la página)
		var distancia = $('div[id^="' + puntero + '"]').offset(); //capturamos la distancia que hay desde arriba del documento hasta nuestro target

	    $('body, html').animate({ //creamos la animación para el body
	        scrollTop: distancia.top - 50 + 'px' //que mueva el scroll desde nuestra posicion hasta la distancia en vertical que se encuentra nuestro target
	    }, 600); //en el tiempo que queramos (milisegundos)
	});
};
```

Por último añadimos la animación al cuerpo de nuestra página. Si queda alguna duda, los -50 px son para ajustar un poco la distancia, os recomiendo que lo hagáis ya que a veces la distancia la coje un poco más arriba dependiendo de la posición de nuestro div target.
Como véis es muy fácil hacer que el movimiento de la web no quede brusco, solo hace falta un poco de jquery. Espero que os haya servido y nos vemos en la próxima entrada.
Os vuelvo a dejar los enlaces a los ejemplos en vivo para que podáis ver como queda el movimiento: <a href="https://jsfiddle.net/s4o4feug/" target="_blank">sin jquery</a>, <a href="https://jsfiddle.net/5z8365oq/1/" target="_blank">con jquery</a>.