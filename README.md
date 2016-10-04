11) Deshacer el último commit (perdiendo los cambios realizados en el working copy)

 **¿Qué comando utilizaste en el paso 11? ¿Por qué?**

`git reset --hard HEAD~1`

La *Figura 1.1* muestra que estábamos en el segundo commit y hemos vuelto al commit inicial:

![Figura 1.1](http://i.imgur.com/jsI28To.png)
*Figura 1.1*

También podría haberse hecho un:

`git log`

Para saber el hash del primer commit y después hacer:

`git reset --hard hashDelCommit`

Donde hash es el hash obtenido en git log, que en nuestro caso sería:

`git reset --hard 14f3040426039532a754c90ba2746ea15b9fc8b0`

Debe ser --hard para que nuestra “working copy” se vea modificada, de lo contrario no perderíamos los cambios que realizamos en el segundo commit y al realizar un git status nos diría que el archivo git-nuestro.md ha sido modificado.


----------


12) Rehacer el último commit (el que acabamos de deshacer)

**¿Qué comando o comandos utilizaste en el paso 12? ¿Por qué?**

Puesto que ya no tenemos acceso al commit que hemos deshecho con git log, pero sigue existiendo, buscaremos su hash en el historial con:

`git reflog`

Que en nuestro caso nos devuelve la imagen de la *Figura 1.2*:

![Figura 1.2](http://i.imgur.com/aTNTP8S.png)
*Figura 1.2*

Y, una vez localizado el hash donde hacíamos el segundo commit, que en nuestro caso es cd9f24e:

`git reset --hard cd9f24e`

Que también debería ser - -hard para hacer que nuestro git-nuestro.md quede con los cambios del segundo commit.
El resultado sería el mostrado en la *Figura 1.3*:

![Figura 1.3](http://i.imgur.com/jCdCDTm.png)
*Figura 1.3*


----------


13) Hacer un merge con ‘master’ (styled absorbe a master)

**El merge del paso 13, ¿Causó algún conflicto? ¿Por qué?**

En este caso realizar un merge no genera ningún conflicto y directamente no hace nada, simplemente dice “Already up-to-date” porque, aunque hay dos ramas, ambas forman una lista y *styled* está por encima de *master*, como se muestra en la *Figura 1.4*:

![Figura 1.4](http://i.imgur.com/NPeHPYj.png)
*Figura 1.4*

Se ve que el grafo no se ha bifurcado en ningún momento y que *styled* tiene acceso a todos los commits.


----------


19) Hacer un merge de “htmlify” en “styled” (styled absorbe a htmlify)

**El merge del paso 19, ¿Causó algún conflicto? ¿Por qué?** 

El merge genera conflicto,  tal y como se muestra en la *Figura 1.5*, ya que el archivo git-nuestro.md ha sido modificado en las mismas líneas en ambas ramas.

![Figura 1.5](http://i.imgur.com/lge4Kzg.png)
*Figura 1.5*


----------


21) Desde “master”, hacer un merge con “styled”

**El merge del paso 21, ¿Causó algún conflicto? ¿Por qué?** 

Hacer un merge de la rama styled con master no genera ningún conflicto ya que se realiza Fast-forward porque ambas ramas forman una lista y solo hay que mover el puntero de la rama *master* a donde está la rama *styled*. El resultado se muestra en la *Figura 1.6*.

![Figura 1.6](http://i.imgur.com/Pi4SoE2.png)
*Figura 1.6*


----------


25) Dibujar el diagrama 

**¿Qué comando o comandos utilizaste en el paso 25?** 

Utilizamos el comando:

`git log --graph`

Aunque en nuestro caso mostramos más información también con - -decorate tal y como se muestra en la *Figura 1.7*.

![Figura 1.7](http://i.imgur.com/BhJEfq8.png)
*Figura 1.7*


----------


26) Hacer un merge “no fast-forward” de “title” en “master” (master absorbe a title)

**El merge del paso 26, ¿Podría ser fast forward? ¿Por qué?**

Hemos forzado que sea no fast-forward con el comando:

`git merge - -no-ff title`

Si no hubiéramos puesto - -no-ff hubiera sido fast forward ya que la rama *title* y la rama *master* formaban una lista y tan solo se hubiera realizado la acción de mover el puntero de *master* a *title*.

Por ello hemos generado un nuevo commit que nos hace tener el grafo tal y como muestra la *Figura 1.8*:

![Figura 1.8](http://i.imgur.com/wvDewPv.png)
*Figura 1.8*


----------


27) Deshacer el merge (sin perder los cambios del working copy) 

**¿Qué comando o comandos utilizaste en el paso 27?**

Utilizamos el comando:

`git reset HEAD~1`

Esta vez no es necesario --hard ya que queremos preservar el estado de nuestra working copy.


----------


28) Descartar los cambios 

**¿Qué comando o comandos utilizaste en el paso 28?**

Descartamos los cambios con el comando:

`git checkout - - git-nuestro.md`


----------


29) Eliminar la rama “title” 

**¿Qué comando o comandos utilizaste en el paso 29?**

Eliminamos la rama title utilizando el comando:

`git branch -D title`

Podríamos intentar hacerlo con el comando:

`git branch -d title`

Pero no nos funcionaría ya que nos diría que la rama no ha sido totalmente *mergeada* tal y como se muestra en la *Figura 1.9*:

![Figura 1.9](http://i.imgur.com/4LNwtWG.png)
*Figura 1.9*


----------

**30) Rehacer el merge que hemos deshecho**

¿Qué comando o comandos utilizaste en el paso 30?

Puesto que hemos eliminado la rama con la que mergeamos y estamos por debajo del commit al que nos interesaría volver, necesitamos saber el hash del commit en el que se hizo el merge para poder volver a él con un git reset - -hard.
Por lo que primero necesitaremos un git reflog y para después realizar el git reset - -hard.
De esta manera nos moveremos al commit donde mergeamos *master* con *title*.

También podríamos realizar lo mismo de una forma un poco más “sucia” que consistiría en localizar el commit de la modificación que se hizo en title, situarnos en él, crear la rama title en ese punto, volver a master y volver a realizar el merge.
Sin embargo esta opción, aunque válida, no deja de ser más sucia ya que, aunque uno no se viera, tendríamos dos commit de merge de la rama *master* con la rama *title*.

En la *Figura 1.10* se muestran los pasos que hemos se han realizado:

![Figura 1.10](http://i.imgur.com/TBHhOj2.png)
*Figura 1.10*

Y podemos ver que hemos vuelto a donde queríamos con un:

`git log --graph --decorate`

Que se muestra en la *Figura 1.11* donde, además, vemos que la rama title no está:

![Figura 1.11](http://i.imgur.com/0txbR3c.png)
*Figura 1.11*


----------


32) Volver al commit inicial cuando se creó el poema 

**¿Qué comando o comandos usaste en el paso 32?**

Sirve con un:

`git log`

Para saber el hash del commit inicial y posteriormente un:

`git reset --hard hashDelCommitInicial`


----------


33) Volver al estado final, cuando pusimos título al poema

**¿Qué comando o comandos usaste en el punto 33?**

Como no vemos los commits necesitamos un:

`git reflog`

Y posteriormente realizar otra vez un:

`git reset --hard hashDelCommitFinal`

Los puntos 32 y 33 podrían haberse hecho perfectamente sin --hard ya que al volver al commit inicial sin hard se nos habrían quedado los archivos como en el último commit al que después volvemos en el punto 33 y tampoco necesitaríamos hard.

PD (leer aporta poco): Soy medio tonto y cuando se pide crear tags me he puesto a crear ramas hasta que me he dado cuenta xD por lo que en el reflog se verán unos checkouts duplicados porque la primera vez me he ido a crear ramas, luego las he eliminado y después he tenido que volver para crear los tags. Pero no hay ningún lío con esto, las diferencias entre rama y tag son claras, simplemente me ha dado una pájara.

