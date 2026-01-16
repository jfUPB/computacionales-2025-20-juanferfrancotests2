# Unidad 1

## 🔎 Fase: Set + Seek

### Actividad 01

Deduciendo el codigo de la actividad 1 puedo hallar los siguientes apuntes;

-  @(numero) :es A no explicita un numero en un espacio de la rom
- D=A: A aquiere y asigna el valor a D el numero del la rom anterior
- D=D+A :una suma de sus valores actuales
- M=D : se usa para guardar la informacion de D en una parte de la ram
- 0,JMP : si el valor de A es igual a 0 salta a la pocision #0 de la ROM pero el valor que posea D se mantiene
- @i : Accede a la dirección de la variable i
- D=M: Copia el valor contenido en la dirección de memoria apuntada actualmente por A en D.
- @SCREEN:
- @READKEYBOARD : Dirección de salto si el teclado está presionado
- @KBD = @24576
- M=M+1 :En la direccion actualmente apuntada por A suma 1
- A=M : Carga en el registro A el valor que hay en la dirección de memoria actualmente apuntada por A

#### Extraido de Chat GPT

| Código de salto | Significado en español          | Condición para que salte (si D...)          |
|------------------|---------------------------------|---------------------------------------------|
| JGT              | Saltar si es mayor              | D > 0                                       |
| JEQ              | Saltar si es igual              | D == 0                                      |
| JGE              | Saltar si es mayor o igual      | D >= 0                                      |
| JLT              | Saltar si es menor              | D < 0                                       |
| JNE              | Saltar si es diferente          | D ≠ 0                                       |
| JLE              | Saltar si es menor o igual      | D <= 0                                      |
| JMP              | Saltar incondicionalmente       | Siempre salta                               |

#### Experimento 1

*  ¿Qué sucede? se observa como los valores (PC,A y D) van cambiando a lo largo de la interaccion 
* ¿Qué valor se almacena en la dirección de memoria 16? Se guardo el valor de D 
* ¿Por qué crees que es ese valor? creo que es porque en el anterior paso se le indico el numero 16 a A y M lo tomo como una orden de posicion 
* ¿Qué instrucciones se ejecutan en cada ciclo Fetch-Decode-Execute? se asigna un numero en D -> se suman numeros -> se obtiene un resultado-> se asina el resultado a un apocision de memoria
* ¿Qué cambios observas en el contenido de la memoria y los registros? que la RAM # 16 tiene un valor de 5

#### Experimento 1
 Escribe un programa en lenguaje ensablador que sume los números 5 y 10, y almacene el resultado en la dirección de memoria 20. Utiliza el simulador de la CPU Hack para ejecutar tu programa y verifica que el resultado es correcto.

#### Programa
@5

D=A

@10

D=D+A

@20

M=D

### Actividad 02

Reporta en tu bitácora de aprendizaje:

Identifica una instrucción que use la ALU y explica qué hace. Se vuleve negra de arriba hacia abajo y se vuelve blanca de abajo hacia arriba

¿Para qué sirve el registro PC? Para guardar informacion en la RAM... creo

¿Cuál es la diferencia entre @i y @READKEYBOARD? @i se una como un punto de almacenamiento de la informacion, @READKEYBOARD toma el dato leido cuando una persona oprime una tecla tambien, se usa para designar saltos en el programa, algunos de estos saltos dirigen al PC a funciones.

Describe qué se necesita para leer el teclado y mostrar información en la pantalla. se necesita instanciar @KBD en la memoria RAM, luego A=D y M=D, 

- Identifica un bucle en el programa y explica su funcionamiento.

``` asm
@SCREEN
D=A
@i
M=D
(READKEYBOARD)
@KBD
D=M
@KEYPRESSED
D;JNE
@i
D=M
@SCREEN
D=D-A
@READKEYBOARD
D;JLE
```

El programa delimita la pantalla colocando en la RAM[16] la posición del primer píxel (@SCREEN). Luego, D = @SCREEN, y después accedemos a la dirección @KBD, haciendo que D lea la información del teclado (@KBD), la cual varía según la tecla que estemos oprimiendo.

Si D es diferente de 0, se realiza un salto. Pero en este caso no se oprimirá ninguna tecla, por lo tanto el programa sigue corriendo y hace que D lea la información de la posición @i en la RAM.

Si D = D - A da como resultado 0, se realiza un salto hacia la posición 4 del contador de programa (PC).

- Identifica una condición en el programa y explica su funcionamiento.

``` asm
(KEYPRESSED)
@i
D=M
@KBD
D=D-A
@READKEYBOARD
D;JGE
@16
A=M
M=-1
@i
M=M+1
@READKEYBOARD
0;JMP
```

En esta parte del programa, se detecta que la persona está oprimiendo una tecla. Esto activa un contador progresivo que recorre la memoria desde @SCREEN hasta @KBD, escribiendo el valor -1 en cada dirección de memoria correspondiente a un píxel.

El valor -1 en la memoria hace que esos píxeles se coloreen en negro (pantalla encendida).

Cuando se deja de oprimir la tecla, el programa comienza a restaurar los píxeles, escribiendo 0 en esas posiciones, lo que equivale a apagar los píxeles (pantalla en blanco).

