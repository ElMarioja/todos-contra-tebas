# 🚀 Cómo publicar "Todos Contra Tebas" en internet

Tu app necesita 2 cosas gratis: **Supabase** (la base de datos donde se guardan los participantes y videos) y **Vercel** (donde vive la página). Sigue los pasos en orden. Toma unos 15 minutos.

---

## PARTE 1 — Crear la base de datos (Supabase)

### 1. Crea tu cuenta
- Entra a **https://supabase.com** y haz clic en **Start your project**.
- Regístrate (puedes usar tu cuenta de GitHub o tu correo). Es gratis.

### 2. Crea un proyecto nuevo
- Clic en **New project**.
- Ponle un nombre, por ejemplo `todos-contra-tebas`.
- Inventa una contraseña para la base de datos (guárdala por si acaso, aunque no la necesitarás para esto).
- Elige la región más cercana (ej. *East US* o *South America*).
- Clic en **Create new project** y espera 1-2 minutos a que se cree.

### 3. Crea la tabla donde se guardan los datos
- En el menú de la izquierda, busca el ícono **SQL Editor** (parece `</>`).
- Clic en **New query**.
- Copia y pega EXACTAMENTE esto y dale a **Run** (botón verde abajo a la derecha):

```sql
create table tct (
  id integer primary key,
  data jsonb
);

alter table tct enable row level security;

create policy "acceso publico" on tct
  for all using (true) with check (true);

insert into tct (id, data) values (1, '{}');
```

- Si dice "Success" abajo, ¡listo! Ya tienes la base de datos.

### 4. Copia tus 2 datos de conexión
- En el menú de la izquierda ve a **Settings** (el engranaje) → **API**.
- Vas a ver dos cosas que necesitas:
  1. **Project URL** — algo como `https://abcdxyz.supabase.co`
  2. **Project API keys** → la que dice **anon public** — una cadena larga de letras.
- Cópialas, las usarás en la Parte 2.

---

## PARTE 2 — Poner tus datos en el archivo

1. Abre el archivo **todos-contra-tebas.html** con cualquier editor de texto (el Bloc de notas sirve).
2. Casi al inicio vas a encontrar este bloque:

```js
const SUPABASE_URL = 'PEGA_AQUI_TU_PROJECT_URL';
const SUPABASE_ANON_KEY = 'PEGA_AQUI_TU_ANON_PUBLIC_KEY';
```

3. Reemplaza el texto entre comillas por tus datos de Supabase. Te debe quedar algo así:

```js
const SUPABASE_URL = 'https://abcdxyz.supabase.co';
const SUPABASE_ANON_KEY = 'eyJhbGciOiJIUzI1NiIs...(la cadena larga)...';
```

4. Guarda el archivo. **No le cambies el nombre todavía** (déjalo como `.html`).

> 💡 Estas dos claves son públicas y seguras de poner en el código (Supabase está diseñado así). La seguridad real para borrar la sigue dando tu PIN de admin dentro de la app.

---

## PARTE 3 — Subir a Vercel

### Opción FÁCIL (arrastrar y soltar, sin instalar nada)

1. Crea una carpeta nueva en tu compu, por ejemplo `tebas-web`.
2. Mete dentro tu archivo y **renómbralo a `index.html`** (importante: Vercel busca ese nombre).
3. Entra a **https://vercel.com** y crea cuenta gratis (puedes usar GitHub).
4. En el panel, busca la opción de desplegar. La forma más simple:
   - Instala la herramienta de Vercel abriendo una terminal y escribiendo: `npm i -g vercel`
   - Luego, dentro de tu carpeta `tebas-web`, escribe: `vercel`
   - Sigue las preguntas (acepta los valores por defecto dándole Enter).
5. Al terminar te dará un link público tipo `https://tebas-web.vercel.app`. ¡Ese es tu sitio!

### Opción SIN terminal (usando GitHub)

1. Crea una cuenta en **https://github.com** si no tienes.
2. Crea un repositorio nuevo y sube tu archivo `index.html`.
3. En Vercel, clic en **Add New → Project**, conecta tu GitHub y elige ese repositorio.
4. Clic en **Deploy**. En segundos te da el link público.

---

## ✅ Listo

Comparte el link de Vercel con tus 20 miembros. Todos verán y editarán lo mismo en tiempo real (la app se refresca sola cada pocos segundos).

Recuerda: solo tú sabes el **PIN de admin**, así que solo tú podrás borrar o expulsar.

### Si algo no funciona
- La página carga pero sale vacía y dice "No se pudo conectar": revisa que pegaste bien las 2 claves de Supabase (Parte 2).
- Sale "Falta configurar Supabase": no reemplazaste los datos, siguen los textos `PEGA_AQUI...`.
- No guarda: confirma que corriste el comando SQL de la Parte 1 (paso 3) completo.
