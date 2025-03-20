# Expresiones en BASH

---

### **1. Expresiones en Bash**

Las expresiones en Bash se utilizan para evaluar condiciones, realizar operaciones aritméticas, manipular cadenas y comparar valores. Se pueden clasificar en varios tipos:

### **1.1 Expresiones Aritméticas**

Se usan para realizar operaciones matemáticas y evaluarlas en diferentes formas:

```bash
a=10
b=5

echo $((a + b))  # 15
echo $((a - b))  # 5
echo $((a * b))  # 50
echo $((a / b))  # 2
echo $((a % b))  # 0
```

O con `let`:

```bash
let suma=a+b
echo $suma  # 15
```

También con `expr`:

```bash
expr $a + $b  # 15
```

### **1.2 Expresiones de Comparación Numérica**

Se utilizan con `[[ ... ]]`, `(( ... ))` o `[ ... ]`.

```bash
a=10
b=5

# Con [[ ]]
if [[ $a -gt $b ]]; then
    echo "$a es mayor que $b"
fi

# Con (( ))
if (( a > b )); then
    echo "$a es mayor que $b"
fi

# Con [ ]
if [ $a -gt $b ]; then
    echo "$a es mayor que $b"
fi
```

| **Operador** | **Significado** |
| --- | --- |
| `-eq` | Igual (==) |
| `-ne` | Diferente (!=) |
| `-gt` | Mayor que (>) |
| `-lt` | Menor que (<) |
| `-ge` | Mayor o igual (>=) |
| `-le` | Menor o igual (<=) |

---

### **1.3 Expresiones de Comparación de Cadenas**

Se usan con `[[ ... ]]` o `[ ... ]` para comparar strings.

```bash
str1="Hola"
str2="Mundo"

if [[ $str1 == "Hola" ]]; then
    echo "Las cadenas son iguales"
fi

if [[ $str1 != $str2 ]]; then
    echo "Las cadenas son diferentes"
fi

```

| Operador | Significado |
| --- | --- |
| `==` | Igual a |
| `!=` | Diferente de |
| `-z` | Cadena vacía |
| `-n` | Cadena no vacía |

Ejemplo con `-z` y `-n`:

```bash
cadena=""

if [[ -z $cadena ]]; then
    echo "La cadena está vacía"
fi
```

---

### **1.4 Expresiones de Comparación de Archivos**

Para verificar existencia, permisos, tipos de archivos, etc.

```bash
archivo="ejemplo.txt"

if [[ -e $archivo ]]; then
    echo "El archivo existe"
fi
```

| **Operador** | **Significado** |
| --- | --- |
| `-e` | Existe |
| `-f` | Es un archivo |
| `-d` | Es un directorio |
| `-r` | Tiene permiso de lectura |
| `-w` | Tiene permiso de escritura |
| `-x` | Es ejecutable |

Ejemplo con directorios:

```bash
if [[ -d "/home/user" ]]; then
    echo "El directorio existe"
fi
```

---

### **1.5 Expresiones Lógicas**

Para combinar condiciones (`&&` y `||`).

```bash
if [[ $a -gt 5 && $b -lt 10 ]]; then
    echo "Ambas condiciones son verdaderas"
fi

if [[ $a -gt 20 || $b -lt 10 ]]; then
    echo "Al menos una condición es verdadera"
fi
```