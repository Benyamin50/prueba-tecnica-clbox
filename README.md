# Mi prueba técnica para CLBOX – Filebrowser con Docker
Candidato: Benjamín Calderón
Fecha: 13/05/2026

¿Qué hice?
Desplegué Filebrowser, con persistencia de archivos y control de acceso.

Comandos que usé:
bash
Levantar el servicio (en segundo plano)
docker compose up -d

Ver si todo va bien o hay errores
docker logs clbox-filebrowser

Borrar todo (con volúmenes) para empezar de cero
docker compose down -v

Problemas que tuve y cómo los solucion:

1. Docker no arrancaba – Virtualización desactivada
Mi pc tenía el SVM Mode apagado en la BIOS.
Entré a la BIOS, activé SVM, reinicié WSL2 y Docker funcionó.

2. La base de datos (SQLite) se peleaba con Windows
Quise mapear filebrowser.db directo en mi disco y el contenedor se bloqueaba por permisos de Windows.
 Solución práctica:

Usé un volumen nombrado fb_database solo para la base de datos.

Dejé la carpeta ./data para mis archivos normales, accesible desde el explorador de Windows.

3. admin / admin no funcionaba – contraseña aleatoria

La imagen moderna de Filebrowser genera una contraseña aleatoria en el primer arranque (por seguridad)
Revisé los logs con docker logs y allí aparecía la clave real. La usé una vez y luego la cambié por una mía.

¿Funciona?
Sí, subí un archivo hola-mundo.txt y se veía en la interfaz.
En la carpeta assets estan todas las pruebas.
