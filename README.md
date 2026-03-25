# 🚀 Laboratorio AWS: Control de Acceso por IP y Horario en S3

Este laboratorio demuestra cómo aplicar **seguridad granular en AWS** restringiendo el acceso a un bucket S3 mediante políticas IAM que combinan:
- Dirección IP de origen.
- Rango horario específico (hora Perú convertida a UTC).
Esto permite reforzar la seguridad y aplicar controles granulares sobre los datos almacenados.

## 🛠️ Servicios Utilizados
- **Amazon S3**: Creación y configuración del bucket.
- **IAM Policies**: Definición de reglas de acceso basadas en condiciones.
- **AWS CLI**: Validación y pruebas de acceso.

1. **Creación del Bucket S3**
   - Nombre: `s3-ip-test-jack`
   - Configuración inicial sin acceso público.

2. **Definición de Política IAM con Condiciones y Restricción por horario **
   - Crear una cuenta personal.
   - Crear una política por Json
     *Restricción por IP:
      ```json
     "Condition": {
       "IpAddress": {"aws:SourceIp": "190.XX.XX.XX/32"}
     }
     ```
     * Restricción por horario (ejemplo: acceso solo entre 08:00 y 18:00 UTC):
     ```json
     "Condition": {
       "DateGreaterThan": {"aws:CurrentTime": "2026-03-25T08:00:00Z"},
       "DateLessThan": {"aws:CurrentTime": "2026-03-25T18:00:00Z"}
     }
     ```
   - Descargar CLI de AWS para hacer pruebas de conexión.

3. **Pruebas de Acceso**
   - Utilizar PowerShell para conectarnos con AWS.
   - Configurar Usuario para conexión:
     comando : aws configure --profile UserTest
   - Ingresamos los Datos de Usuario
   - Listar Nuestro S3 para comprobar la conexión y permisos
     comando: aws s3 ls s3://s3-ip-test-jack --profile UserTest
     
## ✅ Resultados
- El bucket solo aceptó conexiones desde la IP configurada.
- Los intentos fuera del horario definido fueron bloqueados correctamente.
- Se validó la efectividad de las condiciones en la política IAM.

## 🧠 Aprendizajes
- Cómo aplicar **condiciones avanzadas** en políticas IAM.
- La importancia de combinar restricciones por **IP y tiempo** para mayor seguridad.


   
