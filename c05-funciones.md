# Funciones
Una función es un trozo de código entre llaves identificado con un nombre y que hace algo muy concreto las veces que sean necesarias. 

En `PS` se define una función básicamente utilizando la instrucción `function`, un nombre y el código de la función entre llaves. Definamos la función `saludo`:

```powershell
function saludo {

  write-host "Buenas tardes"

}
```
Hemos definido una función para saludar. Después, al escribir el nombre de la función, que se denomina `llamar a la función`, ejecuta su código que es visualizar el texto `Buenas tardes`:
```powershell
function saludo {

  write-host "Buenas tardes"

}

saludo
```

## Uso de parámetros en funciones
A una función se le pueden pasar variables en forma de parámetros para poder utilizarlas dentro de la función.

En la definición de la función los parámetros se indican a la derecha del nombre de la función entre paréntesis. Por ejemplo, definamos una función `saludo` con el parámetro `$nombre`:
```powershell
function saludo( $nombre ) {

  write-host "Buenas tardes $nombre"

}

saludo "Pedro"
```
Para ejecutar la función con el parámetro simplemente la llamamos con el valor del parámetro a la derecha.

Si la función tiene dos o más parámetros, se indican entre comas en la definición y entre un espacio en la llamada a la función. Por ejemplo para sumar 1 más 4:

```powershell
function suma( $numero1, $numero2 ) { 
	
  $resultado = $numero1 + $numero2

  return $resultado

}

suma 1 4
```
Al final de la función hemos utilizado `return $resultado` para asegurarnos de que el valor que devolverá la función es `$resultado`. Hablaremos de `return` en el apartado posterior.

Como vemos al llamar a la función indicamos su nombre y a su derecha los parámetros separados por un espacio.

Para tener más claro qué parámetros utiliza una función, podemos llamar a la función `suma` indicando el nombre de los parámetros con el prefijo `-`, un espacio y el valor correspondiente:
```powershell
suma -numero1 43 -numero2 35
```
Otra forma de indicar los parámetros en la definición de una función es mediante el uso de `param()`:
```powershell
function suma {

  param ( $numero1, $numero2 )

  $resultado = $numero1 + $numero2

  return $resultado
}

suma -numero1 43 -numero2 35
```
Como vemos, los parámetros no se indican a la derecha del nombre de la función, se indican entre paréntesis a la derecha de `param` al principio del código de la función.

El resultado de una función puede guardarse en una variable para su uso posterior:
```powershell
$resultado_suma = suma -numero1 43 -numero2 35
```

## Devolución del resultado de una función
En el apartado anterior vimos el uso de `return` dentro de una función para devolver la variable `$resultado`.

Además de devolver variables, `return` también puede devolver de forma abreviada el resultado de alguna operación entre paréntesis:
```powershell
function suma {

  param ( $numero1, $numero2 )

  return ( $numero1 + $numero2 )	
}

suma -numero1 32 -numero2 45
```
De esta forma, ahorramos la línea de la definición de la variable `$resultado` y lo devolvemos igualmente.

## Scripts y estructura de funciones
En PS, para llamar a una función antes es necesario definirla. Si estamos desarrollando un script con muchas funciones conviene colocarlas en orden para después utilizarlas. El problema de seguir este orden es la dificultad de saber dónde comienza el código del script, pues lo encontraremos después de la definición de la última función.

Una solución a este problema sería definir primero una función, por ejemplo `main` y colocar en ella el código principal del script. Después de esta función se definen el resto de funciones y al final de la última función el script finalizaría con la llamada a la función `main`:

```powershell
function main {

  write-host "Comienzo del script dentro de la función main..."

  $nombre = "Pedro"

  # Llamada a la primera función
  saludo -nombre $nombre

  # Llamada a la segunda función
  despedida -nombre $nombre

}

function saludo ( $nombre ) {

  write-host "Hola $nombre"

}

function despedida ( $nombre ) {
    
  write-host "Adiós $nombre"
    
}

# Llamada a la función principal
main
```
De esta forma, el comienzo del código del script aparece al principio y es más fácil seguir el orden del código. 

Es muy importante indicar la llamada a la función `main` al final del script, pues en caso contrario no se ejecutará nada.

Siguiente apartado: [Archivos](./c06-archivos.md#archivos)