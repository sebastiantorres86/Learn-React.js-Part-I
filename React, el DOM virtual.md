# React: el DOM virtual

### Lucha contra el despilfarro en la manipulación del DOM

## El problema

[La manipulación del DOM](https://www.codecademy.com/courses/build-interactive-websites/lessons/javascript-dom/exercises/document) es el corazón de la web moderna e interactiva. Desafortunadamente, también es mucho más lento que la mayoría de las operaciones de JavaScript.

Esta lentitud empeora por el hecho de que **la mayoría de los frameworks de JavaScript actualizan el DOM mucho más de lo necesario**.

Como ejemplo, supongamos que tiene una lista que contiene diez elementos. Usted marca el primer artículo. La mayoría de los frameworks de JavaScript reconstruirían _la lista completa_. ¡Eso es diez veces más trabajo del necesario! Solo cambió un artículo, pero los nueve restantes se reconstruyeron exactamente como estaban antes.

Reconstruir una lista no es gran cosa para un navegador web, pero los sitios web modernos pueden usar grandes cantidades de manipulación DOM. La actualización ineficiente se ha convertido en un problema grave.

Para abordar este problema, la gente de React popularizó algo llamado _DOM virtual_.

## El DOM virtual

En React, para cada [objeto DOM](http://eloquentjavascript.net/13_dom.html), hay un "objeto DOM virtual" correspondiente. Un objeto DOM virtual es una _representación_ de un objeto DOM, como una copia ligera.

Un objeto DOM virtual tiene las mismas propiedades que un objeto DOM real, pero carece del poder real para cambiar directamente lo que está en la pantalla.

La manipulación del DOM es lenta. Manipular el DOM virtual es mucho más rápido, porque nada se dibuja en la pantalla. Piense en manipular el DOM virtual como editar un plano, en lugar de mudarse de una casa real.

## Como ayuda

Cuando renderiza un elemento JSX, cada objeto DOM virtual se actualiza.

Esto suena increíblemente ineficiente, pero el costo es insignificante porque el DOM virtual puede actualizarse muy rápidamente.

Una vez que el DOM virtual se ha actualizado, React compara el DOM virtual con una _instantánea_ del DOM virtual que se tomó justo antes de la actualización.

Al comparar el nuevo DOM virtual con una versión previa a la actualización, React descubre _exactamente qué objetos DOM virtuales han cambiado_. Este proceso se llama "diferir".

Una vez que React sabe qué objetos DOM virtuales han cambiado, React actualiza esos objetos, _y solo esos objetos_, en el DOM real. En nuestro ejemplo de antes, React sería lo suficientemente inteligente como para reconstruir su único elemento de lista marcado y dejar solo el resto de su lista.

¡Esto hace una gran diferencia! React puede actualizar solo las partes necesarias del DOM. La reputación de rendimiento de React proviene en gran medida de esta innovación.

En resumen, esto es lo que sucede cuando intenta actualizar el DOM en React:

1. Todo el DOM virtual se actualiza.
2. El DOM virtual se compara con su aspecto antes de actualizarlo. Reaccionar descubre qué objetos han cambiado.
3. Los objetos modificados, y solo los objetos modificados, se actualizan en el DOM _real_.
4. Los cambios en el DOM real hacen que la pantalla cambie.

Si desea obtener más información sobre el DOM virtual, [este es un buen lugar para comenzar](http://reactkungfu.com/2015/10/the-difference-between-virtual-dom-and-dom/).


