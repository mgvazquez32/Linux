# Practica1 AWK

En esta practica vamos a trabajar con un archivo CSV (deliminado por comas) llamado empleados.csv.

## 1. Crear un archivo de CSV llamado empleados.csv con el siguiente contenido:

```csv
Nombre,Apellido,Departamento,Salario
Juan,Pérez,Ventas,35000
María,González,Recursos Humanos,42000
Carlos,Rodríguez,Finanzas,48000
Ana,Martínez,Marketing,38000
Pedro,Díaz,Producción,40000
Laura,Fernández,Ventas,36000
Javier,Ruiz,Recursos Humanos,43000
Sofía,López,Marketing,39000
Diego,Hernández,Producción,41000
Elena,García,Finanzas,47000
```

## 2. Ejecuta las siguientes intrucciones dentro del archivo main.sh en replit.com

### 2.1 Imprimir el contenido de un archivo

```bash
printf "Archivo\n"
awk '{print}' empleados.csv
```

### 2.2 Imprime los empleados que pertenecen al departamento de Marketing

```bash
printf "Busca Marketing:\n"
awk 'NR > 1 && /Marketing/ {print}' empleados.csv
```

### 2.3 Muestra la columna Nombre y Salario
```bash
printf "Columna Nombre y Salario:\n"
awk -F',' 'NR > 1 {print $1,$4}' empleados.csv
```

### 2.4 Muestra el numero de linea

```bash
printf "Numero de linea:\n"
awk 'NR > 1 {print NR,$0}' empleados.csv
```

### 2.5 Imprime dinamicamente el ultimo campo

```bash
printf "Imprime Nombre y Salario:\n"
awk -F',' 'NR > 1 {print $1,$NF}' empleados.csv
```

### 2.6 Muestra el contenido entre la linea 3 y 6

```bash
printf "Contenido entre la linea 3 y 6:\n"
awk -F',' 'NR==3, NR==6 {print NR,$0}' empleados.csv
```
### 2.7 Imprime el nombre y el salario separado con un guion.

```bash
awk -F',' 'NR > 1 {OFS="-"; print $1, $4}' empleados.csv
```

### 2.8 Imprime cada linea y lo separa con un enter.

```bash
awk -F',' 'NR > 1 {print $0 ORS}' empleados.csv
```

## Links:

- [Documentacion AWK](https://linux.die.net/man/1/awk)