# Breve recordatorio de apuntadores

En un curso introductorio a C, podemos trabajar un poco con apuntadores y sus capacidades.
Vamos a recordar un poco con ayuda de una parte del código de `whoami.cc`.

```c

int
main (int argc, char **argv)
{
...
  set_program_name (argv[0]);

```

Aquí podemos observar que este código podría esperar argumentos desde la línea de comandos.
Para esto hay dos argumentos en la función main que los describen:

`int argc`: Es el número de argumentos pasados desde la línea de comandos, este incluye el
el nombre del programa, por lo que siempre incluye al menos uno.

`char **argv`: Es un arreglo de cadena de caracteres, donde cada elemento apunta a un argumento
y el elemento `argv[0]`, siempre es el nombre del programa. Otra notación que podemos tener
es: `char *argv[]`.


```c

  struct passwd *pw;
...
  errno = 0;
  uid = geteuid ();
  pw = uid == NO_UID && errno ? nullptr : getpwuid (uid);
  if (!pw)
    error (EXIT_FAILURE, errno, _("cannot find name for user ID %lu"),
           (unsigned long int) uid);
  puts (pw->pw_name);
```

También vemos que tenemos un apuntador a cierta estructura, en este caso tenemos la funcion `getpwuid`
que nos regresa información del usuario dependiendo de un `uid`. La estructura que nos regresa
es la siguiente:

```c
/* A record in the user database.  */
struct passwd
{
  char *pw_name;		/* Username.  */
  char *pw_passwd;		/* Hashed passphrase, if shadow database
                                   not in use (see shadow.h).  */
  __uid_t pw_uid;		/* User ID.  */
  __gid_t pw_gid;		/* Group ID.  */
  char *pw_gecos;		/* Real name.  */
  char *pw_dir;			/* Home directory.  */
  char *pw_shell;		/* Shell program.  */
};
```

Pero ahora, es importante observar que la notación con la que estamos accediendo al contenido de
la estructura (después de verificar que no es un apuntador nulo), es con el operador de acceso
indirecto: _"->"_, sin tener que desreferenciar de alguna manera y acceder mediente el operador _"."_,

# Apuntadores a funciones

En nuestro código de investigación nos encontramos con una funcion muy interesante. `atexit`, al parecer
es una función que nos ayuda a hacer algo antes de salir del programa. Al buscar la definición de esta
función podemos ver lo siguiente:

```c
{{#include ../code/coreutils/gnulib/lib/atexit.c}}
```

La función recibe una argumento algo diferente a lo que estamos acostumbrados. En este caso `void (*f) (void)`
se refiere a un apuntador a una función con ciertas caracteristicas, void como retorno y void como parametros.
En resumen una función sin retorno y sin parametros pero también se puede describir otro tipo de funciones con
retornos y parametros diferentes.

Este tipo de funciones son muy utilizadas en el manejo de callbacks cuando la programación es orientada a eventos
o la seleción dinámica de funciones a ejecutar, también en algunas ocaciones hace más flexible el código y
reutilizable.