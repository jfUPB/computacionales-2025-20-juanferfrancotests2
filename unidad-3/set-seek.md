# Unidad 3

## 🔎 Fase: Set + Seek

## Actividad 01


* ¿Para qué sirven los breakpoints?

Sirven para correr los el progrma o el codigo en un punto en especifico y poder hacer un rastreo paso a paso para saber como se esta ejecutando el codigo

* ¿Para qué se usa la ventana de depuración Autos?

  La ventana de depuracion sirve para que el programa corra correctamnte, es una ventana en donde el programa escanea la receta de lo que se va a realizar.

## Actividad 02


## Actividad 03


```cpp

#include <iostream>
#include <cstdlib>

using namespace std;

// Variables globales
int global_inicializada = 42;
int global_no_inicializada;

// Constante global
const char* const mensaje_ro = "Hola, memoria de solo lectura";

// Función de ejemplo que muestra la dirección de su variable local estática
void funcionConStatic() { // Segmento de código (instrucciones, funciones)
    static int var_estatica = 100;  // Variables globales y estáticas
    cout << "Dirección de var_estatica (static): " << &var_estatica << endl;
} 

// Función que asigna memoria dinámica (heap)
int* crearArrayHeap(int tam) {
    int* arr = new int[tam];
    for (int i = 0; i < tam; i++) {
        arr[i] = i;
    }
    return arr;
}

// Una función simple para representar el código (se encontrará en la región de código)
int suma(int a, int b) {
    int c = a + b; // "c" es una variable local (stack)
    return c;
}

int main() {
    // Variable local (stack)
    int a = 10;  // Variable local (stack)
    int b = 20;  // Variable local (stack)
    int c = suma(a, b);  // Variable local (stack)

    cout << "Resultado de suma(a, b): " << c << endl;
    cout << "Dirección de variable local 'a': " << &a << endl;
    cout << "Dirección de variable local 'b': " << &b << endl;
    cout << "Dirección de la variable local 'c' (resultado): " << &c << endl;

    // Variables globales
    cout << "Dirección de 'global_inicializada': " << &global_inicializada << endl;
    cout << "Dirección de 'global_no_inicializada': " << &global_no_inicializada << endl;

    // Constante global (solo lectura)
    cout << "Dirección de 'mensaje_ro' (zona de solo lectura): " << static_cast<const void*>(mensaje_ro) << endl;

    // Llamada a función que tiene variable estática
    funcionConStatic();

    // Uso del Heap: asignación dinámica
    int tamArray = 10;
    int* arrayHeap = crearArrayHeap(tamArray);
    cout << "Dirección del primer elemento del array asignado en Heap: " << arrayHeap << endl;
    for (int i = 0; i < tamArray; i++) {
        cout << "arrayHeap[" << i << "] = " << arrayHeap[i]
            << " en " << (arrayHeap + i) << endl;
    }
    delete[] arrayHeap; // Liberamos la memoria dinámica

    return 0;
}

```

## Actividad 04

### Experimento 1: modificar el segmento de texto:

<img width="778" height="313" alt="image" src="https://github.com/user-attachments/assets/00147607-d7f3-4f04-85bd-62a15a0a36f4" />

- ¿Qué ocurre?

se bloquea el programa
  
- ¿Por qué?

porque se intenta modificar la funcion main, lo cual el sistema operativo lo detecta y lo bloquea

### Experimento 2: modificar el segmento de datos (constante global):

<img width="761" height="275" alt="image" src="https://github.com/user-attachments/assets/dcddb2da-aa7a-40d4-a68c-30760c6685a5" />

¿Qué ocurre? 

se bloquea el programa

¿Por qué?

porque se intenta modificar un segmento de datos, ya que estoy tratando de sobrescribir los bytes que representan la dirección del puntero, lo cual es aún más peligroso y también es comportamiento indefinido.7


### Experimento 3: modificar el segmento de datos (variables globales):
<img width="799" height="352" alt="image" src="https://github.com/user-attachments/assets/ecfa65d6-ccce-4559-b9b4-d50a689948d0" />

¿Qué ocurre? 

el valor no inicializado toma un valor y luego modifica

¿Por qué?

porque la consola le da automaticamente un valor 0 al valor no inicializado.

### Experimento 4: modificar la variable local estática de una función por fuera de ella:

¿Qué ocurre?

nada, el codigo me aparece que esta incorrecto 

¿Por qué?

la variable var_estatica = 42 no esta bien definidad

¿Qué pasa con las variables cada que entras y sales de la función?

las variables estaticas funcionan como globales dentro de la funcion, entonces cuando entran o salen la varible estatica permanece dentro dela funcion y sus modificaciones se mantinene

En relación a la pregunta anterior ¿Qué pasa con las variables locales estáticas?

Se guardan en la parte de la memoria de las variables estaticas y no en las globales.



## Experimento 5: variables locales estática vs no estática:

<img width="449" height="428" alt="image" src="https://github.com/user-attachments/assets/6f864c44-a365-49ad-95a9-94ab7834032b" />

* ¿Qué ocurre? ¿Por qué?

la variable entera se repitio 5 veces, mientras que la variable estatica se imprimia de 100 hasta 104, esto sucede porque la varible entera cuando sale de la funcion se destruye, encambio la statica se guarda en una parte de la memoria como una global pero solo se puede interactuar con ella por dentro de la funcion.

Ves alguna diferencia entre las variables locales estáticas y no estáticas?

Si, que se inicialisan con la palabra `static int` y la entera solo `int`.

* ¿Qué pasa con las variables cada que entras y sales de la función?

## Experimento 6: modificar el segmento de heap:

<img width="613" height="148" alt="image" src="https://github.com/user-attachments/assets/221f7b5f-7467-47ad-befd-f7cf29bd780a" />

¿Qué ocurre? ¿Por qué?

se crea una tabla con 5 elementos

Comenta la línea de genera el error y analiza las siguientes preguntas:

¿Qué diferencias notas entre el comportamiento y la gestión del Heap en comparación con el Stack?

Stack:

* Se gestiona automáticamente: las variables locales se crean al entrar en un bloque y se destruyen al salir.

* Muy rápido, porque el sistema solo “mueve” el puntero de la pila.

* Espacio limitado (si reservas demasiado → stack overflow).

* Tiempo de vida corto y ligado al alcance (scope).

Heap:

* Se gestiona manualmente: el programador debe pedir memoria con new y liberarla con delete.

* Más flexible: puedes reservar memoria en tiempo de ejecución con el tamaño que quieras.

* Más lento de asignar y liberar (hay que buscar bloques libres en la memoria).

* Tiempo de vida largo: persiste hasta que se llame a delete o termine el programa.

¿Qué consecuencias tendría no liberar la memoria reservada con new?

Aparece una fuga de memoria (memory leak):

la memoria sigue ocupada aunque ya no tengas acceso a ella.

En programas pequeños quizás no notes nada, pero en aplicaciones grandes o servidores de larga ejecución, las fugas acumuladas pueden:

* Agotar la memoria disponible.

* Degradar el rendimiento.

* Provocar que el sistema operativo mate tu programa.

¿Por qué es importante usar delete[] al liberar memoria asignada para un arreglo?

delete[] es obligatorio para arreglos porque garantiza que toda la memoria y todos los elementos sean correctamente liberados.


## Actividad 05

<img width="654" height="197" alt="image" src="https://github.com/user-attachments/assets/86521d6e-2ffa-4582-9f45-50fcc9635736" />


Explica qué ocurre al copiar un objeto en C++ y en C#.

¿Qué diferencias encuentras?

que en C++ se usa paso por valor y en C# paso por referencia.

¿Qué es copia en C++ y en C#?

En C++ es una copia independiente a la original mientras que en C# el puntero y la original apuntan a la misma posicion de memoria

¿Es una copia independiente de original?

En C# no para hacerlo ay que agregar el metodo ICloneable.Clone()
