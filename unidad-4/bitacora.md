# Evidencias para la unidad 4

## preguntasa para el profe (siento que lo puede explicar mejor que una IA)

¿ cuando se crea un destructor, y elimina todo automaticamente, como en el programa no se borran los resultados? ¿se hace una copia en otro lugar?

> [!NOTE]
> Como funciona la funcion bob_back
>
> Supón que tienes una lista con 3 nodos:
>
>  ``[10] -> [20] -> [30] -> NULL``
>
>
> Si temp apunta al primer nodo (10):
>
> * ``temp->data`` vale 10.
>
> * ``temp->next`` apunta al nodo con 20.
>
>  Si mueves ``temp = temp->next``;
>  ahora temp apunta al nodo con 20.



## Código

Código para ofApp.h:

``` cpp
ofApp.h

```

Código para ofApp.cpp:

``` cpp
ofApp.cpp

```

Código para main.cpp:
``` cpp
main.cpp

```

## Demostración:

[Aquí está el video demostrativo de mi aplicación](url del video no listado en youtube)

## 🤔 Fase: Reflect

1. Construir un nodo y enlazarlo a otro.

2. en esta unidad entendi como funcionan las listas enlazadas, como funciona un nodo y como enlazarlo con otro con node->next, aprendi que los destructores no se ejecutan al instante de crear un objeto creado con un constructor, mis conceptos de como crear un constructor y que deben tener estan un poco mas claros, aprendi lo teorico de como funciona y se divide la memoria.

3. quiero profundizar en saber como funcinan el update y el draw, tengo una nocion muy basica, y estos se relacionan entre si, pero cuando estaba haciendo el codigo con ayuda de la IA tuve un dilema, y es que a la ora de programar la opacidad, en el update la opacidad se crea aleatoria pero en lo personal sentia que no servia de nada ya que el draw es el que se enccarga de eso,es el que le dice a la computadora que dibucar y el que controla la opacidad de cada nodo, preguntadole a la IA me dio la razon; que el codigo del update no afectaba mucho pero si me parece un codigo algo mediocre para una IA y un codigo de bajo nivel. me gustaria crear constructores con mas seguridad, y debo mejorar la logica de las funciones, aunque en la mayoria de los casos desconocia algunas cosas, mi logica estaba muy por debajo viendo que las herramientas estaban frente a mi (front y el  rear) no logre construir una buena logica.


