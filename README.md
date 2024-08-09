# Git_Howto--->Español
Guia primeros pasos usando git y github
aaaaaaa
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

*NOTA IMPORTANTE*: Cada vez que quieras realizar un commit, debes añadir elementos a la snapshoot usando `git add .`

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
**Sobre las Frases de Contraseña para Claves SSH**

Puedes acceder y escribir datos en los repositorios de GitHub.com utilizando el protocolo Secure Shell (SSH). Al conectarte a través de SSH, la autenticación se realiza mediante un archivo de clave privada en tu equipo local. Para obtener más información, consulta "Acerca de SSH".

Al generar una clave SSH, tienes la opción de agregar una frase de contraseña para aumentar la seguridad de la clave. Cada vez que utilices la clave, deberás ingresar la frase de contraseña correspondiente. Si deseas evitar escribir la frase de contraseña cada vez que uses la clave, puedes agregarla al agente SSH. El agente SSH se encargará de administrar las claves SSH y recordar la frase de contraseña asociada.

Si aún no tienes una clave SSH, es necesario generar una nueva para utilizarla en la autenticación. Si no estás seguro de si ya tienes una clave SSH, puedes verificar la existencia de claves existentes. Para obtener más información, consulta "Comprobación de tus claves SSH existentes".

Si deseas autenticarte en GitHub utilizando una llave de seguridad de hardware, necesitarás generar una nueva clave SSH específicamente para esto. Deberás conectar tu llave de seguridad de hardware a tu computadora cuando te autentiques utilizando el par de claves. Para obtener más detalles, consulta las notas de la versión de OpenSSH 8.2.

**Generación de una Nueva Clave SSH**

Puedes generar una nueva clave SSH en tu equipo local. Después de generar la clave, puedes agregar la clave pública a tu cuenta en GitHub.com para habilitar la autenticación para las operaciones de Git a través de SSH.

Nota: A partir del 15 de marzo de 2022, GitHub ha mejorado la seguridad eliminando los tipos de clave antiguos y no seguros.

A partir de esta fecha, las claves DSA (ssh-dss) ya no son compatibles. No podrás agregar nuevas claves DSA a tu cuenta personal en GitHub.com.

Las claves RSA (ssh-rsa) con una fecha de validez anterior al 2 de noviembre de 2021 pueden seguir utilizando cualquier algoritmo de firma. Sin embargo, las claves RSA generadas después de esta fecha deben utilizar un algoritmo de firma del tipo SHA-2. Es posible que algunos clientes más antiguos necesiten actualizarse para admitir firmas del tipo SHA-2.

<details>
  <summary>Linux</summary>
Aquí está la documentación para generar y agregar una clave SSH, adaptada para el uso en la Terminal:

---

**Generar y Agregar una Clave SSH a tu Cuenta de GitHub**

**Paso 1: Generar una Clave SSH**

1. Abre Terminal.

2. Pega el siguiente texto, reemplazando "tu_correo_electronico@example.com" con tu dirección de correo electrónico de GitHub:

```bash
ssh-keygen -t ed25519 -C "tu_correo_electronico@example.com"
```

Nota: Si estás utilizando un sistema heredado que no admite el algoritmo Ed25519, usa el siguiente comando:

```bash
ssh-keygen -t rsa -b 4096 -C "tu_correo_electronico@example.com"
```

3. Cuando se te solicite, presiona Enter para aceptar la ubicación de archivo predeterminada.

4. Luego, ingresa una frase de contraseña segura cuando se te solicite.

**Paso 2: Agregar tu Clave SSH al ssh-agent**

1. Antes de agregar una nueva clave SSH al ssh-agent, verifica si ya tienes claves SSH existentes y has generado una nueva clave SSH.

2. Inicia el agente SSH en segundo plano ejecutando el siguiente comando en la Terminal:

```bash
eval "$(ssh-agent -s)"
```

Dependiendo de tu entorno, es posible que necesites usar un comando diferente. Por ejemplo, podrías necesitar usar sudo -s -H antes de iniciar ssh-agent si estás usando macOS Sierra 10.12.2 o una versión posterior.

3. Agrega tu clave privada SSH al ssh-agent ejecutando el siguiente comando en la Terminal:

```bash
ssh-add ~/.ssh/id_ed25519
```

Nota: Si has creado tu clave con otro nombre, reemplaza "id_ed25519" en el comando con el nombre de tu archivo de clave privada.

**Paso 3: Agregar la Clave Pública SSH a tu Cuenta de GitHub**

1. Copia la clave pública SSH ejecutando el siguiente comando en la Terminal:

```bash
pbcopy < ~/.ssh/id_ed25519.pub
```

2. Ve a tu cuenta de GitHub y haz clic en tu foto de perfil.

3. Selecciona "Settings" (Configuración) en el menú desplegable.

4. En el panel lateral izquierdo, haz clic en "SSH and GPG keys" (Claves SSH y GPG).

5. Haz clic en "New SSH key" (Nueva clave SSH).

6. En el campo "Title" (Título), pega un nombre descriptivo para tu clave SSH.

7. En el campo "Key" (Clave), pega la clave pública SSH que copiaste anteriormente.

8. Haz clic en "Add SSH key" (Agregar clave SSH).
  

</details>

<details>
  <summary>Windows</summary>
  
**Para generar una nueva clave SSH:**

1. Abre Git Bash.

2. Copia y pega el siguiente texto, asegurándote de reemplazar "your_email@example.com" con tu dirección de correo electrónico de GitHub:

```bash
ssh-keygen -t ed25519 -C "tu_correo_electronico@example.com"
```

Si estás utilizando un sistema heredado que no admite el algoritmo Ed25519, utiliza el siguiente comando:

```bash
ssh-keygen -t rsa -b 4096 -C "tu_correo_electronico@example.com"
```

Esto generará una nueva clave SSH utilizando la dirección de correo electrónico proporcionada como etiqueta.

Cuando se te solicite, presiona Enter para aceptar la ubicación de archivo predeterminada. Si ya has creado claves SSH anteriormente, es posible que ssh-keygen te pida que especifiques un nombre de archivo para la nueva clave. En este caso, se recomienda utilizar un nombre de archivo personalizado en lugar de aceptar la ubicación de archivo predeterminada. Para hacerlo, ingresa la ubicación de archivo predeterminada y reemplaza "id_ALGORITHM" con el nombre personalizado de la clave.

Cuando se te solicite, ingresa una frase de contraseña segura. Para obtener más información, consulta "Trabajar con contraseñas de clave SSH".

**Agregar tu Clave SSH al ssh-agent**

Antes de agregar una nueva clave SSH al ssh-agent para que administre tus claves, asegúrate de haber verificado la existencia de claves SSH existentes y de haber generado una nueva clave SSH.

Si has instalado GitHub Desktop, puedes utilizarlo para clonar repositorios y evitar la necesidad de utilizar claves SSH.

Para agregar tu clave privada SSH al agente ssh:

1. En una nueva ventana de PowerShell con privilegios de administrador, asegúrate de que el agente ssh esté en funcionamiento. Puedes utilizar las instrucciones de "Auto-lanzamiento ssh-agent" en "Trabajar con contraseñas de clave SSH", o iniciar el agente manualmente con los siguientes comandos:

```powershell
# Inicia el ssh-agent en segundo plano
Get-Service -Name ssh-agent | Set-Service -StartupType Manual
Start-Service ssh-agent
```

2. En una ventana de terminal sin privilegios de administrador, agrega la clave privada SSH al agente ssh. Si has creado tu clave con un nombre diferente o estás agregando una clave existente que tiene un nombre diferente, reemplaza "id_ed25519" en el comando con el nombre de tu archivo de clave privada.

```bash
ssh-add c:/Users/YOU/.ssh/id_ed25519
```

**Agregar una Clave SSH Nueva a tu Cuenta de GitHub**

Para agregar la clave pública SSH a tu cuenta de GitHub, consulta "Agregar una clave SSH nueva a tu cuenta de GitHub".

**Generar una Nueva Clave SSH para una Clave de Seguridad de Hardware**

Si estás utilizando macOS o Linux, es posible que necesites actualizar tu cliente SSH o instalar uno nuevo antes de generar una nueva clave SSH. Para obtener más información, consulta "Error: Tipo de clave desconocido".

Para generar una nueva clave SSH para una clave de seguridad de hardware:

1. Inserta tu clave de seguridad de hardware en tu computadora.

2. Abre Git Bash.

3. Copia y pega el siguiente texto, asegurándote de reemplazar "your_email@example.com" con la dirección de correo electrónico asociada a tu cuenta de GitHub:

```bash
ssh-keygen -t ed25519-sk -C "tu_correo_electronico@example.com"
```

Si recibes un error al ejecutar el comando y ves los errores "invalid format" o "feature not supported", es posible que estés utilizando una clave de seguridad de hardware que no admite el algoritmo Ed25519. En este caso, utiliza el siguiente comando en su lugar:

```bash
ssh-keygen -t ecdsa-sk -C "tu_correo_electronico@example.com"
```

Cuando se te solicite, presiona el botón en tu clave de seguridad de hardware.

Cuando se te solicite "Ingresar un archivo en donde se pueda guardar la llave", presiona Enter para aceptar la ubicación predeterminada.

Cuando se te solicite que ingreses una frase de contraseña, presiona Enter.

---

</details>

<details>
  <summary>MacOS</summary>
  
Aquí tienes la documentación técnica para generar una clave SSH y agregarla a GitHub, adaptada para su uso en la Terminal:

---

**Generar y Agregar una Clave SSH a tu Cuenta de GitHub**

**Paso 1: Generar una Clave SSH**

1. Abre Terminal.

2. Pega el siguiente texto, reemplazando "tu_correo_electronico@example.com" con tu dirección de correo electrónico de GitHub:

```bash
ssh-keygen -t ed25519 -C "tu_correo_electronico@example.com"
```

Nota: Si estás utilizando un sistema heredado que no admite el algoritmo Ed25519, usa el siguiente comando:

```bash
ssh-keygen -t rsa -b 4096 -C "tu_correo_electronico@example.com"
```

3. Cuando se te solicite, presiona Enter para aceptar la ubicación de archivo predeterminada.

4. Luego, ingresa una frase de contraseña segura cuando se te solicite.

**Paso 2: Agregar tu Clave SSH al ssh-agent**

1. Antes de agregar una nueva clave SSH al ssh-agent, verifica si ya tienes claves SSH existentes y has generado una nueva clave SSH.

2. Inicia el agente SSH en segundo plano ejecutando el siguiente comando en la Terminal:

```bash
eval "$(ssh-agent -s)"
```

Dependiendo de tu entorno, es posible que necesites usar un comando diferente. Por ejemplo, podrías necesitar usar sudo -s -H antes de iniciar ssh-agent si estás usando macOS Sierra 10.12.2 o una versión posterior.

3. Si estás utilizando macOS Sierra 10.12.2 o una versión posterior, necesitarás modificar tu archivo ~/.ssh/config para cargar las claves automáticamente en el agente ssh-agent y almacenar las contraseñas en tu cadena de claves.

Primero, verifica si el archivo ~/.ssh/config existe en la ubicación predeterminada ejecutando el siguiente comando en la Terminal:

```bash
open ~/.ssh/config
```

Si el archivo no existe, créalo ejecutando:

```bash
touch ~/.ssh/config
```

Abre el archivo ~/.ssh/config y modifícalo para que contenga las siguientes líneas:

```
Host github.com
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_ed25519
```

Nota: Si decides no agregar una frase de contraseña a la clave, omite la línea UseKeychain.

4. Agrega tu clave privada SSH al ssh-agent y almacena tu contraseña en tu keychain ejecutando el siguiente comando en la Terminal:

```bash
ssh-add --apple-use-keychain ~/.ssh/id_ed25519
```

Nota: Si has creado tu clave con otro nombre, reemplaza "id_ed25519" en el comando con el nombre de tu archivo de clave privada.

**Paso 3: Agregar la Clave Pública SSH a tu Cuenta de GitHub**

1. Copia la clave pública SSH ejecutando el siguiente comando en la Terminal:

```bash
pbcopy < ~/.ssh/id_ed25519.pub
```

Nota: Si has utilizado un nombre diferente para tu clave SSH, reemplaza "id_ed25519.pub" en el comando con el nombre de tu archivo de clave pública.

2. Ve a tu cuenta de GitHub y haz clic en tu foto de perfil.

3. Selecciona "Settings" (Configuración) en el menú desplegable.

4. En el panel lateral izquierdo, haz clic en "SSH and GPG keys" (Claves SSH y GPG).

5. Haz clic en "New SSH key" (Nueva clave SSH).

6. En el campo "Title" (Título), pega un nombre descriptivo para tu clave SSH.

7. En el campo "Key" (Clave), pega la clave pública SSH que copiaste anteriormente.

8. Haz clic en "Add SSH key" (Agregar clave SSH).

</details>

## Trabajo remoto aplicando ssh
<details>
   <summary>Y? </summary>
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
</details>


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
