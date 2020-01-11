# Clase60 
## Introduccion al DOM

* El `DOM` (document object model) proporciona una representación estructural de un documento html, permitiendo la modificación de su contenido
* Esto significa que tenemos acceso a elementos que tienen propiedades, métodos y eventos disponibles para crear, eliminar y modificar elementos en un documento web

![DOM](http://girldevelopit.github.io/gdi-featured-js-intro/dist/img/dom-tree.png)

* Podes leer más sobre `dom` en el [sitio del MDN](https://developer.mozilla.org/es/docs/DOM)

### Selectores
* Para poder interactuar con los elementos y el documento lo primero que tenemos que hacer es poder seleccionarlos
* Existen formas de acceder a los elementos de una página de manera muy simple utilizando el concepto de selectores
* Cada selector puede retornar un solo elemento o una lista según cual sea la intención del selector
* El objeto document tiene los siguientes selectores (los más conocidos) como método:
  * **getElementById:** acepta un string con el valor del atributo ID como parámetro y retorna un elemento. Retorna null en caso de no encontrar el elemento buscado.
  * **getElementsByTagName:** acepta un string con el valor del  nombre del TAG como parámetro y retorna una lista/array de elementos. Retorna una lista/array vacía en caso de no encontrar elementos del TAG buscado.
  * **getElementsByClassName:** acepta un string con el valor del atributo class como parámetro y retorna una lista/array de elementos. Retorna una lista/array vacía en caso de no encontrar elementos con la class buscada.
  * **querySelector:** acepta un string con un selector de css como parámetro y retorna un elemento que esté dentro del rango seleccionado utilizando el css query. Retorna null en caso de no encontrar elemento en dicho contexto
  * **querySelectorAll:** acepta un string con un valor de selector de css como parámetro y retorna una array de elementos que estén comprendidos en el contexto de búsqueda utilizando el query de css. Retorna una array vacío en caso de no encontrar elementos en dicho contexto.


**Ejemplo:**
```html
<body>
  <p>Un texto</p>
  <p class="rojo">Un texto en rojo</p>
  <p class="rojo">Un texto en rojo</p>
  <p class="azul">Un texto en azul</p>
  <p id="principal">Un texto principal</p>
</body>
```

```js
// obtenemos una referencia al elemento con id="principal"
var elemento = document.getElementById('principal');

// obtenemos una colección con todos los elementos de tag <p> de nuestro documento
var elementosP = document.getElementsByTagName('p');

// obtenemos una referencia al elemento con el contenido 'Un texto'
var otroElemento = document.querySelector('p');

// obtenemos una colección con todos los elementos párrafo de nuestro documento que tienen la clase 'rojo'
var elementosRojos = document.querySelectorAll('p.rojo');
```

* querySelectorAll, getElementsByTagName y getElementsByClassName retornan una colección de elemento, es decir que podemos acceder a cada uno de los elementos de la misma forma que lo hacemos con un array. El primer elemento está en el índice 0

**Ejemplo:**
```html
<body>
  <p>Un texto</p>
  <p class="rojo">Un texto en rojo</p>
  <p class="rojo">Un texto en rojo</p>
  <p class="azul">Un texto en azul</p>
  <p id="principal">Un texto principal</p>
</body>
```

```js
// obtenemos una colección con todos los elementos párrafo de nuestro documento
var parrafos = document.getElementsByTagName('p');

parrafos[0]; // <p>Un texto</p>
parrafos[1]; // <p class="rojo">Un texto en rojo</p>
parrafos[2]; // <p class="rojo">Un texto en rojo</p>
parrafos[3]; // <p class="azul">Un texto en azul</p>
parrafos[4]; // <p id="principal">Un texto principal</p>
```
**Otra opcion**
```js
// obtenemos una colección con todos los elementos párrafo de nuestro documento
var parrafos = document.querySelectorAll('p');

parrafos[0]; // <p>Un texto</p>
parrafos[1]; // <p class="rojo">Un texto en rojo</p>
parrafos[2]; // <p class="rojo">Un texto en rojo</p>
parrafos[3]; // <p class="azul">Un texto en azul</p>
parrafos[4]; // <p id="principal">Un texto principal</p>
```

* Podemos sacar como conclusión que si queremos seleccionar un elemento lo podemos hacer utilizando los selectores `getElementById` o `querySelector`. En caso de querer seleccionar varios elementos podemos utilizar `querySelectorAll`


* Los elementos tienen una propiedad classList que nos permite obtener una colección de las clases que tienen un elemento

**Ejemplo:**
```html
<p id="principal" class="rojo negrita">texto principal en rojo</p>
```
```js
var elemento = document.querySelector('p');
console.log(elemento.classList[0]); // rojo
console.log(elemento.classList[1]); // negrita
```

* La classList tiene funciones y propiedades que nos permiten interactuar con las clases de un elemento de la siguiente manera:
  * **add:** acepta como parámetro el nombre de la clase que queremos agregar en formato de string. Si la clase existe es ignorada
  * **remove:** acepta una clase como parámetro en formato string y la quita del elemento
  * **item:** acepta un número como parámetro que representa la posición de la lista. Retorna el nombre de la clase que está en esa posición
  * **toggle:** acepta un nombre de clase como string. Agrega o quita la clase según exista o no en el elemento. Nos permite por ejemplo mostrar y ocultar elementos
  * **contains:** acepta un nombre de clase como string y retorna un valor boolean según si el elemento tiene o no esa clase
  * **replace:** acepta como primer parámetro el nombre de la clase que queremo remplazar, como segundo valor acepta el nombre de la clase que va a remplazar la anterior

**Ejemplo:**
```html
<p id="principal" class="rojo negrita">texto principal en rojo</p>
```
```js
var elemento = document.querySelector('p');

// agregamos la clase ocultar
elemento.classList.add('ocultar');

// como tenía la clase ocultar con toggle lo sacamos
elemento.classList.toggle('ocultar');

// sacamos la clase negrita
elemento.classList.remove('negrita');

// Retorna rojo que es la primer clase que tiene este elemento
elemento.item(0);

// Retorna true ya que el elemento tiene la clase rojo
elemento.contains('rojo');

// cambiamos la clase rojo por verde
elemento.replace('rojo', 'verde');
```

* classList es súper util para interactuar con clases

 

### Modificar el contenido de un elemento

* La propiedad standar de los elementos para leer o modificar el contenido de un elemento se llama `textContent`

**Ejemplo:**
```html
  <p>Mi Texto</p>
```
```js
var parrafo = document.querySelector('p');
parrafo.textContent; // Mi Texto

parrafo.textContent = 'ECMAScript en el browser está muy bueno';
parrafo.textContent; // ECMAScript en el browser está muy bueno
```

* Con `textContent` podemos asignar o leer el contenido de un elemento en formato de string


* Existe otra forma de establecer o cambiar el contenido de un elemento y se llama `innerHTML`
* `innerHTML` paresea el texto que se va a asignar al elemento y si encuentra que ese texto tiene formato de HTML intenta crear elementos con ese contenido

**Ejemplo:**
```html
  <p>Mi Texto</p>
```
```js
var parrafo = document.querySelector('p');
parrafo.innerHTML; // Mi Texto

parrafo.innerHTML = '<span>ECMAScript en el browser está muy bueno</span>';
parrafo.innerHTML; // <span>ECMAScript en el browser está muy bueno</span>
```

* Si bien en el ejemplo puede parecer que sólo modificamos el texto en el browser este código crea un nuevo span con el contenido "ECMAScript en el browser está muy bueno" y lo asigna dentro del elemento párrafo

