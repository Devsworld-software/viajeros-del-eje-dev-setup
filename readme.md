<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Proyecto Viajeros del Eje</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      line-height: 1.6;
      padding: 20px;
      background-color: #f9f9f9;
      color: #333;
    }
    h1, h2, h3 {
      color: #2c3e50;
    }
    pre {
      background: #eee;
      padding: 10px;
      border-radius: 5px;
      overflow-x: auto;
    }
    code {
      background: #eee;
      padding: 2px 5px;
      border-radius: 3px;
    }
    table {
      border-collapse: collapse;
      margin-bottom: 20px;
      width: 100%;
    }
    table, th, td {
      border: 1px solid #ccc;
    }
    th, td {
      padding: 8px;
      text-align: left;
    }
    blockquote {
      border-left: 4px solid #2c3e50;
      padding-left: 10px;
      color: #555;
      margin: 10px 0;
      background: #f0f0f0;
    }
    hr {
      border: 0;
      border-top: 1px solid #ccc;
      margin: 20px 0;
    }
  </style>
</head>
<body>

<h1>Proyecto <strong>Viajeros del Eje</strong></h1>

<p>Este proyecto consiste en un <strong>frontend</strong> en <strong>Next.js</strong> y un <strong>backend</strong> en <strong>Laravel</strong>, con un entorno de desarrollo local unificado usando <strong>Docker Compose</strong>.</p>

<ul>
  <li><strong>Producción</strong>
    <ul>
      <li>Frontend → Desplegado en Vercel</li>
      <li>Backend → Desplegado en VPS o hosting propio</li>
    </ul>
  </li>
  <li><strong>Desarrollo local</strong>
    <ul>
      <li>Docker Compose permite levantar todos los servicios de manera rápida y consistente en cualquier máquina.</li>
    </ul>
  </li>
</ul>

<hr>

<h2>1️⃣ Estructura del proyecto</h2>

<pre>
proyecto-padre/
├── viajeros-del-eje-web/                  # Repositorio frontend (Next.js)
├── viajeros-del-eje-api/                   # Repositorio backend (Laravel)
└── docker-compose.dev.yml  # Entorno de desarrollo local
</pre>

<blockquote>⚠️ Nota: <code>docker-compose.dev.yml</code> solo se usa para <strong>desarrollo local</strong>. No se despliega en producción.</blockquote>

<hr>

<h2>2️⃣ Repositorios</h2>

<table>
  <tr>
    <th>Repositorio</th>
    <th>Tecnología</th>
    <th>Descripción</th>
  </tr>
  <tr>
    <td>viajeros-del-eje-web</td>
    <td>Next.js</td>
    <td>Frontend del proyecto</td>
  </tr>
  <tr>
    <td>viajeros-del-eje-api</td>
    <td>Laravel</td>
    <td>Backend del proyecto</td>
  </tr>
</table>

<p>Cada repositorio es independiente, con su propio flujo de <strong>commits</strong> y <strong>despliegues</strong>.</p>

<hr>

<h2>3️⃣ Requisitos para desarrollo</h2>
<ul>
  <li>Docker y Docker Compose</li>
  <li>Git</li>
  <li>Opcional (si no se usa Docker): Node.js y Composer</li>
</ul>

<hr>

<h2>4️⃣ Configuración inicial para un nuevo desarrollador</h2>

<h3>4.1 Clonar los repositorios</h3>
<pre>
git clone git@github.com:tu-org/viajeros-del-eje-web.git front
git clone git@github.com:tu-org/viajeros-del-eje-api.git back
</pre>

<h3>4.2 Colocar Docker Compose</h3>
<pre>
proyecto-padre/
├── front/
├── back/
└── docker-compose.dev.yml
</pre>

<h3>4.3 Configurar variables de entorno</h3>

<p><strong>Frontend (<code>front/.env</code>)</strong></p>
<pre>
NEXT_PUBLIC_API_URL=http://backend:8000/api
NEXTAUTH_URL=http://backend:8000
NEXTAUTH_SECRET=XXXXXXXXXXXXX
</pre>

<p><strong>Backend (<code>back/.env</code>)</strong></p>
<pre>
APP_URL=http://backend:8000
DB_CONNECTION=pgsql
DB_HOST=postgres
DB_PORT=5432
DB_DATABASE=viajeros_del_eje_api
DB_USERNAME=devsworld
DB_PASSWORD=root
</pre>

<blockquote>Puedes copiar <code>.env.example</code> y completarlo según tu entorno local.<br>❌ Nunca subir <code>.env</code> a Git.</blockquote>

<hr>

<h2>5️⃣ Levantar el entorno de desarrollo</h2>

<p>Desde la carpeta padre:</p>
<pre>
docker compose -f docker-compose.dev.yml up --build
</pre>

<p><strong>Contenedores disponibles:</strong></p>
<table>
  <tr>
    <th>Servicio</th>
    <th>URL / Puerto</th>
  </tr>
  <tr>
    <td>Frontend</td>
    <td>http://localhost:3000</td>
  </tr>
  <tr>
    <td>Backend</td>
    <td>http://localhost:8000/api</td>
  </tr>
  <tr>
    <td>PostgreSQL</td>
    <td>Puerto 5435</td>
  </tr>
</table>

<blockquote>Docker monta las carpetas locales, por lo que los cambios se reflejan automáticamente (<strong>hot reload</strong>).</blockquote>

<hr>

<h2>6️⃣ Flujo de trabajo para desarrollo</h2>
<ol>
  <li>Editar código en <code>front/</code> o <code>back/</code></li>
  <li>Probar cambios en <code>localhost</code></li>
  <li>Realizar commit y push en el repositorio correspondiente:</li>
</ol>

<pre>
git add .
git commit -m "Descripción del cambio"
git push origin main
</pre>

<ul>
  <li><strong>Frontend</strong> → Vercel detecta el commit y realiza deploy automático</li>
  <li><strong>Backend</strong> → Deploy según configuración del VPS / hosting</li>
</ul>

<blockquote>Docker solo se usa para desarrollo local y <strong>no afecta producción</strong>.</blockquote>

<hr>

<h2>7️⃣ Producción</h2>
<ul>
  <li><strong>Frontend</strong>: Deploy en Vercel desde el repositorio <code>front/</code></li>
  <li><strong>Backend</strong>: Deploy en VPS / hosting desde el repositorio <code>back/</code></li>
</ul>

<p><strong>Variables de entorno en producción:</strong></p>

<p>Frontend:</p>
<pre>
NEXT_PUBLIC_API_URL=https://api.viajerosdeleje.com/api
</pre>

<p>Backend: Configurar en servidor (DB real, API keys, etc.)</p>

<blockquote>❌ Nunca usar <code>.env</code> local en producción.</blockquote>

<hr>

<h2>8️⃣ Buenas prácticas</h2>
<ul>
  <li>Docker Compose → solo para <strong>desarrollo local</strong></li>
  <li>Repositorios separados → commits y deploys independientes</li>
  <li>Git → fuente de verdad</li>
  <li>Cambios en la API → mantener compatibilidad hacia atrás (<code>/api/v1</code>) hasta que frontend se actualice</li>
  <li>Variables de entorno → nunca subir a Git</li>
</ul>

<hr>

<h2>9️⃣ Flujo visual de desarrollo y producción</h2>
<pre>
Desarrollo local:
front/ + back/ + postgres (Docker)
        ↓
localhost:3000 (frontend)
localhost:8000 (backend)

Producción:
front/ repo → Vercel
back/ repo → VPS / hosting
        ↓
Comunicación vía API pública: http://localhost:8000/api
</pre>

<hr>

<h2>🔟 Soporte</h2>
<ul>
  <li><strong>Contacto:</strong> devsworldsoftware@gmail.com</li>
  <li><strong>Documentación de API interna:</strong> Revisar endpoints en Laravel y Swagger (si aplica)</li>
</ul>

<blockquote>Este README asegura que cualquier nuevo desarrollador pueda levantar todo el proyecto localmente, entender la separación de repositorios y manejar correctamente los commits y despliegues.</blockquote>

</body>
</html>
