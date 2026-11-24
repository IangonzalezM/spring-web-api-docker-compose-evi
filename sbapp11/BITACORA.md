Bitácora – TP Integrador EVI 2026 
Integrantes: Damian Sponza · Ian Gonzalez | Repo: spring-web-api-docker-compose-evi 
(sbapp11) 
Decisiones con IA 
• Decisión 1 – Vista web (index.html) y actualización de README.md 
o Autoría: Damian Sponza.  
o Herramienta y consulta: IA; cómo crear un frontend estático (index.html) 
sobre /api/v1 y completar el README.md sin alterar su base.  
o Respuesta relevante: CRUD web conectado a la API y secciones faltantes 
(acceso web, arquitectura, persistencia/recuperación y autoría).  
o Aceptado / descartado: Se aceptó sumar index.html y los agregados al 
README.md para probar desde el navegador y documentar el entorno; se 
descartó reescribir el README.md o cambiar la estructura de carpetas 
original.  
• Decisión 2 – Docker Compose, separación de servicios y volumen mysql_data 
o Autoría: Ian Gonzalez.  
o Herramienta y consulta: IA; despliegue multi-contenedor con Docker 
Compose, salud de MySQL y persistencia.  
o Respuesta relevante: Servicios evitest-app (:4455) y mysql-evitest (:3306, 
base EVITest) con healthcheck y volumen mysql_data.  
o Aceptado / descartado: Se aceptó separar API y BD con volumen 
persistente para aislar el entorno y conservar datos al recrear 
contenedores.  
Prueba propia 
• Resultado esperado: Tras crear un alumno (index.html o POST 
/api/v1/insertStudent12), hacer docker compose down (sin -v) y docker compose 
up -d, los datos de mysql_data deben persistir en GET /api/v1/getStudent12; al 
detener evitest-app (docker stop evitest-app), el servicio debe volver a quedar 
operativo.  
• Resultado observado: Con docker compose down y docker compose up -d, el 
alumno se mantuvo en EVITest (en web y GET /api/v1/getStudent12). Tras docker 
stop evitest-app, volvió a estar activo mediante docker compose up -d y verificado 
con docker compose ps (capturas previstas: docker compose ps, UI con alumno, 
GET /api/v1/getStudent12 y persistencia post-down/up).  
• Conclusión: Se verificó que mysql_data conserva los registros al recrear 
contenedores y que evitest-app recupera su funcionamiento tras detenerse, sin 
pérdida de datos en EVITest.
