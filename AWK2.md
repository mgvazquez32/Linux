# Practica2 AWK

En esta practica vamos a trabajar con un archivo de texto llamado datos.txt, este archivo a diferencia del anterior esta separado por tabulaciones en lugar de comas.

## 1. Crear un archivo llamado datos.txt con el siguiente contenido:

```txt
A  B  C
Tarun  A12  1
Man  B6  2
Praveen  M42  3
```

## 2. Ejecuta las siguientes intrucciones dentro del archivo main.sh en replit.com

### 2.1 Imprimir el contenido de un archivo

```bash
printf "Muestra #line +  - + columna1\n"
awk '{print NR "-" $1}' datos.txt
```

### 2.2 Muestra el contenido de la columna 2

```bash
printf "Muestra columna 2\n"
awk '{print $2}' datos.txt
```

### 2.3 Contar las lineas de un archivo

```bash
printf "Contar las lineas de un archivo\n"
awk 'END {print "Numero de lineas:", NR -1}' datos.txt
```

### 2.4 Mostrar las lineas con mas de 10 caracteres

```bash
printf "Mostrar las lineas con mas de 10 caracteres\n"
awk 'length($0) > 10' datos.txt
```

### 2.5 Imprimir el cuadrado de los numeros del 1 al 10

```bash
printf "Imprimir el cuadrado de los numeros del 1 al 10\n"
awk 'BEGIN {for (i=1; i<=10; i++) print i, i*i}'
```