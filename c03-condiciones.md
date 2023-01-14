# Condiciones
Evaluar condiciones sirve para tomar decisiones y controlar el flujo de ejecución. Este es uno de los aspectos fundamentales en la programación y en este apartado veremos algunas formas de hacerlo con PS.

Para facilitar la compresión de los ejemplos es recomendable escribirlos en un script de PS y ejecutarlos para ver los resultados.

## If
`if` evalúa un valor entre paréntesis. El resultado de esta evaluación puede ser verdadero o falso. Si la evaluación es verdadera se ejecuta el código entre llaves a continuación.

Por ejemplo, podemos averiguar si una variable está vacía o si tiene algún valor que sea válido. Declaremos la variable `$texto` con un valor y después evaluemos con `if`:
```powershell
$texto = "hola"

if ( $texto ) {

  write-host "Verdadero"

}
```
Como `$texto` tiene el valor válido `"hola"` se ejecuta el código entre llaves que es visualizar `Verdadero`.

Si además necesitas ejecutar código en caso de que la evaluación no sea verdadera utiliza `else` de la siguiente forma:

```powershell
$texto = ""

if ( $texto ) { 

  write-host "Verdadero" 

} else { 

  write-host "Falso"

}
```
También tenemos casos a tener en cuenta al evaluar algunos valores:
- Los valores vacíos como `""` o `$null` o `$false` se evalúan como no verdaderos o falsos
- El valor de un espacio de texto o más de uno, como `" "` se evalúa como verdadero

El operador `-not` delante de una variable a evaluar invierte su evaluación, por ejemplo:
```powershell
$texto = ""

if ( -not $texto ) { 

  write-host "Falso" 

} else { 

  write-host "Verdadero

}
```

También puedes utilizar la versión en una sola línea, para más comodidad al realizar pruebas en la línea de comandos:
```powershell
$texto = $null

if ( $texto ) { write-host "Verdadero" } else { write-host "Falso" }
```

## Operadores condicionales

PS dispone de varios operadores para comparar dos valores. Por ejemplo, veamos como comprobar una contraseña utilizando el operador condicional `-eq` (equal o igual):
```powershell
$pass = "pass123456"

if ( $pass -eq "pass123456" ) { write-host "Contraseña correcta" }
```
También podemos evaluar si dos variables son distintas utilizando el operador `-ne` (not equal o distinto):
```powershell
$nombre1 = "Pedro"
$nombre2 = "Pablo"

if ( $nombre1 -ne $nombre2 ) { write-host "Los nombres son distintos." }
```
A continuación otros operadores condicionales orientados a la comparación de dos números:

|Operador|Significado|
|--------|-----------| 
|-gt|mayor que|
|-ge|mayor o igual que|
|-lt|menor que|
|-le|menor o igual que|

Por ejemplo:
```powershell
$manzanas = 5
$peras    = 4

if ( $manzanas -gt $peras ) { write-host "Hay más manzanas que peras" }
```
## Múltiples evaluaciones
Puedes realizar varias evaluaciones separando cada una con los operadores lógicos `-and` y `-or`. 

El operador `-and` se utiliza para comprobar si se cumplen `todas` las evaluaciones, por ejemplo:
```powershell
if ( ( $nombre1 -eq $nombre2 ) -and ( $manzanas -eq $peras ) ) {

  write-host "Los nombres son iguales y el número de manzanas y peras también"
}
```
Todas las evaluaciones deben estar dentro de los paréntesis principales del `if`.

El operador `-or` se utiliza para averiguar si se cumple `alguna` de las evaluaciones. Por ejemplo, si me da igual que un color sea rojo o verde:
```powershell
$color = "rojo"

if ( ( $color -eq "rojo" ) -or ( $color -eq "verde" ) ) {

  write-host "El color es rojo o verde"
}
```
Utilizando `else` puedes averiguar si se trata de cualquier otro color:
```powershell
$color = "amarillo"

if ( ( $color -eq "rojo" ) -or ( $color -eq "verde" ) ) {

  write-host "El color es rojo o verde"

} else {

  write-host "El color no es ni rojo ni verde"

}
```

## Switch
Si tienes una serie de valores conocidos y necesitas saber si el valor de una variable es alguno de ellos puedes utilizar `switch`:
```powershell
$color = "verde"

switch ( $color ) {
  
  "rojo"     { write-host "El color es rojo"  }
  "verde"    { write-host "El color es verde"  }
  "amarillo" { write-host "El color es amarillo"   }  
  default    { write-host "Color no registrado"  }
}
```
Como vemos, `switch` evalúa el valor entre paréntesis y debajo se colocan los posibles valores entre comillas dobles, uno por línea, de forma que si uno de ellos coincide, ejecuta el código correspondiente entre llaves.

En caso de que no se produzca ninguna coincidencia, se ejecuta el código indicado en `default`.

En el caso de evaluar números, los distintos valores se escriben directamente:
```powershell
$numero = 4

switch ( $numero ) {

  1 { write-host "El número es 1" }
  2 { write-host "El número es 2" }
  3 { write-host "El número es 3" }
  default { write-host "Número no registrado"  }
}
```

También puedes evaluar comparaciones, por ejemplo:
```powershell
$numero = 4

switch ( $numero ) {

  {$_ -gt 1} { write-host "$_ es mayor a 1" }
  {$_ -gt 3} { write-host "$_ es mayor a 3" }
  {$_ -gt 5} { write-host "$_ es mayor a 5" }  
}
```
Observa como la variable especial `$_` toma el valor de `$numero` y puede utilizarse.

Cada comparación va entre llaves, con el correspondiente código a ejecutar también entre llaves. 

Se ejecutan todas las comparaciones que se cumplan en orden.

Si necesitamos detener las comparaciones una vez se cumpla una de ellas, utilizamos `break` antes de cerrar la llave correspondiente:
```powershell
$numero = 4

switch ( $numero ) {

  {$_ -gt 1} { write-host "$_ es mayor a 1"; break }  
  {$_ -gt 3} { write-host "$_ es mayor a 3"; break }
  {$_ -gt 5} { write-host "$_ es mayor a 5"        }  
}
```

# Where

Sabemos que podemos redirigir la salida de un cmdlet, objeto o colección de elementos por una tubería `|` y acceder a sus propiedades. Para encontrar alguna propiedad concreta con algún valor concreto utilizamos `Where`.

Por ejemplo, ¿es 2022 el año actual?
```powershell
get-date | where { $_.year -eq 2022 }
```
En este ejemplo, si el año actual es 2022 aparece la fecha actual y en caso contrario no aparece nada. Como vemos, utilizamos la variable especial `$_`, que en este caso es la fecha.

Si el valor está alojado en una variable el resultado es el mismo:
```powershell
$fecha = get-date

$fecha | where { $_.year -eq 2022 }
```

Si necesitamos buscar en la salida de algún cmdlet para averiguar si alguna propiedad tiene algún valor concreto:
```powershell
get-process | where { $_.Processname -eq "svchost" }
```
En este caso, de todos los procesos listados por `get-process` visualizamos los que se llaman `svchost`. La propiedad que contiene el nombre del proceso es `Processname`.

Siguiente apartado: [Bucles](./c04-bucles.md#bucles)