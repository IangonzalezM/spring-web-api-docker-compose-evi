# Autoevaluación – TP Integrador Entornos Virtualizados (EVI 2026)

**Integrantes:** Damian Sponza · Ian Gonzalez  
**Repositorio:** `spring-web-api-docker-compose-evi` (`sbapp11`)  
**Instancia:** V1

| Criterio | Nivel marcado (V1) | Evidencia concreta |
| :--- | :--- | :--- |
| Despliegue reproducible | Logrado | Pasos en `README.md`, `Dockerfile`, archivo Compose y `.env.example`, junto con ejecución de `docker compose up -d` y `docker compose ps`. |
| Persistencia y recuperación | Logrado | Alta de registro + `docker compose down` (sin `-v`) + `docker compose up -d` + consulta a `GET /api/v1/getStudent12` / vista web verificando persistencia en `mysql_data`, más recuperación de `evitest-app`. |
| Red y exposición | Logrado | Diagrama de arquitectura en `README.md` y configuración de puertos `4455` (API/UI) y `3306` (MySQL) coincidente con la implementación. |
| Seguridad básica | Logrado | Archivo `.env.example` con valores ficticios, exclusión de credenciales reales del repositorio y configuración por variables de entorno. |
| Evidencias y bitácora | Logrado | Bitácora de una carilla con las dos decisiones (autoría, IA y aceptación/descarte), prueba con esperado/observado/conclusión y capturas de funcionamiento. |
| Uso documentado de la IA | Logrado | Registro en la bitácora de herramienta/consulta, respuesta relevante, razones de aceptación o descarte y prueba propia. |
| Transferencia y defensa | A verificar en defensa | Despliegue y pruebas en equipo donde cada integrante sostiene su decisión y comprobación propia en la revisión/defensa. |
