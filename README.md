# Clase60 
## Introduccion al DOM

* El `DOM` (document object model) proporciona una representación estructural de un documento html, permitiendo la modificación de su contenido
* Esto significa que tenemos acceso a elementos que tienen propiedades, métodos y eventos disponibles para crear, eliminar y modificar elementos en un documento web
* En el DOM encontramos los siguientes tipos de datos:
  * **document:** representa el documento en si mismo. Es el nodo principal.
  * **element:** representa un nodo elemento
  * **attribute:** representan los atributos de los nodos / elementos
  * **nodeList:** es un array con nodos. Sus elementos se pueden acceder por medio items o indice del array.

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

### Atributos
* Al seleccionar un elemento podemos acceder a sus atributos utilizando la propiedad attributes
* Esta propiedad retorna un mapa (es como un array) que tiene valores key/value con los nombres y valores de los atributos de ese elemento

**Ejemplo:**
```html
<p id="principal" class="rojo">texto principal en rojo</p>
```

```js
var elemento = document.querySelector('p')
console.log(elemento.attributes); // retorna un objeto del tipo NamedNodeMap con toda la descripción de los atributos
```

* Podemos acceder de forma indiviudal a los atributos de un elemento utilizando el método `getAttribute`
* Este método acepta un string como parámetro con el nombre del atributo que quiero obtener
* Retorna el valor del atributo y null en caso de no encontrarlo

**Ejemplo:**
```html
<p id="principal" class="rojo">texto principal en rojo</p>
```

```js
var elemento = document.querySelector('p')
var id = elemento.getAttribute('id'); // retorna principal
var clase = elemento.getAttribute('class'); // retorna rojo
console.log(id);
```

* Otra forma de acceder a las propiedades es utilizar los atributos de HTML como propiedades de objeto

**Ejemplo:**
```html
<p id="principal" class="rojo">texto principal en rojo</p>
```
```js
var elemento = document.querySelector('p')
var id = elemento.id;
console.log(id);
```

* Hay un caso especial y es el uso del atributo class dado que es una palabra reservada en JavaScript
* Para acceder o establecer el atributo class tenemos que utilizar `className`

**Ejemplo:**
```html
<p id="principal" class="rojo">texto principal en rojo</p>
```
```js
var elemento = document.querySelector('p')

var clase = elemento.className;
console.log(clase); // rojo

clase = elemento.getAttribute('class');
console.log(clase); // rojo
```

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

* Podemos saber si un elemento tiene o no un atributo en particular utilizando el método `hasAttribute`
* Acepta un string como parámetro con el nombre del atributo que quiero saber si existe en ese elemento
* Retorna un valor booleano

**Ejemplo:**
```html
<p id="principal" class="rojo">texto principal en rojo</p>
```

```js
var elemento = document.querySelector('p');
console.log(elemento.hasAttribute('class')); // true
```

* También existe el método `hasAttributes` que nos permite saber si un elemento tiene o no atributos
* Este método retorna un valor boolean, true en caso de que el elemento tenga atributos y false en caso de que no los tenga.
* Destacamos que la diferencia entre `hasAttribute` y `hasAttributes` es que el primero nos dice si tiene o no un atributo en especial y el segundo si tiene atributos en general

**Ejemplo:**
```html
<p id="principal" class="rojo">texto principal en rojo</p>
<h2>Elemento sin atributos</h2>
```

```js
var elemento = document.querySelector('p');
var titulo = document.querySelector('h2');
console.log(element.hasAttributes():); // true
console.log(titulo.hasAttributes():); // false
```

* Para establecer atributos utilizamos el método setAttribute
* Este método acepta como primer parámetro un string con el nombre del atributo que queremos agregar
* Como segundo parámetro acepta un string con el valor que queremos para el atributo

**Ejemplo:**
```html
<h2>Elemento sin atributos</h2>
```

```js
var titulo = document.querySelector('h2');
console.log(titulo.hasAttributes():); // false

titulo.setAttribute('id', 'principal');
console.log(titulo.hasAttributes():); // true
```

* En este ejemplo vemos que al seleccionar el elemento `h2` no tiene atributos y luego utilizando `setAttribute` le podemos asignar un atributo `id` con un valor de `principal`
* En caso de querer quitar un atributo lo podemos hacer utilizando el método `removeAttribute`
* Este método acepta un string como parámetro con el nombre del atributo que queremos remover

**Ejemplo:**
```html
<h2 id="principal">Elemento sin atributos</h2>
```

```js
var titulo = document.querySelector('h2');
console.log(titulo.hasAttributes():); // true

titulo.removeAttribute('id');
console.log(titulo.hasAttributes():); // true
```

### Relación entre elementos
* Un elemento que contiene otros elementos se considera como un elemento padre de los elementos que contiene
* Un elemento que esta dentro de otro elemento se considera hijo del elemento que lo contiene
* Por medio de el atributo `parentElement` podemos acceder **al elemento padre** del elemento seleccionado
* Con el atributo `children` podemos acceder a **la colección de elementos hijos** de un elemento

**Ejemplo:**
```html
<div>
  <p>Elemento hijo</p>
  <p>Elemento hijo</p>
  <p>Elemento hijo</p>
</div>
```

```js
var div = document.querySelector('div');
var parrafos = div.children; // obtengo la colección de elementos hijo
parrafos[0].parentElement;
/*
  Dado que children retorna una colección puedo acceder al primer elemento utilizando un índice como en los arrays
  Utilizamos parentElement para obtener una referencia al elemento div que contiene todos los párrafos
*/
```

* Otra relación entre elementos es la de `sibling` es decir los que estan continuos o al mismo nivel que el elemento seleccionado
**Ejemplo:**
```html
  <p>Elemento hijo</p>
  <p>Elemento hijo</p>
  <p>Elemento hijo</p>
```

* En este ejemplo vemos que los 3 elementos párrafo están al mismo nivel, es decir que son sibling
* Podemos acceder al elemento que está antes que el elemento seleccionado utilizando la propiedad `previousElementSibling`
* También podemos acceder al elemento que sigue gracias a la propiedad `nextElementSibling`

**Ejemplo:**
```html
  <p>Elemento hijo</p>
  <p>Elemento hijo</p>
  <p>Elemento hijo</p>
```
```js
var parrafos = document.querySelectorAll('p');
parrafos[1].previousElementSibling; // De esta forma accedemos al primer párrafo parrafos[0]
parrafos[1].nextElementSibling; // De esta forma accedemos al elemento que sigue parrafos[2]
```

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


### Manejo de propiedades de CSS
* Los elementos HTML tienen una propiedad llamada `style` que retorna un `objeto literal` que representa los estilos que tiene un objeto
* Al ser un objeto de ECMAScript podemos agregar o modificar sus atributos
* Los nombres de las propiedades de CSS en ECMAScript se escriben con el siguiente formato: `nombreDePropiedadDeCss`
* Por ejemplo la propiedad de CSS `background-color` se escribe en ECMA como `backgroundColor`

**Ejemplo:**
```html
  <p>Elemento sin estilo pero se lo vamos a agregar de forma dinámica</p>
```
```js
var elemento = document.querySelector('p');
elemento.style; // {}
elemento.style.color = ‘red’; // seteo el color a rojo
elemento.style.fontWeight = ‘bold’; //seteo el weight a bold
```

* De esta forma podemos manipular las propiedades de `style` en nuestros elementos

### CRUD elementos
* CRUD significa:
  * Create
  * Read
  * Update
  * Delete
* Esto significa que podemos crear, actualizar y borrar un elemento
* La parte de read podemos decir que es obtener el elemento y leer sus propiedades

#### Crear un elemento
* El objeto `document` tienen un método llamado `createElement` que nos permite crear nuevos nodos elementos HTML
* `createElement` acepta como parámetro un string con el nombre de una etiqueta de HTML (a, div, span, li, ul, etc)

**Ejemplo:**
```js
var nuevoElemento = document.createElement('p');
```
* En este ejemplo podemos ver que creamos un elemento párrafo y lo guardamos en la variable nuevoElemento
* Este nuevo elemento está en memoria y tiene la estructura de un elemento párrafo pero por el momento no tiene contenido
* Al tener una referencia de un elemento podemos interactuar con él como por ejemplo establecer un contenido, insertarlo en otro elemento, cambiarle sus atributos de `style`, etc

#### Insertar un elemento
* Los objetos tienen un método llamado `appendChild` que nos permite insertar un nodo dentro del otro
* Este método inserta el nuevo nodo como último nodo hijo del nodo contenedor

**Ejemplo:**
```js
var parrafo = document.createElement('p');
parrafo.textContent = 'Hola soy un párrafo';
var div = document.createElement('div');
div.appendChild(p);
```

* En este ejemplo vemos que creamos 2 elementos párrafo y div
* Al tener la referencia de los dos elementos podemos interactuar con ellos y en este caso estamos insertando el párrafo dentro del div

#### Remover un elemento
* Los elementos tienen un método llamado `removeChild` que nos permite remover nodos hijos
* Para poder remover un nodo tenemos que primero seleccionarlo

**Ejemplo:**
```html
<div>
  <p>Elemento sin estilo pero se lo vamos a agregar de forma dinámica</p>
</div>
```
```js
var div = document.querySelector('div');
var parrafo = div.children.item(0); // selecciono el párrafo
div.removeChild(parrafo);
```

* En este ejemplo vemos como podemos seleccionar los elementos que son hijos de otro elemento y borrarlo
* Si queremos borrar todo el contenido de un elemento podemos utilizar `innerHTML`

**Ejemplo:**
```html
<div>
  <p>Elemento sin estilo pero se lo vamos a agregar de forma dinámica</p>
</div>
```
```js
var div = document.querySelector('div');
div.innerHTML = ''; // chau chau contenido
```
