# Variables en BASH

---

### 1. **Variables Locales**

Son variables definidas dentro de un script o una función y solo son accesibles dentro de ese ámbito.

```bash
my_var="Hola Mundo"
echo $my_var  # Salida: Hola Mundo
```

Cuando se definen dentro de una función, solo existen dentro de ella:

```bash
mi_funcion() {
    local mensaje="Hola desde la función"
    echo $mensaje
}

mi_funcion  # Salida: Hola desde la función
echo $mensaje  # No mostrará nada porque es local
```

---

### 2. **Variables de Entorno (Globales)**

Son accesibles en todo el entorno de trabajo, incluidos los scripts y procesos hijos. Se crean con `export`.

```bash
export PATH="/usr/local/bin:$PATH"
echo $PATH  # Se mantiene en todos los procesos hijos
```

Ejemplo de cómo un proceso hijo puede acceder a una variable de entorno:

```bash
export MI_VARIABLE="Soy global"
bash -c 'echo $MI_VARIABLE'  # Salida: Soy global
```

---

### 3. **Variables de Posición**

Permiten acceder a los argumentos pasados a un script o función.

```bash
#!/bin/bash
echo "Primer argumento: $1"
echo "Segundo argumento: $2"
echo "Número total de argumentos: $#"
```

Si ejecutamos `./script.sh Hola Mundo`, la salida será:

```
Primer argumento: Hola
Segundo argumento: Mundo
Número total de argumentos: 2
```

También se pueden usar `"$@"` y `"$*"` para manejar múltiples argumentos:

```bash
echo "Todos los argumentos: $@"
```

---

### 4. **Variables Especiales**

Son variables internas de Bash con significados específicos:

- `$?` → Código de salida del último comando ejecutado
- `$$` → PID del proceso actual
- `$#` → Número de argumentos pasados al script
- `$@` → Todos los argumentos como una lista
- `$*` → Todos los argumentos como una sola cadena
- `$0` → Nombre del script

Ejemplo:

```bash
ls /home
echo "Código de salida del último comando: $?"  # 0 si tuvo éxito, otro número si falló
echo "PID del script actual: $$"
```

---

### 5. **Variables de Cadena**

Bash trata todas las variables como cadenas a menos que se evalúen de manera aritmética.

```bash
cadena="Hola Mundo"
echo ${cadena:5}  # Mundo (subcadena desde el índice 5)
echo ${#cadena}  # 10 (longitud de la cadena)
```

Concatenación:

```bash
nombre="Juan"
mensaje="Hola, $nombre"
echo $mensaje  # Salida: Hola, Juan
```

---

### 6. **Variables Aritméticas**

Aunque Bash no tiene tipos de datos numéricos explícitos, se pueden realizar operaciones aritméticas con `(( ))`, `let` o `expr`.

```bash
a=10
b=5

echo $((a + b))  # 15
let c=a*b
echo $c  # 50
expr $a - $b  # 5
```

Ejemplo de incremento:

```bash
contador=0
((contador++))
echo $contador  # 1
```