# Módulos
Si desarrollas un script que utiliza muchas funciones, utilizar módulos te permite repartir estas funciones en otros archivos, que son los módulos en sí. De esta forma es más sencillo localizar y revisar código. Los módulos en PS son archivos con extensión `.psm1`.

Por otro lado, tanto Microsoft como otros fabricantes proporcionan módulos para utilizarlos con sus servicios y productos. La comunidad de PS también proporciona módulos con diversas funcionalidades.

Para ver un ejemplo de un módulo funcionando, crearemos una calculadora mediante un script principal denominado `calculadora.ps1` y un módulo denominado `operaciones.psm1`. Ambos archivos los crearemos en la misma carpeta.

El código del archivo del módulo `operaciones.psm1` tiene las funciones `suma` y `resta` y es el siguiente:

```powershell
# Módulo operaciones.psm1

function suma {

  param ( $numero1, $numero2 )

  $resultado =  $numero1 + $numero2

  return $resultado
}

function resta {

  param ( $numero1, $numero2 )

  $resultado = $numero1 - $numero2

  return $resultado
}

Export-ModuleMember -Function *
```
Como puedes ver, aparecen las dos funciones mencionadas y al final el cmdlet `Export-Module -Function *` indica que todas las funciones definidas en este archivo quedarán disponibles para otros scripts y módulos de PS.

Escribamos ahora el script principal `calculadora.ps1` en la misma carpeta donde hemos guardado el módulo, con el siguiente código:

```powershell
import-module "$PSScriptRoot\operaciones.psm1"

$num1 = 8
$num2 = 5

$resultado_suma  = suma -numero1 $num1 -numero2 $num2
$resultado_resta = resta -numero1 $num1 -numero2 $num2

write-host "La suma de $num1 y $num2 es $resultado_suma"
write-host "La resta de $num1 y $num2 es $resultado_resta"
```
El script primero importa el módulo con:
```powershell
import-module "$PSScriptRoot\operaciones.psm1"
```
La variable especial `$PSScriptRoot` contiene la ruta de la carpeta del script en ejecución `calculadora.ps1`, y como esta carpeta es la misma donde se encuentra el módulo `operaciones.psm1`, construimos la ruta completa del archivo del módulo utilizando la barra invertida y se la proporcionamos como parámetro al cmdlet `import-module` que se encarga de cargar el módulo.

Después inicializamos un par de variables con los números para realizar las operaciones de suma y resta y por último escribimos el resultado de cada función.

Para ver el resultado ejecuta `calculadora.ps1`.

Si en la misma sesión donde ejecutas este script necesitas que el módulo no esté disponible utiliza:
```powershell
remove-module operaciones
```
Fíjate bien que el cmdlet `remove-module` especifica como parámetro el nombre del módulo sin la extensión `.psm1`.

Esta operación no elimina el archivo del módulo, simplemente hace que el módulo y sus funciones no estén disponibles.

Fin de los apartados: [Ir al índice](./README.md#indice)