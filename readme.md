Proyecto Viajeros del Eje

Este proyecto contiene un frontend en Next.js y un backend en Laravel, con un entorno de desarrollo local unificado usando Docker Compose.  

En producción:
- Frontend → desplegado en Vercel
- Backend → desplegado en un VPS o hosting propio

Docker Compose se utiliza solo para desarrollo local, permitiendo levantar todos los servicios de manera rápida y consistente en cualquier máquina.

---

1️⃣ Estructura del proyecto

proyecto-padre/
├── front/       ← Repositorio frontend (Next.js)
├── back/        ← Repositorio backend (Laravel)
└── docker-compose.dev.yml  ← Entorno de desarrollo local

Nota: docker-compose.dev.yml solo se usa para desarrollo. No se despliega en producción.

---

2️⃣ Repositorios

- Frontend (Next.js): [viajeros-del-eje-web](#)
- Backend (Laravel): [viajeros-del-eje-api](#)

Cada repositorio es independiente, con su propio flujo de commits y despliegue.

---

3️⃣ Requisitos para desarrollo

- Docker y Docker Compose
- Git
- Opcional para desarrollo local sin Docker: Node.js y Composer

---

4️⃣ Configuración inicial para un nuevo desarrollador

4.1 Clonar los repositorios

git clone git@github.com:tu-org/viajeros-del-eje-web.git front
git clone git@github.com:tu-org/viajeros-del-eje-api.git back

4.2 Copiar el Docker Compose de desarrollo

Colocar docker-compose.dev.yml en la carpeta padre, junto a front/ y back/:

proyecto-padre/
├── front/
├── back/
└── docker-compose.dev.yml

4.3 Configurar variables de entorno

Frontend (front/.env)
NEXT_PUBLIC_API_URL=http://backend:8000/api
NEXTAUTH_URL=http://backend:8000
NEXTAUTH_SECRET=XXXXXXXXXXXXX

Backend (back/.env)
APP_URL=http://backend:8000
DB_CONNECTION=pgsql
DB_HOST=postgres
DB_PORT=5432
DB_DATABASE=viajeros_del_eje_api
DB_USERNAME=devsworld
DB_PASSWORD=root

Puedes copiar .env.example y completarlo según las variables locales. Nunca subir .env a Git.

---

5️⃣ Levantar el entorno de desarrollo

Desde la carpeta padre (proyecto-padre/):

docker compose -f docker-compose.dev.yml up --build

Esto levantará los contenedores:
- Frontend: http://localhost:3000
- Backend: http://localhost:8000/api
- PostgreSQL: puerto 5435

Docker monta las carpetas locales, por lo que los cambios en el código se reflejan automáticamente (hot reload).

---

6️⃣ Flujo de trabajo para desarrollo

1. Edita código en front/ o back/
2. Prueba los cambios en localhost
3. Realiza commit y push en el repositorio correspondiente:

git add .
git commit -m "Descripción del cambio"
git push origin main

4. Frontend → Vercel detecta el commit y realiza deploy automático
5. Backend → Deploy según configuración del VPS / hosting

Docker es solo para desarrollo local, no afecta producción.

---

7️⃣ Producción

- Frontend: Deploy en Vercel desde el repositorio front/
- Backend: Deploy en VPS / hosting desde el repositorio back/

Variables de entorno en producción:
- Frontend: NEXT_PUBLIC_API_URL=https://api.viajerosdeleje.com/api
- Backend: configurar en servidor (DB real, API keys, etc.)

Nunca usar .env local en producción.

---

8️⃣ Buenas prácticas

- Docker Compose solo para desarrollo
- Repos separados → commits y deploys independientes
- Git → fuente de verdad
- Cambios en la API → mantener compatibilidad hacia atrás (/api/v1) hasta que frontend se actualice
- Variables de entorno → no subir a Git

---

9️⃣ Flujo visual de desarrollo y producción

Desarrollo local:
front/ + back/ + postgres (Docker)
       ↓
     localhost:3000 (frontend)
     localhost:8000 (backend)

Producción:
front/ repo → Vercel
back/ repo  → VPS / hosting
       ↓
    Comunicación via API pública (https://api.viajerosdeleje.com)

---

🔟 Soporte

- Contacto: devsworldsoftware@gmail.com
- Documentación de API interna: revisar endpoints en Laravel y Swagger (si aplica)

Este README asegura que cualquier nuevo desarrollador pueda levantar todo el proyecto localmente, entender la separación de repositorios y manejar correctamente los commits y despliegues.
