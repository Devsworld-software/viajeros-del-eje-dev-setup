Proyecto Viajeros del Eje
=========================

Este proyecto consiste en un frontend en Next.js y un backend en Laravel, con un entorno de desarrollo local unificado usando Docker Compose.

Producción:
- Frontend → Desplegado en Vercel
- Backend → Desplegado en VPS o hosting propio

Desarrollo local:
- Docker Compose permite levantar todos los servicios de manera rápida y consistente en cualquier máquina.

------------------------------------------------------------------

1️⃣ Estructura del proyecto

proyecto-padre/
├── viajeros-del-eje-web/   # Repositorio frontend (Next.js)
├── viajeros-del-eje-api/   # Repositorio backend (Laravel)
└── docker-compose.dev.yml  # Entorno de desarrollo local

Nota: docker-compose.dev.yml solo se usa para desarrollo local. No se despliega en producción.

------------------------------------------------------------------

2️⃣ Repositorios

Repositorio: viajeros-del-eje-web
Tecnología: Next.js
Descripción: Frontend del proyecto
Enlace: https://github.com/tu-org/viajeros-del-eje-web

Repositorio: viajeros-del-eje-api
Tecnología: Laravel
Descripción: Backend del proyecto
Enlace: https://github.com/tu-org/viajeros-del-eje-api

Cada repositorio es independiente, con su propio flujo de commits y despliegues.
Los repositorios deben clonarse dentro de la carpeta padre donde también se colocará docker-compose.dev.yml.

------------------------------------------------------------------

3️⃣ Requisitos para desarrollo

- Docker y Docker Compose
- Git
- Opcional (si no se usa Docker): Node.js y Composer

------------------------------------------------------------------

4️⃣ Configuración inicial para un nuevo desarrollador

4.1 Clonar los repositorios dentro de la carpeta padre

cd proyecto-padre
git clone git@github.com:tu-org/viajeros-del-eje-web.git viajeros-del-eje-web
git clone git@github.com:tu-org/viajeros-del-eje-api.git viajeros-del-eje-api

4.2 Colocar Docker Compose

proyecto-padre/
├── viajeros-del-eje-web/
├── viajeros-del-eje-api/
└── docker-compose.dev.yml

4.3 Configurar variables de entorno

Frontend (viajeros-del-eje-web/.env)

NEXT_PUBLIC_API_URL=http://backend:8000/api
NEXTAUTH_URL=http://backend:8000
NEXTAUTH_SECRET=XXXXXXXXXXXXX

Backend (viajeros-del-eje-api/.env)

APP_URL=http://backend:8000
DB_CONNECTION=pgsql
DB_HOST=postgres
DB_PORT=5432
DB_DATABASE=viajeros_del_eje_api
DB_USERNAME=devsworld
DB_PASSWORD=root

Puedes copiar .env.example y completarlo según tu entorno local.
Nunca subir .env a Git.

------------------------------------------------------------------

5️⃣ Levantar el entorno de desarrollo

Desde la carpeta padre:

docker compose -f docker-compose.dev.yml up --build

Contenedores disponibles:

Servicio      URL / Puerto
---------    ----------------------
Frontend     http://localhost:3000
Backend      http://localhost:8000/api
PostgreSQL   Puerto 5435

Docker monta las carpetas locales, por lo que los cambios se reflejan automáticamente (hot reload).

------------------------------------------------------------------

6️⃣ Flujo de trabajo para desarrollo

1. Editar código en viajeros-del-eje-web/ o viajeros-del-eje-api/
2. Probar cambios en localhost
3. Realizar commit y push en el repositorio correspondiente:

git add .
git commit -m "Descripción del cambio"
git push origin main

- Frontend → Vercel detecta el commit y realiza deploy automático
- Backend → Deploy según configuración del VPS / hosting

Docker solo se usa para desarrollo local y no afecta producción.

------------------------------------------------------------------

7️⃣ Producción

- Frontend: Deploy en Vercel desde el repositorio viajeros-del-eje-web
- Backend: Deploy en VPS / hosting desde el repositorio viajeros-del-eje-api

Variables de entorno en producción:

Frontend:
NEXT_PUBLIC_API_URL=https://api.viajerosdeleje.com/api

Backend: Configurar en servidor (DB real, API keys, etc.)

Nunca usar .env local en producción.

------------------------------------------------------------------

8️⃣ Buenas prácticas

- Docker Compose → solo para desarrollo local
- Repositorios separados → commits y deploys independientes
- Git → fuente de verdad
- Cambios en la API → mantener compatibilidad hacia atrás (/api/v1) hasta que frontend se actualice
- Variables de entorno → nunca subir a Git

------------------------------------------------------------------

9️⃣ Flujo visual de desarrollo y producción

Desarrollo local:
viajeros-del-eje-web/ + viajeros-del-eje-api/ + postgres (Docker)
        ↓
localhost:3000 (frontend)
localhost:8000 (backend)

Producción:
viajeros-del-eje-web/ repo → Vercel
viajeros-del-eje-api/ repo → VPS / hosting
        ↓
Comunicación vía API pública: https://api.viajerosdeleje.com

------------------------------------------------------------------

🔟 Soporte

Contacto: devsworldsoftware@gmail.com
Documentación de API interna: Revisar endpoints en Laravel y Swagger (si aplica)

Este README asegura que cualquier nuevo desarrollador pueda levantar todo el proyecto localmente, entender la separación de repositorios y manejar correctamente los commits y despliegues.
