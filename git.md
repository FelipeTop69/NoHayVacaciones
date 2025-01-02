# GIT HUB
> *Usos y Comandos de GIT con GitHub*

## INDICE
* [Configuracion de GIT](#confiGit)
* [Comandos Basicos](#comandosBasicos)
* [Ignorar Archivos](#ignore)
* [Ramas](#ramas)
* [Funciones de GIT](#funcionesGit)
* [Git Stash](#stash)
* [Repositorios Remotos](#reposRemotos)
* [Comandos Extras](#comandosExtras)
* [Informacion Adicional](#infoAdicional)
* [Enlaces Informativos](#linksInfo)
* [Referencias 📚](#referencias)

---
---

1. <h3 id="confiGit">Configuracion de GIT</h3>

* Configurar nombre: git config --global user.name "" 

* Configurar correo: git config --global user.email 

* Configurar editor de codigo: git config --global core.editor "code --wait"

* Configurar saltos de linea: git config --global core.autocrlf (true(Windows), input(Mac o Linux))

* Ver la configuracion: git config --global -e

* Ver toda la configuracion disponible de git: git config -h

---
---

2. <h3 id="comandosBasicos">Comandos Basicos</h3>

#### Carpetas o Directorios

* Listar archivos y carpetas: **ls** o **ls -l** para mas detalles o **ls -a** para ver tambien archivos ocultos

* Saber en que directorio o carpeta se encuentra: **pwd**

* Moverse entre carpetas o directorios: **cd**

* Salir una carpeta o directorio atras: **cd ..**

* Crear carpeta o directorio: mkdir (nombre)

* Crear archivo: touch (nombre + extension) - Se pueden crear mas archivos en una sola linea, separanadolos por espacios

* Eliminar carpeta: rm -r (nombre)

* Eliminar archivo: rm (nombre + extension)

***Eliminar archivo o carpeta y agregar de una vez al stage: Se le agrega 'git' (git rm -r (carpeta) - git rm (archivo))***

* Renombrar archivos o carpetas: mv (before/) (after/)

* Abrir ubicacion actual en el explorador: explorer .

---

#### Repositorios

* Incializar un repositorio local: git init

* Ver estado de los archivos en el repo: git status - Para mas simplicidad de puede agregar **-s**

* Ver mas a detalles los cambios hechos con la version anterior: git diff - Al agregar **--stage** se veran los cambios en la zona

* Agregar archivos a la zona de stage: 
    * Agregar archivo especifico: git add (nombre + extension) - Se puede agregar multiples archivos en una sola linea

    * Agregar archivos de una carpeta o directorio: git add carpeta/

    * Agregar todos los archivos en el repositorio (modificados, nuevos o eliminados): git add .

    * Agregar todos los archivos rastrados, pero no nuevos archivos: git add -u 

    * Agregar archivos segun un patron: git add *.txt

    * Quitar Archivos de la zona de stage: git restore --stage (nombre + extension) - Tambien aplica con varios archivos o patrones

    * Confirmar archivos y crear version: git commit -m ""

    * Ver los commits o versiones: git log - Para mas simplicidad **git log --oneline**. Manera mas grafica **git log --graph**


---
---

3. <h3 id="ignore">Ignorar Archivos</h3> 

* Crear Archivo .gitignore

* Indicar la rutas de los archivos a ignorar o carpetas
    ```
    .env
    carpeta/
    ```

* Ignorar archivos o carpetas donde sea que se creen (este formato ignorara todos los ficheros que tengan ese nombre): 
    ```
    **/style.css
    ```

---
---

4. <h3 id="ramas">Ramas</h3>

    #### Locales

* Listar ramas locales: git branch - Agregar **-v** para ver el ultimo commit de cada rama

* Crear Ramas - Por defecto las ramas se crean a partir de la rama central
    * Crear rama : git branch (nombre)
    * Crear rama y posicionarse en ella: git checkout -b (nombre)

* Renombrar ramas
    * Renombar rama actual: git branch -m (nombre)
    * Renombar rama especifica: git branch -m (before) (after) 

* Eliminar rama: git branch -d (nombre) - Para forzar la eliminacion **-D**

* Cambiar entre ramas: git switch (nombre)

---

#### Remotas

* Listar ramas remotas: git branch -r 

* Subir ramas locales al remoto
    * Subir rama ya creada sin la sincronizacion: git push origin (nombre)
        * Para hacer push en este tipo de ramas: git push origin (nombre)
        * Para hacer pull en este tipo de ramas: git pull origin (nombre)

    * Rama sincronizada
        * Crear rama y pasarse a ella: git checkout -b (nombre)
        * Subir rama sincronizada: git push -u origin (nombre)
        ***No es necesario especificar 'origin' para hacer push o pull***

* Descargar cambios del repo remoto: git fecth origin (nombre) - Si la rama ya esta sincro no es necesario **origin (nombre)**

* Eliminar rama remota: git push origin --delete (nombre) - **Si es necesario 'origin'**

* Pasarse a una rama remota en el repo local:
    * Descargar Cambios: git fetch
    * Cambiar a la rama: git checkout (rama remota)

---

* Listar ramas locales y remotas: git branch -a

* Fusionar ramas: Ubicarse en la rama que va recibir los cambios y lanzar: git merge (nombre de la rama que tiene los cambios)

---
---

5. <h3 id="funcionesGit">Funciones de GIT</h3>

#### Versiones

* ##### Volver a una version anterior 
    * Consultar versiones: git log --oneline

    * Ubicar el hash version a volver: Buscar en la lista la version, una vez ubicada se debe copiar el hash de la version

    * Volver a la version: git checkout (hash de la version)

    * Apuntar el repo a una version especifica: git checkout HEAD 

    * Volver a la version mas reciente: git checkout (nombre de la rama - Ejemplo: git checkout main)

    ***Si se desea volver a una version anterior, se debe asegurar que la version actual este limpia, es decir, que no tenga cambios. Para esto se debe hacer un commit o guardar los cambios temporalmente mediante 'git stash'***
    
---

* ##### Resetear Versiones
    * Volver a una version y eliminar las versiones previas: git reset --hard (hash al que se desa volver)

        > Si el repo local esta vinculado con un repo remoto y se desean subir lo cambios:
            git push origin main --force (Si los repo estan sincro, no es necesario 'origin main')

    * Volver a versiones eliminadas
        * Consultas todas las versiones, tanto eliminadas como existentes: git reflog
        * Ubicar el hash de la version eliminada 
        * Volver a la version eliminada git reset --hard (hash de la version eliminada a volver)

    ***El 'git reset --hard' funciona tanto para delante como para atras***

---
---

6. <h3 id="stash">Git Stash</h3>

***El stash sirve para guardar temporalemnte cambios no confirmados. Esto nos puede servir cuando hacemos cambios de ramas o cambios entre versiones. Un ejemplo podria ser; estoy trabajando en mi rama y el equipo de trabajo me solicita que me vaya a otra rama a solucionar algo, pero resulta que en la rama donde estoy trabajando hay codigo incompleto y no puedo confirmar aun, y si hago switch puede que pierda lo que tenga en mi rama, ahi es cuando entra el stash, que nos permite guardar estos cambios de manera temporal sin confirmar ni nd***

* Crear Stash (Guarda todos los cambios no confirmados y restaura tu directorio al último commit limpio): git stash

* Listar los Stash: git stash list 

* Aplicar el stash mas reciente: git stash apply

* Aplicar stash especifico: git stash apply stash@{1} -> Indice del stash

* Eliminar Stash aplicado: git stash drop

* Combinar la aplicacion del Stash y eliminacion (Recomenado usar este): git stash pop

* Eliminar todos los Stash: git stash clear

---

* Comandos Avanzados
    * Guardar archivos no rastreados: git stash -u

    * Tambien guardar archivos ignorados: git stash -a

    * Nombrar Stash: git stash save "Cambios en el sistema de login"

    * Inspeccionar el contenido de un Stash: git stash show -p stash@{0}

    * Crear una rama desde un Stash: git stash branch nueva-rama stash@{0}

***No siempre de debe usar el Stash, solo en casos muy especificos, es mejor siempre confirmar los cambios***

---
---

7. <h3 id="reposRemotos">Repositorios Remotos</h3>

#### Crear un repositorio local y vincularlo con un remoto

* Inicializar repo local: git init

* Crear la version: git commit -m "Primer Commit"

* Cambiar el nombre de la rama actual: git branch -M main

* Conectar al remoto: git remote add origin URL-del-repositorio (HTPPS O SHH)

* Comprobar conexion con el remoto: git remote show origin 

* Sincronizar repos: git push -u origin main

---

#### Vincular repo remoto a un repo local existente

* Conectar al remoto: git remote add origin URL-del-repositorio (HTPPS O SHH)

* Comprobar conexion con el remoto: git remote show origin 

* Cambiar el nombre de la rama actual: git branch -M main

* Sincronizar repos: git push -u origin main

---

#### Clonar Repositorio Limitado

***Los siguiente comandos ayudaran a ahorrar tiempo y espacio a la hora de clonar repos***

* Clonar con el ultimo commit: git clone --depth 1 URL-del-repositorio (HTPPS O SHH)

* Clonar con más commits recientes: git clone --depth # URL-del-repo (HTPPS O SHH)

> Estos comando clonaran la rama prederteminada de los repos (main). Para clonar o descargar otras ramas diferentes se puede hacer lo siguiente:

* Clonar una rama específica: git clone --depth 1 --branch nombre-de-la-rama URL-del-repo

* Descargar una rama limitada de un repo ya clonado:
    * Descargar cambios limitados: git fetch --depth 1
    * Ver la ramas remotas disponibles: git branch -r
    * Pasarse a la rama: git checkout (rama remota)

* Obtener Repositorio Completo:
    * git fetch --unshallow
    * git fecth --all

---

#### Forks
* Bifurcaciones

* Contribucciones

* Pull Requets (PR)

* Resolver conflictos de PR directamente en github

---
---

<h3 id="comandosExtras">Comandos Extras</h3>

* Ver contenido de archivos: cat (nombre + extension)

* Agregar una alias a un comando: git config --global alias.(nombre alias) "comando"
    * Ejemplo: git config --global alias.tree "log --graph"
    * Uso: git tree

* Tags: Los tags son etiquetas caracteristicas que se le agregan a versiones importantes, como la primera version de un programa.
    * Agregar Tag: git tag (nombre) - Para buenas practicas los tag siempre van en minusculas y raya al piso
    * Listar Tags: git tag 
    * Moverse entre Tags: git checkout tags/(nombre)

---
---

<h3 id="infoAdicional">Informacion Adicional</h3>

* ### Herramienta Grafica Ideal
    > ***GitKraken***

---

* ### Flujo de Trabajo Git Flow:
    * Main: Rama de versionamiento

    * Develop: Rama de desarrollo del codigo fuente

    * Features: Rama en la que se desarlloran diferentes caracteristicas o funciones que luego iran a la rama Develop

    * Release: Rama que comunica Main como Develop para fusionar 

    * Hot Fix: Rama que se encargar de resolver issues en produccion

---

* ### Comandos :disappointed_relieved: :trollface:
    * Traer un commit especifico e implementarlo en la rama deseada: git cherry-pick 

    * Traer una rama y fusionarla con otra rama (Se usa comunmente con la rama central): git rebase

---
---

<h3 id="linksInfo">Enlaces Informativos</h3>

* ### Comandos Basicos de Git
    > [Comandos de Git](https://training.github.com/downloads/es_ES/github-git-cheat-sheet/ "Comandos")

* ### Documentacion de Git Flow 
    > [Git FLow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow "Git Flow")

---
---

<h3 id="referencias">Referencias 📚</h3>

Video Tutoriales y Canales de donde obtuve la información:

1. [Curso de GIT y GITHUB desde CERO para PRINCIPIANTES](https://www.youtube.com/watch?v=3GymExBkKjE&t=14725s "Tutorial") - MoureDev by Brais Moure
2. [Aprende GIT ahora! curso completo GRATIS desde cero](https://www.youtube.com/watch?v=VdGzPZ31ts8&t=3392s) - HolaMundo
3. [Curso de GIT y GITHUB DESDE CERO Para Aportar a Proyectos](https://www.youtube.com/watch?v=qdec2M4NwT0&list=PLNfAFIq5pE5UNS6HWrfB44vha8Gfje5wq&index=2) - midulive
4. ***TheHarryCode***
5. ***Reliquias del Software***
5. ***EDteam***
