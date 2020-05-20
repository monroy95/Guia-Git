# Guía Básica Git

>   [Git ](https://git-scm.com/)es el sistema de control de versiones distribuidas de código abierto que facilita las actividades de [GitHub](https://github.com/) en su computadora portátil o escritorio. Esta hoja de trucos resume las instrucciones de línea de comando de Git utilizadas comúnmente para referencia rápida.



- [Guía Básica Git](#gu-a-b-sica-git)
  * [CONFIGURACIONES INICIALES](#configuraciones-iniciales)
  * [INICIALIZAR REPOSITORIO](#inicializar-repositorio)
  * [AGREGAR ORIGEN DE REPOSITORIO](#agregar-origen-de-repositorio)
  * [AGREGAR, MODIFICAR Y CONFIRMAR CAMBIOS](#agregar--modificar-y-confirmar-cambios)
  * [HISTORIAL DE COMMITS](#historial-de-commits)
  * [VIAJES EN EL TIEMPO](#viajes-en-el-tiempo)
  * [CAMBIAR NOMBRES DE ARCHIVOS CON GIT](#cambiar-nombres-de-archivos-con-git)
  * [IGNORANDO ARCHIVO (.gitignore)](#ignorando-archivo--gitignore-)
  * [RAMAS](#ramas)
  * [TAGS Y ETIQUETAS](#tags-y-etiquetas)
  * [GIT STASH](#git-stash)
  * [EMPUJANDO LOS CAMBIOS](#empujando-los-cambios)
  * [GIT PULL Y GIT FETCH](#git-pull-y-git-fetch)
  * [ERROR AL AGREGAR ARCHIVOS](#error-al-agregar-archivos)



## CONFIGURACIONES INICIALES

Para más información puedes ver la documentación [**aquí.**](https://git-scm.com/doc)

Configura la información del usuario para todos los repositorios locales.

Establece el nombre que desea adjuntar a sus commits.

```
git config --global user.name "nombre_usuario"
```

Establece el correo electrónico que desea adjuntar a sus commits.

```
git config --global user.email "correo_electronico"
```

## INICIALIZAR REPOSITORIO

Inicializa un nuevo repositorio en el directorio donde se encuentre ubicado o uno con un nombre específico.

```
git init
```

Descarga un proyecto y con él todo su historial de versiones.

```
git clone [url]
```

Clonar un proyecto con un nombre alternativo

```
git clone git://github.com/schacon/grit.git my_nuevo_proyecto
```

## AGREGAR ORIGEN DE REPOSITORIO

Existen dos formas para agregar el origen de un repositorio.

1.  Por medio de https:

```
git remote add origin https://github.com/nombre/hold1.git
```

2.  Por medio de ssh:

```
git remote add origin git@github.com:nombre/hold1.git
```

Para ver una descripción de la configuración global puede utilizar:

```
git config --global -l
```

Ver los repositorios remotos configurados.

```
git remote -v
```

Si desea cambiar el repositorio remoto, antes debe quitar los que ya tiene inicializados esto lo puede realizar con el comando.

```
git remote rm origin
```

## AGREGAR, MODIFICAR Y CONFIRMAR CAMBIOS

Ver las ediciones, cambios.

```
git status
```

Otra forma de ver el estado.

```
git status -s
```

Pero también podemos ver más detalles del estado.

```
git status -s -b
```

En caso existan archivos por agregar, hay que agregarlos a la cola de archivos para comprometer. Este es el “staging area” o área de presentación. Es importante agregar archivos aca, previo a hacer un commit. Aquí agregamos todo, esto lo hacemos con los siguientes comandos y las diferentes opciones.

Este comando agrega todos los archivos modificados.

```
git add .
```

También podemos agregar archivos individualmente.

```
git add nombre_archivo
```

Podemos agregar la cantidad de archivos que queramos con determinada extensión, esto aplica para los archivos en el mismo directorio.

```
git add *.py
```

Para agregar todos los archivos con especifica extensión no importando el directorio en el que se encuentren utilizamos lo siguiente.

```
git add "*.js"
```

Agregar todos los archivos de un especifico directorio.

```
git add public/
```

Agregar todos los archivos que hayan sido modificados.

```
git add -A
```

Excluir un archivo del stage.

```
git reset *.json
```

Agregar todos los archivos, se parece al comando `**git add .**`

```
git add --all
```

Si no sabe cuáles cambios han sido agregados al área de (add .) y desea ver cuales son las diferencias existentes en el área de presentación y los archivos que usted ha trabajado, entonces use el siguiente comando que muestra las diferencias.

```
git diff
```

Luego agregados todos los archivos, podemos comprometerlos, la bandera -a (para agregar archivos con cambios y quitar los archivos borrados del índice local) y -m (de mensaje) agregando un comentario entre comillas que sirva de referencia.

```
git commit -am "Mi Primer Commit"ogit commit -m "Mi Primer Commit" (Recomendado)ogit commit
```

Si solamente utilizar el comando `git commit` se abrirá un editor vim allí puedes editar tu mensaje.

Si por alguna razón cometes un error en el mensaje del commit, no hay problema esto se puede resolver con el siguiente comando que permite modificar el mensaje del commit.

```
git commit --amend -m "Mensaje Corregido"
```

## HISTORIAL DE COMMITS

Para ver el listado de commits.

```
git log
```

Ver una descripción resumida de los commits.

```
git log --oneline
```

Una descripción más detallada.

```
git log --oneline --decorate --all --graph
```

Si queremos ver el log aunque hayamos realizado un` reset --hard`

```
git reflog
```

## VIAJES EN EL TIEMPO

Restaurar hacia el último cambio para hacer un nuevo commit corregido.

```
git reset --soft HEAD^
```

Si queremos regresar hacia un punto en específico del historial de cambios en el repositorio podemos utilizar.

```
git reset --mixed [número-hash]
```

Esta opción restaura hacia determinado commit, pero aún mantiene los archivos que hayamos estado trabajando después de ese commit.

La forma recomenda a utilizar es:

```
git reset --hard [número-hash]
```

Esta opción nos permite restaurar hacia un punto en específico, descartando todos los cambios que hayamos hecho después de ese commit.



Para recuperar los últimos cambios realizados tras un posible error o pérdida de código puede ejecutar lo siguiente comando, este permite recuperar la información del último commit registrado.

```
git checkout -- .
```

Si desea recuperar los últimos cambios registrados de un archivo en especifico.

```
git checkout -- nombre_archivo
```

## CAMBIAR NOMBRES DE ARCHIVOS CON GIT

Cuando cambiamos el nombre de un archivo manualmente, git puede detectar como si fuera un archivo nuevo, para evitar esto utilizamos lo siguiente:

```
git mv nombre_script.py nombre_nuevo_script.py
```

Esto permite que git lleve el registro sobre el mismo archivo y que únicamente detecte que se renombro.

Otra recomendación para cuando se elimina un archivo y para que git lleve un correcto registro podemos hacer los siguiente después de eliminar los n archivos.

```
git add -u
git add -A
```

## IGNORANDO ARCHIVO (.gitignore)

Si deseamos que git no reconozca ciertos archivos o carpetas, solamente debemos crear un nuevo archivo llamado `.gitignore` en la raíz del proyecto, donde en cada línea podemos ir agregando que archivos queremos ignorar. Ejemplo:

```
*.DS_Store
*.pyc
*.egg-info
*.swp
tags/
mi_proyecto/docs/
```

## RAMAS

Crear una rama.

```
git branch nombre_rama
```

O puede utilizar el siguiente comando que permite crear una rama y switchear a la misma.

```
git checkout -b nombre_rama
```

Ver listado de ramas y listado completo.

```
git branchogit branch -a
```

Cambiar de rama.

```
git checkout nombre_rama
```

Ver diferencias entre ramas. En este ejemplo, es la diferencia entre la rama nueva y la rama master.

```
git diff rama_nueva master
```

Fusionar ramas, esto se debe hacer desde la rama master.

```
git merge nombre_rama
```

Eliminar una rama.

```
git branch -d nombre_rama
```

Eliminar rama de forma forzada.

```
git branch -D nombre_rama
```

Después de haber eliminado las ramas locamente puede limpiar el registro de nuevo, para que ya no aparezcan en el repositorio remoto, esto es opcional.

```
git remote prune origin
```

## TAGS Y ETIQUETAS

Los tags, etiquetas nos permiten crear descripciones para ciertos releases, por ejemplo para una versión de aplicación.

Crear un tag.

```
git tag release-v1
```

Ver el listado de tags.

```
git tag
```

Eliminar un tag.

```
git tag -d nombre-tag
```

Forma Correcta para crear un **release** (**-a** = anotación).

```
git tag -a v1.0.0 -m "Mensaje descriptivo de la versión"
```

Crear un tag o release para cualquier punto en el historial de nuestra proyecto.

```
git tag -a v1.0.0 [numero-hash] -m "Mensaje"
```

Ejemplo:

```
git tag -a v1.0.0 ca82a6d -m "Versión Producción"
```

Ver informacion sobre un tag.

```
git tag show nombre_tag
```

## GIT STASH

Git stash nos permite dejar lo que estamos trabajando en un punto, para enfocarnos en otro punto para luego recuperar lo que no terminamos.

```
git stashogit stash save
```

Agregando mensajes a los stash, ya podemos tener más de un stash.

```
git stash save "Mensaje"
```

Ver informacion de los stash.

```
git stash list

git stash list --stat

git stash show
```

Recuperar un stash, esto extrae el último stash registrado con sus respectivos datos, cuando se ejecuta recupera el último stash y lo elimina, como si fuera de una pila.

```
git stash pop
```

Tambien podemos utilizar apply.

```
git stash apply

o

git stash apply [hash]
```

Si ya no vamos a utilizar un stash, hay que eliminarlo! Después de esto hay que verificarlo viendo el listado usando cualquiera de los comandos anteriores.

```
git stash drop

o

git stash drop [hash]
```

## EMPUJANDO LOS CAMBIOS

Ahora empujemos los cambios a nuestro repositorio en GitHub, esto lo hacemos con:

```
git push -u origin master
```

La bandera -u nos permite indicar a que rama queremos hacer el push, para que la proxima vez podamos solamente utilizar

```
git push
```

o bien puedes utilizar.

```
git push origin master
```

Hacer Push de Tags

```
git push --tags
```

## GIT PULL Y GIT FETCH

Git pull nos permite sincronizar los cambios remotos con los cambios locales, cuando se utiliza git pull este automaticamente hacer merge los cambios remotos con los datos que tengamos en local.

```
git pull origin master

o

git pull

y en caso no funcionen los comandos anteriores

git pull --all
```

Git Fetch nos permite actualizar nuestro repositorio local con los cambios realizados en el repositorio remoto.

```
git fetch
```

Para ver los cambios, actualizaciones de un repositorio forkeado de algun compañero podemos utilizar.

```
git remote add upstream <repositorio_original>

git fetch upstream
```

## ERROR AL AGREGAR ARCHIVOS

Puede ocurrir el error que git no nos permita agregar archivos, esto lo podemos solucionar con.

```
rm -f ./.git/index.lock
```

Esto eliminará de forma forzada el archivo index.lock lo cual provoca el error.

