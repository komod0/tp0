# Informe TP0

**Alumno:** Julián Crespo

## <u>Paso 0</u>

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

## <u>Paso 1</u>

##### a)

![](/home/julianc/Imágenes/Screenshot_20200418_215102.png)

###### Archivo paso1_wordscounter.h:

- ***Lines should be <= 80 characters long  [whitespace/line_length]***: El error significa que hay una linea en el archivo que supera los 80 caracteres de largo.
  
  

###### Archivo paso1_wordscounter.c:

- ***Missing space before ( in while(  [whitespace/parens]***: No se agrego un espacio entre la condición del while y el keyword "while" es decir en vez de poner `while (condicion)` se uso `while(condicion)`

- ***Mismatching spaces inside () in if  [whitespace/parens]***: Se usaron una cantidad de espacios diferente entre el primer paréntesis del if y la condición y entre la condición y la condición y el paréntesis de cierre, es decir `if ( condicion)` en vez de `if (condicion)` o `if ( condicion )`

- ***Should have zero or one spaces inside ( and ) in if  [whitespace/parens]***: Se usaron dos espacios entre los paréntesis y la condición cuando se debería usar uno o cero.

- ***An else should appear on the same line as the preceding }  [whitespace/newline]***: El else debería aparecer en la misma linea que la llave de cerrado de la condición del if correspondiente.

- ***Missing space before ( in if(  [whitespace/parens]***: Lo mismo que el segundo error pero para un if.

- ***Extra space before last semicolon. If this should be an empty statement, use {} instead.  [whitespace/semicolon]***: Significa que hay un espacio entre la sentencia y el punto y coma que le corresponde, es decir `return algo ;` cuando debería ser `return algo;`
  
  

###### Archivo paso1_main_.c:

- ***Almost always, snprintf is better than strcpy  [runtime/printf]***: Se refiere a que el uso de snprintf es mejor o mas seguro en la mayoría de los casos ya que strcpy por ejemplo no tiene forma de saber el tamaño del buffer y esto puede causar problemas de corrupción de memoria por pasarse del tamaño máximo del buffer.

- ***An else should appear on the same line as the preceding }***: Ya explicado

- ***If an else has a brace on one side, it should have it on both  [readability/braces]***: Quiere decir que un else debería tener una cierta simetría con respecto a las llaves, es decir que si se tiene la llave de cierre del if correspondiente en la misma linea que el else, entonces la llave de apertura del else debería también estar en la misma linea que el else, análogamente si la llave de cierre del if correspondiente no esta en la misma linea que el else, entonces la llave de apertura del else tampoco debería estar en esa linea, el problema con esto ultimo es que entraría en conflicto con el error anterior de que el else este en la misma linea que el "}" predecesor.



---

##### b)

![](/home/julianc/Imágenes/Screenshot_20200418_233532.png)

Todos los errores que se observan son de funciones sin declarar, es decir que el compilador no pudo encontrar la declaración de las funciones que indica, todos los errores son debido a que no se incluyo el archivo `paso1_wordscounter.h` que es el que contiene las declaraciones de las funciones que se indican.

Son todos errores de compilación ya que el proceso de linking es posterior a la compilación y en este caso no se esta llegando a compilar el archivo `paso1_main.c`.



---

##### c)

No se reporto ningún warning, esto es debido a que a que se utiliza el flag `-Werror` que hace que el compilador trate los warnings como si fuesen errores.



---

## <u>Paso 2</u>






