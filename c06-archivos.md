# Archivos
Toda la información se guarda en archivos. Veamos como PS realiza operaciones con archivos de texto.

Para facilitar los siguientes ejemplos con archivos, creamos una carpeta en `c:` denominada `pruebas`:
```powershell
$carpeta = "c:\pruebas"
mkdir $carpeta
```

## Creación de archivos

Dentro de la nueva carpeta creamos un archivo de texto denominado `datos.txt` conteniendo tres líneas:
```powershell
$nombre_archivo = "datos.txt"
$ruta_archivo = "$carpeta\$nombre_archivo"
"primera`nsegunda`ntercera" | out-file $ruta_archivo
```
Como vemos, dentro de un texto indicamos un salto de línea con ``n`.

El cmdlet `out-file` recibe el texto desde una tubería y lo escribe en un nuevo archivo denominado `datos.txt` indicando su ruta completa.

## Comprobación de archivos

Podemos averiguar si el archivo `datos.txt` existe utilizando el cmdlet `test-path`:
```powershell
if ( test-path $ruta_archivo ) { 
  
  write-host "El archivo $ruta_archivo existe" 

} else { 
  
  write-host "El archivo $ruta_archivo no existe" 

}
```

## Lectura de archivos
Leamos el contenido de nuestro archivo de texto con el cmdlet `get-content` y dejemos su contenido en la variable `$contenido`:
```powershell
$contenido = get-content $ruta_archivo
```
La variable `$contenido` ahora contiene una colección de elementos donde cada uno es cada línea leída del archivo de texto. 

## Escritura de archivos
Ya hemos visto como utilizar el cmdlet `out-file` para crear un archivo de texto y escribir información en él.

Vamos a agregar una cuarta línea utilizando la opción `-append` del cmdlet `out-file`:
```powershell
"cuarta" | out-file $ruta_archivo -append
```

Es importante entender que el cmdlet `out-file` sin la opción `-append` crea un archivo nuevo. Esto quiere decir que si el archivo ya existe, lo sobreescribirá perdiendo la información que ya contenga.

Siguiente apartado: [Expresiones regulares](./c07-regex.md#expresiones-regulares)
