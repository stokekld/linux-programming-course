# Primero conceptos

Algunos conceptos útiles despues de un curso básico podrían ser los que veremos en este tema.
Tomaremos de ejemplo el código fuente de un comando de linux que nos ayuda a saber el usuario
con el que estamos logeados.

`whoami` es el comando que analizaremos primero, para esto abriremos el código fuente en nuestro
editor de código preferido.

```bash
vim src/whoami.c
```

El código es el siguiente, donde se muestra a primera instancia una pequeña documentación del código
donde se observa una breve descripción de lo que hace y la licencía de este. Después de este procede
el código que analizaremos.

```c
{{#include ../code/coreutils/src/whoami.c}}
```