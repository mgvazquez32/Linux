# Practica comando sed

Al igual que las practicas anteriores vamos a ejecutar los siguiente comandos en nuestro archivo main.sh.

## 1. Buscar y remplazar

```bash
echo "Este es un texto de ejemplo." > archivo.txt
cat archivo.txt

sed -i 's/ejemplo/ejemplo modificado/g' archivo.txt
cat archivo.txt
```

## 2. Eliminar una linea que coincida con un patron.

```bash
echo -e "Primera línea\nSegunda línea\nLínea con patrón\nCuarta línea" > archivo.txt
cat archivo.txt

sed -i '/patrón/d' archivo.txt
cat archivo.txt
```

## 3. Añadir una linea luego de una linea que coincida con un patron.

```bash
echo -e "Línea 1\nLínea con patrón\nLínea 3" > archivo.txt
cat archivo.txt

sed -i '/patrón/a\
Nueva línea añadida' archivo.txt

cat archivo.txt
```

## 4. Eliminar un texto especifico de todas las lineas.

```bash
echo -e "Texto a borrar\nOtra línea con texto a borrar\nTexto sin borrar" > archivo.txt
cat archivo.txt

sed -i 's/texto a borrar//g' archivo.txt
cat archivo.txt
```

## 5. Igual que la anterior solo que contempla mayusculas y minusculas.

```bash
echo -e "Texto a borrar\nOtra línea con texto a borrar\nTexto sin borrar" > archivo.txt
cat archivo.txt

sed -i 's/[Tt]exto a borrar//g' archivo.txt
cat archivo.txt
```

## 6. Reemplazar todas las apariciones de una palabra en un archivo

```bash
echo -e "Hola mundo\nMundo feliz\nEl mundo es grande" > archivo.txt
cat archivo.txt

sed -i 's/mundo/planeta/g' archivo.txt

cat archivo.txt
```

## 7. Insertar una línea antes de una línea que coincida con un patrón

```bash
echo -e "Línea 1\nLínea con patrón\nLínea 3" > archivo.txt
cat archivo.txt

sed -i '/patrón/i\
Línea insertada antes' archivo.txt

cat archivo.txt
```

## 8. Eliminar la primera línea de un archivo

```bash
echo -e "Primera línea\nSegunda línea\nTercera línea" > archivo.txt
cat archivo.txt

sed -i '1d' archivo.txt

cat archivo.txt
```