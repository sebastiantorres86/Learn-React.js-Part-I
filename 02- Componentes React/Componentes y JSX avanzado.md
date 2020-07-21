# Utilice Multiline JSX en un componente

En esta lección, aprenderá algunas formas comunes en que los componentes JSX y React trabajan juntos. Te sentirás más cómodo con JSX y componentes, mientras aprendes algunos trucos nuevos.

Echa un vistazo a este HTML:

```HTML
<blockquote>
  <p>
    The world is full of objects, more or less interesting; I do not wish to add any more.
  </p>
  <cite>
    <a target="_ blank"
      href="https://en.wikipedia.org/wiki/Douglas_Huebler">
      Douglas Huebler
    </a>
  </cite>
</blockquote>
```

¿Cómo podrías hacer un componente React que represente este HTML?

Seleccione **QuoteMaker.js** para ver una forma de hacerlo.

Lo clave a tener en cuenta en `QuoteMaker` son los paréntesis en la declaración `return`, en las líneas 6 y 18. Hasta ahora, las declaraciones `return` de la función de renderizado se han visto así, sin paréntesis:

```jsx
return <h1>Hello world</h1>;
```

Sin embargo, una expresión JSX de varias líneas siempre debe estar entre paréntesis. Es por eso que la declaración de retorno de `QuoteMaker` tiene paréntesis a su alrededor.

```jsx
import React from "react";
import ReactDOM from "react-dom";

class QuoteMaker extends React.Component {
  render() {
    return (
      <blockquote>
        <p>
          The world is full of objects, more or less interesting; I do not wish
          to add any more.
        </p>
        <cite>
          <a
            target="_blank"
            href="https://en.wikipedia.org/wiki/Douglas_Huebler"
          >
            Douglas Huebler
          </a>
        </cite>
      </blockquote>
    );
  }
}

ReactDOM.render(<QuoteMaker />, document.getElementById("app"));
```

---

# Usar un atributo variable en un componente

Eche un vistazo a este objeto JavaScript llamado `redPanda`:

```jsx
const redPanda = {
  src: 'https://upload.wikimedia.org/wikipedia/commons/b/b2/Endangered_Red_Panda.jpg',
  alt: 'Panda rojo',
  width: '200px
};
```

¿Cómo podría renderizar un componente React y obtener una imagen con las propiedades de `redPanda`?

Seleccione **RedPanda.js** para ver una forma de hacerlo.

¡Tenga en cuenta todas las inyecciones de JavaScript con llaves dentro de la función de renderizado! Las líneas 16, 17 y 18 usan inyecciones de JavaScript.

Puede, y a menudo lo hará, inyectar JavaScript en JSX dentro de una función de renderizado.

```jsx
import React from "react";
import ReactDOM from "react-dom";

const redPanda = {
  src:
    "https://upload.wikimedia.org/wikipedia/commons/b/b2/Endangered_Red_Panda.jpg",
  alt: "Red Panda",
  width: "200px",
};

class RedPanda extends React.Component {
  render() {
    return (
      <div>
        <h1>Cute Red Panda</h1>
        <img src={redPanda.src} alt={redPanda.alt} width={redPanda.width} />
      </div>
    );
  }
}

ReactDOM.render(<RedPanda />, document.getElementById("app"));
```

---

# Poner lógica en una función de renderizado

Una función `render()` debe tener una declaración `return`. Sin embargo, eso no es _todo_ lo que puede tener.

Una función `render()` también puede ser un buen lugar para colocar cálculos simples que deben realizarse justo antes de que se renderice un componente. Aquí hay un ejemplo de algunos cálculos dentro de una función `render`:

```jsx
class Random extends React.Component {
  render() {
    // Primero, algo de lógica que debe suceder
    // antes de renderizar:
    const n = Math.floor(Math.random() * 10 + 1);
    // A continuación, una declaración de devolución
    // usando esa lógica:
    return <h1>The number is {n}!</h1>;
  }
}
```

Cuidado con este error común:

```jsx
class Random extends React.Component {
  // Esto debería estar en la función de renderizado:
  const n = Math.floor(Math.random() * 10 + 1);

  render() {
    return <h1>The number is {n}!</h1>;
  }
};
```

En el ejemplo anterior, la línea con la declaración `const n` causará un error de sintaxis, ya que no debería ser parte de la declaración de la clase en sí, sino que debería ocurrir en un método como `render()`.

---

# Use un condicional en una función de renderizado

¿Cómo podría usar una declaración _condicional_ dentro de una función `render()`?

Seleccione **TodaysPlan.js** para ver una forma de hacerlo.

Observe que la instrucción `if` se encuentra _dentro_ de la función de renderizado, pero _antes_ de la instrucción `return`. Esta es prácticamente la única forma en que verá una declaración `if` utilizada en una función de renderizado.

```js
import React from "react";
import ReactDOM from "react-dom";

class TodaysPlan extends React.Component {
  render() {
    let task;
    if (!apocalypse) {
      task = "learn React.js";
    } else {
      task = "run around";
    }

    return <h1>Today I am going to {task}!</h1>;
  }
}

ReactDOM.render(<TodaysPlan />, document.getElementById("app"));
```

---

# Use this en un componente

¡La palabra `this` se usa mucho en React!

Es especialmente probable que vea `this` dentro del cuerpo de una declaración de componente de clase. Aquí hay un ejemplo:

```jsx
class IceCreamGuy extends React.Component {
  get food() {
    return "ice cream";
  }

  render() {
    return <h1>I like {this.food}.</h1>;
  }
}
```

En el código, ¿qué significa `this`?

Una vez que tenga una conjetura, desplácese hacia abajo para ver la respuesta.

...

...

...

...

...

...

La respuesta simple es que `this` se refiere a una instancia de `IceCreamGuy`. La respuesta menos simple es que `this` se refiere al objeto en el que se llama `this` es el método que lo envuelve, en este caso `.render()`. Es casi inevitable que este objeto sea una instancia de `IceCreamGuy`, pero técnicamente podría ser otra cosa.

Supongamos que `this` se refiere a una instancia de su componente de clase, como será el caso en todos los ejemplos de este curso. `IceCreamGuy` tiene dos métodos: `.food` y `.render()`. Como `this` evaluará a una instancia de `IceCreamGuy`, `this.food` evaluará a una llamada del método `.food` de `IceCreamGuy` . Este método, a su vez, evaluará a la cadena "ice cream".

¿Por qué no necesitas paréntesis después de `this.food`? ¿No debería ser `this.food()`?

No necesita esos paréntesis porque `.food` es un método _getter_. Puede deducir esto del `get` en el cuerpo de declaración de clase anterior.

¡No hay nada específico de React sobre los métodos getter, ni sobre `this` comportandose de esta manera! Sin embargo, en React verá que `this` se usa de esta manera casi constantemente.

¡`This` en JavaScript puede ser un concepto difícil! Aquí hay un buen recurso para [comprender `this` en JavaScript](https://dmitripavlutin.com/gentle-explanation-of-this-in-javascript/).

---

# Usar un Event Listener en un componente

Las funciones de procesamiento a menudo contienen oyentes de eventos. Aquí hay un ejemplo de un detector de eventos en una función de renderizado:

```jsx
render () {
  return (
    <div onHover={myFunc}>
    </div>
  );
}
```

Recuerde que un _controlador_ de eventos es una función que se llama en respuesta a un evento. En el ejemplo anterior, el controlador de eventos es `myFunc()`.

En React, define manejadores de eventos como _métodos_ en un componente de clase. Como este:

```jsx
class MyClass extends React.Component {
  myFunc() {
    alert("Stop it. Stop Hovering");
  }

  render() {
    return <div onHover={this.myFunc}></div>;
  }
}
```

Observe que el componente de clase tiene dos métodos: `.myFunc()` y `.render()`. `.myFunc()` se está utilizando como _controlador de eventos_. Se llamará a `.myFunc()` cada vez que un usuario pase el mouse sobre el `<div></div>` renderizado.

---

# Resumen de componentes

¡Felicidades! Ha terminado la unidad en componentes React.

Los componentes de react son complicados. Su sintaxis es complicada, y el razonamiento detrás de su sintaxis es especialmente complicado.

Has aprendido mucho sobre su sintaxis y su razonamiento. Has aprendido sobre componentes de clase e instancias de componentes. Ha aprendido sobre `React.Component` y sobre las instrucciones que debe proporcionar a un componente de clase. Aprendió a `importar` y a renderizar una instancia de componente.

Se le han presentado algunas formas comunes de usar JSX en componentes React. Ha procesado componentes utilizando expresiones JSX multilínea, lógica dentro de la función de renderizado, una declaración condicional, `this` y un detector de eventos.

¡Ha pasado mucho tiempo estudiando los componentes React de forma aislada! Ahora, es hora de comenzar a aprender cómo los componentes encajan con el mundo que los rodea.

---

