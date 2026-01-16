# Unidad 1

## 🛠 Fase: Apply

### Actividad 03

- Escribe un programa que compare el valor almacenado en la dirección de memoria 5 con el valor 10. Si el valor es menor que 10, guarda el valor 1 en la dirección 7. Si el valor es mayor o igual a 10, guarda el valor 0 en la dirección 7.

``` asm

(INICIO)
@12 //cualquier valor que va a estar en la memoria RAM 5
D=A
@5
M=D // guarda el numero 10 en la RAM5

@10 //cualquier valor que va a estar en la memoria RAM 4
D=A
@4
M=D // guarda el numero 10 en la RAM4

(CALCULAR)
@5
M=M-1
M=D
@(SUMA UNO)
D;JEQ   
@4
M=M-1
M=D
@(RESTA UNO)
D;JEQ
@(CALCULAR)
D;JGT  


(RESTA UNO)
D;ALGUN JUPM
@7
M=-1
@(INICIO)
D;JLE

(SUMA UNO)
@7
M=1
@(INICIO)
0;JMP

```

### Actividad 04

“Crea un programa que use un ciclo para sumar los números del 1 al 5 y guarde el resultado en la dirección de memoria 12.”

``` asm
(INICIO)
@0 // Valor inicial
D=A
@12
M=D // guarda el numero 0 en la RAM12

(CALCULAR)
@12
M=D
D=D+1
D=M   // guarda la suma quw se acabo de realizar
@5
A=D
@12
A=M
D=D-A
@(CALCULAR)
D;JGT 
```

### Actividad 05

### Dibujando un punto en la pantalla

Vamos a resolver juntos este problema:

“La pantalla del computador Hack se controla a través de un mapa de memoria que comienza en la dirección 16384 (SCREEN). Cada bit en este mapa de memoria representa un pixel en la pantalla (1 = negro, 0 = blanco). Escribe un programa que dibuje un punto negro en la esquina superior izquierda de la pantalla. (Recuerda que la esquina superior izquierda corresponde al primer bit del primer word en la dirección SCREEN).”

``` asm
@16384M
M=A
M=-1
```
### Actividad 06
### Dibujando una línea horizontal
Vamos a resolver juntos este problema:

“Modifica el programa anterior para que dibuje una línea horizontal negra de 16 pixeles de largo en la esquina superior izquierda de la pantalla. (Recuerda que cada word en la memoria representa 16 pixeles).”

``` asm
(Variable)
@16384
D=A
@16
M=D
(DRAW)
@16
A=M
M=-1
@16
M=M+1
@16400
D=A
@12
A=M
D=D-A
@(DRAW)
D;JGT
```
**Reflexion:** para realizar este trazo se necesito crear una variable y un bucle contador que determinara cuando esta variable pintara sus 16 pixeles

### Actividad 07
### Entrada salida interactiva

Modifica el programa de la actividad anterior de tal manera que puedas mover la línea horizontal de derecha a izquierda usando las teclas d y i respectivamente. Tu programa no tiene que verificar si la línea se sale de la pantalla.


``` asm
(Variable1)
@16384
D=A
@16
M=D
(ALTO)
@0
D=A
@15
M=D
@KBD
M=D
@100
D=D-A
@(DRAWBLACK)
D;JEQ
@KBD
M=D
@105
@(DRAWWHITE)
D;JEQ
(DRAWBLACK)
@16
A=M
M=-1
@16
D=M
D=D+A
M=D
@16
D=A
@15
A=M
D=D-A
@(ALTO)
(DRAWWHITE)
@16
A=M
M=M+1
@16
D=M
D=D+A
M=D
@16
D=A
@15
A=M
D=D-A
@(ALTO)
D;JEQ
```

