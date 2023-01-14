# Introducción
PS es un lenguaje de programación interpretado y basado en .NET, ideal para administrar sistemas Windows, realizar automatizaciones e integraciones con distintas tecnologías.

Las características más interesantes de PS son el uso de:
- Línea de comandos
- Scripting
- Comandos (cmdlets) para administrar sistemas y servicios
- Cualquier función de la librería de .NET
- Módulos personalizados para extender funcionalidades
- Módulos de Microsoft
  - Windows
  - Directorio Activo
  - SQLServer
  - Exchange y Exchange Online
  - Azure  
- Módulos de otros fabricantes
  - AWS
  - VMWare
  - Citrix
  - Google Cloud

Todas las versiones de Windows actuales incorporan PS. Para comprobarlo clica en `Inicio` y teclea `powershell`, clica en `Windows Powershell` y aparecerá una ventana de línea de comandos.

En esta ventana el cursor está dentro de la carpeta por defecto del usuario que estás utilizando y además al principio de la línea aparece `PS` que quiere decir que estás en la línea de comandos de Powershell.

Aquí puedes escribir y ejecutar tanto comandos de Windows como `cmdlets` y código PS. 

Teclea `$host`, pulsa `ENTER` y aparecerá la versión de PS junto con más información.

Adicionalmente, es recomendable instalar `Visual Studio Code` y configurarlo para utilizar las extensiones relacionadas con PS para desarrollar scripts de PS y sobre todo para depurarlos.

## Privilegios de ejecución
El entorno de ejecución de Powershell está protegido por una política de ejecución para evitar la ejecución de scripts maliciosos. Para saber cual es la política que actualmente está aplicada utiliza el siguiente `cmdlet` de PS en la ventana de línea de comandos de PS:
```powershell
get-executionpolicy
```
Si el resultado es distinto de `unrestricted`, teclea:
```powershell
set-executionpolicy unrestricted -scope currentuser
```
y acepta el cambio. De esta forma el usuario actual no tendrá problemas para ejecutar código PS.

## Comportamiento de errores
Para comprobar cual es el modo actual del comportamiento de errores teclea la siguiente variable especial:
```powershell
$ErrorActionPreference
```
Y devolverá uno de estos cuatro modos:

-	`Continue`: muestra errores y continúa con la ejecución.
-	`SilentlyContinue`: no muestra errores y continúa la ejecución.
-	`Inquire`: al producirse errores pregunta al usuario qué hacer.
-	`Stop`: detiene la ejecución.

El modo por defecto es `Continue`. Puedes cambiar a cualquier otro modo asignándolo directamente, por ejemplo:

```powershell
$ErrorActionPreference = "SilentlyContinue"
```

## Uso básico de Powershell

PS denomina `cmdlet` a lo que en otros lenguajes de programación se denomina `instrucción` o `comando` y es la forma elemental para realizar alguna operación.

Si bien PS dispone de cmdlets para realizar todo tipo de operaciones, casi todos se identifican por el prefijo que tienen, así, los que comienzan con `get` como `get-date` suelen mostrar información, los que comienzan con `set` como `set-location` sirven para establecer valores o configuraciones, etc.

Si quieres ver los `cmdlets` que tienes disponibles en un momento dado, en la `línea de comandos de PS` escribe:
```powershell
get-command | where Commandtype -eq Cmdlet | more
```

Por ejemplo, si quieres saber la fecha/hora actual, pon:
```powershell
get-date
```
y devolverá la fecha/hora actual en el formato predefinido.

Si quieres ver el resultado en otro formato, puedes utilizar la tubería `|` para redirigir su salida y aplicar otro formato aprovechando la funcionalidad de objetos y propiedades. Por ejemplo:
```powershell
get-date | fl
```
`fl` significa `format-list` y devuelve cada una de las propiedades del objeto `get-date` en un formato de lista vertical. Si en lugar de `fl` utilizas `ft` que significa `format-table` devolverá la misma información pero horizontalmente, como una tabla.

Para obtener el valor de una propiedad de un cmdlet, encierra entre paréntesis el cmdlet, después un punto y el valor de la propiedad. Por ejemplo, para obtener la propiedad `año` del cmdlet `get-date` utiliza:
```powershell
(get-date).year
```
Para ver todas las propiedades (y métodos) de un cmdlet, redirige su salida al cmdlet `get-member` con una tubería. Por ejemplo, las propiedades y métodos del cmdlet `get-date` se obtienen así:
```powershell
get-date | get-member 
```
También puedes guardar lo que devuelve un cmdlet asignándolo a una variable. Las variables en PS se definen utilizando el símbolo `$` y después un nombre. Por ejemplo, puedo guardar la fecha actual en la variable `$fecha` así:
```powershell
$fecha = get-date
```
Ahora `$fecha` tiene la fecha/hora del momento en que se asignó. Si escribes ahora:
```powershell
$fecha
```
también aparece la fecha/hora, igual que si escribes `get-date`, pero ojo, visualizará la fecha/hora del momento en que se asignó la variable `$fecha`. 

Después puedes utilizar la variable `$fecha` de la misma manera que el cmdlet `get-date`. Por ejemplo, puedes visualizar el año así:
```powershell
$fecha.year
```
y obtener las propiedades y métodos de la siguiente forma:
```powershell
$fecha | get-member
```

El cmdlet `write-host` muestra por pantalla lo que le pongas a su derecha:
```powershell
write-host Hola, ¿que tal?
```
En caso de mostrar texto, es aconsejable indicarlo entre comillas dobles:
```powershell
write-host "Hola, ¿que tal?"
```
También puedes visualizar una variable:
```powershell
write-host $fecha
```
y también una propiedad de una variable:
```powershell
write-host $fecha.year
```

El cmdlet `read-host` pregunta por teclado e introduce la respuesta en una variable:
```powershell
$nombre = read-host "Introduce tu nombre"
```
Después puedes visualizar lo que has introducido:
```powershell
write-host $nombre
```

En una misma línea puedes ejecutar varias expresiones separadas por punto y coma `;`, así:
```powershell
$edad = read-host "Pon tu edad"; write-host $edad; "¡Qué viejo!"
```

## Ejecución de scripts
PS ejecuta scripts en ficheros de texto plano con extensión `.ps1`.

Para crear y editar scripts sólo necesitas un editor de texto pero es recomendable utilizar [Visual Studio Code](https://code.visualstudio.com/) pues incorpora resaltado de sintaxis, autocompletar, ejecución y depuración paso a paso.

Para probar los ejemplos que vamos a ver a continuación crearemos una carpeta en el Escritorio de Windows que se llame `scripts-powershell` y ahí dentro con cualquier editor de texto o con `Visual Studio Code` crea un nuevo archivo de texto que se llame `pruebas.ps1`. Dentro de este archivo escribe:
```powershell
write-host "Hola mundo"
```
Guárdalo y vamos a ejecutarlo desde la ventana de línea de comandos de PS que tenemos abierta y vimos antes. Primero vamos a la carpeta donde está el script `pruebas.ps1` dentro del Escritorio de Windows:
```powershell
cd $home\desktop\scripts-powershell
dir
```
y aparecerá el script `pruebas.ps1`. Para ejecutarlo utiliza:
```powershell
.\pruebas.ps1 
```
y si todo va bien aparecerá el resultado `Hola mundo`.

Ya sabemos ejecutar un script de PS, así que volvamos a lo que podemos hacer con él modificando el código de `pruebas.ps1` y ejecutándolo.

Dentro del script puedes comentar líneas utilizando el símbolo `#` a la izquierda del texto que quieras comentar. Este texto no se tendrá en cuenta y sirve para orientar a la persona que lea el código. Por ejemplo:

```powershell
# Asigna la fecha
$fecha = get-date
$fecha2 = get-date # Asigna otra fecha
```
También puedes comentar varias líneas entre `<#` y `#>`:
```powershell
<#
Asigna la fecha
y asigna el año
#>
$fecha = get-date
$year  = $fecha.year
```
Ya sabes utilizar y ejecutar PS de forma básica. En el siguiente apartado aprenderás a utilizar los ladrillos básicos de PS que son los tipos de variables.

Siguiente apartado: [Tipos](./c02-tipos.md#tipos)