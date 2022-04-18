# git-essentials / Git for everybody
Este curso se va a eneseña como usar el GIT

git config --global user.name "Carlos Oliveira"
git config --global user.email "cdoliveirar@gmail.com"
cat ~/.gitconfig

ssh-keygen -o

ver commits, history
------------
git log

importante saber
---------------
unstaged work
stage work
commit work
push work

El comando mas usado
--------------------
git status


## Unstaging a file: 

no usar en fichero borrados!!
devolver a Unstaging
git restore --staged first-push.txt


devolverlo a unstaging
git reset sample.txt



## Undeleting a file

Restaurar un archivo borrado que esta stage, y antes de hacer commit
git restore first-push.txt       (new)
git checkout -- first-push.txt   (old)



## Git origins and remotes

git remote -v
origin  https://github.com/cdoliveirar/git-essentials.git (fetch) # de donde trata de bajar los updates a la computadora
origin  https://github.com/cdoliveirar/git-essentials.git (push) # push de la computadora a github


## Git branching

git checkout -b new-branc
git branch
git checkout master


## Committing to a new branch

git push  origin new-branch


## Merging a branch into master

primero bajamos el ultimo cambio de master !!!
git pull origin master
git merge new-branch



## Seeing your Git history

git log
git log --oneline
git log --oneline --graph --decorate --all    ** ver como arbol


## Downloading updates from GitHub

git pull origin master
si hay cambios en el repositorio github no podras hacer el : git push origin master
muestra el siguiente mensaje:

git push origin master
To https://github.com/cdoliveirar/git-essentials.git
 ! [rejected]        master -> master (fetch first)
error: failed to push some refs to 'https://github.com/cdoliveirar/git-essentials.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.

git pull origin master  # crea un merge.
git push  origin master # listo

## How to get updates from GitHub

se ha cambiado el nombre de un fichero y se modificó su contenido.

Baja los cambios pero NO SE APLICA en el codigo aun con, fetch
git fetch origin master   
ver los cambios: git log --oneline --graph --decorate --all

* 9c1d8d0 (origin/master) updated the empty file to not be empty anymore
*   64fc4c1 (HEAD -> master) Merge branch 'master' of https://github.com/cdoliveirar/git-essentials  
|\
| * cb03d49 updated new-branch-file.txt
* | 74fff34 agraga un nuevo archivo vacio
|/
* dc7464b updated README.md
* 4c90cbb (origin/new-branch, new-branch) new branch file
* 66a6ae6 segundo cambio al fichero
* 6c6b4c8 mofificanco el fichero
* db7cf15 Primer push oficial
* d189f48 first commit

luego se ejecuta el comando pull para obtener el mismo valor de github
git pull origin master

* 9c1d8d0 (HEAD -> master, origin/master) updated the empty file to not be empty anymore
*   64fc4c1 Merge branch 'master' of https://github.com/cdoliveirar/git-essentials
|\
| * cb03d49 updated new-branch-file.txt
* | 74fff34 agraga un nuevo archivo vacio
|/
* dc7464b updated README.md
* 4c90cbb (origin/new-branch, new-branch) new branch file
* 66a6ae6 segundo cambio al fichero
* 6c6b4c8 mofificanco el fichero
* db7cf15 Primer push oficial
* d189f48 first commit

digamos que git pull es igual que 
git fetch origin master && git merge origin/master


## Checkout: code-time travel

checkout algun commit anterior.
git checkout d189f48bf338149f11f6ccdd50ae3c2d7833b104     **** You are in 'detached HEAD' state.  
git checkout -b timewarp-branch
luego se crea un fichero: timewarp.txt en ese branch y se hace un merge con master.
$ git merge timewarp-branch
Merge made by the 'ort' strategy.
 timewarp.txt | 0
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 timewarp.txt

terminar!
git push origin master


## README.md files

explicar hacerca el readme file: mark down


## Viewing file differences

git diff filename.txt



## How to ignore files

agrega el archivo .gitignore
y hacer pruebas con ficheros .algo



## Create a custom Git alias

nano ~/.gitconfig

[user]
        name = Carlos Oliveira
        email = cdoliveirar@gmail.com
[alias]
		lg = log --oneline --graph --decorate --all



## Fixing Git commit messages

git commit --amend
una ves corregido el comentario se procede con el push



## How to fork a repo

mostrar como hacer el forking de otros repositorios hacia tu repo.


## Git issues

Se puede crear un issue usando la interface de github/gitlab,
comentar issues, asignar issues, cerrar issues. agragar un #1 para ver en enlace.


## How to open a pull request

Create a Pull Request por la interface, si esta como: Able to merge, entonces crear el PR
Se puede crear un PR o un Draff PR (se crear con esta opción)

Borrar un branch local
---
git branch -d pr-test



## Undoing a commit

con el comando: hard

cuando estas en un branch equivocado y deseas deshacer un commit
creamos un archivos sample.txt, add y comiteamos.
git log --oneline

eace26b (HEAD -> master) deshacer este commit por favor  #### este es el commit que deseamos eliminar
5c7767f (origin/master) Merge pull request #2 from cdoliveirar/pr-test
b2ec639 (origin/pr-test) actualiza el readme...
66d0da3 A typo here (typo in commit message was fixed)
327db84 ignorar ficheros
74d6c91 Merge branch 'timewarp-branch'
99bcf31 (origin/timewarp-branch, timewarp-branch) timewarp

git reset --hard 5c7767f  (este comando elimina el commit eace26b con todo su contenido como el fichero sample.txt y regresamos al commit 5c7767f (origin/master) )

con el comando: soft

creamos otro fichero sample.txt, add y commiteamos 
git reset --soft origin/master

el fichero sample.txt que se ha creado aun esta en stage y queremos ponerlo a unstaged
git reset sample.txt
revisa el archivo y lo eliminas
rm sample.txt



## Force pushing

crea archivo undo-me.txt y push a github, en LOCAL regresar al penultimo commit con reset --hard a 5c7767f

* 6859adc (HEAD -> master, origin/master) Elmina este commit de github
*   5c7767f Merge pull request #2 from cdoliveirar/pr-test
|\
| * b2ec639 (origin/pr-test) actualiza el readme...
|/
* 66d0da3 A typo here (typo in commit message was fixed)
* 327db84 ignorar ficheros
*   74d6c91 Merge branch 'timewarp-branch'

luego hacer un push a master, tenemos el error
git push origin master

To https://github.com/cdoliveirar/git-essentials.git
 ! [rejected]        master -> master (non-fast-forward)
error: failed to push some refs to 'https://github.com/cdoliveirar/git-essentials.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.

como no queremos el ultimo commit en githib le damos el comando force desde local para borrar en github!

git push origin master --force



## How to rebase

se crea un branch : rebase-branch

$ git log --oneline
c0a9949 (HEAD -> rebase-branch) simple rebase
5c7767f (origin/master, master) Merge pull request #2 from cdoliveirar/pr-test
b2ec639 (origin/pr-test) actualiza el readme...
66d0da3 A typo here (typo in commit message was fixed)
327db84 ignorar ficheros
74d6c91 Merge branch 'timewarp-branch'
99bcf31 (origin/timewarp-branch, timewarp-branch) timewarp
9c1d8d0 updated the empty file to not be empty anymore
64fc4c1 Merge branch 'master' of https://github.com/cdoliveirar/git-essentials

* c0a9949 (rebase-branch) simple rebase
*   5c7767f (HEAD -> master, origin/master) Merge pull request #2 from cdoliveirar/pr-test
|\
| * b2ec639 (origin/pr-test) actualiza el readme...
|/
* 66d0da3 A typo here (typo in commit message was fixed)
* 327db84 ignorar ficheros
*   74d6c91 Merge branch 'timewarp-branch'
|\
| * 99bcf31 (origin/timewarp-branch, timewarp-branch) timewarp
* | 9c1d8d0 updated the empty file to not be empty anymore
* |   64fc4c1 Merge branch 'master' of https://github.com/cdoliveirar/git-essentials


retornamos a master git checkout master
git rebase rebase-branch

$ git log --oneline
c0a9949 (HEAD -> master, rebase-branch) simple rebase                     **** se realiz+o el rebase
5c7767f (origin/master) Merge pull request #2 from cdoliveirar/pr-test
b2ec639 (origin/pr-test) actualiza el readme...
66d0da3 A typo here (typo in commit message was fixed)
327db84 ignorar ficheros
74d6c91 Merge branch 'timewarp-branch'
99bcf31 (origin/timewarp-branch, timewarp-branch) timewarp
9c1d8d0 updated the empty file to not be empty anymore
64fc4c1 Merge branch 'master' of https://github.com/cdoliveirar/git-essentials

* c0a9949 (HEAD -> master, rebase-branch) simple rebase                  **** se realiz+o el rebase
*   5c7767f (origin/master) Merge pull request #2 from cdoliveirar/pr-test
|\
| * b2ec639 (origin/pr-test) actualiza el readme...
|/
* 66d0da3 A typo here (typo in commit message was fixed)
* 327db84 ignorar ficheros
*   74d6c91 Merge branch 'timewarp-branch'
|\
| * 99bcf31 (origin/timewarp-branch, timewarp-branch) timewarp
* | 9c1d8d0 updated the empty file to not be empty anymore
* |   64fc4c1 Merge branch 'master' of https://github.com/cdoliveirar/git-essentials


tambien se puede usar un merge en vez de un rebase.

git push origin master



## Resolving merge and rebase conflicts

crea un fichero en github, se crea otro fichero localmente.
git push origin master

 ! [rejected]        master -> master (fetch first)
error: failed to push some refs to 'https://github.com/cdoliveirar/git-essentials.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally.

realizamos el pull
git pull origin master

remote: Enumerating objects: 9, done.
remote: Counting objects: 100% (9/9), done.
remote: Compressing objects: 100% (8/8), done.
remote: Total 8 (delta 4), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (8/8), 1.87 KiB | 58.00 KiB/s, done.
From https://github.com/cdoliveirar/git-essentials
 * branch            master     -> FETCH_HEAD
   c0a9949..88bc41a  master     -> origin/master
Auto-merging merge-conflict.txt
CONFLICT (add/add): Merge conflict in merge-conflict.txt				**** existe un conflicto.
Automatic merge failed; fix conflicts and then commit the result.

vemos eñl fichero
git diff merge-conflict.txt


  linea 1 por github
  linea 2 por github
++<<<<<<< HEAD
 +linea TRES por github ---> SE EDITA LOCALMENTE.
 +linea 4 por github
 +linea 5 por github
- linea 6 por github
++linea 6 por github
++=======
+ linea 3 por github
+ linea 4 por github
+ linea 5 por github
+ linea 6 por github
+
++>>>>>>> 88bc41ac0c1260233400dae6ee00cbce5958ed19


editamos el fichero para evitar los conflictos
git add merge-conflict.txt
git commit   (sin mensaje)  realizando el MERGE

git push origin master

/* resumen comandos merge conflictos */
resuelve conflictos
git add file
git commit


ahora con REABSE
--- 
crea un fichero: rebase-conflict.txt LOCAL, commitea

412d22b (HEAD -> master) rebase conflict Example
8fca858 (origin/master) Merge branch 'master' of https://github.com/cdoliveirar/git-essentials   *** regresar a esta lina del tiempo con git checkout <ID>
b1582df Merge conflict agregado localmente
88bc41a agrega  merge-conflict.txt file
9b5020d Rename merge-conflicy.txt to merge-conflict.txt
1a0aa10 added merge conflict file
c0a9949 (origin/rebase-branch, rebase-branch) simple rebase
5c7767f Merge pull request #2 from cdoliveirar/pr-test


git checkout 8fca858   *** regresar a esta lina del tiempo con git checkout <ID>

8fca858 (HEAD, origin/master) Merge branch 'master' of https://github.com/cdoliveirar/git-essentials   ***
b1582df Merge conflict agregado localmente
88bc41a agrega  merge-conflict.txt file
9b5020d Rename merge-conflicy.txt to merge-conflict.txt
1a0aa10 added merge conflict file
c0a9949 (origin/rebase-branch, rebase-branch) simple rebase

git checkout -b rebase-conflict-branch
creamos el mismo fichero rebase-conflict.txt en el branch rebase-conflict-branch
y le damos commit.
regresamos a master
git checktout master

git rebase rebase-conflict-branch

Auto-merging rebase-conflict.txt
CONFLICT (add/add): Merge conflict in rebase-conflict.txt
error: could not apply 412d22b... rebase conflict Example

git status

	both added: rebase-conflict.txt   *** both significa que hay que revisar los conflictos en este fichero

git diff
editar el fichero para ver y resolver los conflictos
git diff    ** nuevamente
git add rebase-conflict.txt

NO HACER COMMIT ES UN REBASE
git rebase --continue

/* resumen comandos merge conflictos */
resuelve conflictos
git add file
git rebase --continue




## How to stash code   : revisasr otros casos con STASH comando

create branch stash-example, edita el README.md y los cambios se ve tambien en el master branch
en la rama stash-example ejecutar
git stash
git status   *** no se ve los cambios
git stash list
retornamos a master
git checkout master  *** y vemos que no hay cambios
editamos el fichero README.md
git add y git commit (en master)

regresamos a rama stash-example
git checkout stash-example
git stash list   ** vemos la lista de 
git stash apply  ** aplicamos el cambio que estaba en stash
git stash drop



## Adding tags to your commits

crear un tag:
git tag v0.1
listar tag:
git tag
enviar el tag a github
git push origin v0.1

se puede taggear en diferentes commit tiempo atras
git checkout 9c1d8d0
git tag beta
enviando todos los tags creados:
git push origin --tags

eliminar un tag
git tag -d inicial   
enviando a eliminar en github
git push origin --delete inicial

tambien se puede hacer un checkout al tag
git checkout beta


## anterior
pero eso solo si master esta mas adelantado q tu
en tal caso solo haces
git checkout master
git pull origin master
git checkout tubranch
git merge master

#create new Branch
git checkout -b iss53

# trae todo los branch a local
git fetch --all

ver branch remotos y localles
$ git branch -a

Ver solo ramas remotas
$ git branch -r

ver branch locales
$ git branch -v



## Elminar remote origin

git remote remove origin
Agregar remote origin
git remote add origin https://bitbucket.lima.bcp.com.pe/scm/shared/demo-kotlin.git

 
// delete branch locally
git branch -d localBranchName


Eliminar branch remote
git push origin --delete release/0.0.2

Eliminar un tag
git push origin --delete RC-1.0.0-CERT-20210513183328


 
Listar los tags
git tag -l

 
Eliminar los tags
git tag -d released/aug2002

 
git push --delete origin


desabilitar SSL GIT
git config --global http.sslVerify false



## mover repositorio

git clone --mirror https://avillalobos@mycompany.com/repoAAA.git
cd repoAAA
git branch -a
git tag
git remote -v
git remote rm origin
git remote add origin https://avillalobos@mycompany.com/newrepo.git
git remote -v
Enviar los datos de nuestro repositorio local al nuevo repositorio remoto
git push origin --all
git push origin --tags
