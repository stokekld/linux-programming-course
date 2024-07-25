# Que sigue después de un curso básico

Esta es la continuación del curso básico de C de todos los tiempos.
La idea es poder adentrarnos a códigos más estructurados y complejos que
los dados por los instructores en este tipo de seguimientos. Como saben las
personas que ya llevan más tiempo dedicándose al desarrollo, la manera de
aprender códigos más complejos es leyendo código legado o entrando a projectos más grandes.
Los proyectos FOSS (Free and Open Source Software) nos ayudan en esta parte y nos dan
la oportunidad de leer código que ha pasado por uno, dos o muchos más programadores
y nos da una visión de como tienen que ser nuestro proyectos con respecto a estructura,
escritura, guía de estilos, etc.

Nos adentraremos al proyecto [coreutils](https://www.gnu.org/software/coreutils/coreutils.html)
y analizaremos el código de algunos comandos para aprender paulatinamente los temas del curso
de C avanzado.

Clonaremos el código fuente del proyecto desde la plataforma [Github](https://github.com/coreutils/coreutils.git)
y trataremos de compilarlo. Para esto necesitaremos la herrmienta [git](https://git-scm.com/) y adicionalmente
una cuenta en Github si quisieramos crear un fork del proyecto.

Para clonar el proyecto ejecutaremos el siguiente comando en lugar donde lo alojaremos dentro de nuestro filesystem.

```bash
$ mkdir Proyectos && cd Proyectos
$ git clone https://github.com/coreutils/coreutils.git
```

Dentro del proyecto clonado nos encontramos con varios archivos que para un programador principiante podrían ser
desafientes, pero siempre hay algunos por donde debemos empezar. Uno de ellos es el archivo README. Puede tener
diferentes estilos de nombre (README, README.md, readme, etc) pero siempre podremos identificarlo. En este caso,
el *readme* nos dice, entre más información, que para contruir el proyecto debemos ir al archivo README-hacking.

El archivo nos dice que debemos sincronizar los submódulos necesarios para el proyecto, para esto ejecutamos:

```
$ git submodule update --init --recursive
```

Una vez hecho lo anterior podremos ejecutar el script `bootstrap` que es una herramienta para verificar otros archivos
y paquetes necesarios en la construcción.

```
./bootstrap
```

Si genera un error lo anterior puedes referirte al archivo README-prereq, el cual contiene la información para
instalar las herrmientas necesarias. De la misma manera siempre puedes agregar las herremientas necesarias mediente
tu sistema operativo, con ayuda de apt o algún otro comando.

Si lo anterior no tuvo problemas, podremos configurar nuestro proyecto y compilarlo.

```
./configure
make
```