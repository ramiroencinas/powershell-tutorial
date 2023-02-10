# Tipos
En este apartado veremos cómo utilizar tipos de datos en PS, desde los más simples para utilizar números o textos, pasando por colecciones de elementos como matrices, listas y hashes.

## Variables
Una variable es una especie de contenedor con un nombre donde puedes alojar un valor para utilizarlo. También puedes cambiar el valor.

El nombre de una variable tiene el prefijo `$`. Es aconsejable que el nombre comience con una letra y después puede contener letras, números y guiones bajos, pero nunca espacios. Por ejemplo: `$contador`.

El valor de una variable se asigna a ésta utilizando el símbolo `=` entre el nombre de la variable y el valor. El valor puede indicarse de varias formas.

Los números se indican directamente:
```powershell
$numero = 34
```
También con decimales utilizando un punto:
```powershell
$numero_decimal = 1.5
```
Una letra puede indicarse entre comillas simples:
```powershell
$letra = 'a'
```
Un texto mejor entre comillas dobles:
```powershell
$texto = "los números son 1, 2 y 3"
```
El valor de una variable puede asignarse a otra:
```powershell
$texto2 = $texto
```
El resultado de un cmdlet, como ya vimos, puede guardarse en una variable para su posterior uso:
```powershell
$fecha = get-date
```
Si quieres visualizar el valor de cualquier variable, escribe el nombre de la variable directamente:
```powershell
$numero
```

En el momento que se asigna el valor a una variable, PS detecta el tipo del valor y lo tiene en cuenta de forma automática.

Si tienes una variable de un tipo y le asignas un valor de otro tipo, el tipo de la variable cambiará en consecuencia. Es recomendable no hacer esto para no producir confusiones.

Si tienes claro el tipo de una variable y quieres asegurarte de que su tipo no cambie, puedes crear la variable indicando su tipo entre corchetes como prefijo al nombre. Aquí tienes algunos ejemplos:

Números enteros de 32bit:
```powershell
[int]$numero_32bit = 999999999
```
Números enteros de 64bit:
```powershell
[long]$numero_64bit = 999999999999999999
```
Número decimal:
```powershell
[decimal]$numero_decimal = 467.45
```
Número de 8bit:
```powershell
[byte]$numero_8bit = 255
```
Cadena de texto:
```powershell
[string]$cadena = "cadena en unicode"
```
Un caracter:
```powershell
[char]$caracter = 'a'
```
Variable booleana, que puede alojar uno de dos estados: $true o $false:
```powershell
[bool]$verdad = $true
```
Si después de crear variables de esta forma intentas asignar un valor de un tipo distinto a la variable, dará un error y el valor no cambiará.
## Operaciones básicas
Puedes realizar operaciones aritméticas con números:
```powershell
1 + 1.5
```
Con variables que contengan números:
```powershell
$numero + $numero_decimal
```
O con números y variables:
```powershell
$numero + 5
```
Para incrementar una variable numérica utiliza el sufijo `++`:
```powershell
$numero++
```

El símbolo `+` en el contexto de cadenas de texto sirve para unir dos o más cadenas de texto:
```powershell
"y " + "esto es una cadena"
```

Observa que los espacios en blanco dentro de una cadena de texto se tienen en cuenta.

El resultado de cualquiera de las operaciones que hemos visto puede guardarse en una variable:
```powershell
$resultado = $numero + 5

$cadena_final = "y " + "esto es una cadena"
```

Puedes incluir el valor de una variable dentro del valor de una variable de texto colocando el valor entre comillas dobles `"`:
```powershell
$n = 3
$texto_final = "El resultado son $n cajas"
```

En el caso anterior, si utilizas comillas simples el valor será totalmente literal:
```powershell
$n = 3
$texto_final = 'El resultado son $n cajas'
```

Llegados a este punto, ya sabes cómo operar básicamente con variables. En el siguiente apartado aprenderás a utilizar conjuntos o colecciones de variables o mejor dicho, de elementos.

## Matrices
Una matriz es una variable que sirve para alojar una colección de elementos. Esta colección puede contener cualquier número de elementos de cualquier tipo. Los elementos se indican separados por comas:
```powershell
$matriz = "Esto es una cadena",44,$numero_decimal,$letra
```
El primer elemento tiene la posición 0. Puedes acceder a cualquier elemento indicando su posición entre corchetes `[ ]`:
```powershell
$matriz[2]
```

Para obtener un rango de elementos indica la posición de inicio y de fin entre corchetes y separados entre dos puntos seguidos:
```powershell
$matriz[2..4]
```	
La posición del último elemento es -1:
```powershell
$matriz[-1]
```

Puedes obtener el número de elementos de una matriz con el método `.count`:
```powershell
$matriz.count
```
Puedes modificar el valor de un elemento indicando su posición y asignando el nuevo valor:
```powershell
$matriz[-1] = "esto es otra cadena"
```

## Listas
Una lista es una colección de elementos, como una matriz, pero es más fácil agregar y eliminar elementos.

Para crear la lista vacía `$lista` utiliza:
```powershell
$lista = New-Object System.Collections.ArrayList
```
Como puedes ver, la variable `$lista` es un objeto de tipo `ArrayList` de .NET.

Una lista tiene varios métodos. El método `.add` se utiliza para añadir elementos de cualquier tipo mediante el parámetro entre paréntesis:
```powershell
$lista.add("cadena")
$lista.add(45)
$lista.add("otra cadena")
$lista.add(450)
$lista.add("otra cadena más")
```
Puedes visualizar el contenido de la lista escribiendo su nombre, como cualquier otra variable:
```powershell
$lista
```
El método `.remove` elimina un elemento de la lista indicando su valor como parámetro:
```powershell
$lista.remove(45)
```
Si existe algún valor repetido, eliminará solo el primero que se encuentre.

Puedes eliminar un rango de elementos con el método `.removerange` indicando la posición donde quieres empezar a eliminar elementos y el número de posiciones que quieres eliminar en total (al igual que las matrices, recuerda que el primer elemento tiene la posición 0). Por ejemplo, para eliminar dos elementos desde la posición 1:
```powershell
$lista.removerange(1,2)
```

También puedes eliminar un solo elemento indicando su posición con el método `.removeat`:
```powershell
$lista.removeat(0)
```

Por último, puedes eliminar todos los elementos de la lista con el método `.clear` sin parámetros:
```powershell
$lista.clear()
```

## Hashes
Un hash es una colección de elementos donde cada uno se compone de una clave única y su valor correspondiente (par clave - valor). Un hash es como un diccionario, donde localizas un nombre (clave) y puedes ver lo que significa (valor). Conociendo una clave puedes acceder a su valor y también puedes cambiarlo.

Vamos a crear un hash vacío denominado `$hash`:
```powershell
$hash = @{}
```

Agregar al hash un elemento cuyo nombre o clave es `primero` con el valor `1`:
```powershell
$hash["primero"] = 1
```
Como ves, el nombre o clave va entre corchetes a la derecha del nombre del hash, después el igual y después el valor.

Si la clave es un texto debe ir entre comillas dobles, si se trata de un número puede ir directamente. Agreguemos un elemento al hash cuya clave es el número 2 y el valor es "dos":
```powershell
$hash[2] = "dos"
```
Se pueden agregar valores como otras variables:
```powershell
$hash["fecha"] = $fecha
```
O incluso matrices:
```powershell
$hash["matriz"] = 1,"dos",3,4.5
```

Para ver el contenido del hash, simplemente escríbelo y aparecerá la lista con el nombre de la clave `Name` y el valor correspondiente `Value`:
```powershell
$hash
```
Para visualizar o disponer del valor de un elemento, indica el nombre del hash seguido de un punto y el nombre de la clave:
```powershell
$hash.primero
$hash.fecha
$hash.matriz
$hash.2
```
También puedes indicar la clave sin el punto y entre corchetes:
```powershell
$hash["primero"]
$hash["fecha"]
$hash["matriz"]
$hash[2]
```
Utiliza el método `.keys` para obtener las claves del hash:
```powershell
$hash.keys
```
Y el método `.values` para obtener los valores:
```powershell
$hash.values
```

El elemento `$hash["matriz"]` tiene como valor una matriz de elementos. Para acceder a cualquiera de los elementos de esta matriz indica su posición así:
```powershell
$hash.matriz[0]
$hash.matriz[1]
$hash.matriz[-1]
```
También puedes utilizar la otra forma con comillas dobles:
```powershell
$hash["matriz"][0]
$hash["matriz"][1]
$hash["matriz"][-1]
```

La eliminación de un elemento de `$hash` se realiza mediante el método `.remove` indicando la clave correspondiente:
```powershell
$hash.remove("fecha")
```

El método `.clear()` elimina todos los elementos del hash:
```powershell
$hash.clear()
```
Siguiente apartado: [Condiciones](./c03-condiciones.md#condiciones)