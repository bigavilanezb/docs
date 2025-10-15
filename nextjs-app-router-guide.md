# 🗂️ Guía Completa del App Router de Next.js

## 📁 Estructura Básica

El App Router usa la carpeta `app/` donde **cada carpeta = una ruta** y los archivos especiales definen el comportamiento:

```
src/app/
├── layout.tsx          # Layout global (obligatorio)
├── page.tsx            # Ruta: "/" (Home)
├── loading.tsx         # Loading UI para esta ruta
├── error.tsx           # Error handling
│
├── about/
│   └── page.tsx        # Ruta: "/about"
│
├── blog/
│   ├── page.tsx        # Ruta: "/blog"
│   └── [slug]/
│       └── page.tsx    # Ruta dinámica: "/blog/mi-post"
│
└── dashboard/
    ├── layout.tsx      # Layout específico del dashboard
    ├── page.tsx        # Ruta: "/dashboard"
    └── settings/
        └── page.tsx    # Ruta: "/dashboard/settings"
```

---

## 🎯 Archivos Especiales

| Archivo         | Propósito                                  |
| --------------- | ------------------------------------------ |
| `layout.tsx`    | UI compartida entre rutas (navbar, footer) |
| `page.tsx`      | Contenido único de cada ruta               |
| `loading.tsx`   | UI de carga mientras se obtienen datos     |
| `error.tsx`     | Manejo de errores                          |
| `not-found.tsx` | Página 404 personalizada                   |
| `route.ts`      | API Route (endpoints)                      |

---

## 🚀 Ejemplo: Proyecto con 3 Páginas

### **Estructura del proyecto:**

```
src/app/
├── layout.tsx           # Layout global
├── page.tsx             # Home "/"
├── about/
│   └── page.tsx         # About "/about"
└── contact/
    └── page.tsx         # Contact "/contact"
```

### **1. Layout Global** (`src/app/layout.tsx`)

```typescript
import "./globals.css";
import { Navbar } from "@/components/navbar";

export const metadata = {
  title: "Mi App",
  description: "Ejemplo de App Router",
};

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="es">
      <body>
        <Navbar />
        <main className="min-h-screen p-8">{children}</main>
        <footer className="bg-gray-800 text-white p-4 text-center">
          © 2025 Mi App
        </footer>
      </body>
    </html>
  );
}
```

### **2. Home** (`src/app/page.tsx`)

```typescript
export default function Home() {
  return (
    <div>
      <h1 className="text-4xl font-bold mb-4">Bienvenido a Mi App</h1>
      <p className="text-lg">Esta es la página principal</p>
    </div>
  );
}
```

### **3. About** (`src/app/about/page.tsx`)

```typescript
export const metadata = {
  title: "Sobre Nosotros",
};

export default function About() {
  return (
    <div>
      <h1 className="text-4xl font-bold mb-4">Sobre Nosotros</h1>
      <p className="text-lg">
        Somos un equipo dedicado a crear experiencias web increíbles.
      </p>
    </div>
  );
}
```

### **4. Contact** (`src/app/contact/page.tsx`)

```typescript
"use client"; // Necesario si usas hooks o interactividad

import { useState } from "react";

export default function Contact() {
  const [email, setEmail] = useState("");

  const handleSubmit = (e: React.FormEvent) => {
    e.preventDefault();
    console.log("Email enviado:", email);
  };

  return (
    <div>
      <h1 className="text-4xl font-bold mb-4">Contacto</h1>
      <form onSubmit={handleSubmit} className="max-w-md">
        <input
          type="email"
          value={email}
          onChange={(e) => setEmail(e.target.value)}
          placeholder="tu@email.com"
          className="w-full p-2 border rounded mb-4"
        />
        <button
          type="submit"
          className="bg-blue-500 text-white px-4 py-2 rounded"
        >
          Enviar
        </button>
      </form>
    </div>
  );
}
```

### **5. Navbar Component** (`src/components/navbar.tsx`)

```typescript
import Link from "next/link";

export function Navbar() {
  return (
    <nav className="bg-gray-900 text-white p-4">
      <div className="max-w-6xl mx-auto flex gap-6">
        <Link href="/" className="hover:text-blue-400">
          Home
        </Link>
        <Link href="/about" className="hover:text-blue-400">
          About
        </Link>
        <Link href="/contact" className="hover:text-blue-400">
          Contact
        </Link>
      </div>
    </nav>
  );
}
```

---

## 🔄 Server vs Client Components

### **Server Components (por defecto)**

- Se ejecutan en el servidor
- Pueden acceder a bases de datos directamente
- No pueden usar hooks (`useState`, `useEffect`)
- Mejor rendimiento y SEO

```typescript
// Server Component (por defecto)
async function fetchData() {
  const res = await fetch("https://api.example.com/data");
  return res.json();
}

export default async function ServerPage() {
  const data = await fetchData();
  return <div>{data.title}</div>;
}
```

### **Client Components**

- Se ejecutan en el navegador
- Pueden usar hooks e interactividad
- Necesitan la directiva `'use client'`

```typescript
"use client"; // 👈 Obligatorio

import { useState } from "react";

export default function ClientPage() {
  const [count, setCount] = useState(0);

  return <button onClick={() => setCount(count + 1)}>Clicks: {count}</button>;
}
```

---

## 🎨 Rutas Dinámicas

### **Blog con posts dinámicos:**

```
src/app/blog/
├── page.tsx            # "/blog" - Lista de posts
└── [slug]/
    └── page.tsx        # "/blog/mi-post" - Post individual
```

**Lista de posts** (`src/app/blog/page.tsx`):

```typescript
import Link from "next/link";

const posts = [
  { slug: "primer-post", title: "Mi primer post" },
  { slug: "segundo-post", title: "Segundo post" },
];

export default function Blog() {
  return (
    <div>
      <h1>Blog</h1>
      <ul>
        {posts.map((post) => (
          <li key={post.slug}>
            <Link href={`/blog/${post.slug}`}>{post.title}</Link>
          </li>
        ))}
      </ul>
    </div>
  );
}
```

**Post individual** (`src/app/blog/[slug]/page.tsx`):

```typescript
export default function Post({ params }: { params: { slug: string } }) {
  return (
    <div>
      <h1>Post: {params.slug}</h1>
      <p>Contenido del post...</p>
    </div>
  );
}

// Generar páginas estáticas en build time
export async function generateStaticParams() {
  return [{ slug: "primer-post" }, { slug: "segundo-post" }];
}
```

---

## 🚀 Desplegar en Vercel

### **Pasos:**

1. **Push a GitHub:**

```bash
git add .
git commit -m "App con 3 páginas"
git push
```

2. **En Vercel:**

- Importa tu repo de GitHub
- Vercel detecta automáticamente Next.js
- Configura variables de entorno si las necesitas
- Deploy automático

3. **Resultado:**

```
tuapp.vercel.app/         → Home
tuapp.vercel.app/about    → About
tuapp.vercel.app/contact  → Contact
```

### **Variables de entorno en Vercel:**

```
Settings → Environment Variables

NEXT_PUBLIC_API_URL=https://api.example.com
DATABASE_URL=postgres://...
```

---

## 💡 Tips Importantes

1. **`'use client'` solo cuando sea necesario** - Mantén componentes como Server Components por defecto

2. **Usa `export const dynamic = 'force-dynamic'`** cuando necesites datos en tiempo real (como con Supabase)

3. **Metadata para SEO:**

```typescript
export const metadata = {
  title: "Mi Página",
  description: "Descripción para SEO",
};
```

4. **Loading states:**

```typescript
// src/app/blog/loading.tsx
export default function Loading() {
  return <div>Cargando posts...</div>;
}
```

5. **Error handling:**

```typescript
// src/app/blog/error.tsx
"use client";

export default function Error({
  error,
  reset,
}: {
  error: Error;
  reset: () => void;
}) {
  return (
    <div>
      <h2>¡Algo salió mal!</h2>
      <button onClick={reset}>Intentar de nuevo</button>
    </div>
  );
}
```

---

## 📚 Recursos

- [Documentación oficial de Next.js](https://nextjs.org/docs)
- [App Router Guide](https://nextjs.org/docs/app)
- [Vercel Deployment Docs](https://vercel.com/docs)
