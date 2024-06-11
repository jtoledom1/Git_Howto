**Sobre las Frases de Contraseña para Claves SSH**

Puedes acceder y escribir datos en los repositorios de GitHub.com utilizando el protocolo Secure Shell (SSH). Al conectarte a través de SSH, la autenticación se realiza mediante un archivo de clave privada en tu equipo local. 
  
Si aún no tienes una clave SSH, es necesario generar una nueva para utilizarla en la autenticación. Si no estás seguro de si ya tienes una clave SSH, puedes verificar la existencia de claves existentes. 
  

**Generación de una Nueva Clave SSH**

Puedes generar una nueva clave SSH en tu equipo local. Después de generar la clave, puedes agregar la clave pública a tu cuenta en GitHub.com para habilitar la autenticación para las operaciones de Git a través de SSH.

<details>
  <summary>Linux</summary>
Documentación para generar y agregar una clave SSH, adaptada para el uso en la Terminal:

---

**Generar y Agregar una Clave SSH a tu Cuenta de GitHub**

**Paso 1: Generar una Clave SSH**

1. Abre Terminal. (ctrl+alt+t)

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

2. Copia y pega el siguiente texto, asegurándote de reemplazar "tu_correo_electronico@example.com" con tu dirección de correo electrónico de GitHub:

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

1. En una nueva ventana de PowerShell **con privilegios de administrador**, asegúrate de que el agente ssh esté en funcionamiento. Puedes utilizar las instrucciones de "Auto-lanzamiento ssh-agent" en "Trabajar con contraseñas de clave SSH", o iniciar el agente manualmente con los siguientes comandos:

```powershell
# Inicia el ssh-agent en segundo plano
Get-Service -Name ssh-agent | Set-Service -StartupType Manual
Start-Service ssh-agent
```

2. En una ventana de terminal **sin privilegios de administrador**, agrega la clave privada SSH al agente ssh. Si has creado tu clave con un nombre diferente o estás agregando una clave existente que tiene un nombre diferente, reemplaza "id_ed25519" en el comando con el nombre de tu archivo de clave privada, así como la ruta, es decir el "/YOU" por tu usuario de windows.

```bash
ssh-add c:/Users/YOU/.ssh/id_ed25519
```

**Agregar una Clave SSH Nueva a tu Cuenta de GitHub**

Para agregar la clave pública SSH a tu cuenta de GitHub, consulta "[Agregar una clave SSH nueva a tu cuenta de GitHub](https://docs.github.com/es/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)".

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

Para agregar la clave pública SSH a tu cuenta de GitHub, consulta "[Agregar una clave SSH nueva a tu cuenta de GitHub](https://docs.github.com/es/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)". Donde encontrás información más detallada, aunque siempre puedes seguir este resumen 

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
