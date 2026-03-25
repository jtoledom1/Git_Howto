<p align="center">
  <a href="https://github.com/jtoledom1">
  <img src="https://github.com/jtoledom1/Git_Howto/blob/8d4681cd93d95531537ac07e101c7cd0fbc20fae/static/Git%20Github.png" alt="Git_Welcome" width="600"/>
</a>
</p>

Please select for english  
[![Static Badge](https://img.shields.io/badge/Language-EN-7EF12E)](https://github.com/jtoledom1/Git_Howto/blob/21380b9c098f79a271741afb035fbf0b7ef9be47/Readme.md)

<hr></hr>

Bienvenido a este curso para aprender a usar Github, esperamos que te sea de utilidad para empezar a trabajar de manera colaborativa. 


Te brindaremos los recursos necesarios para que puedas empezar sin contratiempos. Diseñamos este curso para que puedas trabajar sin importar tu sistema operativo. Te recomendamos adecuar tu entorno de trabajo acorde a tus necesidades, ya que estaremos trabajando con la terminal del sistema, es recomendable que esta sea un entorno amigable para ti. Por el momento puedes acceder a tutoriales que ha creado la comunidad, y que a su vez han sido probados por nosotros con resultados prometedores. 
  
## Tabla de contenido
- [Generalidades](#generalidades)
- [Primeros pasos](#primeros-pasos)
    - [git](#git)
    - [github](#github)
    - [.gitignore](#gitignore)
- [Integración de Git y Github](#integración-de-git-y-github)
- [Git push](#git-push)
- [Enlaces](#enlaces)


## Generalidades
En virtud de que esta guía sea de rápido acceso en tu día a día excluímos partes que en principio deberías usar sólo una vez. Será necesario que para empezar este curso realices los módulos siguientes, ya que sin ellos no podrás avanzar:

- [configuración inicial de git](Notas%20Separadas/Initial_config)
- [Configuración ssh](Notas%20Separadas/Git_ssh_init.md)
## Primeros pasos
Es importante iniciar este curso sabiendo que git y github son cosas diferentes aunque guardan cierta relación, la cual se profundisará a continuación :
  
### Git
  Sistema de control de versiones ejecutado de manera local, sirve como un historial de cambios, cada "breakpoint" será declarado por el usuario. Para hablar en terminos de git a este se le llamará "commit", y es el mismo que se utilizará en github. Ahora bien, cada commit tendrá una descripción para saber la modificación que se hizo.

  Posteriormente podrás regresar a cualquier punto del desarrollo de tu proyecto.

  > En git es posible viajar en el tiempo 

  Veremos nuestro primer comando el cual servirá para inicializar nuestro git, es decir con esto lograremos que la carpeta en la que estaremos trabajando tendrá ahora un control de versiones por git, lo anterior no significa que ya tenemos algo en github, para eso hay más pasos a segir.

  ```bash
  git init
  ```

Para empezar a crear commits (que como ya habíamos visto, serán puntos en el tiempo), debemos de decirle a git qué queremos guardar en ese momento específico, para eso es necesaria la instrucción:
```bash
git add hellowold.html
```
La instrucción anterior añadirá a tu commit el archivo "hellowold.html" a pesar de que puedas tener más archivos el único que será guardado será ese.

Pero.... y si necesito añadir una gran cantidad de archivos ¿Qué debo hacer?

No te estreses porque git tiene la solución, puedes añadir todos tus archivos con la instrucción:
```bash
git add .
```

Con la instrucción anterior debes de tener cuidado, ya que puede que tu sistema operativo genere archivos temporales en la carpeta o directorio en el que te encuentres trabajando, o simplemente tengas demasiados archivos pero, quieres excluir alguno, a continuación te dejo el procedimiento necesario dependiendo del tu sistema operativo para que git pueda ignorar un cierto archivo. 

### .gitignore

<details>
<summary>MacOs/Linux</summary>
En MacOs es común que se generen archivos temporales (aunque en linux se prían llegar a generar, y los pasos son los mismos), para esto crearemos un archivo que dará las instrucciones para que ese archivo no se guarde:

```bash
touch .gitignore
```
El archivo anterior lo deberás abrir en un editor de código (recomendamos visual studio code), al abrirlo deberás escribir lo siguiente:

```bash
**/ .NombreArchivoIgnorado
```

Normalmete los archivos temporales suelen empezar su nombre con  un punto, agregalos en la instrucción anterior con todo y el punto

Para saber cómo se llama el archivo temporal usa la instrucción:

```bash
ls -la
```

</details>

<details>
<summary>Windows</summary>
Los comandos que aquí veremos son algo diferentes a MacOs y Linux.
Crearemos un archivo que dará las instrucciones para que ese archivo no se guarde:

```bash
echo "">.gitignore
```
El archivo generado anteriormente deberás de abrirlo en un editor de texto o de código (Recomendmos el uso de visual studio code), e introducir la siguiente line de código:
```bash
**/ .NOMBREARCHIVOIGNORADO
```
Normalmete los archivos temporales suelen empezar su nombre con  un punto, agregalos en la instrucción anterior con todo y el punto

Para saber cómo se llama el archivo temporal usa la instrucción:

```bash
dir /a
```

o si lo prefieres te puede servir de manera similar(Dependiendo de las versiones)

```bash
Get-ChildItem -Force
```
</details>

### Github
Tu sistema de control de versiones, pero en la nube. Con esto accedemos a una amplia gama de herramientas para el trabajo colaborativo, publicación de proyectos, inluso una versión light de "[Hosting](https://pages.github.com/)"

Para empezar a trabajar de manera colaborativa, será necesario hacer uso de repositorios, los cuales podrás crear desde tu perfil o página home en el boton de "+" > Crear repositorio.

## Integración de Git y Github
La manera más fácil de empezar a trabajar desde este punto sería crear un repositorio nuevo e ir subiendo todo con las herramientas de git, aunque suponiendo que tu repositorio ya está en producción o simplemente, ya tiene trabajo inicializado, se puede seguir el siguiente procedimiento:

```bash
git clone URL-REPO-SSH 
```
Por ejemplo: 

```bash
git clone git@github.com:jtoledom1/Git_Howto.git
```

**Importante:** debes de seleccionar la opción ssh, si aún no configuras tu git para trabajar con ssh, dirígete a: [Configuración-ssh](Notas%20Separadas/Git_ssh_init.md)
### Agregar un repositorio github al directorio / carpeta actual
Otra manera de trabajar es suponiendo que quieras fusionar un repo de git y uno en github en el cual ambos tienen información:

```bash
git remote add origin git@github.com:jtoledom1/Git_Howto.git
```
```bash
git pull
```
Sólo si te da errores en este punto deberás usar: 
```bash
  git pull origin main --allow-unrelated-histories
```
 Este se recomienda usar esta sólo al principio, es decir cuando fusionas los repos
```bash
  git config pull.rebase false
```
De aquí en adelante se deberá de seguir el procedimiento de "Push" que se verá más adelante

## Git push

Se deberá de añadir los archivos que se quieran agregar:
```bash
git add .
```
Posteriormente crear un commit con el método acortado 

(*Se recomienda usar este método ya que de lo contrario se deberá usar vim lo cual se puede tornar complicado sobretodo si no estás acostumbrado a este*)
```bash
git commit -m "🐛 Mi primer commit"
```
Lo anterior ha creado un commit de manera local, es decir, nuestro github aún no tiene ese commit, para esto se necesita traer cualquier cambio que se haya realizado en el repositorio. 


```bash
git pull origin main
```
(Sustituir main por la rama en la que estés trabajando)

Ahora puedes proceder a subir tus cambios a github con: 

```bash
git push -u origin main
```
(Sustituir main por la rama en la que estés trabajando)

## Enlaces

<details>
<summary>Terminal Windows</summary>
<a href="https://youtu.be/6SGIFVJ5Izs?si=YtPVl0M8lFIBufIR"><p>Aquí</p></a>
<img src="static/Terminal Windows.png">
</details>
<details>

<summary>Descarga git</summary>
<a href="https://www.git-scm.com/download/win"><p>Windows</p></a>
<a href="https://www.git-scm.com/download/linux"><p>Linux</p></a>
<a href="https://www.git-scm.com/download/mac"><p>MacOs</p></a>
</details>

<a href="https://github.com/jtoledom1/Git_Howto/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=jtoledom1/Git_Howto" />
</a>

Made with [contrib.rocks](https://contrib.rocks).
