# Objetos personalizados

De forma básica, un objeto personalizado es un registro donde podemos indicar una serie de campos y utilizarlos.

## Creación de un objeto personalizado

Para crear un objeto personalizado le damos un nombre y utilizamos el tipo `[PSCustomObject]` de la siguiente manera:

```powershell
$registro1 = [PSCustomObject]@{

  Nombre   = "Pepe"
  Altura   = 1.76
  Email    = "pepe@gmail.com"
}

$registro1

Nombre Altura Email
------ ------ -----
Pepe   1,76   pepe@gmail.com
```
Para acceder a un campo concreto:
```powershell
$registro1.Nombre

Pepe
```
Para cambiar el valor de un campo:
```powershell
$registro1.Altura = 1.92

$registro1

Nombre Altura Email
------ ------ -----
Pepe   1,92   pepe@gmail.com
```

## Tablas con objetos personalizados

Podemos agrupar varios registros en una lista y colocarlos en una tabla. Esta es la forma ideal para guardar muchos datos y después poder operar fácilmente con ellos.

En la tabla, el registro forma una fila que contiene campos y cada campo de cada registro forma una columna.

Declaramos la tabla `$tabla` de tipo lista:

```powershell
$tabla = New-Object System.Collections.ArrayList
```

Agregamos `$registro1` a `$tabla`y vemos el resultado:
```powershell
$tabla.add($registro1)

$tabla

Nombre Altura Email
------ ------ -----
Pepe   1,92   pepe@gmail.com
```
Agregamos otra fila a la tabla creando otro registro denominado `$registro2` y agregándolo a `$tabla`:
```powershell
$registro2 = [PSCustomObject]@{

  Nombre   = "Manuel"
  Altura   = "1,83"
  Email    = "manuel@hotmail.com"
}

$tabla.add($registro2)

$tabla

Nombre Altura Email
------ ------ -----
Pepe   1,92   pepe@gmail.com
Manuel 1,83   manuel@hotmail.com

```
Mediante el índice de la posición de cada registro en la tabla podemos extraer el valor de las propiedades y también cambiarlos:
```powershell
$tabla[0].Nombre

Pepe

$tabla[1].Nombre

Manuel

$tabla[1].Nombre = "Pedro"

$tabla

Nombre Altura Email
------ ------ -----
Pepe     1,92 pepe@gmail.com
Pedro    1,83 manuel@hotmail.com
```

## Búsqueda de registros

Con `Where-Object` podemos buscar registros que tengan algún valor en alguna de sus propiedades o campos.

Por ejemplo si queremos encontrar los registros que tengan el valor `Pepe` del campo o propiedad `Nombre`:

```powershell
$tabla | Where-Object Nombre -eq "Pepe"
```

El uso de paréntesis puede facilitar mucho la búsqueda de un valor y cambiar el valor de cualquier propiedad del registro encontrado:
```powershell
($tabla | Where-Object Nombre -eq "Pepe").Email = "pepe.perez@gmail.com"

$tabla

Nombre Altura Email
------ ------ -----
Pepe     1,92 pepe.perez@gmail.com
Manuel   1,83 manuel@hotmail.com
```
En el ejemplo anterior hemos realizado la búsqueda que vimos antes pero la hemos encerrado entre paréntesis. 

Lo que hay entre paréntesis también es el valor devuelto de la búsqueda y es el registro encontrado. 

Si después de los paréntesis indicamos el punto y el nombre de una propiedad como `Email` podemos operar directamente con ella y cambiar su valor como es el caso. Ahora el campo `Email` del registro de `Pepe` ha cambiado de `pepe@gmail.com` a `pepe.perez@gmail.com`

Siguiente apartado: [Control de errores](./c09-control-de-errores.md#control-de-errores)