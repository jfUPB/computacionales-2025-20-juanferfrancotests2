# Unidad 2


## 🛠 Fase: Apply

Implementa el programa anterior en lenguaje ensamblador aplicando el concepto de punteros.

```cpp

int arr[] = {1,2,3,4,5,6,7,8,9,10};
int sum = 0;

for (int j = 0; j < 10; j++) {
    sum = sum + arr[j];
}

```

```asm

// Inicializamos i en 16
@16
D=A
@i
M=D          // i = 16

// Inicializamos n = 0
@0
D=A
@n
M=D

(MATRIZ)
// Cargamos n
@n
D=M

// Comparamos si n == 10
@10
D=D-A
@FIN DE LA MATRIZ
D;JEQ        // Si n == 10, saltamos al final

// Calculamos i + n para saber dónde guardar el número
@n
D=M
@i
A=M
A=A+D       // A = i + n

// Guardamos n + 1 en esa posición (para tener 1...10)
@n
D=M
D=D+1
M=D         // RAM[i + n] = n + 1

// Incrementamos n
@n
M=M+1

@MATRIZ
0;JMP       // Volvemos a empezar

(FIN DE LA MATRIZ)

; creamos el ciclo for: en el ciclo se debe intanciar
@j
M=0

(FOR)
; ahora j debe coger el dato de la posicion indicada La matriz i
@j
D=M
@i
D=D+A
@R13    ; Vamos a usar R13 como temporal
M=D     ; Guardamos D en R13
@10     ; que el puntero de j se reste con 10
D=A
@R13
A=M    ; estamos en la posicion M(j) + i para coger el dato que existe en la posicion actual
A=M
D=D-A  ; que el puntero de j se reste con 10

        ;comparamos si D = 0, si no que vuelva a @FOR
@FIN
D;JEQ
@j
M=M+1
@FOR
D;JMP

(FIN)
```




