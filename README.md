Mi prueba técnica para CLBOX – Filebrowser con Docker
Candidato: Benjamín Calderón
Fecha: 13/05/2026

Resumen del Proyecto
Desplegué con éxito Filebrowser utilizando Docker, asegurando la persistencia de archivos, una gestión eficiente de la base de datos y control de acceso configurado.

Comandos de Gestión
Utilicé los siguientes comandos para la administración del contenedor:

Levantar el servicio: Ejecución en segundo plano.

Bash
docker compose up -d
Monitoreo: Verificación de logs para control de errores.

Bash
docker logs clbox-filebrowser
Limpieza total: Eliminación de contenedores y volúmenes para un reinicio limpio.

Bash
docker compose down -v
 Desafíos y Soluciones
1. Error de arranque: Virtualización desactivada
Problema: Docker no iniciaba debido a que la virtualización estaba desactivada a nivel de hardware.

Solución: Accedí a la BIOS para activar el SVM Mode, reinicié WSL2 y el motor de Docker funcionó correctamente.

2. Conflicto de permisos: SQLite vs Windows
Problema: Al intentar mapear el archivo filebrowser.db directamente en el host, el contenedor se bloqueaba por restricciones de permisos del sistema de archivos de Windows.

Solución: Implementé un volumen nombrado (fb_database) exclusivamente para la base de datos, mientras que la carpeta ./data se mantuvo mapeada localmente para facilitar el acceso a los archivos desde el explorador de Windows.

3. Acceso inicial: Credenciales por defecto
Problema: El login estándar admin/admin no permitía el acceso.

Solución: Identifiqué que las versiones modernas generan una contraseña aleatoria por seguridad en el primer arranque. Consulté los logs del contenedor para obtener la clave temporal y procedí a cambiarla por una credencial personalizada tras el primer ingreso.

Validación de Funcionamiento
El servicio está totalmente operativo:

Se confirmó la persistencia al subir el archivo hola-mundo.txt, visualizándose correctamente en la interfaz.

Las evidencias adicionales se encuentran disponibles en la carpeta assets.
