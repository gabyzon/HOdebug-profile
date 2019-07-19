# Respuestas

## Varios Bugs

### Corriendo el programa con un debugger, sin agregar flags de debug. 
**¿Tienen toda la información que requerían?**
*En el ejercicio segfault:*
Si compilo el programa sin agregar flag de debug, el programa no compila y nos 
informa que hubo un problema de acceso de memoria.

*En el ejercicio de static:*
Si compilo el programa sin agregar flag de debug, el programa compila pero 
dan un informe de warning en la función add_array. 
Al correrlos devuelven un resultado que cambia cada vez que lo ejecuto.

*En el ejercicio de no bugs:*
Si compilo el programa sin agregar flag de debug, el programa compila pero 
dan un informe de warning en la función add_array. 
Al correrlo devuelve un resultado = 6.

*En el ejercicio dynamic:*
Si compilo el programa sin agregar flag de debug, el programa compila sin errores ni
warnings.
Al correrlo, devuelve un resultado erróneoneo.

**¿Qué pasa si ponen el flag de debug?**
*En el ejercicio segfault:*
Si lo compilo utilizando un flag de debug (-g), el programa no compila pero nos indica que 
el error de memoria ocurre en la linea 18 y 19.

*En el ejercicio de static:*
No hay información nueva.
Si compilo el programa utilizando un flag de debug (-g), el programa compila pero 
dan un informe de warning en la función add_array. 
Al correrlos devuelven un resultado que cambia cada vez que lo ejecuto.

*En el ejercicio no bugs:*
No hay información nueva.
Si compilo el programa utilizando un flag de debug (-g), el programa compila pero 
dan un informe de warning en la función add_array. 
Al correrlos devuelven un resultado = 6.

*En el ejercicio dynamic:*
Si compilo el programa usando un flag de debug, el programa compila sin errores ni
warnings.
Al correrlo, sigue devolviendo un resltado erróneo.

**¿Qué flag de optimización es el mejor para debuggear?**
*En general*, para debuggear es mejor realizar lo compilación sin ninguna optimización.
Es decir, el flag que debemos usar es `-O0`

### Agreguen algún flag para que informe todos los warnings en la compilación, como -Wall. 
**¿Alguno les da alguna pista de por qué el programa se rompe?**
*En el ejercicio segfault:*
Si, los warnings nos indican que la variable no esta definida. Además si hacemos un print de a
vemos que no tiene asignado una dirección de memoria.

*En el ejercicio static:*
No, el unico warning que devuelve la compilación no indica donde puede estar el error (asumiendo
que existe uno).

*En el ejercicio no bugs:*
No, el unico warning que devuelve la compilación no indica donde puede estar el error (si
existiera).

*En el ejercicio dynamic:*
Este programa no genera warnings al compilar y las herramientas del programa no detectan
ningun error debido a que es un error de calculo y no de sintáxis. Para encontrar el error
debemos ir controlando las variable sum (que es nuestra variable de interés) y monitorear 
los cambios que ocurren cuando la función es llamada. Luego, si verificamos que el error en la
función, debemos revisar paso por paso el comportamiento de la función para detectar
en que linea ocurre el error. Una vez identificada la linea con error, revisar lo escrito.


## Floating point exception
**¿Qué función requiere agregar -DTRAPFPE? ¿Cómo pueden hacer que el programa linkee adecuadamente?**


**Para cada uno de los ejecutables, ¿qué hace agregar la opción -DTRAPFPE al compilar?**
El flag `-D` en la compilación seguida de TRAPFPE incluira en la compilación del programa el 
siguiente código
```
#ifdef TRAPFPE
set_fpe_x87_sse();
#endif 
```
Esto sirve para seleccionar si la función set_fpe_x87_sse se utilizará o no en el programa al momento de compilar.
Podemos decir que se habilita una porción de código.

**¿En qué se diferencian los mensajes de salida de los programas con y sin esa opción cuando tratan de hacer una operación matemática prohbida, como dividir por 0 o calcular la raíz cuadrada de un número negativo?**
*La salida de los programas cuando sin la opción:*
Cuando los programas se compilan sin esta opción y se introduce una entrada prohibida,
los programas devuelven resultados como *inf* o *nan* según corresponda.

*La salida de los programas cuando con la opción:*
Cuando los programas se compilan con esta opción y se introduce una entrada prohibida,
los programas devuelven un mensaje de error *Floating point exception*.


## Segmentation Fault
**Identifiquen los errores que devuelven al ejecutar por primera vez**
El error que ocurre al ejecutar `./big.e` es:
*Segmentation fault (core dumped)*
Al ejecutar `./small.e` no devuelve ningún error.

### Ejecutando ulimit -s unlimited y volviendo a correr el programa**
**¿Devuelven el mismo error que antes?**
No, pero big.e queda ejecutandose inlimitadamente.

**Averigüen qué hicieron al ejecutar la sentencia ulimit -s unlimited.**
*Algunas pistas son: abran otra terminal distinta y fíjense si vuelve al mismo error, fíjense*
*la diferencia entre ulimit -a antes y después de ejecutar ulimit -s unlimited, googleen, etcétera*
Al abrir una nueva terminal y ejecutar nuevamente big.e, el programa devuelve nuevamente el error
inicial. Claramenre el comando `ulimit -s unlimited` no modifica el archivo .e
Lo que hacemos es darle stack ilimitado al programa. Esto puede verse ejecutando ulimit -a
antes y despues del comando.
Primero veremos esto:
`stack size              (kbytes, -s) 8192`
y despues veremos esto:
`stack size              (kbytes, -s) unlimited`

**La "solución" anterior, ¿es una solución en el sentido de debugging?**
No, porque no resuelve los problemas del programa internamente.

**¿Cómo harían una solución más robusta que la anterior, que no requiera tocar los ulimits?**


## Valgrind
El tipo de problemas que detecta incluye principalmente: (1) uso de memoria sin inicializar, 
(2) lectura/escritura de memoría después de que se libere, (3) lectura/escritura en secciones 
ilegales, y (4) potenciales fugas de memoria. 

**Describan el error y por qué sucede**
Los errores que devuelve cuando ejecutamos `source1.e` con valgrind son dos. Uno es un error
de fuga que genera la perdida de 12.000.000 bytes en 3 bloques y el otro es una posible fuga de 
4.000.000 bytes en 1 bloque.

Los errores que devuelve cuando ejecutamos `test_oob4.e` con valgrind son dos. Uno es un error
de fuga que genera la perdida de 200 millones de bytes en 5 bloques y el otro es una posible fuga de 
12.000.000 bytes en 3 bloques.


## Funny
En la carpeta funny/ hay un código de C. Describan las diferencias de los ejecutables al compilar 
con y sin el flag -DDEBUG. 

**¿De dónde vienen esas diferencias?**
Cuando compilo sin el flag, no se habilitan las partes del codigo que trabajan con otra memoria alocada.
Al habilitar el flag `-DDEBUG` incluyo en la compilación la creación de un string alocado de 1024 valores
que contiene los caracteres *I'm HERE !!!!* 

















