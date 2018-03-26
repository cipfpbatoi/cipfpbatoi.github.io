# Conceptos básicos
Aquí veremos lo básico para conover el framework Vue2 y ser capaces de utilizarlo como plataforma de desarrollo de aplicaciones web.

Este material está basado en la [guía oficial de Vue2](https://vuejs.org/v2/guide/) y veremos además los servicios de vue-router y axios entre otros.

Vue es un framework progresivo para la construcción de interfaces de usuario desde el lado del cliente. Lo de framework
"progresivo" significa que está diseñado para ser crecer: su núcleo está enfocado sólo en la capa de visualización (como React) pero es fácil añadirle otras bibliotecas o proyectos existentes (algunos desarrollados por el mismo equipo de Vue) que nos permitan crear incluso complejas SPA.

**¿Qué framework es mejor?**
Depende de la aplicación a desarrollar y de los gustos del programador. Tenéis algunos enlaces al respecto:
* [Comparativa VueJs](https://vuejs.org/v2/guide/comparison.html)
* [Comparativa Openwebminars](https://openwebinars.net/blog/los-6-mejores-frameworks-javascript/?utm_source=customer-io&utm_medium=newsletter)
* [Openwebminars: Vue vs Angular](https://openwebinars.net/blog/vue-vs-angular/)
* [Carlos Azaustre: Vue vs Angular (vídeo)](https://www.youtube.com/watch?v=jTtab_rnvic)
* [Angular vs. React vs. Vue: A 2017 comparison](https://medium.com/unicorn-supplies/angular-vs-react-vs-vue-a-2017-comparison-c5c52d620176)
* ...


## Instalar Vue
Para utilizar Vue sólo necesitamos enlazarlo en nuestra página desde un CDN:
```[HTML]
<!-- development version, includes helpful console warnings -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```
o
```[HTML]
<!-- production version, optimized for size and speed -->
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
```

Más adelante usaremos la herramienta `vue-cli` para crear un completo _scaffolding_ para nuestras aplicaciones (donde 
podremos fácilmmente incluir otras bibliotecas, trabajar con componentes o construir una SPA de forma sencilla).

## Hello World
Vamos a ver cómo se hace una página con Vue viendo un [ejemplo en JSFiddle](https://jsfiddle.net/chrisvfritz/50wL7mdz/).

### HTML
En en HTML debemos vincular los scripts de la librería de Vue y de nuestro código. 

Vue se ejecutará dentro de un elemento de nuestra página (al que se le poner como id _app_) que en este caso es un `<div>`.
Dentro de ese elemento podemos usar expresiones de Vue. En este ejemplo se usa el _moustache_ ( `{{ ... }}` ) que muestra en
la página la variable o expresión Javscript que contiene.

### Javascript
En el fichero JS debemos crear un nuevo objeto Vue que recibe como parámetro un objeto con varias propiedades:
* el: el elemento que contendrá la aplicación identificado en notación CSS (# para id, . para clase, ...). Si hubiera más 
de 1 elemento identificado así se cogería sólo el primero (es como hacer un querySelector del mismo)
* data: objeto donde definiremos todas las variables que vamos a usar en la vista. En nuestro caso sólo tenemos una que 
es _message_. A cada variable le debemos dar un valor inicial.
* pueden haber más como methdos (objeto con métodos que podemos llamar desde la vista), props (array de variables que se 
pasan de inicio, usado en componentes), computed (propiedades calculadas),... que veremmos más adelante.

### _Binding_ de variables
Para probar su funcionamiento conviene que nos descarguemos los ficheros y los abramos en local.

Fichero HTML:
```[HTML]
<!DOCTYPE html>
<html>
<head>
  <title>Hello world</title>
</head>
<body>

  <div id="app">
    <p>{{ message }}</p>
  </div>

  <script src="https://unpkg.com/vue"></script>
  <script src="01-HelloWorld.js"></script>
</body>
</html>
```
Nuestro código debemos cargarlo después de cargar la librería y de crear el elemento HTML que cnotenga la aplicación.

Fichero JS:
```[Javascript]
var miApp = new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue.js!'
  }
})
```

Hemos creado una variable _miApp_ que contiene nuestro objeto Vue y que podemos ver y manipular desde la consola. Si cambiamos el valor de la variable _message_
```[Javascript]
miApp.message = "Hola Vue2!";
```
vemos que cambia lo que muestra nuestra página.

Esto es porque Vue (al igual que Angular o React) enlazan el DOM y los datos de forma que cualquier cambio en uno se refleja automáticamente en el otro.

Para mostrar un dato en el DOM usamos `{{ }}` pero si queremos nostrarlo como atributo de una etiqueta debemos usar `v-bind`:
```[HTML]
  <p v-bind:title="message">
    Hover your mouse over me for a few seconds
    to see my dynamically bound title!
  </p>
```
Vue incorpora estos '_atributos_' que podemos usar en las etiquetas HTML y que se llaman **directivas**. Todas las directivas comienzan por `v-`. Como la directiva `v-bind` se utiliza mucho se puede abreviar símplemente como `:`. El siguiente código es equivalente al de antes:
```[HTML]
  <p :title="message">
```
Tanto `{{ }}` como `v-bind` son un enlace unidireccional: muestran en el DOM el valor de un dato y reaccionan ante cualquier cambio en dicho valor. Además está la directiva `v-model` que es un enlace bidireccional que enlace un dato a un campo de formulario y permite cambiar el valor del campo al cambiar el dato pero también cambia el dat si se modifica lo introducido en el input. 
```[HTML]
  <input v-model="message">
```
Vemos que al escribir en el _input_ automáticamente cambia lo mostrado en el primer párrafo. Esta característica nos permite ahorrar innumerables líneas de código para hacer que el DOM refleje los cambios que se producen en los datos (cosa que no tiene por ejemplo la librería jQuery).

### [Vue devtools](https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd?utm_source=chrome-app-launcher-info-dialog)
Es una extensión para Chrome que nos permite inspeccionar nuestro objeto Vue y acceder a todos los datos de nuestra aplicación. Conviene instalarlo porque nos ayudará mucho a depurar nuestra aplicación, especialmente cuando comencemos a usar componentes.

Para trabajar sin servidor hay que habilitar el acceso a ficheros en la extensión.

