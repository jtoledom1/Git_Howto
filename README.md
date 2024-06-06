# Git_Howto
Guia primeros pasos usando git y github
## Índice

1. [Configuración inicial](#configuración-inicial)
2. [Merge](#merge)
3. [Stash](#stash)
4. [Git Alias](#git-alias)
5. [Git Tag](#git-tag)
6. [Git remote método SSH](#git-remote-método-ssh)
7. [Fork y Pull Request](#fork-y-pull-request)
   
## Configuración inicial

Configura tu nombre de usuario:

```bash
git config --global user.name "USER"
```

Configura tu correo electrónico:

```bash
git config --global user.email USER@example.com
```
### Cambiar la branch en la que estamos trabajando:

Sólo si es por primera vez, ya que este cómando la creará y te moverá a ella

```bash
git branch -m main
```
Sí tenemos una rama ya creada el comando para movernos a esa rama será el siguiente:

```bash
git checkout main
```


### Obtener información acerca del estado

```bash
git status
```

### Añadir elementos para entrar en la snapshoot

```bash
git add NOMBRE_ARCHIVO
```

También puedes usar un punto al final para indicar que se añada todo lo que se tenga que añadir, especialmente si son varios ficheros:

```bash
git add .
```

### Realizar un commit (snapshoot)

De esta forma se nos abrirá un vim donde manualmente tendremos que ingresar el comentario:

```bash
git commit
```

Realizar commit de forma corta (No olvidar las comillas dobles):

```bash
git commit -m "COMENTARIO"
```

*NOTA IMPORTANTE*: Cada vez que quieras realizar un commit, debes añadir elementos a la snapshoot usando `git add`.

### Volver a la anterior versión guardada

```bash
git checkout HASH_COMMIT -- NOMBRE_ARCHIVO
```

### Para ver la lista de nuestros cambios, podremos usar los siguientes comandos

- `git log` (Versión extendida)
- `git log --graph` (Versión extendida tipo línea vertical de los cambios)
- `git log --graph --pretty=oneline` (Versión resumida del commit, incluye hash completo y el comentario)
- `git log --graph --decorate --all --oneline` (Versión resumida del commit, incluye hash RESUMIDO y el comentario)

### Git reset

- `git reset` (Borra lo que hay después de la ÚLTIMA snapshot)
- `git reset --hard HASH` (Borra lo que hay después de la snapshot que especifiquemos)
- `git reflog` (Te da un historial de los cambios)

Para deshacer el `--hard`, entra a `reflog` para ver el hash y con un `checkout` te puedes regresar a una snapshot anterior.

### Crear un método abreviado para los comandos

```bash
git config --global alias.NOMBREDELALIAS "log --graph --decorate --all --oneline"
```

De esta manera, cada vez que llamemos al alias, se estará ejecutando dicho comando, por ejemplo:

```bash
git NOMBREDELALIAS
```

### Saber si se han realizado cambios, y te dice qué cambios fueron

```bash
git diff
```


## Git Alias

La versión corta de uno o varios comandos:

```bash
git config --global alias.<nombre_del_alias> '!comando1 && comando2'
```

Por ejemplo, para crear un alias llamado "superpush" que haga un pull de la rama main desde el origen y luego haga push a la misma rama en el origen, puedes usar:

```bash
git config --global alias.superpush 'pull origin main && push -u origin main'
```

## Git Tag

*Usar snake_case*

Etiquetar una versión:

```bash
git tag "nombre_1"
```

Moverse a un tag:

```bash
git checkout tags/clase_1
```

## Git Branches 

Se usan para agregar características sin modificar la rama principal

Para crear una nueva rama y agregar características sin modificar la rama principal:

```bash
git branch NOMBRE
```

Para cambiar a una rama específica:

```bash
git switch NOMBRE
```

## MERGE

Traer a la rama actual los cambios generados en la rama main:

```bash
git merge main
```

Si se toca la misma línea de código del mismo archivo, se genera un CONFLICTO, y te muestra las dos posibilidades: el cambio actual y el entrante.

Para saber si tenemos conflictos antes de hacer el merge, usaremos un comando visto previamente:

```bash
git diff RAMA
```

Anteriormente se había usado para comparar archivos, pero también sirve para comparar ramas.

## STASH

Hacer un commit de manera temporal que queda guardado en el host local y no se ve reflejado en el árbol general:

```bash
git stash
```

Listar los stashed:

```bash
git stash list
```

Recuperar el stash:

```bash
git stash pop
```

Al momento de usar `git stash pop`, recuperas la información pero aún no está en el árbol, lo que significa que si te tienes que cambiar de rama, tendrías que repetir los pasos: darle `git stash` y cuando regreses a la rama en la que estabas, volver a hacer `git stash pop`. Es importante mencionar que se puede realizar el comando anterior desde una rama diferente a la que se generó y Git lo interpretará como un merge.

Borrar la información guardada en el stash:

```bash
git stash drop
```

## Eliminar ramas

Se pueden eliminar conforme las ramas pierdan su utilidad, es decir, cuando los cambios ya están unificados con la rama principal.

```bash
git branch -d RAMA
```
Aquí está la documentación Markdown actualizada:

## Agregar características sin modificar la rama principal

Se utilizan las ramas para agregar características sin modificar la rama principal.

### Crear una nueva rama

Para crear una nueva rama y agregar características sin modificar la rama principal, se utiliza el siguiente comando:

```bash
git branch NOMBRE
```

## Cambiar a una rama específica

Para cambiar a una rama específica, se utiliza el siguiente comando:

```bash
git switch NOMBRE
```
## Git remote método SSH

### Iniciar con un repositorio existente y combinar los avances en local con GitHub:

1. Agregar el origen remoto al repositorio local:

```bash
git remote add origin git@github.com:USER/Git_Howto.git
```

2. Agregar los archivos modificados al área de preparación:

```bash
git add .
```

3. Realizar un commit con un mensaje descriptivo:

```bash
git commit -m "Mensaje de commit"
```

4. Traer los cambios remotos y fusionarlos con los locales:

```bash
git pull origin main --allow-unrelated-histories
```

5. Configurar la opción de rebase para futuros pull:

```bash
git config pull.rebase false
```

(se recomienda usar esta solo al principio)

6. Empujar los cambios locales al repositorio remoto:

```bash
git push -u origin master
```

### Empezar a trabajar desde cero con un repositorio ya existente:

Para comenzar a trabajar desde cero con un repositorio existente, simplemente clónalo dentro de la carpeta donde deseas almacenar tu repositorio local:

```bash
git clone git@github.com:USER/Git_Howto.git
```

### Realizar commit y push:

Cada vez que desees hacer un commit y push, sigue estos pasos:

1. Agregar los archivos modificados al área de preparación:

```bash
git add .
```

2. Realizar un commit con un mensaje descriptivo:

```bash
git commit -m "MENSAJE"
```

3. Traer los cambios remotos y fusionarlos con los locales:

```bash
git pull origin main
```

4. Empujar los cambios locales al repositorio remoto:

```bash
git push -u origin main
```

## FORK y PULL REQUEST

### Hacer un fork del repositorio

1. Dirígete al repositorio en GitHub que deseas hacer fork.
2. Haz clic en el botón "Fork" en la esquina superior derecha de la página.
3. Selecciona tu cuenta como destino para el fork.

### Clonar el repositorio forked

Una vez que hayas hecho el fork, clona el repositorio a tu máquina local:

```bash
git clone URL_DEL_REPOSITORIO_FORKED
```

### Realizar cambios y subirlos al repositorio clonado

1. Haz los cambios necesarios en los archivos clonados.
2. Agrega los archivos modificados al área de preparación:

```bash
git add .
```

3. Realiza un commit con un mensaje descriptivo:

```bash
git commit -m "Descripción de los cambios"
```

4. Empuja los cambios al repositorio forked en GitHub:

```bash
git push origin NOMBRE_DE_LA_RAM
```

### Crear una pull request

1. Ve al repositorio forked en GitHub.
2. Haz clic en el botón "Pull Request" (Solicitud de extracción) en la parte superior.
3. Completa la información necesaria para la pull request, como una descripción detallada de los cambios realizados.
4. Haz clic en "Crear pull request" para enviar la solicitud al repositorio original.

¡Listo! Has hecho un fork de un repositorio, clonado el fork, realizado cambios y enviado una pull request al repositorio original.

<a href="https://github.com/jtoledom1/Git_Howto/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=jtoledom1/Git_Howto" />
</a>

Made with [contrib.rocks](https://contrib.rocks).
