# this.props

Anteriormente, aprendió una forma en que los componentes pueden interactuar: un componente puede _renderizar_ a otro componente.

En esta lección, aprenderá otra forma en que los componentes pueden interactuar: un componente puede _pasar información_ a otro componente.

La información que se pasa de un componente a otro se conoce como "props".

---

# Acceder a los props de un componente

Cada componente tiene algo llamado `props`.

Los `props` de un componente son un objeto. Contiene información sobre ese componente.

Para ver el objeto de `props` de un componente, use la expresión `this.props`. Aquí hay un ejemplo de `this.props` utilizados dentro de un método de renderizado:

```jsx
render() {
  console.log("Props object comin' up!");

  console.log(this.props);

  console.log("That was my props object!");

  return <h1>Hello world</h1>;
}
```

¡La mayor parte de la información en `this.props` es bastante inútil! Pero algo de esto es extremadamente importante, como verá.

---

# Pase `props` a un Componente

Puede _pasar información_ a un componente React.

¿Cómo? Al darle a ese componente _un atributo_:

```jsx
<MyComponent foo="bar" />
```

Supongamos que desea pasar a un componente el mensaje `"This is some top secret info"`. Así es como puedes hacerlo:

```jsx
<Example message="This is some top secret info". />
```

Como puede ver, para pasar información a un componente, necesita un _nombre_ para la información que desea pasar.

En el ejemplo anterior, utilizamos el nombre `message`. Puedes usar el nombre que quieras.

Si desea pasar información que no sea una cadena, envuelva esa información entre llaves. Así es como pasarías una matriz:

```jsx
<Greeting myInfo={["top", "secret", "lol"]} />
```

En el siguiente ejemplo, pasamos varios datos a <Greeting />. Los valores que no son cadenas están envueltos en llaves:

```jsx
<Greeting name="Frarthur" town="Flundon" age={2} haunted={false} />
```

---

# Renderizar los props de un componente

¡Acaba de _pasar_ información al objeto de `props` de un componente!

A menudo querrás que un componente _muestre_ la información que pasas.

A continuación, le mostramos cómo hacer que un componente muestre información transmitida:

1- Encuentra el _componente de clase_ que va a recibir esa información.
2- Incluya `this.props.name-of-information` en la declaración `return` del método _render_ de ese componente de clase.

---

# Pase props de componente a componente

Has aprendido cómo pasar un `prop` a un componente:

```jsx
<Greeting firstName="Esmerelda" />
```

También ha aprendido cómo acceder y mostrar un `prop` pasado:

```jsx
  render() {
    return <h1>{this.props.firstName}</h1>;
}
```

El uso más común de `props` es pasar información a un componente, _desde un componente diferente_. Aún no lo ha hecho, pero es muy similar a lo que ya ha visto.

En este ejercicio, pasarás un `prop` de un componente a otro.

**Una aclaración cascarrabias sobre la gramática:**
Es posible que haya notado un poco de uso de las palabras prop y `props`. Desafortunadamente, esto es bastante inevitable.

`props` es el nombre del objeto que almacena la información transmitida. `this.props` se refiere a ese objeto de almacenamiento. Al mismo tiempo, cada pieza de información que se pasa se llama prop. Esto significa que los `props` podrían referirse a dos datos pasados, o podría referirse al objeto que almacena esos datos :(

---

# Renderiza una interfaz de usuario diferente basada en props

¡Increíble! ¡Pasó un prop de un componente a un componente diferente, accedió a ese prop desde el componente receptor y lo renderizó!

Puedes hacer más con `props` que solo mostrarlos. También puedes usar `props` para tomar decisiones.

En el editor de código, mire el componente de clase `Welcome`.

Se puede deducir de `this.props.name` en la línea 5 que `Welcome` espera recibir una información llamada _name_. Sin embargo, ¡`Welcome` nunca brinda esta información! En cambio, utiliza la información para tomar una decisión.

Las instancias de `<Welcome />` mostrarán el texto `WELCOME "2" MY WEB SITE BABYYY!!!!!`, a menos que el usuario sea Mozart, en cuyo caso renderizará el mas respetuoso `hello sir it is truly great to meet you here on the web`.

¡El _name_ pasado no se muestra en ninguno de los casos! El nombre se usa para _decidir_ qué se mostrará. Esta es una técnica común.

Seleccione **Home.js** y mirel componente de clase `Home`. ¿Qué mostrará `<Welcome />` en la pantalla?

```jsx
// Welcome.js
import React from "react";

export class Welcome extends React.Component {
  render() {
    if (this.props.name == "Wolfgang Amadeus Mozart") {
      return <h2>hello sir it is truly great to meet you here on the web</h2>;
    } else {
      return <h2>WELCOME "2" MY WEB SITE BABYYY!!!!!</h2>;
    }
  }
}
```

```jsx
// Home.js
import React from "react";
import ReactDOM from "react-dom";
import { Welcome } from "./Welcome";

class Home extends React.Component {
  render() {
    return <Welcome name="Ludwig van Beethoven" />;
  }
}

ReactDOM.render(<Home />, document.getElementById("app"));
```

---

# Poner un Event Handler en un componente de clase

Puede, y con frecuencia lo hará, pasar funciones como `props.` Es especialmente común pasar las funciones _event handler_.

En la próxima lección, pasará una función de controlador de eventos como prop. Sin embargo, debe _definir_ un controlador de eventos antes de poder pasar uno a cualquier lugar. En esta lección, definirá una función de controlador de eventos.

¿Cómo define un controlador de eventos en React?

Define un controlador de eventos como un método en el componente de clase, al igual que el método _render_. Casi todas las funciones que defina en React se definirán de esta manera, como métodos en una clase.

Echa un vistazo en el editor de código. En las líneas 4 a 8, se define un método de _controlador de eventos_, con una sintaxis similar a la del método de renderizado. En la línea 12, ese método de controlador de eventos se adjunta a un _evento_ (un evento de clic, en este caso).

```jsx
import React from "react";

class Example extends React.Component {
  handleEvent() {
    alert(`I am an event handler.
      If you see this message,
      then I have been called.`);
  }

  render() {
    return <h1 onClick={this.handleEvent}>Hello world</h1>;
  }
}
```

---

# Pase un controlador de eventos como prop

¡Bien! Ha definido un nuevo método en el componente de clase `Talker`. Ahora está listo para _pasar_ esa función a otro componente.

Puede pasar un método exactamente de la misma manera que pasa cualquier otra información. He aquí, el poderoso JavaScript.

---

# Recibe un controlador de eventos como prop

¡Excelente! Acaba de pasar una función de `<Talker />` a `<Button />`.

En el editor de código, seleccione **Button.js**. Observe que `Button` renderiza un elemento `<button></button>`.

Si un usuario hace clic en este elemento `<button></button>`, entonces desea que se llame a su función `talk` transmitida.

Eso significa que debe adjuntar `talk` al `<button></button>` como _controlador de eventos_.

¿Cómo haces eso? De la misma manera que adjunta cualquier controlador de eventos a un elemento JSX: le da a ese elemento JSX un _atributo_ especial. El _nombre_ del atributo debe ser algo como `onClick` u `onHover`. El _valor_ del atributo debe ser el controlador de eventos que desea adjuntar.

```jsx
// Button.js
import React from "react";

export class Button extends React.Component {
  render() {
    return <button>Click me!</button>;
  }
}
```

---

# handleEvent, onEvent y this.props.onEvent

Hablemos de nombrar cosas.

Cuando pasa un _controlador de eventos_ como prop, como acaba de hacer, hay dos nombres que debe elegir.

Ambas opciones de nomenclatura se producen en el componente de clase _principal_, es decir, en el componente de clase que define el controlador de eventos y lo pasa.

El primer nombre que debe elegir es el nombre del controlador de eventos en sí.

Mire **Talker.js**, líneas 6 a 12. Este es nuestro controlador de eventos. Elegimos nombrarlo `talk`.

El segundo nombre que debe elegir es el nombre del prop que usará para _pasar_ el controlador de eventos. Esto es lo mismo que el nombre de su atributo.

Para nuestro nombre de prop, también elegimos `talk`, como se muestra en la línea 15:

```jsx
return <Button talk={this.talk} />;
```

Estos dos nombres pueden ser lo que quieras. Sin embargo, hay una convención de nomenclatura que a menudo siguen. No tiene que seguir esta convención, pero debe entenderla cuando la vea.

Así es como funciona la convención de nomenclatura: primero, piense en qué _tipo de evento_ está escuchando. En nuestro ejemplo, el tipo de evento fue "clic".

Si está escuchando un evento de "clic", entonces nombra su _controlador de evento_ `handleClick`. Si está escuchando un evento “keyPress”, entonces nombra su manejador de evento `handleKeyPress`:

```jsx
class MyClass extends React.Component {
  handleHover() {
    alert("I am an event handler.");
    alert('I will be called in response to "hover" events.');
  }
}
```

Su nombre de prop debe ser la palabra `on`, más su tipo de evento. Si está escuchando un evento de "click", entonces nombra su prop `onClick`. Si está escuchando un evento "keyPress", entonces nombra su prop `onKeyPress`:

```jsx
class MyClass extends React.Component {
  handleHover() {
    alert("I am an event handler.");
    alert('I will listen for a "hover" event.');
  }

  render() {
    return <Child onHover={this.handleHover} />;
  }
}
```

```jsx
// Talker.js
import React from "react";
import ReactDOM from "react-dom";
import { Button } from "./Button";

class Talker extends React.Component {
  talk() {
    let speech = "";
    for (let i = 0; i < 10000; i++) {
      speech += "blah ";
    }
    alert(speech);
  }

  render() {
    return <Button talk={this.talk} />;
  }
}

ReactDOM.render(<Talker />, document.getElementById("app"));
```

---

# this.props.children

El objeto de `props` de cada componente tiene una propiedad llamada `children`.

`this.props.children` devolverá todo entre las etiquetas JSX de apertura y cierre de un componente.

Hasta ahora, todos los componentes que ha visto han sido _etiquetas de cierre automático_, como `<MyComponentClass />`. ¡No tienen que serlo! Podría escribir `<MyComponentClass></MyComponentClass>`, y aún así funcionaría.

`this.props.children` devolvería todo entre `<MyComponentClass>` y `</MyComponentClass>`.

Mira **BigButton.js**. En el _Example 1_, `<BigButton>`, el `this.props.children` equivaldría al texto, "I am a child of BigButton.".

En el _Example 2_, `<BigButton>`, el `this.props.children` equivaldría a un componente `<LilButton />`.

En el _Example 3_, `<BigButton>` el `this.props.children` equivaldría a `undefined`.

Si un componente tiene más de un elemento secundario entre sus etiquetas JSX, `this.props.children` devolverá esos elementos secundarios en una matriz. Sin embargo, si un componente tiene solo un hijo, `this.props.children` devolverá el hijo único, _no_ envuelto en una matriz.

```jsx
// BigButton.js
import React from 'react';
import { LilButton } from './LilButton';

class BigButton extends React.Component {
  render() {
    console.log(this.props.children);
    return <button>Yo I am big</button>;
  }
}


// Example 1
<BigButton>
  I am a child of BigButton.
</BigButton>


// Example 2
<BigButton>
  <LilButton />
</BigButton>


// Example 3
<BigButton />
```

---

# defaultProps

Eche un vistazo al componente de clase `Button`.

Observe que en la línea 8, `Button` espera recibir un prop llamado `text`. El `text` recibido se mostrará dentro de un elemento `<button></button>`.

¿Qué pasa si nadie pasa ningún `text` a `Button`?

Si nadie pasa ningún `text` a `Button`, la pantalla de `Button` estará en blanco. Sería mejor si `Button` pudiera mostrar un mensaje predeterminado en su lugar.

Puede hacer que esto suceda dando a su componente de clase una propiedad llamada `defaultProps`:

```jsx
class Example extends React.Component {
  render() {
    return <h1>{this.props.text}</h1>;
  }
}

Example.defaultProps;
```

La propiedad `defaultProps` debe ser igual a un objeto:

```jsx
class Example extends React.Component {
  render() {
    return <h1>{this.props.text}</h1>;
  }
}

// Establecer defaultProps igual a un objeto:
Example.defaultProps = {};
```

Dentro de este objeto, escriba propiedades para cualquier `props` predeterminado que desee establecer:

```jsx
class Example extends React.Component {
  render() {
    return <h1>{this.props.text}</h1>;
  }
}

Example.defaultProps = { text: "yo" };
```

Si un `<Example />` no pasa ningún texto, mostrará "yo".

Si un `<Example />` _pasa_ algún texto, mostrará ese texto pasado.

```jsx
// Button.js
import React from "react";
import ReactDOM from "react-dom";

class Button extends React.Component {
  render() {
    return <button>{this.props.text}</button>;
  }
}

// defaultProps goes here:

ReactDOM.render(<Button />, document.getElementById("app"));
```

---

# Resumen de this.props

¡Eso completa nuestra lección sobre `props`!

`props` es posiblemente la lección más larga y difícil en todos nuestros cursos de React. ¡Felicitaciones por llegar hasta aquí!

Estas son algunas de las habilidades que ha aprendido:

- Pasar un prop dando un _atributo_ a una instancia de componente
- Acceder a un prop pasado a través de `this.props.prop-name`
- Mostrar un prop
- Usar un prop para tomar decisiones sobre qué mostrar
- Definir un controlador de eventos en un componente de clase
- Pasar un controlador de eventos como prop
- Recibir un controlador de eventos prop y adjuntarlo a un oyente de eventos
- Nombrar controladores de eventos y atributos de controladores de eventos de acuerdo con la convención
- `this.props.children`
- `getDefaultProps`

¡Eso es mucho! No te preocupes si todo es un poco borroso. ¡Pronto tendrás mucha práctica!
