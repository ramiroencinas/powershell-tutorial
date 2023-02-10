# Bucles

Los bucles sirven para realizar operaciones con cada elemento de una colección.

PS dispone de varios tipos de bucles y distintas maneras de controlar el flujo de cada uno.

## foreach

Recorre una colección de elementos desde el primero hasta el último:

```powershell
$nombres = ('Pablo','Pedro','Pepe')

foreach ( $nombre in $nombres ) {

  write-host $nombre

}
```
Como vemos, proporcionamos la matriz `$nombres` con tres elementos que son cadenas de texto alojando nombres. 

Dentro de los parámetros entre paréntesis de `foreach ` indicamos primero el nombre de la variable que tendrá el elemento en cada vuelta o iteración `$nombre` seguido de `in` y después el nombre de la colección `$nombres`.

Esta variable `$nombre` va tomando su nuevo valor en cada vuelta por el valor de cada elemento de la colección `$nombres`, y como resultado escribe el valor de los tres elementos, uno en cada línea con `write-host`.

Existe otra forma más abreviada y elegante de utilizar `foreach`:
```powershell
$nombres | foreach {

  write-host $_

}
```
utilizando una tubería desde la colección `$nombres` dirigida al cmdlet `foreach`. Observa el uso de la variable especial `$_`. Esta variable va tomando el valor de cada elemento de la colección `$nombres`.

Todavía existe una forma más reducida de realizar un `foreach` sustituyéndolo por `%`:
```powershell
$nombres | %{ write-host $_ }
```
De forma parecida, si necesitas recorrer rápidamente una serie de números consecutivos:
```powershell
$primero = 1
$ultimo  = 10

$primero..$ultimo | %{ write-host $_ }
```
y también funciona al revés:
```powershell
$primero = 1
$ultimo  = 10

$ultimo..$primero | %{ write-host $_ }
```

## for
La instrucción `for` ejecuta código mientras se cumpla una condición numérica. El número de veces se controla mediante una variable numérica que se va incrementando. Por ejemplo, si necesitas visualizar los números comprendidos entre 5 y 10:
```powershell
$primero = 5
$ultimo  = 10
for ( $i = $primero; $i -le $ultimo; $i++ ) { write-host $i }
```
Dentro de los paréntesis de `for` se realizan 3 operaciones separadas entre punto y coma:

- Creamos una variable `$i` hace de índice y la inicializamos con el primer valor `$primero` cuyo valor es 5
- Evaluamos si `$i` es menor o igual a `$ultimo`
- Incrementamos uno a `$i` mediante `$i++`

Si en una vuelta el valor de `$i` es menor o igual que `$ultimo` que es 10, ejecuta lo que hay a continuación entre llaves (en este caso muestra el valor de `$i`) y después `$i` se incrementa en uno mediante `$i++`. 

En la última vuelta `$i` tiene valor 10, lo muestra y se incrementa a 11. Ahora `$i` tiene valor 11. En la siguiente vuelta, que será la última, `$i` no cumple la condición y el bucle finaliza sin ejecutar nada.

## while
Esta instrucción repite el código entre llaves `mientras` se cumpla una condición `al principio` del bucle:
```powershell
$i = 1
while ($i -le 3) {
	
  write-host $i 
  $i++
}
```
El ejemplo anterior visualiza los números del 1 al 3.

También sirve para validar una entrada del usuario y pedírsela hasta que acierte:
```powershell
$clave = ""
$clave_secreta = "pass"

while ( $clave -ne $clave_secreta ) {

  $clave = read-host "Introduce la clave secreta"

}

write-host "Clave secreta correcta"
```
Hay que tener cuidado y asegurarse de que en algún momento se cumplirá la condición, pues en caso contrario la ejecución nunca saldrá del bucle.

## Until
Ejecuta código hasta que se cumpla una condición que es evaluada `al final del bucle`. Adaptando el ejemplo de la contraseña:
```powershell
$clave_secreta = "pass"

do {
	
  $clave = read-host "Introduce la clave secreta"

} until ( $clave -eq $clave_secreta )

write-host "Clave secreta correcta"
```
Como puedes ver, siempre se ejecuta el código entre llaves de `do` al menos en la primera vuelta. En este caso la evaluación de la condición es más intuitiva que la aportada con `while`.

Siguiente apartado: [Funciones](./c05-funciones.md#funciones)