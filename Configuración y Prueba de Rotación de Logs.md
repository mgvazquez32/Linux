# Configuración y Prueba de Rotación de Logs con Logrotate

---

### **1. Crear un archivo de log de prueba**

Vamos a generar un archivo de log en `/var/log` llamado `mi_aplicacion.log`:

```bash
sudo touch /var/log/mi_aplicacion.log
sudo chmod 644 /var/log/mi_aplicacion.log
```

Este será el archivo de log que rotaremos.

### **2. Crear la configuración de Logrotate**

Creamos un archivo de configuración en `/etc/logrotate.d/` para manejar la rotación de logs de nuestra aplicación.

```bash
sudo nano /etc/logrotate.d/mi_aplicacion
```

Agrega el siguiente contenido:

```bash
/var/log/mi_aplicacion.log {
    daily          
    rotate 5       
    compress       
    missingok      
    notifempty     
    copytruncate
    postrotate
        echo "Rotación completada en $(date)" >> /var/log/mi_aplicacion.log
    endscript
}
```

Esto asegura que:

- Se rota diariamente.
- Se guardan los últimos 5 archivos.
- Se comprimen los logs viejos.
- No da error si el log no existe.
- Se vacía el archivo sin perder la referencia del proceso que lo escribe.

### **3. Agregar contenido al log para probar**

Simulamos la escritura en el log con un bucle `for`:

```bash
for i in {1..20}; do echo "Log entry $i - $(date)" >> /var/log/mi_aplicacion.log; sleep 1; done
```

### **4. Ejecutar Logrotate manualmente**

En lugar de esperar al cron diario, forzamos la rotación con:

```bash
sudo logrotate -f /etc/logrotate.d/mi_aplicacion
```

### **5. Verificar la rotación**

Revisamos los archivos generados en `/var/log/`:

```bash
ls -lh /var/log/mi_aplicacion*
```

Deberías ver archivos como:

```bash
mi_aplicacion.log
mi_aplicacion.log.1.gz
mi_aplicacion.log.2.gz
mi_aplicacion.log.3.gz
mi_aplicacion.log.4.gz
mi_aplicacion.log.5.gz
```

También podemos revisar el contenido de los logs rotados:

```bash
zcat /var/log/mi_aplicacion.log.1.gz
```

## **Posible error de permisos:**

```bash
sudo chmod 755 /var/log
sudo chmod 644 /var/log/mi_aplicacion.log
sudo chown root:root /var/log/mi_aplicacion.log
```