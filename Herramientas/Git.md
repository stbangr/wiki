# Git 
[![Git](https://img.shields.io/badge/Git-2.37+-f14e32?style=for-the-badge&logo=git&logoColor=white&labelColor=101010)](https://git-scm.com/)

---
## Descripcion

Git es un **software de control de versiones distribuido**, que nos permite gestionar el proyecto con un sistema de branch o ramas, asi como puntos de control durante el desarrollo.

---

## Los Tres Estados

Git tiene tres estados principales en los que se pueden encontrar tus archivos:

**Modificado (```modified```)**:`significa que has modificado el archivo pero todavía no lo has confirmado a tu base de datos.

**Preparado (```staged```)**: significa que has marcado un archivo modificado en su versión actual para que vaya en tu próxima confirmación.

**Confirmado (```committed```)**: significa que los datos están almacenados de manera segura en tu base de datos local. 

- El directorio de Git (**Git directory**)
- El directorio de trabajo (**working directory**)
- El área de preparación (**staging area**)

![](https://git-scm.com/book/en/v2/images/areas.png)

El flujo de trabajo básico en Git es algo así:

1. **Modificas** una serie de archivos en tu directorio de trabajo.

2. **Preparas** los archivos, añadiéndolos a tu área de preparación.

3. **Confirmas** los cambios, lo que toma los archivos tal y como están en el área de preparación y almacena esa copia instantánea de manera permanente en tu directorio de Git.

El directorio de Git es donde se almacenan los metadatos y la base de datos de objetos para tu proyecto. Es la parte más importante de Git, y es lo que se copia cuando clonas un repositorio desde otra computadora.

El directorio de trabajo es una copia de una versión del proyecto. Estos archivos se sacan de la base de datos comprimida en el directorio de Git, y se colocan en disco para que los puedas usar o modificar.

El área de preparación es un archivo, generalmente contenido en tu directorio de Git, que almacena información acerca de lo que va a ir en tu próxima confirmación. A veces se le denomina índice (**“index”**), pero se está convirtiendo en estándar el referirse a ella como el área de preparación.

---

## Configurando Git

Git trae una herramienta llamada **`` git config ``**, que te permite obtener y establecer variables de configuración que controlan el aspecto y funcionamiento de Git. Estas variables pueden almacenarse en tres sitios distintos:

* Archivo **/etc/gitconfig**: Contiene valores para todos los usuarios del sistema y todos sus repositorios. Si pasas la opción **``--system``** a git config, lee y escribe específicamente en este archivo.

* Archivo **~/.gitconfig** o **~/.config/git/config**: Este archivo es específico de tu usuario. Puedes hacer que Git lea y escriba específicamente en este archivo pasando la opción **``--global``**.

* Archivo config en el directorio de Git (es decir, **.git/config**) del repositorio que estés utilizando actualmente: Este archivo es específico del repositorio actual.

Cada nivel sobrescribe los valores del nivel anterior, por lo que los valores de **.git/config** tienen preferencia sobre los de **/etc/gitconfig**.

---

### Tu Identidad

Los "**commits**" de Git usan esta información, y es introducida de manera inmutable en los commits que envías:

>``git config --global user.name`` **"[Mi nombre de usario]"**

>``git config --global user.email`` **[Mi correo electronico]**

---
### Tu Editor

Elegir el editor de texto por defecto que se utilizará cuando Git necesite que introduzcas un mensaje. Git usará el editor por defecto de tu sistema, que generalmente es Vim.

>``git config --global core.editor`` **[Editor]**
---
### Comprovar configuración
Si quieres comprobar tu configuración:
>``git config --list``
---
## Iniciar un repositorio 

Si estás empezando un proyecto en Git, debes ir al directorio del proyecto y usar el siguiente comando:

>``git init``

Esto crea un subdirectorio nuevo llamado **.git**, el cual contiene todos los archivos necesarios del repositorio -*un esqueleto de un repositorio de Git.* 

### Añadir archivo 
Para especificar qué archivos quieres controlar:
> ``git add`` [**Archivo**]

### Commit inicial
Para confirmar los archivos que hemos añadido:
>``git commit -m`` '[**Mensaje**]'

La flag **-m** añade un mensaje de confirmacion.
El mensaje que se suele poner en el primer mensaje 'initial project version' o 'initial commit'.

***Es importante poner un mensaje siempre***.

Cada vez que realizas un **commit**, guardas una instantánea de tu proyecto la cual puedes usar para comparar o volver a ella luego.

---


## Clonar un repositorio

El comando git clone se utiliza para crear una copia local de un repositorio remoto.


>``git clone`` [URL del repositorio]

El [URL del repositorio] es la dirección del repositorio remoto que deseas clonar. Puede ser una URL HTTPS o SSH.

Al ejecutar el comando git clone, se creará una copia local completa del repositorio remoto, incluyendo todos los archivos, historial de commits y ramas. La copia se almacenará en un nuevo directorio con el mismo nombre que el repositorio.

>``git clone`` https://github.com/usuario/repo.git

Esto clonará el repositorio remoto en el directorio actual y creará una carpeta llamada "repo" con todos los archivos y la historia del repositorio.

También puedes proporcionar una ruta de destino opcional después de la URL para clonar el repositorio en un directorio con un nombre diferente al del repositorio remoto.

>``git clone`` https://github.com/usuario/repo.git [mi-proyecto]

Esto clonará el repositorio remoto en un directorio llamado "mi-proyecto" en lugar de utilizar el nombre del repositorio.

---

## Guardando cambios en el Repositorio

Ya tienes un repositorio Git y un checkout o copia de trabajo de los archivos de dicho proyecto.
Los archivo de tu repositorio puede tener dos estados: 
* Rastreados (**tracked files**): son todos aquellos archivos que estaban en la última instantánea del proyecto.
* Sin rastrear (**untracked files**):cualquier otro archivo en tu directorio de trabajo que no estaba en tu última instantánea y que no está en el área de preparación (**staging area**).

Sin rastrear significa que Git ve archivos que no tenías en el commit anterior. Git no los incluirá en tu próximo commit a menos que se lo indiques explícitamente. Se comporta así para evitar incluir accidentalmente archivos binarios o cualquier otro archivo que no quieras incluir.

Cuando clonas por primera vez un repositorio, todos tus archivos estarán rastreados.

![](https://git-scm.com/book/en/v2/images/lifecycle.png)

### Revisando el Estado de tus Archivos

Para determinar qué archivos están en qué estado es el comando:

>``git status``

### Rastrear Archivos Nuevos

Para comenzar a rastrear un archivo:
> ``git add`` [**Archivo**]

Puedes ver que está siendo rastreado porque aparece como (**“Changes to be committed”**) al hacer el ``git status``.

El comando ``git add`` puede recibir tanto una ruta de **archivo** como de un **directorio**, si es de un directorio, el comando añade recursivamente los archivos que están dentro de él.

### Preparar Archivos Modificados
Si modificas un archivo **rastreado** puedes ver que aparece como (**“Changes not staged for commit”**) al hacer el ``git status``.

Para prepararlo, ejecutas el comando ``git add`` es un comando que cumple varios propósitos: 
* **Rastrear archivos nuevos** 
* **Preparar archivos** 
* Marcar archivos en conflicto por combinación como **resueltos**. 

Es más útil que lo veas como un comando para **“añadir este contenido a la próxima confirmación”** más que para “añadir este archivo al proyecto”.

*Al hacer el* ``git add`` *se guardara la version del archivo en ese momento, aunque luego lo modifiques, al hacer el* ``commit`` *se utilizara la version de cuando hiciste el* ``git add``*.*

### Ignorar Archivos
Para archivo que no quieres que Git añada automáticamente puedes crear un archivo llamado **.gitignore** que liste patrones a considerar.

### Ver los Cambios Preparados y No Preparados

Para ver qué has cambiado pero aun no has preparado:
>``git diff``

Si quieres ver lo que has preparado y será incluido en la próxima confirmación, puedes usar:
>``git diff --stage``

o

>``git diff --cached``

*(**--staged** y **--cached** son sinónimos)*

### Confirmar tus Cambios

Para confirmar lo que has preparado:
>``git commit``

Esto lanzará un editor de texto que te permitirá introducir un mensaje de confirmación.

Si quieres saltar el editor de texto puedes usar la flag **-m** para escribir el mensaje de confirmación:
>``git commit -m`` '**Mensaje**'

### Saltarse el Area de Preparación

En ocasiones, lo que quieres es hacer dos o más modificaciones en tu directorio de trabajo y luego confirmarlas todas en un solo paso. Puedes hacerlo usando la flag **-a** al comando **git commit**:
>``git commit -a -m`` '**Mensaje**'

### Eliminar Archivos

Para eliminar un archivo del repositorio y del directorio de trabajo:
>``git rm`` [**Archivo**]

Para eliminar un archivo del repositorio pero no del directorio de trabajo:
>``git rm --cached`` [**Archivo**]

### Mover Archivos

Para mover un archivo de nombre:
>``git mv`` [**NombreActual**] [**NombreNuevo**]

---

## Ver el Historial de Confirmaciones

Para ver el historial de confirmaciones:
>``git log``

Para ver el historial de confirmaciones con mas información:
>``git log --stat``

Para ver el historial de confirmaciones en una linea:
>``git log --oneline``

Para ver el historial de confirmaciones de un usuario:
>``git log --author=[**Usuario**]``

Para ver el historial de confirmaciones de un archivo:
>``git log --[**Archivo**]``

Para ver el historial de confirmaciones de un archivo de un usuario:
>``git log --author=[**Usuario**] --[**Archivo**]``

Para ver el historial de confirmaciones de un archivo de un usuario en una linea:
>``git log --author=[**Usuario**] --[**Archivo**] --oneline``

Para ver el historial de confirmaciones de un archivo de un usuario en una linea con mas información:
>``git log --author=[**Usuario**] --[**Archivo**] --stat``

Para ver el historial de confirmaciones de un archivo de un usuario en una linea con mas información y fecha:
>``git log --author=[**Usuario**] --[**Archivo**] --stat --date=short``

Para ver el historial de confirmaciones de un archivo de un usuario en una linea con mas información y fecha y hora:
>``git log --author=[**Usuario**] --[**Archivo**] --stat --date=iso``

Para ver el historial de confirmaciones de un archivo de un usuario en una linea con mas información y fecha y hora y con un formato especifico:
>``git log --author=[**Usuario**] --[**Archivo**] --stat --date=format:'%d/%m/%Y'``

Para ver el historial de confirmaciones de un archivo de un usuario en una linea con mas información y fecha y hora y con un formato especifico y con un limite de confirmaciones:
>``git log --author=[**Usuario**] --[**Archivo**] --stat --date=format:'%d/%m/%Y' -n [**Numero**]``

---

## Deshacer Cosas

### Deshacer Cambios en el Directorio de Trabajo

Para deshacer las modificaciones de un archivo que no has preparado:
>``git checkout --`` [**Archivo**]

### Deshacer Cambios en el Area de Preparación

Para deshacer las preparaciones de un archivo:
>``git reset HEAD`` [**Archivo**]

### Deshacer un Commit

Para deshacer un commit y mantener los cambios en el directorio de trabajo:
>``git reset --soft HEAD^``

Para deshacer un commit y los cambios en el directorio de trabajo:
>``git reset --hard HEAD^``

Para deshacer un commit y los cambios en el directorio de trabajo y el area de preparacion:
>``git reset --mixed HEAD^``

### Cambiar el Mensaje del Commit

Para cambiar el mensaje del ultimo commit:
>``git commit --amend -m`` '**Mensaje**'

### Recuperar un Archivo Eliminado

Para recuperar un archivo eliminado:
>``git checkout HEAD`` [**Archivo**]

---

## Trabajar con Remotos

### Mostrar Tus Remotos

Para ver los remotos que tienes configurados:
>``git remote``

Para ver los remotos que tienes configurados con mas información:
>``git remote -v``
---
### Añadir Remotos

Para añadir un nuevo remoto:
>``git remote add`` [**Nombre**] [**URL**]

Para añadir un nuevo remoto sin tener que especificar el nombre:
>``git remote add`` [**URL**]

---

### Inspeccionar un Remoto

Para ver la URL de un remoto:
>``git remote show`` [**Remoto**]

Para ver la URL de un remoto con mas información:
>``git remote show -v`` [**Remoto**]

---

### Renombrar y Eliminar Remotos

Para renombrar un remoto:
>``git remote rename`` [**Remoto**] [**Nombre**]

Para eliminar un remoto:
>``git remote remove`` [**Remoto**]

---

### Enviar a Tus Remotos

Para enviar a un remoto:
>``git push`` [**Remoto**] [**Rama**]

Para enviar a un remoto con la rama especificada como rama por defecto:
>``git push -u`` [**Remoto**] [**Rama**]

Para enviar a un remoto con la rama especificada como rama por defecto y con la flag --force:
>``git push -u --force`` [**Remoto**] [**Rama**]

Para enviar a un remoto con la rama especificada como rama por defecto y con la flag --force y con el mensaje:
>``git push -u --force`` [**Remoto**] [**Rama**] -m '**Mensaje**'

---

### Inspeccionar un Remoto

Para ver la URL de un remoto:
>``git remote show`` [**Remoto**]

Para ver la URL de un remoto con mas información:
>``git remote show -v`` [**Remoto**]

---

### Renombrar y Eliminar Remotos

Para renombrar un remoto:
>``git remote rename`` [**Remoto**] [**Nombre**]

Para eliminar un remoto:
>``git remote remove`` [**Remoto**]

---
