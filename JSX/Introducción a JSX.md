# ¿Por qué React?

React.js es una biblioteca de JavaScript. Fue desarrollado por ingenieros en Facebook.

Estas son solo algunas de las razones por las cuales las personas eligen programar con React:

- React es _rápido_. Las aplicaciones creadas en React pueden manejar actualizaciones complejas y aún así se sienten rápidas y receptivas.

- React es _modular_. En lugar de escribir archivos de código grandes y densos, puede escribir muchos archivos más pequeños y reutilizables. La modularidad de React puede ser una hermosa solución a los problemas de mantenibilidad de JavaScript.

- React es _escalable_. Los grandes programas que muestran muchos datos cambiantes son donde React funciona mejor.

- React es _flexible_. Puede usar React para proyectos interesantes que no tienen nada que ver con hacer una aplicación web. La gente todavía está descubriendo el potencial de React. [Hay espacio para explorar](https://medium.mybridge.co/22-amazing-open-source-react-projects-cb8230ec719f#.o5umedb6v).

- React es _popular_. Si bien es cierto que esta razón tiene poco que ver con la calidad de React, la verdad es que comprender React lo hará más empleable.

Si eres nuevo en React, entonces este curso es para ti! No se espera conocimiento previo de React. Comenzaremos desde el principio y avanzaremos lentamente.

Si es nuevo en JavaScript, considere tomar [nuestro curso de JavaScript](https://www.codecademy.com/learn/javascript) y luego regresar a React.

Los cursos de Codecademy React no son una descripción general de alto nivel. Son una inmersión profunda. ¡Tome su tiempo! Al final, estará listo para programar en React con una comprensión real de lo que está haciendo.

---

# Hola Mundo

Eche un vistazo a la siguiente línea de código:

```jsx
const h1 = <h1> Hola mundo </h1>;
```

¿Qué tipo de código híbrido extraño es ese? ¿Es JavaScript? HTML? ¿O algo mas?

Parece que debe ser JavaScript, ya que comienza con `const` y termina con `;`. Si trataste de ejecutar eso en un archivo HTML, no funcionaría.

Sin embargo, el código también contiene `<h1>Hello world</h1>`, que se ve exactamente como HTML. _Esa_ parte no funcionaría si intentaras ejecutarla en un archivo JavaScript.

¿Que esta pasando?

---

# El misterio revelado

¡Bien!

Eche otro vistazo a la línea de código que escribió.

¿Este código pertenece a un archivo JavaScript, un archivo HTML o en otro lugar?

La respuesta es... ¡un archivo JavaScript! A pesar de lo que parece, su código no contiene HTML en absoluto.

La parte que se parece a HTML, `<h1>Hello world</h1>`, es algo llamado _JSX_.

Más abajo hay información sobre JSX.

---

# ¿Qué es el JSX?

_JSX_ es una extensión de sintaxis para JavaScript. Fue escrito para ser usado con React. El código JSX se parece mucho a HTML.

¿Qué significa "extensión de sintaxis"?

En este caso, significa que JSX no es JavaScript válido. ¡Los navegadores web no pueden leerlo!

Si un archivo JavaScript contiene código JSX, entonces ese archivo deberá _compilarse_. Eso significa que antes de que el archivo llegue a un navegador web, un _compilador JSX_ traducirá cualquier JSX a JavaScript normal.

Finalmente, veremos cómo configurar un compilador JSX en su computadora personal.

---

# Elementos JSX

Una unidad básica de JSX se llama _elemento_ JSX.

Aquí hay un ejemplo de un elemento JSX:

```jsx
<h1>Hello world</h1>
```

¡Este elemento JSX se ve exactamente como HTML! La única diferencia notable es que lo encontraría en un archivo JavaScript, en lugar de en un archivo HTML.

---

# Elementos JSX y sus alrededores

Los elementos JSX se tratan como _expresiones_ de JavaScript. Pueden ir a cualquier lugar al que puedan ir las expresiones de JavaScript.

Eso significa que un elemento JSX puede guardarse en una variable, pasarse a una función, almacenarse en un objeto o matriz... lo que sea.

Aquí hay un ejemplo de un elemento JSX que se guarda en una variable:

```jsx
const navBar = <nav>I am a nav bar</nav>;
```

Aquí hay un ejemplo de varios elementos JSX que se almacenan en un objeto:

```jsx
const myTeam = {
  centro: <li>Benzo Walli</li>,
  powerForward: <li>Rasha Loa</li>,
  smallForward: <li>Tayshaun Dasmot </li>,
  shootingGuard: <li>Colmar Cumberbatch</li>,
  pointGuard: <li>Femi Billon</li>,
};
```

---

# Atributos en JSX

Los elementos JSX pueden tener _atributos_, al igual que los elementos HTML.

Un atributo JSX se escribe utilizando una sintaxis similar a HTML: un _nombre_, seguido de un signo igual, seguido de un _valor_. El valor debe estar entre comillas, así:

```jsx
my - attribute - name = "mi-atributo-value";
```

Aquí hay algunos elementos JSX con _atributos_:

```jsx
<a href="http://www.example.com">Welcome to the web</a>;

const title = <h1 id="title">Introduction to React.js: Part I</h1>;
```

Un solo elemento JSX puede tener muchos atributos, al igual que en HTML:

```jsx
const panda = (
  <img src="images/panda.jpg" alt="panda" width="500px" height="500px" />
);
```

---

# JSX anidado

Puede _anidar_ elementos JSX dentro de otros elementos JSX, al igual que en HTML.

Aquí hay un ejemplo de un elemento JSX `<h1>`, anidado dentro de un elemento JSX `<a>`:

```jsx
<a href="https://www.example.com">
  <h1>Click me!</h1>
</a>
```

Para hacerlo más legible, puede usar saltos de línea y sangría de estilo HTML:

```jsx
<a href="https://www.example.com">
  <h1>Click me!</h1>
</a>
```

Si una expresión JSX ocupa más de una línea, debe ajustar la expresión JSX de varias líneas entre paréntesis. Esto parece extraño al principio, pero te acostumbras:

```jsx
<a href="https://www.example.com">
  <h1>Click me!</h1>
</a>
```

¡Las expresiones JSX _anidadas_ se pueden guardar como variables, pasar a funciones, etc., al igual que las expresiones JSX no anidadas! Aquí hay un ejemplo de una expresión JSX _anidada_ que se guarda como una variable:

```jsx
const theExample = (
  <a href="https://www.example.com">
    <h1>Click me!</h1>
  </a>
);
```

---

# Elementos exteriores JSX

Hay una regla que no hemos mencionado: una expresión JSX debe tener exactamente _un_ elemento más externo.

En otras palabras, este código funcionará:

```jsx
const paragraph = (
  <div id="i-am-the-outermost-element">
    <p>I am a paragraph</p>
    <p>I, too, am a paragaraph.</p>
  </div>
);
```

Pero este código no funcionará:

```jsx
const paragraph = (
   <p>I am a aparagraph</p>
   <p>I, too, am a paragraph</p>
);
```

¡La primera _etiqueta de apertura_ y la _etiqueta de cierre final_ de una expresión JSX deben pertenecer al mismo elemento JSX!

Es fácil olvidarse de esta regla y terminar con errores difíciles de diagnosticar.

Si observa que una expresión JSX tiene múltiples elementos externos, la solución generalmente es simple: ajuste la expresión JSX en un `<div></div>`.

---

# Renderizado JSX

¡Aprendiste a escribir elementos JSX! Ahora es el momento de aprender cómo _renderizarlos_.

_Renderizar_ una expresión JSX significa hacer que aparezca en pantalla.

---

# ReactDOM.render() I

Examinemos el código que acaba de escribir. Comience en **previous.js**, en la línea 5, hasta la izquierda.

Puedes ver algo llamado `ReactDOM`. ¿Que es eso?

`ReactDOM` es el nombre de una librería de JavaScript. Esta librería contiene varios métodos específicos de React, todos los cuales tratan con [el DOM](http://www.w3schools.com/js/js_htmldom.asp) de una forma u otra.

Más adelante hablaremos sobre cómo `ReactDOM` ingresó a su archivo. Por ahora, solo comprenda que es suyo.

Muévase ligeramente hacia la derecha y podrá ver uno de los métodos de `ReactDOM`: `ReactDOM.render()`.

`ReactDOM.render()` es la forma más común de _renderizar_ JSX. Toma una expresión JSX, crea un árbol correspondiente de nodos DOM y agrega ese árbol al DOM. Esa es la forma de hacer que una expresión JSX aparezca en pantalla.

Muévete un poco más hacia la derecha y llegarás a esta expresión:

```js
<h1>Hello world</h1>
```

Este es el primer _argumento_ que se pasa a `ReactDOM.render()`. El primer argumento de `ReactDOM.render()` debe ser una expresión JSX y se mostrará en la pantalla.

¡Discutiremos el segundo argumento en la próxima lección!

```jsx
// previous.js

import React from "react";
import ReactDOM from "react-dom";

// This is just an example
ReactDOM.render(<h1>Hello world</h1>, document.getElementById("app"));
```

---

# ReactDOM.render() II

Muévete un poco más hacia la derecha y verás esta expresión:

```jsx
document.getElementById("app");
```

Acabas de aprender que `ReactDOM.render()` hace que su _primer_ argumento aparezca en pantalla. Pero, ¿_en qué lugar_ de la pantalla debería aparecer ese primer argumento?

El primer argumento se _agrega_ a cualquier elemento seleccionado por el _segundo_ argumento.

En el editor de código, seleccione **index.html**. Vea si puede encontrar un elemento que sería seleccionado por`document.getElementById('app')`.

¡Ese elemento actuó como un _contenedor_ para el primer argumento de `ReactDOM.render()`! Al final del ejercicio anterior, esto apareció en la pantalla:

```jsx
<main id="app">
  <h1> ¡Hazme! </h1>
</main>
```

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8">
	<link rel="stylesheet" href="/styles.css">
	<title>Learn ReactJS</title>
</head>

<body>
  <main id="app"></main>
	<script src="https://s3.amazonaws.com/codecademy-content/courses/React/react-course-bundle.min.js"></script>
  <script src="/app.compiled.js"></script>
</body>

</html>
```

---

# Pasar una variable a ReactDOM.render()

El primer argumento de `ReactDOM.render()` debe _evaluar_ a una expresión JSX, no tiene que _ser_ literalmente una expresión JSX.

El primer argumento también podría ser una variable, siempre que esa variable se evalúe como una expresión JSX.

En este ejemplo, guardamos una expresión JSX como una _variable_ llamada `toDoList`. Luego pasamos a `toDoList` como el primer argumento para `ReactDOM.render()`:

```jsx
const toDoList = (
  <ol>
    <li>Learn React</li>
    <li>Become a Developer</li>
  </ol>
);

ReactDOM.render(toDoList, document.getElementById("app"));
```

---

# El DOM virtual

Una cosa especial sobre `ReactDOM.render()` es que _solo actualiza los elementos DOM que han cambiado_.

Eso significa que si renderiza exactamente lo mismo dos veces seguidas, el segundo render no hará nada:

```js
const hello = <h1>Hello world</h1>;

// Esto agregará "Hola mundo" a la pantalla:

ReactDOM.render(hello, document.getElementById("app"));

// Esto no hará nada en absoluto:

ReactDOM.render(hello, document.getElementById("app"));
```

Esto es significativo! Solo actualizar los elementos DOM necesarios es una gran parte de lo que hace que React sea tan exitoso.

React logra esto gracias a algo llamado _DOM virtual_. Antes de pasar al final de la lección, [lea este artículo sobre el DOM virtual](#).

---

# Resumen de JSX

¡Felicidades! ¡Has aprendido a crear y renderizar elementos JSX! Este es el primer paso para ser fluido en React.

En la próxima lección, aprenderá algunas cosas poderosas que puede hacer con JSX, así como algunos problemas comunes de JSX y cómo evitarlos.
