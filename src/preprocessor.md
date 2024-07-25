# Preprocesador

## Inclusión de archivos

En general el preprocesador de C nos ayuda a reemplazar algunas cosas por otras

`#include` nos ayuda a insertar el contenido del archivo que especificamos inmediatamente después.
En las siguientes líneas podemos observar que se agrega varios archivos necesarios para el funcionamiento
del código

```c
{{#include ../code/coreutils/src/whoami.c:21:28}}
```

Encontramos algunas diferencias en las líneas anteriores. Los archivos rodeados por *""* son buscados donde
se encuentra el archivo fuente y los encerrados por *<>* los busca en los directorios especificados por el compilador.

## Constantes simbólicas

En C y en muchos otros lenguajes,
una de las malas prácticas es dejar datos directamente en el código que estamos escribiendo (hardcoding). De esta
manera estamos perdiendo la abertura a cambiar o actualizar esos valores. Una de las maneras de evitarlo es creando
variables para esos valores o en este caso una constante simbólicas.

`#define` nos ayudará a definir una *nombre* que después será reemplazado por algun valor. En la siguiente línea
vemos que se define un nombre que en todos los lugares que se encuentre cambiará por el valor *"whoami"*

```c
{{#include ../code/coreutils/src/whoami.c:31}}
```

## Macros

Otra manera de reemplazar cierto texto es con la ayuda de macros. Como vemos en la siguiente línea `AUTHORS` será
reemplazado por el valor definido, el cual, a primera instancía se observa que es una función.

```c
{{#include ../code/coreutils/src/whoami.c:33}}
```

Pero al buscar la declaración de `proper_name` en el archivo `src/system.h` observamos que no es una función.
Las macros nos ayudan a sustituir cierto valor pero ahora con ayuda de argumentos. La siguiente macro (`proper_name`)
toma el argumento `x` y lo sustituye en el siguiente texto donde encuentra una `x`.

```c
{{#include ../code/coreutils/src/system.h:369}}
```

Ahora, si buscamos la definición de proper_name_lite encontraremos que es en efecto una función.

```c
{{#include ../code/coreutils/gnulib/lib/propername-lite.c:30:36}}
```

## Guardas

Una línea que nos llama la atención es `#include "long-options.h"`, ya que se incluye el archivo y este puede tener
varias referencias para ser usadas en `whoami.c`.

```c
{{#include ../code/coreutils/gnulib/lib/long-options.h:20:51}}
```

Lo primero que tenemos, además de los comentarios, es un bloque especial:

```c
#ifndef LONG_OPTIONS_H_
# define LONG_OPTIONS_H_ 1
...
#endif /* LONG_OPTIONS_H_ */
```

Este bloque se denomina _guarda_ y es muy utilizado para ser usado en los archivos de cabecera. La guarda realiza una
protección para no declarar varias veces las funciones (variables, estructuras, etc) que hay dentro. Con una simple
condición, si no esta declarada una variable (llamada igual que el archivo), declara la misma variable y además todo el
contenido. De esta manera si se incluye varias veces, se puede protejer declarando una sola vez el contenido.


## Condicionales

Ahora, como pueden ver en el contenido de `long-options.h`, el preprocesador cuenta con condicionales que pueden afectar
qué se incluye y que no, en la compilación (como ya lo vimos en las guardas). `#if`, `#ifdef`, `#ifndef`, `#else`,
`#elif`, `#endif`, pueden ser usados para habilitar o deshabilitar una línea o líneas que pueden cambiar el 
comportamiento del código, y esto no solo en las cabeceras, en los archivos fuente también son usados comunmente.