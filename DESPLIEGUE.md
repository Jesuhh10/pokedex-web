# Guía de Despliegue Técnico - PokeDex

Este documento detalla los comandos, retos técnicos y configuraciones específicas implementadas para el despliegue exitoso de la aplicación en Azure.

## 1. Gestión de Versiones y Trazabilidad (Git)

El historial de versiones refleja un progreso lógico de 11 ejecuciones de flujo de trabajo (Workflow Runs), donde se gestionaron los siguientes hitos técnicos:

* **Estandarización de Ramas:** Se utilizó `git branch -M main` para alinear el repositorio local con el estándar de producción de GitHub y Azure.
* **Sincronización mediante Rebase:** Para integrar los archivos de configuración generados automáticamente por Azure sin generar commits de unión innecesarios, se aplicó `git pull origin main --rebase`.
* **Resolución de Conflictos:** Se presentó un "Merge Conflict" en el archivo `README.md` debido a cambios simultáneos en la nube y el entorno local. Se resolvió manualmente integrando ambas fuentes de información.
* **Control de Errores:** Se gestionaron errores de tipo `rejected (fetch first)` asegurando que la historia del repositorio estuviera siempre sincronizada antes de cada push.

## 2. Implementación de Seguridad (Security Headers)

Para obtener la calificación **A** en el escaneo de seguridad, se configuró el archivo `staticwebapp.config.json` con los siguientes encabezados:

* **Strict-Transport-Security (HSTS):** Configurado con un `max-age` de un año para forzar conexiones seguras.
* **Content-Security-Policy (CSP):** Implementado para prevenir ataques de inyección de scripts (XSS).
* **X-Frame-Options (DENY):** Configurado para mitigar ataques de Clickjacking.
* **Permissions-Policy:** Se deshabilitaron sensores del dispositivo (cámara, micrófono) para reducir la superficie de ataque.

## 3. Infraestructura y CI/CD (Azure)

La aplicación utiliza el modelo de **Azure Static Web Apps**. La automatización se gestiona mediante **GitHub Actions**, donde cada commit dispara una compilación automática de Angular y el despliegue inmediato al entorno de producción global.

link pokedex publica: https://lively-island-09b4f7010.7.azurestaticapps.net

