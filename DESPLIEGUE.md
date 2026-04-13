## bitácora de Despliegue - Pueblo Paleta Inc.##

Este documento detalla el proceso técnico, los comandos ejecutados y la resolución de conflictos para el despliegue de la aplicación PokeDex en Azure Static Web Apps.

1. Preparación del Entorno Local
Para garantizar un despliegue limpio, se realizó una migración de los archivos fuente desde el repositorio base a un nuevo repositorio local optimizado.

Inicialización del repositorio:
    en bash:     git init
    git branch -M main
Limpieza de estructura: Se movieron los archivos desde la subcarpeta técnica source/pokedex-angular directamente a la raíz del proyecto para facilitar la detección de Azure.

2. Configuración de CI/CD (GitHub a Azure)
El despliegue se automatizó mediante GitHub Actions. La configuración en el portal de Azure se definió de la siguiente manera:

App Location: / (Raíz del proyecto).

Output Location: / (Archivos estáticos procesados).

Workflow: Se generó un archivo .yml en la carpeta .github/workflows que se dispara automáticamente con cada push a la rama main.

3. Comandos de Gestión de Cambios
Durante el desarrollo y documentación, se utilizaron los siguientes comandos de Git:

    en bash:
    Bash
    git add .
    git commit -m "Mensaje descriptivo del cambio"
    git push origin main

4. Errores Encontrados y Soluciones


1 error: Permission denied (publickey) 
    causa: Intento de conexión vía SSH sin llaves configuradas. 
    solucion: Se cambió el origen del remoto a HTTPS con git remote set-url.

2 error: rejected - fetch first 
    causa: Desincronización entre el repositorio local y los archivos generados por Azure en la nube.
    solucion: Se ejecutó un git pull origin main --rebase para unificar las versiones.

3 error: No such file or directory
    causa: Error en la referencia de rutas relativas debido a la profundidad de carpetas.
    swolucion:Uso de rutas absolutas y comandos de navegación cd paso a paso.

5. Verificación Final
El proyecto se encuentra operativo en la siguiente URL de producción:
[https://lively-island-09b4f7010.7.azurestaticapps.net/]
