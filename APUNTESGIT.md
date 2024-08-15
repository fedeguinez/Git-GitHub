# Git - Fundamentos ==============================================================
## Primeros comandos - git config - git help --------------------------------------

**git --version** : para ver la version de git
**git help** muestra todos los comnando mas utilizados, si queremos saber mas sobre un comando en particular, hacemos **git help "nombre del comando"**

Antes de comenzar con repositorios debemos hacer:
- **git config --global user.name "nombre de usuario"** : para configurar el nombre
- **git config --global user.email "correo electronico"** : para configurar el correo
de esta manrea va guardando las cosas con estos parámetros

PAra ver donde estan esos registros podemos hacer 
**git config --global -e**, no apareceran lo datos de user y name (lo que congiremos)
para salir hacermos **:-q + enter** (escribimos dos puntos -q y damos enter)
**git config --global -l**, nos aparecen todas las conficuraciones realizadas, pero en tipo listado

## 04.Iniciando un proyecto y creando nuestro repositorio --------------------------

Nos ubicamos dentro de la carpeta del proyecto y hacemos

**git init**, asi comenzaremos a trabajar con git, se crearà la carpeta **.git**, es decir creamos el repositorio central
**git status**, apareceran todas las carpetas del proyecto, pero en rojo las que todavía no fueron agregador
- Archivos en rojo, fueron modificados pero no comiterados, se encuentran en el stage
- Archivos en verde, fueron comiteados 
**git add .**, agregamos todos los archivos del proyecto, si queremos agregar archivos especificos
**git add "nombre del archivo"** sirve para colocar el archivo a dispocisión de un commit
**git status**, ahora apareceran todos los archivos en verde, indicando que ya fueron agregados
**git commit -m "mensaje de commit"**, aqui podemos agregar un mensaje de commit, que 
es un mensaje que se va a guardar en la historia del proyecto, para saber que cambio
- Si volvemos a hacer un git status, veremos que nos aparece "On branch master", esto nos indica que todo está guardado en la rama master

## ¿Qué hace git por nosotros en estos momentos? -------------------------------------

**git checkout -- .** lo utilizazamos cuando borramos cosas del proyecto o todo el proyecto por accidente, y no podemos salvarlo con ctl+z, recupera segùn el último commit realizado.
**git checkout -- nombreArchivo .** para restaurar el archivo a una version anterior

**git log** aparecen todo el historial de commit
- Para hacer un commit con todos los archivos con la misma extensiòn, hacemos
**git add *.png** agrega todos los archivos con esa extension, pero solamente de la carpeta en que estemos.
**git add "*.txt"** Agrega todos los archivos con esa extension, pro de todo el proyecto
- Ahora, si queremos guardos solo lo de una carpeta, podemos hacer:
**git add nombreCarpeta/**
**git add --all** agrega todos los archivos, es parecido a 
**git reset nombreArchivo o *.extensionArchivo** para quitarlo del stage en caso de haberlo agregado con add.
**git -am "menasaje del commit"** con esto agreagos el archivo al stage y al mismo tiempo agreagos el mensaje.

## Otras formas de revisar el log y los cambios desde el último commit --------------------

HEAD -> master, nos indica donde se realizo el commit

**git log** vemos los commits
**git log --online** vemos las descripciones de los commits en una linea debao de otra, segun el orden de tiempo en que se realizaron
**git log --graph** nos muestra el grafo de los commits, es decir, los que 
se realizaron en paralelo, los que se realizaron en serie, etc.
**git log --all** nos muestra todos los commits, incluyendo los que se realizaron
**git log --all --graph** nos muestra todos los commits, incluyendo los que se
realizaron en paralelo, los que se realizaron en serie, etc.
**git log --all --graph --online** nos muestra todos los commits, incluyendo los
que se realizaron en paralelo, los  que se realizaron en serie, etc., y
los mensajes de los commits en una linea debajo de otra, segun el orden de tiempo en
que se realizaron.
**git log --online -- decorate --all --graph** muestra mejor ordenado y diferenciados los commits

**git status -s -b ó -sb** podemos ver cuales archivos fueron agregados para un commit y cuales no, ademas de en que rama se encuentran.
- En rojo, no agregados
- en verde, no agregados

### ALIAS EN GIT -------------------------------------------------------------------------

- **git config --global alias.s status -s -b** para crear un alias de status y branches
 ahora solo escibimos **git s** y lo ejecutará
- **git config --global alias.lg "log --online -- decorate --all --graph"**, para realizar
 ahora solo escibimos **git lg** y lo ejecutará

## Diferencias entre commits y restauración de archivos -------------------------------------

- Para comparar el archivo como estaba antes y como esta ahora, es decir que cambio hicimos, podemos hacer:
***git diff**
- Si queremos comparar depues de hacer hecho un git add sin el commit, hacemos
**git diff --staged** 

## Actualizar mensaje del commit y revertir commits -----------------------------------------

**git commit --amend -m "mensaje"**, de esta manera modificamos el mensaje del ultimo commit, en caso de querer cambiarle o agregarle algo.
- Para revertir un commit, es decir, para que el proyecto vuelva a estar como estaba
antes de ese commit, podemos hacer:
**git reset --soft HEAD^**
- HEAD apunta el úlltimo commit que hicimos
- si hacemos git s, vemos que nos aparecen como dos M o sea MM, una en rojo y otro en verde,
esto se debe a que el archivo se movio, ahora hacemos los cambios necesarios y procedemos como de costumbre.

## Preparando un repositorio para viajes en el tiempo --------------------------------------

- si solo hacemos **git commit**, sin el mensaje, nos aprece una pantalla que al presionar la letra A, podemos escribir el mensaje del commit, para salir hacemos :wq (w de writhe y q de quit)

## Viajes en el tiempo, resets y reflog --------------------------------------------------

**git reset --soft idDelCommit** puedo modificar ese commit, agregando modificaciones, una vez realizado los cambios, lo guado como de costumbre git -am "mensaje"
**git reset mixed idDelCommit**
**git reset --hard idDelCommit** si quiero borrarlo por completo, y no quiero
tenerlo en la historia del proyecto, pero si quiero tenerlo en el reflog, para poder
recuperarlo si es necesario.
**git reflog** muestra todos los commits que se han realizado, incluyendo los que se
borraron con el reset --hard, pero no los que se borraron con el reset --
mixed, ya que estos si se borran de la historia del proyecto y del reflog.
**git reset --hard idDelCommit** recuperamos los archivos hasta ese momento realizados

## Cambiar el nombre y eliminar archivos mediante git ---------------------------------------

**git mv nombreDelArchivo.extension nuevoNombreDelArchivo.extension** con este comando cambiamos el nombre del archivo y esto se vera reflejaod si hacemos un git lg
**git rm archivo** para eliminar un archivo, si queremos eliminarlo de la historia del proyecto
- hacemos git s y vemos que el archivo aparece on cuna D en verde, ahora hacemos un commit y listo, borramos el archivo del proyecto.
**git rm --cached archivo** para eliminarlo de la historia del proyecto pero no de la carpeta actual.

## Cambiar el nombre y eliminar archivos fuera de git ---------------------------------------

- Si cambio el nombre de un archivo por fuera y hacemos ***git s**
- vemos que existen 2 archivos, uno con la letra Den rojo y otro con signos de pregunta, uno estaría eliminado y el otro no tiene seguimiento. Para registrarlo hacemos
**git add -u** --> git s --> git add -A --> git s, en este punto tenemos los cambios en el stage, ahora debemos hacer el commit git commit -m

- Si ELIMINO  un archivo por fuera y hacemos ***git s**
**git add -u** --> git s --> git add -A --> git s, en este punto tenemos los cambios en el stage, ahora debemos hacer el commit git commit -m

## Ignorando archivos que no deseamos -------------------------------------------------------

- creamos un archivo
- con git s, vemos el archiv con signos de pregunta, lo que significa que no tiene seguimiento
- **.gitignore** creamos este archivo y dentro de este colocamos el nombre por ejemplo:
    *.log, en caso de archivos de tipo log por ejemplo
    node_modules/, para ignorar una carpeta de archivos
- Una vez creado el archivo .gitignore, debemos agreagrlo y commitearlo


## Introducción a la sección de ramas (Branch) -----------------------------------------------

- Es una línea de timepo de commits
- Master es una Rama principal
- Por ejemplo, cuando uno llega a un camino que se divide en 2 o más 
- MERGE une las ramas, estre estos estan
     * fast-forward: git detecta que no hay ningún cambio en la rama principal, y los mismo pueden ser integrado a esta
     * Uniones automáticas: git detecta cambios pero al hacer merge, lo indica y lo integra
     * Uniones manuales: git detecta cambios pero al hacer merge, no los integra porque detecta un conflicto y nos pide que lo integremos manualmente
     * Conflicto: git detecta cambios pero al hacer merge, no los integra, haciendo un commit nuevo de tipo Merge, es decir un **Merger Commit**, luego podemos seguir trabajando sin problema


## Merge Fast-Forward ----------------------------------------------------------------------

- Recomendaciones, primero hacer git lg 
- Agreagamos un nuevo archivo en una rama distinta a la rama Master

**git branch nombreRama** creamos una nueva rama
**git branch** vemos las ramas creadas y cual es la utilizada
**git checkout nombreRama** nos ubica en la rama deseada
**git add archivo** agregamos el archivo a la rama deseada
**git commit -m "mensaje"** creamos un commit en la rama deseada

**git diff nombreRama1 nombreRama2** puede ver la difreencia entre las 2 ramas

- PARA UNIR LAS RAMAS, EN ESTE EJMEPLO RAMA1 CON MASTER

**git checkout Master** nos ubica en la rama Master, recordar que primero me debo ubicar en la rama donde deseo hacer el Merge
- El HEAD apunta a Master ahora

***git merge rama1** ahora el Head Apunta a master, rama1

- Una vez terminado el Merge, ya no tiene sentido mantener la rama, para ello la borramos

**git branch -d rama1**, así borramos la rama
**git branch -d nombreRama**, así borramos la rama
con git branch vemos que la rama ya no existe

## Merge Uniones con conflictos ---------------------------------------------------------------

- **git checkout -b nombreRAma**  creamos rama
- Si por ejemplo hacemos modificaciones en 2 ramas distintas, y queremos hacer merge, nos aparecerá **Auto-Mergin nombreArchivo**, para resolver esto debemos modificar el archivo y hacer un commit 

## Tags - Etiquetas ---------------------------------------------------------------------------
- Son Referencias a un commit específico, pueden ser palabras numeros, etc
- Para crear un tag, debemos estar en el commit que queremos etiquetar, y crear el tag
- git s
- git lg
**git tag nombreTag**, creamos el tag
**git tag** vemos los tags creados
**git -d nombreTag** borramos el tag
### Para Renombrar un commit, es decir agregarle un tag ........
 - **git tag -a nombreTag hashDelCommit -m "mensaje" nombreCommit**, creamos un tag

**git show nombreTag** vemos los detalles del tag


## Introducción al git Stash ---------------------------------------------------------------------
- Se lo utiliza cuando por ejemplo estamos trabajando en unas modificaciones del proyecto, y nos piden que despleguemos el proyecto, pero las modificaciones que hicimos todavia no están listas para un commit o para ser desplegadas, podemos guardar nuestro trabajo sin afectar al proyecto utilizando el stage
- Es una forma de guardar los cambios realizados en el proyecto, para poder trabajar en otro proyecto. Es como una caja, donde podemos colocar todo y poder recuperar el trabajo donde nos quedamos
- Para guardar los cambios realizados en el proyecto, debemos estar en el proyecto y hacer un
- WIP (Work In Progress)
**git stash**, esto nos permite guardar los cambios realizados en el proyecto
- git s, git lg
**git stash list**, vemos los cambios realizados en el proyecto
**git stash pop** extrae del stage todos los cambios pendientes, toma el úeltimo movimiento en el stage y los elimina
**git stash apply** aplica los cambios del stash, pero no los elimina
**git stash drop** elimina el stash
**git stash clear** elimina todos los stash creados
**git stash apply stash@{0}** aplica el stash 0
**git stash apply stash@{1}** aplica el stash 1, etc...

### Conflictos con el stash.........
- Supongamos que estamos trabajando en un archivo y hacemos un stage, pero seguimos trabajando en el mismo archivo, pero con otros requeirmientos.
- al hacer git stage pop, nos indicará un conflicto, para resolverlo debemos modificar el archivo, y resolverlo como un conflicto normal.
- Una vez resuelto el conflicto, debemos hacer un commit para poder aplicar el stash.
- debemos hacer un delete de ese stash para eliminarlo
**git stash drop** elimina el ultimo elemento stash registrado

**git stage save --keep-index** guarda todo menos los archivos en el stage o en el escenario
**git stash save --include-untracked** incluye todos los archivos, junto a los que git no le da seguimiento

**git stash list --stat** aparece más informacion de los stage, que con solamente list

**gti show stash** muestra informacion del último registro metido al stage

**git stage save "mensaje"** agreaga un mensaje al stage


## Introducción al git rebase ---------------------------------------------------------------

- tenemos la rama master y un commit
- creamos una rama por ejemplo rama1 y hacemos 2 commits
- luego alguien crea 2 commits más pero en la rama master
- para resolver esto, rebase coloca los commits de la rama1 en un archivo temporal, corre la creacion de la rama1 hacia un lugar posterior al ultimo commit de la rama master, y vuelve a colocar estos commits de la rama1 es su lugar.
- es como si la rama1 se hubiera creado después de los commits de la rama Master
- **git checkout rama1**
- **git rebase master**

### Rebase Interactivo, se lo utiliza para
- Ordena Commits
- Corregir mensajes de los commits
- Unir Commits
- Separar Commits


### Rebase, actualizando una rama...
- vamos a colocar 2 commits de una rama1 al master, sin hacer merge
- git branch, y me coloco en la rama1 --> git checkout rama1
**git rebase master**, m eubico en la rama donde quiero colocar los commits
- git rebase master me permite colocar los commits de la rama1 en el
master, sin hacer merge
- ahora unimos la rama1 al master
- git checkout master --> git merge rama1, nos indica un fast-forward y no existe la separación
- borramos la rama git branch -d rama1

### Rebase Squash, unir dos commits en uno solo...
- Para unir ultimos commits en uno solo, cuando nos damos cuenta que los commits se tratan de los mismo
**git rebase -i HEAD~numeroDeCommitsAUnir**, aparece una pantalla con los ultimos commits que seleccionamos, van en orden ascendente, nos movemos con el cursor hacia el commit y reemplazamos la palabra pick con la palabra squash o simplemente una s, por ejemplo si queremos unir el útimo commit con el anterior, al commit anterior dejamos como está o ponemos la letra p y al último le ponemos la s. Siempre la letra ese, va entre los ultimos commits que queremos unir a partir de la ultima p que tambien se unirá.
- Para salir presionamos Escape, dos puntos, w para escribir y q para salir, ahora nos aparece otra pantalla donde debemos colocar un mensaje para esta modificación, luego para salir presionamos Escape, dos puntos, w para escribir y q para salir. 
si hacemos lg vemos que ya no estan los commits pero hay uno nuevo, el que realizamos.

### Rebase Reword, modificar los mensajes del rebase...
**git rebase -i HEAD~numeroDeUbicación**, por ejemplo la ubicacion 1 HEAD~1, 
abre el editor, presionamos la letra A para editar, y luego cambiamos la palabra pick por la palabra reword o solo la letra r, resionamos Escape, dos puntos, w para escribir y q para salir, ahora nos aparece otra pantalla donde cambiamos el mensaje, luego para salir presionamos Escape, dos puntos, w para escribir y q para salir. 
si hacemos lg vemos que ya no estan los commits pero hay uno nuevo, el que realizamos.


### Rebase edit...
- Si realizamos un commit con 2 archivos modificados y queremos separalos
**git rebase -i HEAD~numeroDeUbicación**, por ejemplo la ubicacion 1 HEAD~1, 
abre el editor, presionamos la letra A para editar, y luego cambiamos la palabra pick por la palabra edit o solo la letra e, resionamos Escape, dos puntos, w para escribir y q para salir, ahora nos aparece un mensaje que nos dice que podemos hacer un git --amend, pero yo quiero separar estos commits, para esto hacemos
**git reset HEAD^** esto me va a revertir los cambios sin destruirlos
git s 
git add nombreArchivo --> git commit -m, y así para el otro
git s, por ultimo
**git rebase continue**
git lg, vemos que tenemos 2 commits mas
