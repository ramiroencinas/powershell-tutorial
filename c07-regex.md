# Expresiones regulares
Una expresión regular `regex` es un patrón de caracteres que queremos encontrar en un texto.

Puede utilizarse para:
- Encontrar información dentro de un texto
- Comprobar si un texto cumple con una serie de requisitos
- Extraer información concreta de un texto

Para utilizar expresiones regulares en PS necesitamos tres elementos:
- El texto donde buscaremos
- El operador `-match`
- Una expresión regular (patrón de texto) que aplicaremos sobre el texto anterior

Estos tres elementos normalmente se colocan entre paréntesis de una condición `if`, de forma que si la expresión regular o patrón es encontrado en el texto devuelve `$true` (cierto) y si no lo encuentra devuelve `$false` (falso). 

Un ejemplo básico es averiguar si la palabra `calabaza` se encuentra dentro de la variable `$texto`:
```powershell
$texto = "Esta calabaza es grande"

if ( $texto -match "calabaza" ) { write-host "Palabra encontrada" }
```
En este ejemplo, la expresión regular o patrón es el texto `calabaza`.

Un ejemplo más potente y práctico es comprobar si dentro de un texto aparece un número de teléfono de 9 cifras que comience por 6:
```powershell
$texto = "El número de teléfono es 654321123"

if ( $texto -match "6\d{8}" ) { write-host "Teléfono encontrado" }
```

Ten en cuenta que `-match` no distingue entre letras mayúsculas de minúsculas. Si necesitas esa distinción, utiliza `-cmatch` en lugar de `-match`.

## Caracteres especiales
Dentro de una expresión regular podemos utilizar caracteres especiales para crear patrones complejos y encontrar cualquier cosa, como hemos visto en el ejemplo anterior. Vamos a verlos.

### El caracter \+

El caracter `+` significa `una o más veces el caracter de la izquierda`:
```powershell
$texto = "Esta calabazzzzzza es grande"

if ( $texto -match "calabaz+a" ) { write-host "Encontrado" }
```
El ejemplo anterior encuentra dentro de `$texto` al menos las siguientes cadenas de texto:
```powershell
calabaza
calabazza
calabazzza
calabazzzzzzzzzzza
```
### El caracter \*
El caracter `*` significa `ninguna, una o más veces el caracter de la izquierda`: 
```powershell
$texto = "Esta calabaa es grande"

if ( $texto -match "calabaz*a" ) { write-host "Encontrado" }
```
El ejemplo anterior encuentra dentro de `$texto` al menos las siguientes cadenas de texto:
```powershell
calabaa
calabaza
calabazza
calabazzzzzzzza
```
### El caracter  ? 
El caracter `?` significa `ninguna o una vez el caracter de la izquierda`:
```powershell
$texto = "Esta calabaa es grande"

if ( $texto -match "calabaz?a" ) { write-host "Encontrado" }
```
El ejemplo anterior encuentra dentro de `$texto` solo las dos siguientes cadenas de texto:
```powershell
calabaa
calabaza
```
### El caracter \.

`.` significa `una vez cualquier carácter` menos el carácter de salto de línea:
```powershell
$texto = "Esta calabaza es grande"

if ( $texto -match "calaba.a" ) { write-host "Encontrado" }
```
El ejemplo anterior encuentra dentro de `$texto` al menos la siguientes cadenas de texto:
```powershell
calabaza
calabaxa
calaba3a
calabara
calabaca
```
Si utilizamos el punto y el asterisco juntos `.*` significa `cualquier caracter un número indeterminado de veces`, por ejemplo:
```powershell
$texto = "Al menos esta calabaza es grande y naranja"

if ( $texto -match "esta.*grande" ) { write-host "Encontrado" }
```
El ejemplo anterior encuentra en `$texto` el texto `esta`, después cualquier texto espacios incluidos y después `grande`.

### Las llaves \{ \}
Las llaves \{ \} indican el `número de ocurrencias del caracter de su izquierda`. Podemos indicar el número mínimo y máximo de ocurrencias separados por una coma:
```powershell
$texto = "calabazzza"

if ( $texto -match "calabaz{1,5}a" ) { write-host "Encontrado" }
```
El ejemplo anterior encuentra cualquiera de las 5 cadenas de texto siguientes, que tienen entre una y cinco efes entre `calaba` y `a`:
```powershell
calabaza
calabazza
calabazzza
calabazzzza
calabazzzzza
```
Si entre llaves sólo indicamos un número, sólo encuentra ese número de ocurrencias:
```powershell
$texto = "calabazzzza"

if ( $texto -match "calabaz{4}a" ) { write-host "Encontrado" }
```
El ejemplo anterior encuentra solamente la cadena de texto `calabazzzza` (con 4 zetas).

Para encontrar un mínimo de ocurrencias sin un máximo, indicamos entre llaves el número mínimo y una coma:
```powershell
$texto = "calabazzzzzzzzzza"

if ( $texto -match "calabaz{4,}a" ) { write-host "Encontrado" }
```
El ejemplo anterior encontrará:
```powershell
calabazzzza
calabazzzzzza
```

### Alternativas de caracter \[ \]
También podemos encontrar alternativas de caracteres indicadas entre corchetes. Por ejemplo, si necesitamos encontrar la palabra `calabaza` o `calabozo` dentro de la variable `$texto`:
```powershell
$texto = "La calabaza es grande"

if ( $texto -match "calab[ao]z[ao]" ) { write-host "Encontrado" }
```
El ejemplo anterior encuentra `calabaza` pero el siguiente con la misma expresión regular encuentra `calabozo`:
```powershell
$texto = "El calabozo es oscuro"

if ( $texto -match "calab[ao]z[ao]" ) { write-host "Encontrado" }
```
Como vemos, la expresión regular comienza con `calab`, después viene la alternativa entre corchetes (`a` o `o`) en la forma `[ao]`, sigue con `z` y por último vuelve de nuevo la alternativa `[ao]`.

### Alternativas de texto \|
Similar al apartado anterior pero con cadenas de texto utilizando tuberías:
```powershell
$texto = "Esta frase es interesante"

if ( $texto -match "es|no es|es poco|es muy" ) { write-host "Encontrado" }
```
El ejemplo anterior encontrará en `$texto` cualquiera de las cadenas de texto indicadas entre las tuberías.

Sustituye el valor de `$texto` con `Esta frase no es interesante` o `Esta frase es poco interesante` y también lo encontrará.

### Anclajes \^ y \$

Se utilizan para comprobar patrones de texto al principio y/o al final de una cadena de texto. 

Si queremos encontrar la palabra `Inicio` al principio del texto alojado en `$texto` utilizamos el acento circunflejo a la izquierda de `Inicio`:
```powershell
$texto = "Inicio de la frase y fin de ella"

if ( $texto -match "^Inicio" ) { write-host "Encontrado" }
```
Para encontrar la palabra `ella` al final del texto alojado en `$texto` utilizamos el símbolo dólar a la derecha de `ella`:
```powershell
$texto = "Inicio de la frase y fin de ella"

if ( $texto -match "ella$" ) { write-host "Encontrado" }
```
Y como puedes imaginar, podemos utilizar ambos símbolos para indicar cómo empieza y cómo termina la cadena de texto independientemente de lo que haya por medio:
```powershell
$texto = "Inicio de la frase y fin de ella"

if ( $texto -match "^Inicio.*?ella$" ) { write-host "Encontrado" }
```

### Encontrar caracteres especiales
Si necesitamos encontrar patrones que incluyan alguno de los caracteres especiales que hemos visto, como el punto, una llave o la interrogación, es necesario indicar este caracter especial pero precedido por la barra invertida o backslash `\`.

Por ejemplo, si queremos encontrar en `$texto` una o más interrogantes juntas, ponemos:
```powershell
$texto = "Es correcto??"

if ( $texto -match "\?+" ) { write-host "Encontrado" }
```
Para encontrar una barra invertida, hay que poner dos juntas:
```powershell
$texto = "c:\pruebas"

if ( $texto -match "c:\\" ) { write-host "Encontrado" }
```
## Secuencias de escape

Las expresiones regulares tienen un mecanismo para identificar ciertos grupos de caracteres. Por ejemplo, si necesito encontrar un dígito del 0 al 9 dentro de `$texto`, utilizamos la secuencia de escape `\d`, así:
```powershell
$texto = "Tengo 4 manzanas"

if ( $texto -match "\d" ) { write-host "Encontrado" }
```
El ejemplo anterior detecta el número `4` mediante la secuencia de escape `\d` que viene a significar `cualquier dígito`.

Aquí tienes una lista de algunas secuencias de escape muy útiles:

| Secuencia de escape | Equivalencia |
| :-----------------: | ------------ |
| \d                  | Cualquier dígito |
| \D                  | Cualquier carácter que no sea un dígito |
| \w                  | Cualquier letra, dígito y guión bajo |
| \W                  | Lo contrario que lo anterior |
| \s                  | Espacio en blanco, tabulador o retorno de carro |
| \S                  | Lo contrario de lo anterior |

Las secuencias de escape se pueden combinar en cualquier forma con los caracteres especiales y otros caracteres como vimos en el ejemplo del principio que encontraba números de teléfono que comienzan con 6 y con 9 dígitos:
```powershell
$texto = "El número de teléfono es 654321123"

if ( $texto -match "6\d{8}" ) { write-host "Teléfono encontrado" }
```
Como vemos, la expresión regular `6\d{8}` significa:
- Un 6
- Un dígito `\d`
- El caracter de la izquierda 8 veces `{8}`

Como vemos `{8}` significa: el dígito de la izquierda 8 veces, más el 6 del principo son los 9 dígitos.

## Extracción de patrones

Cuando `-match` o `-cmatch` encuentran un patrón en un texto, PS crea un hash nuevo denominado `$matches` donde aloja lo encontrado para poder recuperarlo:
```powershell
$texto = "El número de teléfono es 654321123"

if ( $texto -match "6\d{8}" ) { write-host "Teléfono encontrado" }
```

Ahora si vemos lo que contiene `$matches`:
```powershell
$matches

Name                           Value
----                           -----
0                              654321123
```
Queda disponible el resultado en el valor del primer elemento del hash `$matches[0]`:
```powershell
$matches[0]
654321123
```
También podemos extraer el número de teléfono sin la condición, utilizando `-match` directamente:
```powershell
$texto = "El número de teléfono es 654321124"

$texto -match "6\d{8}"
True

$matches[0]

654321124
```

Si necesitamos obtener varios valores de un texto, indicamos los patrones correspondientes entre paréntesis.

Por ejemplo, necesitamos los tres primeros dígitos y los tres últimos de `$texto`:
```powershell
$texto = "123hola456"

$texto -match "(^\d{3}).*?(\d{3}$)"
True

$matches
Name                           Value
----                           -----
2                              456
1                              123
0                              123hola456
```
Como vemos, el hash ahora contiene tres valores:
- En `$matches[1]` queda el valor del primer patrón entre paréntesis`(^\d{3})` que es `123`
- En `$matches[2]` queda el valor del segundo patrón entre paréntesis `(^\d{3})` que es `456`
- En `$matches[0]` queda el valor encontrado por la expresión regular completa

Los valores de `$matches` cambiarán con los resultados del siguiente uso de `-match` o `-cmatch`.

Si te fijas, hemos utilizado la expresión regular `.*?` en lugar de `.*` para indicar cualquier texto entre los números. El uso del símbolo de interrogación sirve para ajustar la amplitud de búsqueda y en el próximo apartado lo vamos a ver.

## Amplitud ajustada
La expresión regular `.*` significa cualquier texto de cualquier longitud. Por ejemplo:
```powershell
$texto = "La calabaza es grande grande"

$texto -match "calabaza.*grande"
True

$matches[0]
calabaza es grande grande
```
Como vemos encuentra el texto `calabaza es grande grande`.

Si necesitamos que solo encuentre `calabaza es grande` es necesario utilizar la expresión regular `.*?` para ajustar la búsqueda:
```powershell
$texto = "La calabaza es grande grande"

$texto -match "calabaza.*?grande"
True

$matches[0]
calabaza es grande
```

## Sustituciones

El operador `-replace` sustituye unas cadenas de texto por otras y también puede utilizar expresiones regulares.

Por ejemplo, dada la cadena `Hola Pedro` alojada en la variable `$texto`, sustituyamos `Hola` por ` Hasta luego` y dejemos el resultado en `$texto2`:
```powershell
$texto = "Hola Pedro"

$texto2 = $texto -replace "Hola", "Hasta luego"

$texto2
Hasta luego Pedro
```
Mediante expresiones regulares también podemos sustituir patrones entre paréntesis con los resultados obtenidos alojados en las variables temporales $1, $2, $3...:
```powershell
$texto = "Hola Pedro"

$texto2 = $texto -replace '(.*) (.*)','$2 $1'

$texto2
Pedro Hola
```
Fíjate bien que entre los dos grupos de paréntesis hay un espacio.

Ten en cuenta que el uso de `-replace` con este tipo especial de variables `$1` y `$2` es necesario utilizar comillas simples en lugar de comillas dobles.

Siguiente apartado: [Objetos personalizados](./c08-objetos-personalizados.md#objetos-personalizados)

