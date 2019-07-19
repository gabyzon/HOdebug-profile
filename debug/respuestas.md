# Respuestas

## Varios Bugs

### Corriendo el programa con un debugger, sin agregar flags de debug. 
**¿Tienen toda la información que requerían? **
En el ejercicio segfault:
Si compilo el programa sin agregar flag de debug, el programa no compila y nos 
informa que hubo un problema de acceso de memoria.

En el ejercicio de static:
Si compilo el programa sin agregar flag de debug, el programa compila pero 
dan un informe de warning en la función add_array. 
Al correrlos devuelven un resultado que cambia cada vez que lo ejecuto.

En el ejercicio de no bugs:
Si compilo el programa sin agregar flag de debug, el programa compila pero 
dan un informe de warning en la función add_array. 
Al correrlo devuelve un resultado = 6.

En el ejercicio dynamic:
Si compilo el programa sin agregar flag de debug, el programa compila sin errores ni
warnings.
Al correrlo, devuelve un resultado erróneoneo.

**¿Qué pasa si ponen el flag de debug? **
En el ejercicio segfault:
Si lo compilo utilizando un flag de debug (-g), el programa no compila pero nos indica que 
el error de memoria ocurre en la linea 18 y 19.

En el ejercicio de static:
No hay información nueva.
Si compilo el programa utilizando un flag de debug (-g), el programa compila pero 
dan un informe de warning en la función add_array. 
Al correrlos devuelven un resultado que cambia cada vez que lo ejecuto.

En el ejercicio no bugs:
No hay información nueva.
Si compilo el programa utilizando un flag de debug (-g), el programa compila pero 
dan un informe de warning en la función add_array. 
Al correrlos devuelven un resultado = 6.

En el ejercicio dynamic:
Si compilo el programa usando un flag de debug, el programa compila sin errores ni
warnings.
Al correrlo, sigue devolviendo un resltado erróneo.

**¿Qué flag de optimización es el mejor para debuggear? **
En general, para debuggear es mejor realizar lo compilación sin ninguna optimización.
Es decir, el flag que debemos usar es `-O0`
### Agreguen algún flag para que informe todos los warnings en la compilación, como -Wall. 
**¿Alguno les da alguna pista de por qué el programa se rompe? **
En el ejercicio segfault:
Si, los warnings nos indican que la variable no esta definida. Además si hacemos un print de a
vemos que no tiene asignado una dirección de memoria.

En el ejercicio static:
No, el unico warning que devuelve la compilación no indica donde puede estar el error (asumiendo
que existe uno).

En el ejercicio no bugs:
No, el unico warning que devuelve la compilación no indica donde puede estar el error (si
existiera).

En el ejercicio dynamic:
Este programa no genera warnings al compilar y las herramientas del programa no detectan
ningun error debido a que es un error de calculo y no de sintáxis. Para encontrar el error
debemos ir controlando las variable sum (que es nuestra variable de interés) y monitorear 
los cambios que ocurren cuando la función es llamada. Luego, si verificamos que el error en la
función, debemos revisar paso por paso el comportamiento de la función para detectar
en que linea ocurre el error. Una vez identificada la linea con error, revisar lo escrito.


## Floating point exception
**¿Qué función requiere agregar -DTRAPFPE? ¿Cómo pueden hacer que el programa linkee adecuadamente? **


**Para cada uno de los ejecutables, ¿qué hace agregar la opción -DTRAPFPE al compilar? ¿En qué se diferencian los mensajes de salida de los programas con y sin esa opción cuando tratan de hacer una operación matemática prohbida, como dividir por 0 o calcular la raíz cuadrada de un número negativo? **



