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

# 
