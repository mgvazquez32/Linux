# Sistema de Archivos

---

## **¿Qué es un sistema de archivos?**

Un sistema de archivos es la forma en que un sistema operativo organiza y almacena archivos en un disco. Es como la "biblioteca" del sistema, donde cada archivo tiene un lugar específico para ser guardado y recuperado.

---

## **Principales Sistemas de Archivos en Linux**

### **1. Ext2 (Second Extended Filesystem)**

📌 **Año:** 1993

📌 **Características:**

- Diseñado para superar limitaciones del primer sistema de archivos en Linux.
- **No tiene journaling**, lo que significa que no guarda un registro de cambios en los archivos.
- Es ideal para **memorias USB** porque **consume menos espacio** y evita escrituras innecesarias.
- Soporta **archivos de hasta 2TB** y un sistema de archivos de **hasta 32TB**.

🛠 **Ejemplo práctico:**

Si quieres formatear una memoria USB con `ext2`, puedes usar el siguiente comando:

```bash
mkfs.ext2 /dev/sdX
```

---

### **2. Ext3 (Third Extended Filesystem)**

📌 **Año:** 2001

📌 **Características:**

- Es una evolución de **ext2** con una gran mejora: **incluye journaling**.
- **El journaling permite recuperar datos en caso de fallos**, ya que guarda un registro de cambios antes de aplicarlos.
- Soporta **2TB por archivo y 32TB en total**.
- Permite hasta **32,000 subdirectorios**.
- Se puede **convertir** un sistema de archivos **ext2 en ext3** sin perder datos.

🛠 **Ejemplo práctico:**

Para convertir un sistema de archivos `ext2` a `ext3`:

```bash
tune2fs -j /dev/sdX
```

---

### **3. Ext4 (Fourth Extended Filesystem)**

📌 **Año:** 2008

📌 **Características:**

- Es la versión mejorada de `ext3`, usada en la mayoría de distribuciones Linux hoy en día.
- Soporta archivos de **hasta 16TB** y un sistema de archivos de **hasta 1 Exabyte (1EB = 1024PB = 1024×1024TB)**.
- Permite hasta **63,000 subdirectorios**.
- Tiene mejoras en rendimiento con **multiblock allocation** y **journal checksum** (mejor seguridad).

🛠 **Ejemplo práctico:**

Para formatear una partición en `ext4`:

```bash
mkfs.ext4 /dev/sdX
```

---

### **4. XFS (Alta Capacidad y Rendimiento)**

📌 **Creador:** Silicon Graphics Inc.

📌 **Características:**

- Diseñado para **altas capacidades** y rendimiento eficiente con archivos grandes.
- Puede manejar **particiones de hasta 1 Exabyte**.
- Es ideal para servidores y bases de datos de alto rendimiento.

🛠 **Ejemplo práctico:**

Para crear un sistema de archivos XFS en una partición:

```bash
mkfs.xfs /dev/sdX
```

---

### **5. SWAP (Memoria Virtual)**

📌 **Uso:** No es un sistema de archivos como tal, sino una partición utilizada para memoria virtual.

📌 **Regla general:**

- Si tienes **menos de 2GB de RAM**, usa el **doble de la RAM** en SWAP.
- Si tienes **más de 2GB de RAM**, usa aproximadamente **1.5 veces la RAM**.

🛠 **Ejemplo práctico:**

Para crear una partición de swap y activarla:

```bash
mkswap /dev/sdX
swapon /dev/sdX
```

---

### **6. Btrfs (B-Tree Filesystem)**

📌 **Características:**

- Es un sistema de archivos moderno con características avanzadas como **snapshots y compresión**.
- Aún **no se considera completamente maduro** para producción.

🛠 **Ejemplo práctico:**

Para crear un sistema de archivos `btrfs`:

```bash
mkfs.btrfs /dev/sdX
```

---

## **¿Cuál sistema de archivos elegir?**

| Sistema | Ventaja Principal | Ideal Para |
| --- | --- | --- |
| **Ext2** | Bajo consumo de espacio | Memorias USB |
| **Ext3** | Recuperación en fallos | Sistemas antiguos |
| **Ext4** | Rápido y confiable | Uso general en Linux |
| **XFS** | Gran capacidad y velocidad | Servidores y bases de datos |
| **Btrfs** | Snapshots y compresión | Experimentación |
| **SWAP** | Memoria virtual | Mejorar rendimiento en RAM baja |

---

## **Conclusión**

El sistema de archivos es **clave** en el almacenamiento y rendimiento del sistema operativo. **Ext4** es el más usado hoy en día, pero **XFS** y **Btrfs** tienen ventajas en casos específicos.

---

### **¿Qué es Journaling en un sistema de archivos?**

📌 **Definición simple:**

Journaling es una técnica que **registra cambios antes de aplicarlos** en el sistema de archivos. Esto ayuda a evitar la pérdida de datos en caso de fallos inesperados, como cortes de energía o bloqueos del sistema.

### **¿Cómo funciona?**

1. **Se registra la acción en un "diario" (journal)** 
    - Antes de modificar un archivo, el sistema guarda una nota sobre el cambio en una zona especial del disco (el journal).
2. **Se aplican los cambios reales** 
    - Luego de registrar el cambio, el sistema modifica el archivo en el disco.
3. **Se marca como completado** 
    - Cuando el cambio se ha aplicado correctamente, el sistema borra la entrada del journal.

💡 **Ejemplo práctico:**

- Sin journaling: Si estás guardando un archivo y hay un corte de luz, el archivo puede quedar dañado o incompleto.
- Con journaling: Cuando el sistema se reinicia, revisa el journal y completa o revierte los cambios pendientes.

---

### **Ejemplo en Linux**

Si tienes una partición con `ext3` y quieres ver si tiene journaling activado:

```bash
tune2fs -l /dev/sdX | grep "Filesystem features"
```

Si ves **has_journal**, significa que el journaling está activo.

<aside>
📝

El journaling es como un **cuaderno de notas** del sistema de archivos. **Ayuda a prevenir pérdida de datos** en caso de fallos y mejora la recuperación del sistema. **Ext3, Ext4, XFS y Btrfs** son sistemas de archivos que lo utilizan.

</aside>