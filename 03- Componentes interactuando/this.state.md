# State

La [información dinámica](http://www.teach-ict.com/as_a2_ict_new/ocr/AS_G061/311_data_info_knowledge/static_dynamic_data/miniweb/pg4.htm) es información que puede cambiar.

Los componentes de react a menudo necesitarán _información dinámica_ para renderizar. Por ejemplo, imagine un componente que muestra el puntaje de un juego de baloncesto. La puntuación del juego puede cambiar con el tiempo, lo que significa que la puntuación es _dinámica_. Nuestro componente tendrá que conocer el puntaje, una pieza de información dinámica, para poder representar de manera útil.

Hay dos formas para que un componente obtenga información dinámica: `props` y `state`. Además de los `props` y `state`, cada valor utilizado en un componente siempre debe permanecer exactamente igual.

Acabas de pasar una larga lección aprendiendo sobre `props`. Ahora es el momento de aprender sobre `state`. Los `props` y `state` son todo lo que necesita para configurar un ecosistema de componentes React interactivos.

---

# Establecer estado inicial

Un componente React puede acceder a información dinámica de dos maneras: `props` y `state`.

A diferencia de los `props`, el `state` de un componente _no_ se pasa desde el exterior. Un componente decide su propio `state`.

Para hacer que un componente tenga `state`, dele al componente una propiedad `state`. Esta propiedad debe declararse dentro de un método constructor, como este:

```jsx
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = { mood: "decent" };
  }

  render() {
    return <div></div>;
  }
}

<Example />;
```

Whoa, un método constructor? `super(props)`? ¿Que está pasando aqui? Veamos más de cerca este código potencialmente desconocido:

```jsx
constructor(props) {
  super(props);
  this.state = { mood: 'decent' };
}
```

`this.state` debería ser igual a un objeto, como en el ejemplo anterior. Este objeto representa el "estado" inicial de cualquier instancia de componente. ¡Lo explicaremos más pronto!

¿Qué tal el resto del código? `constructor` y `super` son características de ES6, no exclusivas de React. No hay nada particularmente Reactico sobre su uso aquí. Una explicación completa de su funcionalidad está fuera del alcance de este curso, pero le recomendamos [familiarizarse](https://hacks.mozilla.org/2015/07/es6-in-depth-classes/). Es importante tener en cuenta que los componentes React _siempre_ tienen que llamar a `super` en sus constructores para configurarse correctamente.

Mire la parte inferior del ejemplo de código más alto en esta columna. `<Exemplo />` tiene un `state`, y su `state` es igual a `{ mood: 'decent' }`.

---

# Acceder al estado de un componente

Para _leer_ el `state` de un componente, use la expresión `this.state.name-of-property`:

```jsx
class TodayImFeeling extends React.Component {
  constructor(props) {
    super(props);
    this.state = { mood: "decent" };
  }

  render() {
    return <h1>I'm feeling {this.state.mood}!</h1>;
  }
}
```

El component de clase anterior lee una propiedad en su `state` desde el interior de su función `render`.

Al igual que `this.props`, puede usar `this.state` desde cualquier propiedad definida dentro del cuerpo de un componente de clase.

---

# Actualizar estado con this.setState

Un componente puede hacer más que solo leer su propio estado. Un componente también puede _cambiar_ su propio estado.

Un componente cambia su estado llamando a la función `this.setState()`.

`this.setState()` toma dos argumentos: un _objeto_ que actualizará el estado del componente y una devolución de llamada. Básicamente nunca necesitas la devolución de llamada.

En el editor de código, eche un vistazo a **Example.js**. Observe que `<Example />` tiene un estado de:

```jsx
{
  mood: 'great',
  hungry: false
}
```

Ahora, digamos que <Example /> llamaría a:

```jsx
this.setState({ hungry: true });
```

Después de esa llamada, aquí está el estado de `<Example />`:

```jsx
{
  mood: 'great',
  hungry: true
}
```

¡La parte del `mood` del estado no se ve afectada!

`this.setState()` toma un objeto y lo _combina_ con el estado actual del componente. Si hay propiedades en el estado actual que no son parte de ese objeto, entonces esas propiedades permanecen como estaban.

```jsx
import React from "react";

class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      mood: "great",
      hungry: false,
    };
  }

  render() {
    return <div></div>;
  }
}

<Example />;
```

---

# Llame this.setState desde otra función

La forma más común de llamar a `this.setState()` es llamar a una función personalizada que _envuelve_ una llamada `this.setState()`. `.makeSomeFog()` es un ejemplo:

```jsx
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = { weather: "sunny" };
    this.makeSomeFog = this.makeSomeFog.bind(this);
  }

  makeSomeFog() {
    this.setState({
      weather: "foggy",
    });
  }
}
```

Observe cómo el método `makeSomeFog()` contiene una llamada a `this.setState()`.

Es posible que hayas notado una línea extraña allí:

```jsx
this.makeSomeFog = this.makeSomeFog.bind(this);
```

Esta línea es necesaria porque el cuerpo de `makeSomeFog()` contiene la palabra `this`. ¡Hablaremos más de eso pronto!

Veamos cómo una función que envuelve `this.setState()` podría funcionar en la práctica. En el editor de código, lea **Mood.js** hasta el final.

Así es como se establecería el estado de `<Mood />`:

1. Un usuario activa un _evento_ (en este caso, un evento de clic, que se activa haciendo clic en un `<button></button>`).

2. El evento del Paso 1 está siendo escuchado (en este caso por el atributo `onClick` en la línea 20).

3. Cuando se produce este evento escuchado, llama a una función de _controlador de eventos_ (en este caso, `this.toggleMood()`, llamada en la línea 20 y definida en las líneas 11-14).

4. Dentro del cuerpo del _controlador de eventos_, se llama a `this.setState()` (en este caso en la línea 13).

5. ¡El `state` del componente ha cambiado!

Debido a la forma en que los controladores de eventos están vinculados en JavaScript, `this.toggleMood()` pierde su `this` cuando se usa en la línea 20. Por lo tanto, las expresiones `this.state.mood` y `this.setState` en las líneas 7 y 8 no significarán lo que se supone que deben hacer... _a menos_ que ya hayas vinculado el `this` correcto a `this.toggleMood`.

Es por eso que debemos vincular `this.toggleMood` a `this` en la línea 8.

Para obtener una explicación detallada de este tipo de trucos vinculantes, comience con [los documentos React](https://facebook.github.io/react/docs/handling-events.html). Para los menos curiosos, solo sepa que en React, cada vez que defina un controlador de eventos que use esto, debe agregar `this.methodName = this.methodName.bind(this)` a su función de constructor.

Mire la declaración en la línea 12. ¿Qué hace eso?

La línea 12 declara un `const` llamado `newMood` igual al opuesto de `this.state.mood`. Si `this.state.mood` es "good", entonces `newMood` será "bad" y viceversa.

Una instancia de `<Mood />` mostraría "I'm feeling good!" junto con un botón. Al hacer clic en el botón, la pantalla cambiará a "I'm feeling bad!" Al hacer clic nuevamente, volvería a "I'm feeling good", etc. Intente seguir el tutorial paso a paso en **Mood.js** y vea cómo funciona todo esto.

Una nota final: ¡_no puedes_ llamar a `this.setState()` desde el interior de la función de renderizado! Explicaremos por qué en el próximo ejercicio.

```jsx
// Mood.js
import React from "react";
import ReactDOM from "react-dom";

class Mood extends React.Component {
  constructor(props) {
    super(props);
    this.state = { mood: "good" };
    this.toggleMood = this.toggleMood.bind(this);
  }

  toggleMood() {
    const newMood = this.state.mood == "good" ? "bad" : "good";
    this.setState({ mood: newMood });
  }

  render() {
    return (
      <div>
        <h1>I'm feeling {this.state.mood}!</h1>
        <button onClick={this.toggleMood}>Click Me</button>
      </div>
    );
  }
}

ReactDOM.render(<Mood />, document.getElementById("app"));
```

---

# this.setState llama automáticamente a render

Hay algo extraño en todo esto.

Mire nuevamente a **Toggle.js**.

Cuando un usuario hace clic en el `<button></button>`, se llama al método `.changeColor()`. Eche un vistazo a la definición de `.changeColor()`.

`.changeColor()` llama a `this.setState()`, que actualiza `this.state.color`. Sin embargo, incluso si `this.state.color` se actualiza de `green` a `yellow`, ¡eso por sí solo no debería ser suficiente para hacer que el color de la pantalla cambie!

El color de la pantalla no cambia hasta que se _renderice_ `Toggle`.

Dentro de la función de renderizado, está esta línea:

```jsx
<div style={{background: this.state.color}}>
```

que cambia el color de un objeto DOM virtual al nuevo `this.state.color`, lo que eventualmente provoca un cambio en la pantalla.

Si llamas a `.changeColor()`, ¿no deberías llamar _además_ a `.render()` nuevamente? `.changeColor()` solo hace que, la próxima vez que renderice, el color sea diferente. ¿Por qué puede ver el nuevo fondo de inmediato si no ha vuelto a representar el componente?

He aquí el por qué: _cada vez que llame a this.setState(), this.setState() llama AUTOMÁTICAMENTE a .render() tan pronto como el estado haya cambiado_.

Piense en `this.setState()` como en realidad dos cosas: `this.setState()`, inmediatamente seguido de `.render()`.

¡Es por _eso_ que no puedes llamar a `this.setState()` desde el interior del método `.render()`! `this.setState()` llama _automáticamente_ a `.render()`. Si `.render()` llama a `this.setState()`, se crea un bucle infinito.

```jsx
// Toggle.js
import React from "react";
import ReactDOM from "react-dom";

const green = "#39D1B4";
const yellow = "#FFD712";

class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = { color: green };
    this.changeColor = this.changeColor.bind(this);
  }

  changeColor() {
    const newColor = this.state.color == green ? yellow : green;
    this.setState({ color: newColor });
  }

  render() {
    return (
      <div style={{ background: this.state.color }}>
        <h1>Change my color</h1>
        <button onClick={this.changeColor}>Change color</button>
      </div>
    );
  }
}

ReactDOM.render(<Toggle />, document.getElementById("app"));
```

---

# Resumen de interacción de componentes

En esta unidad, aprendió a usar `import` y `export` para acceder a un archivo desde otro. Aprendiste sobre los `props` y el `state`, y las innumerables variaciones sobre cómo funcionan.

Antes de esta unidad, aprendió sobre JSX, los componentes y cómo pueden trabajar juntos.

Una aplicación React es básicamente una gran cantidad de componentes, configurando el `state` y pasando `props` entre sí. Ahora que tiene una comprensión real de cómo usar `props` y `state`, ¡tiene con mucho las herramientas más importantes que necesita!

En futuras lecciones, el enfoque se desplazará ligeramente hacia afuera. Además de aprender más habilidades nuevas, también aprenderá sus primeros _patrones de programación_. Estas estrategias a gran escala te ayudarán a combinar lo que has aprendido y realmente comenzar a construir.
