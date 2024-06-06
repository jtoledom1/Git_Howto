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
