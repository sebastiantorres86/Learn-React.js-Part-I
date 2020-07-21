# Hola Mundo, Parte II ... EL COMPONENTE

Las aplicaciones de React están hechas de _componentes_.

¿Qué es un componente?

Un componente es un fragmento de código pequeño y reutilizable que es responsable de un trabajo. Ese trabajo es a menudo renderizar algo de HTML.

Echa un vistazo al código a continuación. Este código creará y representará un nuevo componente React:

```jsx
import React from "react";
import ReactDOM from "react-dom";

class MyComponentClass extends React.Component {
  render() {
    return <h1>Hello world</h1>;
  }
}

ReactDOM.render(<MyComponentClass />, document.getElementById("app"));
```

Gran parte de ese código probablemente no le sea familiar. Sin embargo, puede reconocer algunos JSX allí, así como `ReactDOM.render()`.

Vamos a desempaquetar ese código, una pieza pequeña a la vez. ¡Al final de esta lección, comprenderá cómo construir un componente React!

---

# Import React

Wooo! ¡Tu primer componente React!

Eche un vistazo al código en la línea 1:

```jsx
import React from "react";
```

Esta línea de código crea una nueva variable. El nombre de esa variable es `React`, y su valor es un objeto JavaScript importado particular:

```jsx
// crea una variable llamada React:
import React from "react";
// evalúa esta variable y obtiene un objeto JavaScript importado particular:
React; // {propiedades del objeto importado aquí ...}
```

Este objeto importado contiene métodos que necesita para usar React. El objeto se llama la _librería_ React.

Más adelante, veremos de dónde se importa la librería React y cómo funciona el proceso de importación. Por ahora, solo sé que obtienes la biblioteca React a través de `import React from 'react';`.

Ya has visto uno de los métodos contenidos en la librería React: `React.createElement()`. Recuerde que cuando se _compila_ un elemento JSX, se transforma en una llamada `React.createElement()`.

Por esta razón, _debe_ importar la biblioteca React y guardarla en una variable llamada `React`, antes de poder usar cualquier JSX. `React.createElement()` debe estar disponible para que JSX funcione.

---

# Import ReactDOM

Ahora eche un vistazo al código en la línea 2:

```jsx
import ReactDOM from "react-dom";
```

Esta línea de código es muy similar a la línea 1.

Las líneas 1 y 2 importan objetos JavaScript. En ambas líneas, el objeto importado contiene métodos relacionados con React.

Sin embargo, hay una diferencia!

Los métodos importados de `'react-dom'` están destinados a interactuar con el DOM. Ya estás familiarizado con uno de ellos: `ReactDOM.render()`.

Los métodos importados de `'react'` no tienen nada que ver con el DOM. No se involucran directamente con nada que no sea parte de React.

Para aclarar: el DOM se _usa_ en las aplicaciones React, pero no forma _parte_ de React. Después de todo, el DOM también se usa en innumerables aplicaciones que no son React. Los métodos importados de `'react'` son solo para fines de React puro, como crear componentes o escribir elementos JSX.

---

# Crear un Componente de Clase

Aprendiste que un _componente React_ es un fragmento de código pequeño y reutilizable que es responsable de un trabajo, que a menudo implica renderizar HTML.

Aquí hay otro hecho sobre los componentes: cada componente debe provenir de un _componente de clase_.

Un _componente de clase_ es como una fábrica que crea componentes. Si tiene un _componente de clase_, puede usar esa clase para producir tantos componentes como desee.

Para crear un componente de clase, utiliza una clase base de la biblioteca React: `React.Component`.

¿Qué _es_ `React.Component` y cómo se usa para crear un componente de clase?

`React.Component` es una _clase_ de JavaScript. Para crear su propio componente de clase, debe _subclasificar_ `React.Component`. Puede hacerlo utilizando la sintaxis `class YourComponentNameGoesHere extends React.Component {}`.

Las clases y subclases de JavaScript son un tema complejo más allá del alcance de este curso. Si no se siente cómodo con ellos, aquí hay algunos buenos recursos para consultar: [1](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes) [2](https://hacks.mozilla.org/2015/07/es6-in-depth-classes/) [3](https://hacks.mozilla.org/2015/08/es6-in-depth-subclassing/) [4](http://exploringjs.com/es6/ch_classes.html).

Mira el código en **app.js**. Mucho aún no es familiar, ¡pero puedes entender más de lo que lo hacías antes!

En la línea 4, sabe que está declarando un nuevo _componente de clase_, que es como una fábrica para construir componentes React. Usted sabe que `React.Component` es una clase, que debe subclasificar para crear un componente de clase propio. También sabe que `React.Component` es una propiedad del objeto que fue devuelta por `import React from 'react'` en la línea 1.

```jsx
import React from "react";
import ReactDOM from "react-dom";

class MyComponentClass extends React.Component {
  render() {
    return <h1>Hello world</h1>;
  }
}

ReactDOM.render(<MyComponentClass />, document.getElementById("app"));
```

---

# Nombrar un Componente de Clase

¡Bueno! Subclasificar `React.Component` es la forma de declarar un nuevo _component de clase_.

Cuando declara un nuevo componente de clase, debe darle un _nombre_ a ese componente de clase. En la línea 4, observe que el nombre de nuestro componente de clase es `MyComponentClass`.

¡Los nombres de las variables del componente de clase deben comenzar con letras mayúsculas!

Esto se adhiere a la sintaxis de clase de JavaScript. También se adhiere a una convención de programación más amplia en la que los [nombres de clase se escriben en UpperCamelCase](<https://en.wikipedia.org/wiki/Naming_convention_(programming)#Java>).

Además, hay una razón específica de React por la cual los nombres de las clases de componentes siempre deben estar en mayúscula. ¡Ya llegaremos a eso!

---

# Instrucciones de componente de clase

¡Revisemos lo que has aprendido hasta ahora! Encuentre cada uno de estos puntos en **app.js**:

- En la línea 1, `import React from 'react'` crea un objeto JavaScript. Este objeto contiene propiedades que son necesarias para que React funcione, como `React.createElement()` y `React.Component`.

- En la línea 2, `import ReactDOM from 'react-dom'` crea otro objeto JavaScript. Este objeto contiene métodos que ayudan a React a interactuar con el DOM, como `ReactDOM.render()`.

- En la línea 4, al subclasificar `React.Component`, crea un nuevo _componente de clase_. ¡Esto no es un componente! Un componente de clase es más como una fábrica que produce componentes. Cuando comience a hacer componentes, cada uno vendrá de un componente de clase.

- Siempre que cree un componente de clase, debe darle un nombre a ese componente de clase. Ese nombre debe estar escrito en UpperCamelCase. En este caso, su nombre elegido es `MyComponentClass`.

Algo de lo que aún _no hemos_ hablado es el cuerpo de su componente de clase: el par de llaves después de `React.Component`, y todo el código entre esas llaves.

Como todas las clases de JavaScript, esta necesita un cuerpo. El cuerpo actuará como un conjunto de instrucciones, explicando a su componente de clase cómo debe construir un componente React.

Así es como se vería su cuerpo de clase por sí solo, sin el resto de la sintaxis de declaración de clase. Encuéntralo en **app.js**:

```jsx
{
  render () {
    return <h1>Hello world</h1>;
  }
}
```

¡Eso no parece un conjunto de instrucciones que expliquen cómo construir un componente React! Sin embargo, eso es exactamente lo que es.

```jsx
import React from "react";
import ReactDOM from "react-dom";

class MyComponentClass extends React.Component {
  render() {
    return <h1>Hello world</h1>;
  }
}

ReactDOM.render(<MyComponentClass />, document.getElementById("app"));
```

---

# La función de renderizado

Una componente de clase es como una fábrica que construye componentes. Construye estos componentes consultando un conjunto de instrucciones, que debe proporcionar. ¡Hablemos de estas instrucciones!

Para empezar, estas instrucciones deben tomar la forma de un cuerpo de declaración de clase. Eso significa que estarán delimitados por llaves, así:

```jsx
class ComponentFactory extends React.Component {
  // las instrucciones van aquí, entre llaves
}
```

Las instrucciones deben escribirse en la típica [sintaxis de la clase JavaScript ES2015](http://exploringjs.com/es6/ch_classes.html).

Solo hay una propiedad que debe incluir en sus instrucciones: un _método de renderizado_.

Un métod de renderizado es una propiedad cuyo _nombre_ es `render` y cuyo _valor_ es una función. El término "método de renderizado" puede referirse a toda la propiedad, o solo a la parte de la función.

```jsx
class ComponentFactory extends React.Component {
  render() {}
}
```

Un método de renderizado debe contener una declaración `return`. Por lo general, esta declaración `return` devuelve una expresión JSX:

```jsx
class ComponentFactory extends React.Component {
  render() {
    return <h1> Hola mundo </h1>;
  }
}
```

Por supuesto, nada de esto explica el _punto_ de un método de renderizado. Todo lo que sabe hasta ahora es que su nombre es `render`, necesita una declaración return por alguna razón, y debe incluirlo en el cuerpo de su declaración de componente de clase. ¡Llegaremos al "por qué" pronto!

---

# Crear una instancia de componente

¡`MyComponentClass` ahora es un _componente de clase_ funcional! Está listo para seguir sus instrucciones y hacer algunos componentes React.

Entonces, ¡hagamos un componente React! Solo se necesita una línea más:

```jsx
<MyComponentClass />
```

Para hacer un componente React, escribe un _elemento JSX_. En lugar de nombrar a su elemento JSX como `h1` o `div` como lo hizo anteriormente, asígnele el mismo nombre que un _componente de clase_. ¡Voilà, ahí está tu _instancia de componente_!

Los elementos JSX pueden ser de tipo HTML o _instancia de componente_. ¡JSX usa mayúsculas para distinguir entre los dos! _Esa_ es la razón específica de React por la cual los nombres de los componentes de clase deben comenzar con letras mayúsculas. En un elemento JSX, esa primera letra en mayúscula dice: "Seré una instancia de componente y no una etiqueta HTML".

---

# Renderizar un componente

Ha aprendido que un componente de clase necesita un conjunto de instrucciones, que le indican al componente de clase cómo construir componentes. Cuando crea un nuevo componente de clase, estas instrucciones son el cuerpo de su declaración de clase:

```jsx
class MyComponentClass extends React.Component {
  // todo lo que se encuentra entre estas llaves es instrucciones sobre cómo construir componentes

  render() {
    return <h1>Hello world</h1>;
  }
}
```

Esta declaración de clase da como resultado un nuevo componente de clase, en este caso denominada `MyComponentClass`. `MyComponentClass` tiene un método, denominado `render`. Todo esto sucede a través de la sintaxis estándar JavaScript de clase.

¡_No has_ aprendido cómo funcionan estas instrucciones para crear componentes! Cuando crea un componente utilizando la expresión `<MyComponentClass />`, ¿qué hacen estas instrucciones?

Cada vez que crea un componente, ese componente _hereda_ todos los métodos de su componente de clase. `MyComponentClass` tiene un método: `MyComponentClass.render()`. Por lo tanto, `<MyComponentClass />` también tiene un método llamado `render`.

Podría crear un millón de instancias diferentes de `<MyComponentClass />`, y cada una heredaría el mismo exacto método `render`.

El ejercicio final de esta lección es _renderizar_ su componente. Para renderizar un componente, ese componente debe tener un método denominado `render`. Su componente tiene esto! _Hereda_ un método llamado `render` de `MyComponentClass`.

Como su componente tiene un método de renderizado, todo lo que queda por hacer es llamarlo. Esto sucede de una manera ligeramente inusual.

Para llamar al método `render` de un componente, pasa ese componente a `ReactDOM.render()`. Observe su componente, que se pasa como el primer argumento de `ReactDOM.render()`:

```jsx
ReactDOM.render(<MyComponentClass />, document.getElementById("app"));
```

`ReactDOM.render()` le dirá a `<MyComponentClass />` que llame a _su_ método de renderizado.

`<MyComponentClass />` llamará a su método de renderizado, que devolverá el elemento JSX `<h1>Hello world</h1>`. `ReactDOM.render()` tomará ese elemento JSX resultante y lo agregará al DOM virtual. Esto hará que aparezca "Hello world" en la pantalla.

---

