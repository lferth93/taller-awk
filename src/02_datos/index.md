# Transformar datos con AWK

## while
- Tiene una condición y un cuerpo
- El cuerpo se ejecuta mientras que la condición sea verdad
- Como en C

```admonish example title='while'
i=1
while (i <= $2){
   print i,$1, $2
   i++
}
```

## for
En una sola linea está
- inicialización
- prueba
- incremento

```admonish example title='for'
{ for (i = 1; i <= $2; i++){
   print i, $1, $2
   }
}
```

## Arreglos
Para poder guardar grupos de datos relacionados

```admonish example title='arreglos'
{
   linea[NR] = $0
}
END{
   i=NR
   while(i > 0){
      print linea[i]
      i--
   }
}
```

## for in
forma alternativa de for util para recorrer arreglos

```admonish example title='forin'
{
   linea[NR] = $0
}
END{
   for(i in linea){
      print "animal:", linea[i]
   }
}
```

## arreglos asociativos
En awk los arreglos son asociativos:
- El indice de los arreglos no tiene que ser un entero positivo

El indice puede ser
-  cualquier numero
- o una cadena de texto

```admonish example title='arreglo_aso'
{
   linea[$1] = $2
}
END{
   for(i in linea){
      print i, linea[i]
   }
}
```

# Ejercicios
Utilizando la [base de datos de Pokemon](https://raw.githubusercontent.com/lgreski/pokemonData/refs/heads/master/Pokemon.csv)

1. Muestra las primeras 10 lineas
2. ¿cuántas lineas tiene el archivo?
3. ¿Cuantos campos deberían tener todas las lineas?  Muestra las lineas que no tienen todos los campos si las hay
4. ¿Cuántos pokemon de tipo principal agua hay?
4. ¿Cuántos pokemon de tipo principal secundario agua hay?
6. muestra los nombres de pokemon que tengan numero en su nombre
7. ¿Todos los pokemon tienen los puntos de salud de 0 a 100?
8. ¿qué pokemon tienen más defensa que ataque?
9. muestra los pokemon cuya suma de ataque y defensa especial sea menor a la suma de ataque y defensa normal
10. Muestra nombres de pokemon unicos
11. cuenta el número de veces que se repite cada nombre
12. muestra los pokemon cuyo nombre está más de una vez
13. Muestra las últimas 10 lineas

