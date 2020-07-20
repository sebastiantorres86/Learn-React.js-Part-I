# class vs className

Esta lección cubrirá JSX más avanzado. Aprenderá algunos trucos poderosos y algunos errores comunes a evitar.

La gramática en JSX es principalmente la misma que en HTML, pero hay diferencias sutiles a tener en cuenta. Probablemente el más frecuente de estos involucra la palabra `class`.

En HTML, es común usar `class` como un nombre de atributo:

```jsx
<h1 class="big">Hey</h1>
```

¡En JSX, no puedes usar la palabra `class`! Tienes que usar `className` en su lugar:

```jsx
<h1 className="big">Hey</h1>
```

Esto se debe a que JSX se traduce a JavaScript, y `class` es una palabra reservada en JavaScript.

Cuando se _renderiza_ JSX, los atributos `className` de JSX se representan automáticamente como atributos `class`.

---

# Etiquetas de cierre automático

Otro 'gotcha' de JSX implica _etiquetas de cierre automático_.

¿Qué es una etiqueta de cierre automático?

La mayoría de los elementos HTML usan dos etiquetas: una _etiqueta de apertura_ (`<div>`) y una _etiqueta de cierre_ (`</div>`). Sin embargo, algunos elementos HTML como `<img>` y `<input>` usan solo una etiqueta. La etiqueta que pertenece a un elemento de etiqueta única no es una etiqueta de apertura ni una etiqueta de cierre; Es una _etiqueta de cierre automático_.

Cuando escribe una etiqueta de cierre automático en HTML, es opcional incluir una barra diagonal inmediatamente antes del paréntesis angular final:

```HTML
Bien en HTML con una barra inclinada:

   <br />

También bien, sin la barra:

   <br>
```

¡Pero!

En JSX, _debe_ incluir la barra inclinada. Si escribe una etiqueta de cierre automático en JSX y olvida la barra, generará un error:

```js
Bien en JSX:

   <br />

PARA NADA BIEN en JSX:

   <br>
```

---

# JavaScript en su JSX en su JavaScript

Hasta ahora, nos hemos centrado en escribir expresiones JSX. Es similar a escribir bits de HTML, pero dentro de un archivo JavaScript.

En esta lección, vamos a agregar algo nuevo: JavaScript normal, escrito dentro de una expresión JSX, escrito dentro de un archivo JavaScript.

Whoaaaa...

---

# Llaves en JSX

El código del último ejercicio no se comportó como cabría esperar. En lugar de agregar 2 y 3, imprimió "2 + 3" como una cadena de texto. ¿Por qué?

Esto sucedió porque `2 + 3` se encuentra entre las etiquetas `<h1>` y `</h1>`.

¡Cualquier código entre las etiquetas de un elemento JSX se leerá como JSX, no como JavaScript normal! JSX no agrega números, los lee como texto, al igual que HTML.

Necesita una forma de escribir código que diga: "Aunque esté ubicado entre etiquetas JSX, tráteme como JavaScript ordinario y no como JSX".

Puede hacer esto envolviendo su código entre _llaves_.

---

# 20 dígitos de Pi en JSX

¡Ahora puede inyectar JavaScript normal en expresiones JSX! Esto será extremadamente útil.

En el editor de código, puede ver una expresión JSX que muestra los primeros veinte dígitos de pi.

Estudie la expresión y observe lo siguiente:

- El código está escrito en un archivo JavaScript. Por defecto, todo se tratará como JavaScript normal.
- Busque `<div>` en la línea 5. Desde allí hasta `</div>`, el código se tratará como JSX.
- Encuentra `Math`. Desde allí hasta `(20)`, el código será tratado nuevamente como JavaScript normal.
- Las llaves no se tratarán como JSX ni JavaScript. Son _marcadores_ que señalan el comienzo y el final de una inyección de JavaScript en JSX, similar a las comillas que señalan los límites de una cadena.

```jsx
import React from "react";
import ReactDOM from "react-dom";

const pi = (
  <div>
    <h1>PI, YALL!</h1>
    <p>{Math.PI.toFixed(20)}</p>
  </div>
);

ReactDOM.render(pi, document.getElementById("app"));
```

---

# Variables en JSX

Cuando inyecta JavaScript en JSX, ese JavaScript forma parte del mismo entorno que el resto del JavaScript en su archivo.

Eso significa que puede acceder a las variables dentro de una expresión JSX, incluso si esas variables se declararon en el exterior.

```jsx
// Declara una variable:
const name = "Gerdo";

// Accede a tu variable
// desde el interior de una expresión JSX:
const greeting = <p>Hello, {name}!</p>;
```

---

# Atributos variables en JSX

Al escribir JSX, es común usar variables para establecer _atributos_.

Aquí hay un ejemplo de cómo podría funcionar:

```jsx
// Use una variable para establecer los atributos `height` y`width`:

const sideLength = "200px";

const panda = (
  <img
    src="images/panda.jpg"
    alt="panda"
    height={sideLength}
    width={sideLength}
  />
);
```

Observe cómo en este ejemplo, los atributos de `<img />` obtienen cada uno su propia línea. Esto puede hacer que su código sea más legible si tiene muchos atributos en un elemento.

Las `propiedades de los objetos` también se usan a menudo para establecer atributos:

```jsx
const pics = {
  panda: "http://bit.ly/1Tqltv5",
  owl: "http://bit.ly/1XGtkM3",
  owlCat: "http://bit.ly/1Upbczi",
};

const panda = <img src={pics.panda} alt="Lazy panda" />;

const owl = <img src={pics.owl} alt="Unimpressed Owl" />;

const owlCat = <img src={pics.owlCat} alt="Ghastly Abomination" />;
```

---

# Oyentes de eventos en JSX

Los elementos JSX pueden tener _oyentes de eventos_, al igual que los elementos HTML. Programar en React significa trabajar constantemente con oyentes de eventos.

Puede crear un detector de eventos dando a un elemento JSX un _atributo_ especial. Aquí hay un ejemplo:

```jsx
<img onClick={myFunc} />
```

El _nombre_ de un atributo de escucha de eventos debe ser algo como `onClick` o `onMouseOver`: la palabra `on`, más el tipo de evento que está escuchando. Puede ver una lista de nombres de eventos válidos [aquí](http://facebook.github.io/react/docs/events.html#supported-events).

El _valor_ de un atributo de escucha de eventos debe ser una función. El ejemplo anterior solo funcionaría si `myFunc` fuera una función válida que se hubiera definido en otro lugar:

```jsx
function myFunc() {
  alert("Make myFunc the pFunc... omg that was horrible i am so sorry");
}

<img onClick={myFunc} />;
```

Tenga en cuenta que en HTML, los _nombres_ de escucha de eventos se escriben en minúsculas, como `onclick` o `onmouseover`. En JSX, los nombres de escucha de eventos se escriben en camelCase, como `onClick` o `onMouseOver`.

---

# Condicionales JSX: las declaraciones if que no funcionan

¡Buen trabajo! ¡Aprendiste a usar llaves para inyectar JavaScript en una expresión JSX!

Aquí hay una regla que debe saber: no puede inyectar una declaración if en una expresión JSX.

Este código se romperá:

```jsx
(
 <h1>
   {
     if (purchase.complete) {
       'Thank you for placing an order!'
     }
   }
 </h1>
)
```

El motivo tiene que ver con la forma en que se compila JSX. No necesita comprender la mecánica de esto por ahora, pero si está interesado, puede obtener más información [aquí](http://facebook.github.io/react/tips/if-else-in-JSX.html).

¿Qué sucede si desea que se represente una expresión JSX, pero solo bajo ciertas circunstancias? No puede inyectar una declaración `if`. ¿Qué puedes hacer?

Tienes muchas opciones. En las próximas lecciones, exploraremos algunas formas simples de escribir _condicionales_ (expresiones que solo se ejecutan bajo ciertas condiciones) en JSX.

---

# Condicionales JSX: declaraciones if que funcionan

¿Cómo puede escribir un _condicional_ si no puede inyectar una declaración `if` en JSX?

Bueno, una opción es escribir una declaración `if` y _no_ inyectarla en JSX.

Mira **if.js**. Siga la declaración `if`, desde la línea 6 hasta la línea 18.

`if.js` funciona, porque las palabras `if` y `else` _no_ se inyectan entre etiquetas JSX. La declaración `if` está en el exterior y no es necesaria la inyección de JavaScript.

Esta es una forma común de expresar condicionales en JSX.

```jsx
import React from 'react'
import ReactDOM from 'react-dom'

ñet message;

if (user.age => drinkingAge) {
  message = (
    <h1>
      Hey, check out this alcoholic beverage!
    </h1>
  );
} else {
  message = (
    <h1>
      Hey, check out these earrings I got at Claire's!
    </h1>
  )
}

ReactDOM.render(message, document.getElementById('app'));
```

---

# Condicionales JSX: el operador ternario

Hay una forma más compacta de escribir condicionales en JSX: el _operador ternario_.

El operador ternario funciona de la misma manera en React que en JavaScript normal. Sin embargo, aparece en React sorprendentemente a menudo.

Recordemos cómo funciona: escribes `x ? y : z`, donde x, y y z son todas expresiones de JavaScript. Cuando se ejecuta su código, `x` se evalúa como "verdadero" o "falso". Si `x` es verdadero, entonces todo el operador ternario devuelve `y`. Si `x` es falso, entonces todo el operador ternario devuelve `z`. [Aquí](http://stackoverflow.com/questions/6259982/how-to-use-the-ternary-operator-in-javascript) hay una buena explicación si necesita un repaso.

A continuación, le mostramos cómo puede usar el operador ternario en una expresión JSX:

```jsx
const headline = <h1>{age >= drinkingAge ? "Buy Drink" : "Do Teen Stuff"}</h1>;
```

En el ejemplo anterior, si `age` es mayor o igual que `drinkingAge`, `headline` será igual a `<h1>Buy Drink</h1>`. De lo contrario, `headline` será igual a `<h1>Do Teen Stuff</h1>`.

---

# Condicionales JSX: &&

Vamos a cubrir una última forma de escribir condicionales en React: el operador `&&`.

Al igual que el operador ternario, `&&` no es específico de React, pero aparece en React sorprendentemente a menudo.

En las últimas dos lecciones, escribiste declaraciones que a veces representaban a un gatito y otras a un perrito. `&&` _no_ habría sido la mejor opción para esas lecciones.

`&&` funciona mejor en condicionales que a veces harán una acción, pero otras veces _no hacen nada_.

Aquí hay un ejemplo:

```jsx
const tasty = (
  <ul>
    <li>Applesauce</li>
    {!baby && <li>Pizza</li>}
    {age > 15 && <li>Brussels Sprouts</li>}
    {edad > 20 && <li>Oysters</li>}
    {edad > 25 && <li>Grappa</li>}
  </ul>
);
```

Cada vez que vea `&&` en este ejemplo, se ejecutará algún código o _no se ejecutará ningún código_.

---

# .map en JSX

El método de matriz `.map()` aparece a menudo en React. Es bueno acostumbrarse a usarlo junto con JSX.

Si desea crear una lista de elementos JSX, entonces `.map()` suele ser su mejor opción. Al principio puede parecer extraño:

```jsx
const strings = ['Home', 'Shop', 'About Me'];

const listItems = strings.map(string => <li>{string}</li>);

<ul> {listItems} </ul>
```

En el ejemplo anterior, comenzamos con una serie de cadenas. Llamamos a .map () en esta matriz de cadenas, y la llamada .map () devuelve una nueva matriz de <li> s.

En la última línea del ejemplo, tenga en cuenta que {listItems} se evaluará en una matriz, ¡porque es el valor devuelto de .map ()! Los JSX <li> no tienen que estar en una matriz como esta, pero pueden estarlo.

// Esto está bien en JSX, no en una matriz explícita:

<ul>
   <li> elemento 1 </li>
   <li> elemento 2 </li>
   <li> elemento 3 </li>
</ul>

// ¡Esto también está bien!

const liArray = [

   <li> elemento 1 </li>,
   <li> elemento 2 <li>,
   <li> elemento 3 </li>
];

<ul> {liArray} </ul>
