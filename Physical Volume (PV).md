# Physical Volume (PV)

---

Se puede montar un disco externo y usarlo como **Physical Volume (PV)** en LVM. A continuación, te explico los pasos:

### **1. Conectar y verificar el disco externo**

Conecta el disco externo a tu sistema y usa `lsblk` o `fdisk -l` para identificar su nombre:

```bash
lsblk
```

Supongamos que el disco aparece como `/dev/sdb`.

### **2. Crear una partición LVM en el disco externo (opcional)**

Si el disco no tiene una partición, puedes crearla usando `fdisk`:

```bash
fdisk /dev/sdb
```

Dentro de `fdisk`, sigue estos pasos:

1. Presiona `n` (nueva partición).
2. Selecciona `p` (primaria).
3. Acepta los valores predeterminados (o el tamaño que necesites).
4. Cambia el tipo de partición a LVM con `t` y selecciona el código `8e`.
5. Guarda los cambios con `w`.

Si el disco no tenía tabla de particiones, puedes usar `parted`:

```bash
parted /dev/sdb mklabel gpt
parted /dev/sdb mkpart primary 0% 100%
parted /dev/sdb set 1 lvm on
```

### **3. Crear el Physical Volume (PV)**

Ejecuta el siguiente comando para inicializar el disco como PV:

```bash
pvcreate /dev/sdb1
```

### **4. Crear un Volume Group (VG)**

Si quieres usar solo este disco en un VG nuevo:

```bash
vgcreate mi_vg /dev/sdb1
```

Si deseas agregarlo a un VG existente:

```bash
vgextend mi_vg /dev/sdb1
```

### **5. Crear y usar un Logical Volume (LV)**

```bash
lvcreate -L 10G -n mi_lv mi_vg
mkfs.ext4 /dev/mi_vg/mi_lv  # Formatear el volumen lógico

mkdir /mnt/mi_lv
mount /dev/mi_vg/mi_lv /mnt/mi_lv
```

### **6. Configurar el montaje automático (opcional)**

Para que el LV se monte automáticamente al reiniciar, agrega la entrada a `/etc/fstab`:

```bash
echo "/dev/mi_vg/mi_lv /mnt/mi_lv ext4 defaults 0 2" >> /etc/fstab
```

---

### **Notas importantes**

- Si desconectas el disco externo, el VG y los LVs asociados dejarán de estar accesibles hasta que vuelvas a conectar el disco.
- Si el disco se conecta con otro nombre (`/dev/sdc`, etc.), puedes usar `UUID` en `/etc/fstab` para evitar problemas:

Luego, usa el `UUID` en `/etc/fstab` en lugar de `/dev/mi_vg/mi_lv`.
    
    ```bash
    blkid /dev/mi_vg/mi_lv
    ```