# Tutorial de Powershell

PowerShell (en adelante PS), es un lenguaje de programación interpretado de `línea de comandos` y `scripting` publicado por Microsoft en 2006.

PS está basado en .NET y si bien en sus comienzos estaba orientado a la administración de Windows, con el tiempo ha evolucionado con distintas versiones, ampliando notablemente su funcionalidad e incluso existen versiones para otros sistemas operativos como GNU/Linux.

Este tutorial está dirigido a personas que no conocen PS o lo conocen poco y les gustaría manejarlo bien, pero es recomendable tener nociones de otros lenguajes de programación.

El enfoque de todo el tutorial es práctico, paso a paso y con ejemplos, y su contenido está distribuido en apartados y subapartados.

El primer apartado es la [Introducción](./c01-introduccion.md#introducción), y al finalizar éste existe un enlace para ir al siguiente apartado, así hasta el último.

Puedes hacerte una idea del tamaño del tutorial y también utilizarlo como referencia consultando el siguiente índice:

## Indice

- [Introducción](./c01-introduccion.md#introducción)
  - [Privilegios de ejecución](./c01-introduccion.md#privilegios-de-ejecución)
  - [Comportamiento de errores](./c01-introduccion.md#comportamiento-de-errores)
  - [Uso básico de Powershell](./c01-introduccion.md#uso-básico-de-powershell)
  - [Ejecución de scripts](./c01-introduccion.md#ejecución-de-scripts)
- [Tipos](./c02-tipos.md#tipos)
  - [Variables](./c02-tipos.md#variables)
  - [Matrices](./c02-tipos.md#matrices)
  - [Listas](./c02-tipos.md#listas)
  - [Hashes](./c02-tipos.md#hashes)  
- [Condiciones](./c03-condiciones.md#condiciones)
  - [If](./c03-condiciones.md#if)
  - [Operadores condicionales](./c03-condiciones.md#operadores-condicionales)  
  - [Múltiples evaluaciones](./c03-condiciones.md#múltiples-evaluaciones)
  - [Switch](./c03-condiciones.md#switch)
  - [Where](./c03-condiciones.md#where)
- [Bucles](./c04-bucles.md#bucles)
  - [foreach](./c04-bucles.md#foreach)
  - [for](./c04-bucles.md#for)
  - [while](./c04-bucles.md#while)
- [Funciones](./c05-funciones.md#funciones)
  - [Uso de parámetros en funciones](./c05-funciones.md#uso-de-parámetros-en-funciones)
  - [Devolución del resultado de una función](./c05-funciones.md#devolución-del-resultado-de-una-función)  
  - [Scripts y estructura de funciones](./c05-funciones.md#scripts-y-estructura-de-funciones)
- [Archivos](./c06-archivos.md#archivos)
  - [Lectura de archivos](./c06-archivos.md#lectura-de-archivos)
  - [Escritura de archivos](./c06-archivos.md#escritura-de-archivos)
- [Expresiones regulares](./c07-regex.md#expresiones-regulares)
  - [Caracteres especiales](./c07-regex.md#caracteres-especiales)    
  - [Secuencias de escape](./c07-regex.md#secuencias-de-escape)
  - [Extracción de patrones](./c07-regex.md#extracción-de-patrones)
  - [Amplitud ajustada](./c07-regex.md#amplitud-ajustada)
  - [Sustituciones](./c07-regex.md#sustituciones)
- [Objetos personalizados](./c08-objetos-personalizados.md#objetos-personalizados)
  - [Creación de un objeto personalizado](./c08-objetos-personalizados.md#creación-de-un-objeto-personalizado)
  - [Tablas con objetos personalizados](./c08-objetos-personalizados.md#tablas-con-objetos-personalizados)
  - [Búsqueda de registros](./c08-objetos-personalizados.md#búsqueda-de-registros)
- [Control de errores](./c09-control-de-errores.md#control-de-errores)
- [Módulos](./c10-modulos.md#módulos) 

Primer apartado: [Introducción](./c01-introduccion.md#introducción)
