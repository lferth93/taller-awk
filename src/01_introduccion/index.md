# Introducción a AWK

## ¿Como ejecutar AWK?
AWK se puede ejecutar desde la terminal, el comando base es `awk`.

```bash
awk --version
```

De esta manera podemos verificar que AWK esta instalado en nuestro sistema y tendremos informacion sobre la version de AWK que estamos usando.

## Hola Mundo

```bash
awk 'BEGIN { print "Hola Mundo" }'
```

## Datos

AWK trabaja con datos en forma de tablas, donde cada linea es una fila y cada columna es una columna.

```
Beth 21 0
Dan 19 0
Kathy 15.50 10
Mark 25 20
Mary 22.50 22
Susie 17 18
```

Copia estos datos en un archivo llamado `datos.txt` para usarlos en los ejemplos.


## Estructura de un programa de AWK

Un programa de AWK consta de tres secciones:

```bash
awk 'BEGIN { acciones } patrones { acciones } END { acciones }' archivo
```

- `BEGIN`: Se ejecuta antes de procesar el archivo.
- `patrones`: Se ejecuta para cada linea del archivo.
- `END`: Se ejecuta despues de procesar el archivo.

Por ejemplo:

```bash
awk '{ print $1 }' datos.txt
```

Imprime la primera columna de cada linea del archivo.

Cuando una accion no tiene un patron, se ejecuta para cada linea del archivo.

## Variables

AWK tiene variables internas que podemos usar para acceder a la linea actual y la columna actual.

- `NF`: Numero de campos (columnas) de la linea actual.
- `NR`: Numero de linea actual.
- `FS`: Separador de campos (columnas).
- `RS`: Separador de lineas.
- `OFS`: Separador de campos (columnas) de salida.
- `ORS`: Separador de lineas de salida.

Por ejemplo:

```bash
awk '{ print NF, NR, FS, RS, OFS, ORS }' datos.txt
```

Imprime el numero de campos, numero de linea, separador de campos, separador de lineas, separador de campos de salida y separador de lineas de salida.

## Algo un poco mas interesante

```bash
awk '{ print $1, $2 }' datos.txt
```

Imprime la primera y segunda columna de cada linea del archivo.

```bash
awk '$3>0 { print $1, $2 * $3 }' datos.txt
```

Imprime la primera columna y la segunda columna multiplicada por la tercera columna si la tercera columna es mayor a 0.

```admonish example title="Ejercicio"
Imprime la primera columna de las lineas donde la tercera columna sea igual a 0.
```

## Lineas de archivo

```admonish example title="Ejercicio"
Imprime todas las lineas del archivo `datos.txt` agregando el numero de linea al inicio de cada linea.
```

## Agregar texto a una linea

```bash
awk '{ print "Linea " NR, $0 }' datos.txt
```

Imprime todas las lineas del archivo `datos.txt` agregando la palabra "Linea" y el numero de linea al inicio de cada linea.

```admonish example title="Ejercicio"
Para cada linea del archivo `datos.txt` imprimir el mensaje "NOMBRE tiene que pagar un total de $TOTAL". 

Donde NOMBRE es la primera columna y TOTAL es la segunda columna multiplicada por la tercera columna.
```

## Limitaciones de AWK

AWK es un lenguaje de programacion simple y limitado, no contiene funciones para tareas muy especificas como ordenar, pero si conoces otras herramientas como `sort` puedes usarlas en combinacion con AWK para resolver problemas mas complejos.

Esto gracias a la filosofia de diseño de unix, que es que cada herramienta debe hacer una cosa y hacerla bien.

Ejemplo:

```bash
awk '$3>0 { print $2 * $3, $1 }' datos.txt | sort
```

Imprime la segunda columna multiplicada por la tercera columna y la primera columna ordenada.

```admonish example title="Ejercicio"
Imprime la lista en orden decreciente de el TOTAL y el NOMBRE.

Pista:
sort tiene una opcion inteResante que permite inveRtiR el orden de las lineas.
```



## Patrones mas interesantes
AWK tiene patrones que nos permiten seleccionar lineas de un archivo.

Por ejemplo:

```bash
awk '$3>0 { print $1, $2 * $3 }' datos.txt
```

Imprime todas las lineas donde la tercera columna sea mayor a 0.

Otro ejemplo:

```bash
awk '$2>20 { print $1 , $2 * $3 }' datos.txt
```

Imprime todas las lineas donde la segunda columna sea mayor a 20.

Ademas AWK permite combinar diferentes patrones de seleccion. Mediante el uso de `&&` y `||`.  

```admonish example title="Ejercicio"
Imprime todas las lineas donde la segunda columna sea mayor a 20 y la tercera columna sea mayor a 0.
```

```admonish example title="Ejercicio"
Imprime todas las lineas donde el producto de la segunda columna y la tercera columna sea mayor a 200 y menor a 500.
```

## Seleccionar por texto

AWK tambien permite seleccionar lineas por texto.

```bash
awk '$1=="Mark" { print $1, $2 * $3 }' datos.txt
```

Imprime la primera columna y la segunda columna multiplicada por la tercera columna si la primera columna es igual a "Mark".

Este mismo resultado se puede obtener con expresiones regulares:

```bash
awk '$1~/Mark/ { print $1, $2 * $3 }' datos.txt
```

```admonish example title="Ejercicio"
Imprime las lineas donde el NOMBRE empieza con la letra "M".
```

```admonish example title="Ejercicio"
Imprime las lineas donde el NOMBRE es Mary o Dan.
```

```admonish example title="Ejercicio"
Imprime las lineas donde el NOMBRE empieza con la letra "M" y la tercera columna sea mayor a 0.
```

