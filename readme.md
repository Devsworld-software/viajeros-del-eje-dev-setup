# 🌍 Proyecto Viajeros del Eje

Este proyecto consiste en un ecosistema integral con un **frontend** desarrollado en **Next.js** y un **backend** en **Laravel**, utilizando un entorno de desarrollo unificado mediante **Docker Compose**.

---

## 1️⃣ Estructura del Proyecto

El repositorio principal organiza los componentes mediante submódulos de Git:

```text
proyecto-padre/
├── viajeros-del-eje-web/        # Submódulo frontend (Next.js)
├── viajeros-del-eje-api/        # Submódulo backend (Laravel)
└── docker-compose.dev.yml       # Orquestador de desarrollo local
[!WARNING]El archivo docker-compose.dev.yml es de uso exclusivo para desarrollo local. No debe utilizarse en entornos de producción.2️⃣ RepositoriosRepositorioTecnologíaDescripciónviajeros-del-eje-webNext.jsInterfaz de usuario y lógica de cliente.viajeros-del-eje-apiLaravelAPI REST y gestión de base de datos.Nota: Cada repositorio es independiente, con su propio historial de commits y flujo de despliegue.3️⃣ Requisitos PreviosPara ejecutar este proyecto localmente, asegúrate de tener instalado:Docker y Docker ComposeGitOpcional: Node.js y Composer (si prefieres ejecutar servicios fuera de Docker).4️⃣ Configuración Inicial4.1 Clonar el repositorio con submódulosPara descargar el proyecto padre junto con todo el código de los submódulos, ejecuta:Bash# Clonar con todos los submódulos incluidos
git clone --recurse-submodules <URL_REPO_PADRE> proyecto-padre
cd proyecto-padre

# Si ya habías clonado el repo sin los submódulos:
git submodule update --init --recursive
4.2 Variables de Entorno (.env)Es necesario configurar los archivos de entorno en cada subdirectorio. Puedes basarte en los archivos .env.example existentes.Frontend (viajeros-del-eje-web/.env)Fragmento de códigoNEXT_PUBLIC_API_URL=http://backend:8000/api
NEXTAUTH_URL=http://backend:8000
NEXTAUTH_SECRET=XXXXXXXXXXXXX
Backend (viajeros-del-eje-api/.env)Fragmento de códigoAPP_URL=http://backend:8000
DB_CONNECTION=pgsql
DB_HOST=postgres
DB_PORT=5432
DB_DATABASE=viajeros_del_eje_api
DB_USERNAME=devsworld
DB_PASSWORD=root
[!IMPORTANT]Nunca subas los archivos .env al repositorio de Git.5️⃣ Levantar el Entorno de DesarrolloPara iniciar todos los servicios (Frontend, API y Base de Datos), ejecuta:Bashdocker compose -f docker-compose.dev.yml up --build
Accesos Locales:Frontend: http://localhost:3000Backend (API): http://localhost:8000/apiPostgreSQL: Puerto 5435El entorno soporta Hot Reload, por lo que los cambios realizados en el código se verán reflejados al instante.6️⃣ Flujo de TrabajoRealizar modificaciones en las carpetas viajeros-del-eje-web/ o viajeros-del-eje-api/.Probar los cambios en el entorno local de Docker.Hacer commit y push en el repositorio hijo correspondiente:Bashgit add .
git commit -m "Descripción clara del cambio"
git push origin main
7️⃣ Despliegue (Producción)Frontend: Despliegue automático en Vercel conectado al repositorio del frontend.Backend: Despliegue en VPS / Hosting configurado para Laravel.Variables de Producción: Asegúrate de cambiar la NEXT_PUBLIC_API_URL a la URL real de la API (ej: https://api.viajerosdeleje.com/api).8️⃣ Buenas PrácticasSincronización: Si el repositorio padre se actualiza, recuerda ejecutar:git pull origin main && git submodule update --init --recursiveVersionamiento: Mantén la compatibilidad de la API para no afectar al frontend durante los despliegues.Seguridad: Valida siempre que las credenciales de base de datos sean distintas en producción.9️⃣ Soporte y ContactoDesarrollador: devsworldsoftware@gmail.comDocumentación adicional: Revisar la carpeta de documentación dentro del repositorio de la API.Proyecto desarrollado por DevsWorld.