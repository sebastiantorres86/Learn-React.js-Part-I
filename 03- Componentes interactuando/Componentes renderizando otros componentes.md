# Interacción entre Componentes

Una aplicación React puede contener docenas, o incluso cientos, de componentes.

Cada componente puede ser pequeño y relativamente poco notable por sí solo. Sin embargo, cuando se combinan, pueden formar ecosistemas de información enormes y fantásticamente complejos.

En otras palabras, las aplicaciones React están hechas de componentes, pero lo que hace que React sea especial no son los componentes en sí. Lo que hace que React sea especial es la forma en que interactúan los componentes.

Esta unidad es una introducción a los _componentes que interactúan_.

---

# Un componente en una función de renderizado

Aquí hay un método `.render()` que devuelve un elemento JSX similar a HTML:

```jsx
class Example extends React.Component {
  render() {
    return <h1>Hello world</h1>;
  }
}
```

Ha visto que los métodos de renderizado devuelven `<div></div>`s, `<p></p>`s y `<h1></h1>`s, al igual que en el ejemplo anterior.

Los métodos de renderizado también pueden devolver otro tipo de JSX: _instancias de componentes_.

```jsx
class OMG extends React.Component {
  render() {
    return <h1>Whooaa!</h1>;
  }
}

class Crazy extends React.Component {
  render() {
    return <OMG />;
  }
}
```

En el ejemplo anterior, el método de render de `Crazy` `return` una _instancia_ del componente de clase `OMG`. Se podría decir que `Crazy` renderiza un `<OMG />`.

---

# Aplicar un componente en una función de renderizado

Este es un nuevo territorio! Nunca antes has visto un componente representado por otro componente.

Sin embargo, ha visto un componente representado anteriormente, pero no por otro componente. En su lugar, ha visto un componente representado por `ReactDOM.render()`.

Cuando un componente representa otro componente, lo que sucede es muy similar a lo que sucede cuando `ReactDOM.render()` representa un componente.

```jsx
import React from "react";
import ReactDOM from "react-dom";

class ProfilePage extends React.Component {
  render() {
    return (
      <div>
        <NavBar />
        <h1>All About Me!</h1>
        <p>I like movies and blah blah blah blah blah</p>
        <img src="https://s3.amazonaws.com/codecademy-content/courses/React/react_photo-monkeyselfie.jpg" />
      </div>
    );
  }
}
```

---

# Requerir un archivo

Cuando usa React.js, todos los archivos JavaScript de su aplicación son invisibles para todos los demás archivos JavaScript de forma predeterminada. **ProfilePage.js** y **NavBar.js** no pueden verse.

¡Esto es un problema!

En la línea 9, acaba de agregar una instancia del componente de clase `NavBar`. Pero como estás en **ProfilePage.js**, JavaScript no tiene idea de lo que significa `NavBar`.

Si desea utilizar una variable declarada en un archivo diferente, como `NavBar`, debe _importar_ la variable que desee. Para importar una variable, puede usar una declaración `import`:

```jsx
import { NavBar } from "./NavBar.js";
```

Hemos usado `import` antes, ¡pero no así! Observe las diferencias entre la línea de código anterior y esta línea familiar:

```jsx
import React from "react";
```

La primera diferencia importante son las llaves alrededor de `NavBar`. ¡Llegaremos a esos pronto!

La segunda diferencia importante involucra el contenido de la cadena al final de la declaración: `'react'` vs `'./NavBar.js'`.

Si usa una declaración `import`, y la cadena al final comienza con un punto o una barra diagonal, entonces `import` tratará esa cadena como una _ruta de archivo_. `import` seguirá esa ruta de archivo e importará el archivo que encuentre.

Si su ruta de archivo no tiene una extensión de archivo, se asume ".js". Entonces el ejemplo anterior podría acortarse:

```jsx
import { NavBar } from "./NavBar";
```

**Una última nota importante:**
Ninguno de estos comportamientos es específico de React! Los [sistemas de módulos](http://eloquentjavascript.net/10_modules.html) de archivos independientes importables son una forma muy popular de organizar el código. El [sistema de módulos específico de React proviene de ES6](https://hacks.mozilla.org/2015/08/es6-in-depth-modules/). Más sobre todo eso más tarde.

---

# exportar

¡Bien! Aprendió a usar import para tomar una variable de un archivo que _no sea_ el archivo que se está ejecutando actualmente.

Cuando importa una variable de un archivo que no es el archivo actual, una declaración `import` no es suficiente. También necesita una declaración `export`, escrita en el _otro_ archivo, exportando la variable que espera obtener.

`export` proviene del [sistema de módulos de ES6](http://exploringjs.com/es6/ch_modules.html), al igual que `import`. `export` e `import` están destinadas a usarse juntas, y rara vez se ve una sin la otra.

Hay algunas formas diferentes de usar `export`. En este curso, utilizaremos un estilo llamado "exportaciones con nombre". Así es como funcionan las exportaciones con nombre:

En un archivo, coloque la palabra clave `export` inmediatamente antes de algo que desee exportar. Ese algo puede ser cualquier `var`, `let`, `const`, `function` o `class` de nivel superior:

```jsx
// Manifestos.js:

export const faveManifestos = {
  futurist: 'http://www.artype.de/Sammlung/pdf/russolo_noise.pdf',
  agile: 'https://agilemanifesto.org/iso/en/manifesto.html',
  cyborg: 'http://faculty.georgetown.edu/irvinem/theory/Haraway-CyborgManifesto-1.pdf'
};
```

Puede exportar varias cosas desde el mismo archivo:

```jsx
// Manifestos.js:

export const faveManifestos = {
  futurist: 'http://www.artype.de/Sammlung/pdf/russolo_noise.pdf',
  agile: 'https://agilemanifesto.org/iso/en/manifesto.html',
  cyborg: 'http://faculty.georgetown.edu/irvinem/theory/Haraway-CyborgManifesto-1.pdf'
};

export const alsoRan = 'TimeCube';
```

En un archivo diferente, importe el nombre de var, let, const, function o class del primer archivo:

```jsx
// App.js:

// Importa faveManifestos y alsonRan desde ./Manifestos.js:
import {faveManifestos, alsoRan} from './Manifestos';

// Usa faveManifestos:
console.log(`A Cyborg Manifesto: ${faveManifestos.cyborg}`);
```

Este estilo de importación y exportación en JavaScript se conoce como "exportaciones con nombre". Cuando usa exportaciones con nombre, siempre necesita envolver sus nombres importados en llaves, como:

```jsx
import { faveManifestos, alsoRan } from './Manifestos';
```

[El sistema de módulos ES6 de JavaScript](http://exploringjs.com/es6/ch_modules.html) va más allá de las exportaciones con nombre y tiene varias características de sintaxis avanzadas.

---

# Renderizado de componentes en acción

¡Ahora está listo para que `<ProfilePage />` renderice `<NavBar />`!

Todo lo que queda por hacer es renderizar `<ProfilePage />`.
