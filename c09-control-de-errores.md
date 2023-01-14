# Control de errores
Cuando se produce un error, PS se comporta como indica el valor de `$ErrorActionPreference` como vimos en la introducción.

Si necesitamos realizar alguna operación cuando se produce un error utilizaremos `try` y `catch`. Por ejemplo para personalizar el mensaje de error o ejecutar alguna función.

En el siguiente ejemplo intentaremos descargar un documento que no existe, dará error y mostraremos un mensaje personalizado incluyendo el mensaje de error:

```powershell
try {

  $wc = new-object System.Net.WebClient
  $wc.DownloadFile("http://contoso.com/MyDoc.doc","c:\temp\MyDoc.doc")

} catch {

  write-host "Error al descargar el documento. Error:" $_.Exception.Message
    
}
```
Dentro de las llaves de `try` introducimos las líneas de código donde podría producirse el error.

Dentro de las llaves de `catch` introducimos lo que queremos que se ejecute en caso de que se produzca un error. En este caso mostramos un mensaje personalizado y el mensaje de error correspondiente que viene en `$_.Exception.Message`.

Siguiente apartado: [Módulos](./c10-modulos.md#módulos)
