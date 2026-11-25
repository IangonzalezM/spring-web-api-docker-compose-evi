# Autoevaluación – TP Integrador Entornos Virtualizados (EVI 2026)

**Integrantes:** Damian Sponza · Ian Gonzalez  
**Repositorio:** `spring-web-api-docker-compose-evi` (`sbapp11`)  
**Instancia:** V1

| Criterio | Nivel marcado (V1) | Evidencia concreta |
| :--- | :--- | :--- |
| Despliegue reproducible | Logrado | Pasos en `README.md`, `Dockerfile`, archivo Compose y `.env.example`, junto con ejecución de `docker compose up -d` y captura `01-compose-ps.png` (`docker compose ps` con `evitest-app` y `mysql-evitest` activos). |
| Persistencia y recuperación | Logrado | Alta de alumno + `docker compose down` (sin `-v`) + `docker compose up -d` en consola, y captura `03-persistencia-api-ok.png` (`GET /api/v1/getStudent12 -> 200` y vista web) verificando persistencia en `mysql_data`, más recuperación de `evitest-app`. |
| Red y exposición | Logrado | Diagrama de arquitectura en `README.md` y configuración de puertos `4455` (API/UI) y `3306` (MySQL) coincidente con la implementación y `docker compose ps`. |
| Seguridad básica | Logrado | Captura `04-seguridad-env-gitignore.png` (`type .gitignore` y `type .env.example`) con valores ficticios, exclusión de `.env` y credenciales reales del repositorio y configuración por variables de entorno. |
| Evidencias y bitácora | Logrado | Bitácora de una carilla con las dos decisiones (autoría, IA y aceptación/descarte), prueba con esperado/observado/conclusión y capturas de funcionamiento (`01-compose-ps.png`, `03-persistencia-api-ok.png`, `04-seguridad-env-gitignore.png`). |
| Uso documentado de la IA | Logrado | Registro en la bitácora de herramienta/consulta, respuesta relevante, razones de aceptación o descarte y prueba propia. |
| Transferencia y defensa | En proceso | Despliegue y pruebas realizadas en pareja con evidencia compartida; cada integrante sostendrá su decisión y comprobación propia en la revisión/defensa. |

