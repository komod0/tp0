# Informe TP0

**Alumno:** Julián Crespo

## Paso 0:

##### a)

![](/home/julianc/Facultad/Taller%201/tp0/img/holamundo.png)

---

##### b)

Valgrind es una herramienta que sirve para debuggear y perfilar ejecutables, mas que nada se usa para analizar el uso de memoria de una aplicación y para detectar errores relacionados con el uso de memoria(leaks, uso de memoria sin inicializar o ya liberada, etc).

Las opciones mas comunes(al menos desde mi experiencia) son:

- `--tool=` :
  
  Especifica cual de las herramientas de valgrind se desea utilizar de las disponibles(memcheck, cachegrind, callgrind, etc), la mas usada generalmente es  memcheck que analiza problemas relacionados con la memoria.

- `--leak-check=` :
  
  Determina si se deben analizar perdidas de memoria, muestra cuanta memoria no se libero y en donde se pidió la memoria en cuestión.

- `--show-reachable=` :
  
  Determina si se debe mostrar o no los bloques de memoria que son _alcanzables_ es decir aquellos bloques de memoria que podrían haber sido liberados pero no lo fueron.

- `--track-origins=` :
  
  Si esta activada muestra de donde provienen o donde fueron creados los valores sin inicializar usados en el programa.

- `--num-callers=` :
  
  Especifica el numero de llamadas a mostrar cuando se esta analizando el origen de un cierto valor, ya sea porque se esta usando un valor sin inicializar o porque no se libero o por otro motivo, puede afectar cuando tenemos llamados a funciones muy anidados y la opción tiene un valor bajo.

---

##### c)

`sizeof()` determina el tamaño en bytes de una variable.

En el caso de `sizeof(char)` la salida va a ser igual a 1 independientemente del compilador, en el caso de `sizeof(int)` depende de la arquitectura de la computadora y de el compilador, incluso de la versión del compilador, por lo general tiene un tamaño de 2 o 4 bytes.

---

##### d)

El tamaño de un struct no necesariamente es igual a la suma de sus miembros, esto es debido al padding que agrega el compilador a cierto tipos de variables, esto es ya que es mas rápido acceder a posiciones de memoria múltiplos de cuatro, entonces en ciertos casos el compilador agrega padding para _alinear variables_.

Un ejemplo para probar que no siempre es valido esto es el siguiente:

```c
struct coso {
    int entero;
    char caract;
    float flota;
};
```

En este caso el tamaño del struct no necesariamente va a ser igual a la suma de los miembros, es probable que el compilador agregue padding a la variable `caract` para completar los 4 bytes. Corriendo una prueba localmente se obtiene que `sizeof()` del struct en cuestión devuelve 12 por lo que se observa que en este caso no se cumple.

---

##### e)

STDIN, STDOUT Y STDERR son archivos que se usan para manejar y redireccionar el flujo de entrada-salida de un programa, cada uno sirve para un proposito diferente.

STDIN representa la entrada del programa, es decir de donde el archivo lee para obtener los datos que necesita, en el ejemplo del contador de palabras se usaria el STDIN para ingresar el texto al que se le desea contar las palabras. Para usar un cierto archivo como entrada de un programa se usa el simbolo "<" o "0<" de la siguiente forma:

`programa < mientrada`

o lo que es equivalente:

`programa 0< mientrada`

STDOUT es a donde va cualquier salida de un programa que no sea un mensaje de error, para redireccionar la salida se usa el símbolo > o 1>, en el ejemplo del contador de palabras si quisiéramos guardar la cantidad de palabras de un texto en un archivo llamado "salida" se haría de la siguiente forma:

`contador < archivo > salida`

o equivalentemente:

`contaor 0< archivo 1> salida`

STDERR se usa para redireccionar los mensajes de error que ocurren durante la ejecución del programa, para ello se usa el símbolo 2> de la siguiente forma:

`programa 2> log_errores`

El símbolo | (pipe) se usa para encadenar la salida de un proceso con la entrada de otro, se usa de la manera:

`a | b`

El comando se ejecuta y se interpreta de izquierda a derecha, se ejecuta `a` y su salida sera usada como entrada de `b`

---

## Paso 1:


