# Respuestas

## Corriendo el programa con un debugger, sin agregar flags de debug. 
** ¿Tienen toda la información que requerían? **
En el ejercicio segfault:
Si compilo el programa sin agregar flag de debug, el programa no compila y nos 
informa que hubo un problema de acceso de memoria.

En el ejercicio de static y no bugs:
Si compilo los programas sin agregar flag de debug, los programas compilan pero 
dan un informe de warning en la función add_array. 
Al correrlos devuelven un resultado.

En el ejercicio dynamic:
Si compilo el programa sin agregar flag de debug, el programa compila sin errores ni
warnings.
Al correrlo, devuelve un resultado erróneoneo.

** ¿Qué pasa si ponen el flag de debug? **
En el ejercicio segfault:
Si lo compilo utilizando un flag de debug (-g), el programa no compila pero nos indica que 
el error de memoria ocurre en la linea 18 y 19.

En el ejercicio de static y no bugs:
Si compilo los programas utilizando un flag de debug (-g), el programa compilan pero 
dan un informe de warning en la función add_array. 
Al correrlos devuelven un resultado.

En el ejercicio dynamic:
Si compilo el programa usando un flag de debug, el programa compila sin errores ni
warnings.
Al correrlo, sigue devolviendo un resltado erróneo.

** ¿Qué flag de optimización es el mejor para debuggear? **
En el ejercicio segfault:
Con o sin flag de optimización, el programa no compila.

## Agreguen algún flag para que informe todos los warnings en la compilación, como -Wall. 
** ¿Alguno les da alguna pista de por qué el programa se rompe? **
En el ejercicio segfault:
Si, los warnings nos indican que la variable no esta definida. Además si hacemos un print de a
vemos que no tiene asignado una dirección de memoria.

En el ejercicio dynamic:
Este programa no genera warnings al compilar y las herramientas del programa no detectan
ningun error debido a que es un error de calculo y no de sintáxis. Para encontrar el error
debemos ir controlando las variable sum (que es nuestra variable de interés) y monitorear 
los cambios que ocurren cuando la función es llamada. Luego, si verificamos que el error en la
función, debemos revisar paso por paso el comportamiento de la función para detectar
en que linea ocurre el error. Una vez identificada la linea con error, revisar lo escrito.

En el ejercicio static:
Ocurre lo mismo que en el dynamic.



