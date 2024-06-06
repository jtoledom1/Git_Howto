<details>
  <summary>Linux</summary>
  
  Contenido para Linux.
</details>

<details>
  <summary>Windows</summary>
  
Claro, puedo ayudarte con eso. Aquí tienes la documentación técnica reescrita:

---

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

Para generar una nueva clave SSH:

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
  
  Contenido para MacOS.
</details>
