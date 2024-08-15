# GitHub - Fundamentos =============================================================

- GitHub: Es un repositorio remoto, una plataforma de desarrollo colaborativo de software
   * Repositorios ilimitados (privados o públicos)
   * Páginas HTML, CSS y JS ilimitados
   * Push, Pull, clones ilimitados
   * Issues, wikis, estadíticas ilimitadas
   * Organizaciones ilimitadas
   * Participación gratuita en proyectos privados

- Push: Sube al servidor los cambio
- Pull: Descargo los cambios del servidor
- Cada participante de un proyecto puede hacer su push y su pull, no hay un control de accesos a cada archivo, para eso utilizamos las herramientas 

## Crear repositorio ---------------------------------------------------------------------
- Ir a la pagina de github y hacer click en crear repositorio, este debe ser único en mi cuenta, damos en siguiente
- Dependiendo de lo que seleccionamos, nos lleva a una pantalla de Quick setup, donde vemos la dirección de nuestro repositorio, este puede ser ssh o https
**https://github.com/nombreCuenta/nombreRepositorio.git**

- En la pantalla de Quick setup, podemos agregar un archivo README.md, un archivo .gitignore
- En la pantalla de Quick setup, podemos agregar un archivo LICENSE

## Repositorio Remoto ---------------------------------------------------------------------

**git remote add origin https://github.com/nombreCuenta/nombreRepositorio.git**
- add: es porque quiero agregar un acceso remoto a ese repositorio
- origin: por default es este nombre, o por convension mejor dicho, nos indica donde se ubicará ese repositorio remoto, puede ser cualquier nombre
- https://github.com/nombreCuenta/nombreRepositorio.git: es la dirección del repositorio remoto

**git remote -v** para ver los repositorios remotos que tenemos
**git push -u origin master**
- push: subir los cambios al repositorio remoto
- -u: es para establecer la rama remota como la rama local
- origin: es el nombre del repositorio remoto
- master: es la rama local que quiero subir

--> Cuando ejecutamos este comando, nos va a pedir nuestro usuario y contraseña de gitHub, una vez que la ingresamos, va a realizar el push.

## Subir el Proyecto al repositorio Remoto por https -------------------------------------
- Para subir el proyecto al repositorio remoto, debemos hacer lo siguiente:
- Abrir la terminal y dirigirme al proyecto
- git s, revisar que no quedan commits pendientes
- git lg y asegurarme que tenga movimientos realizados

## PUSH a nuestro repositorio -------------------------------------------------------------

- copiamos y pegamos la dirección remota
**git remote add origin https://github.com/nombreCuenta/nombreRepositorio.git**
**git remote** vemos el origen
**git remote -v** vemos nuestro fetch y nuestro push
**git push -u origin master**, me pide usuario y contraseña
- Comienza a subir el proyecto

### Push de los Tags...
- Cuando subimos el proyecto, no sube por defectos los tagas, hay que hacerlo con el comando
**git push --tags**
- Esto sube los tags a nuestro repositorio remoto


## PULL de nuestro repositorio -------------------------------------------------------------
- Si realizamos cambios en nuetro github, podemos bajar estos cambios a nuestra computadora
- Abrir la terminal y dirigirme al proyecto
**git remote -v** para saber que estamos en el remote deseado
**git pull** descarga las modificaciones realizadas
**git lg** para ver los cambios realizados
**git status** para ver los cambios realizados
**git log** para ver quien hizo las modificaciones realizadas

## CLONAR repositorio -------------------------------------------------------------
- Copiamos el URL desde del repositorio de github, en clone or download, elegimos si es https o ssh
- Abrir la terminal
- ir a una carpeta específica
- **git clone https://github.com/nombreCuenta/nombreRepositorio.git**
- crea la carpeta y cada uno de los archivos
- Para Renombrar la carpeta del proyecto a bajar hacemos 
 **git clone https://github.com/nombreCuenta/nombreRepositorio.git nombreCarpetaDeseada**