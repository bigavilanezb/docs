# 🔄 App Router vs Pages Router

## 📊 Comparación Rápida

| Característica          | **Pages Router** (Antiguo)             | **App Router** (Nuevo)     |
| ----------------------- | -------------------------------------- | -------------------------- |
| **Lanzamiento**         | Next.js 9 (2019)                       | Next.js 13 (2022)          |
| **Carpeta**             | `pages/`                               | `app/`                     |
| **Estado**              | Estable, legacy                        | Recomendado, futuro        |
| **Server Components**   | ❌ No                                  | ✅ Sí (por defecto)        |
| **Layouts compartidos** | Manual con `_app.tsx`                  | ✅ Nativo con `layout.tsx` |
| **Loading states**      | Manual                                 | ✅ `loading.tsx`           |
| **Error handling**      | Manual                                 | ✅ `error.tsx`             |
| **Streaming**           | ❌ No                                  | ✅ Sí                      |
| **Data fetching**       | `getServerSideProps`, `getStaticProps` | `async/await` directo      |

---

## 📁 Estructura de Archivos

### **Pages Router** (Antiguo)

```
pages/
├── _app.tsx           # Layout global
├── _document.tsx      # HTML base
├── index.tsx          # "/" ruta
├── about.tsx          # "/about"
├── blog/
│   ├── index.tsx      # "/blog"
│   └── [slug].tsx     # "/blog/post-1"
└── api/
    └── hello.ts       # "/api/hello"
```

### **App Router** (Nuevo)

```
app/
├── layout.tsx         # Layout global
├── page.tsx           # "/" ruta
├── loading.tsx        # Loading UI
├── error.tsx          # Error handling
├── about/
│   └── page.tsx       # "/about"
├── blog/
│   ├── page.tsx       # "/blog"
│   └── [slug]/
│       └── page.tsx   # "/blog/post-1"
└── api/
    └── hello/
        └── route.ts   # "/api/hello"
```

---

## 🔍 Diferencias Clave

### **1. Data Fetching**

#### **Pages Router:**

```typescript
// pages/blog.tsx
export default function Blog({ posts }) {
  return <div>{posts.map(post => ...)}</div>
}

// Obligatorio usar estas funciones especiales
export async function getServerSideProps() {
  const res = await fetch('https://api.example.com/posts')
  const posts = await res.json()

  return {
    props: { posts }
  }
}
```

#### **App Router:**

```typescript
// app/blog/page.tsx
async function getPosts() {
  const res = await fetch('https://api.example.com/posts')
  return res.json()
}

export default async function Blog() {
  const posts = await getPosts() // ✨ Más simple y directo

  return <div>{posts.map(post => ...)}</div>
}
```

---

### **2. Layouts Compartidos**

#### **Pages Router:**

```typescript
// pages/_app.tsx
import { Navbar } from "@/components/navbar";

export default function App({ Component, pageProps }) {
  return (
    <>
      <Navbar /> {/* Se repite en TODAS las páginas */}
      <Component {...pageProps} />
    </>
  );
}
```

**Problema:** El navbar se remonta en cada navegación ❌

#### **App Router:**

```typescript
// app/layout.tsx
import { Navbar } from "@/components/navbar";

export default function RootLayout({ children }) {
  return (
    <html>
      <body>
        <Navbar /> {/* ✅ Persiste, no se remonta */}
        {children}
      </body>
    </html>
  );
}
```

**Ventaja:** Layouts anidados y persistentes ✅

---

### **3. Loading States**

#### **Pages Router:**

```typescript
// pages/blog.tsx
import { useState, useEffect } from 'react'

export default function Blog() {
  const [posts, setPosts] = useState([])
  const [loading, setLoading] = useState(true)

  useEffect(() => {
    fetch('/api/posts')
      .then(res => res.json())
      .then(data => {
        setPosts(data)
        setLoading(false)
      })
  }, [])

  if (loading) return <div>Cargando...</div>

  return <div>{posts.map(...)}</div>
}
```

**Problema:** Tienes que manejar el loading manualmente ❌

#### **App Router:**

```typescript
// app/blog/loading.tsx
export default function Loading() {
  return <div>Cargando posts...</div>
}

// app/blog/page.tsx
export default async function Blog() {
  const posts = await fetch('/api/posts').then(r => r.json())
  return <div>{posts.map(...)}</div>
}
```

**Ventaja:** Loading automático con Suspense ✅

---

### **4. Error Handling**

#### **Pages Router:**

```typescript
// pages/blog.tsx
export default function Blog({ posts, error }) {
  if (error) {
    return <div>Error: {error.message}</div>
  }

  return <div>{posts.map(...)}</div>
}

export async function getServerSideProps() {
  try {
    const posts = await fetchPosts()
    return { props: { posts } }
  } catch (error) {
    return { props: { error: error.message } }
  }
}
```

#### **App Router:**

```typescript
// app/blog/error.tsx
'use client'

export default function Error({ error, reset }) {
  return (
    <div>
      <h2>Error: {error.message}</h2>
      <button onClick={reset}>Reintentar</button>
    </div>
  )
}

// app/blog/page.tsx
export default async function Blog() {
  const posts = await fetchPosts() // Si falla, error.tsx se muestra
  return <div>{posts.map(...)}</div>
}
```

**Ventaja:** Error boundaries automáticos ✅

---

### **5. Server vs Client Components**

#### **Pages Router:**

```typescript
// TODO es Client Component por defecto
// pages/counter.tsx
import { useState } from "react";

export default function Counter() {
  const [count, setCount] = useState(0);

  return <button onClick={() => setCount(count + 1)}>{count}</button>;
}
```

**Todo el JS se envía al cliente** 📦💨

#### **App Router:**

```typescript
// Server Component por defecto (sin JS al cliente)
// app/blog/page.tsx
async function getPosts() {
  const posts = await db.query("SELECT * FROM posts");
  return posts;
}

export default async function Blog() {
  const posts = await getPosts();
  return <PostList posts={posts} />; // Solo HTML al cliente
}

// Client Component solo cuando sea necesario
// app/components/counter.tsx
("use client"); // 👈 Explícito

import { useState } from "react";

export function Counter() {
  const [count, setCount] = useState(0);
  return <button onClick={() => setCount(count + 1)}>{count}</button>;
}
```

**Ventaja:** Menos JavaScript al cliente = más rápido ⚡

---

### **6. Rutas de API**

#### **Pages Router:**

```typescript
// pages/api/posts.ts
import type { NextApiRequest, NextApiResponse } from "next";

export default async function handler(
  req: NextApiRequest,
  res: NextApiResponse
) {
  if (req.method === "GET") {
    const posts = await getPosts();
    res.status(200).json(posts);
  }
}
```

#### **App Router:**

```typescript
// app/api/posts/route.ts
import { NextResponse } from "next/server";

export async function GET() {
  const posts = await getPosts();
  return NextResponse.json(posts);
}

export async function POST(request: Request) {
  const body = await request.json();
  // ...
  return NextResponse.json({ success: true });
}
```

**Ventaja:** Métodos HTTP más claros ✅

---

## 🎯 ¿Cuál usar?

### **Usa App Router si:**

- ✅ Empiezas un proyecto nuevo
- ✅ Quieres mejor rendimiento
- ✅ Necesitas streaming y Suspense
- ✅ Quieres layouts anidados
- ✅ Prefieres código más simple

### **Usa Pages Router si:**

- ⚠️ Mantienes un proyecto legacy
- ⚠️ Necesitas compatibilidad con librerías antiguas
- ⚠️ Tu equipo no está listo para migrar

---

## 🔄 Migración Gradual

**¡Puedes usar ambos al mismo tiempo!**

```
mi-app/
├── app/              # Nuevas rutas (App Router)
│   ├── dashboard/
│   └── profile/
└── pages/            # Rutas antiguas (Pages Router)
    ├── index.tsx
    └── about.tsx
```

Next.js prioriza `app/` sobre `pages/` para la misma ruta.

---

## 📈 Rendimiento Comparado

| Métrica          | Pages Router       | App Router           |
| ---------------- | ------------------ | -------------------- |
| **Bundle size**  | 📦 Más grande      | ✅ Más pequeño       |
| **Initial load** | 🐢 Más lento       | ⚡ Más rápido        |
| **Navegación**   | 🔄 Remonta layouts | ✅ Layouts persisten |
| **SEO**          | ✅ Bueno           | ✅ Excelente         |
| **Streaming**    | ❌ No              | ✅ Sí                |

---

## 💡 Ejemplo Lado a Lado

### **Blog Post - Pages Router**

```typescript
// pages/blog/[slug].tsx
export default function Post({ post, error }) {
  if (error) return <div>Error</div>;
  if (!post) return <div>Loading...</div>;

  return (
    <article>
      <h1>{post.title}</h1>
      <p>{post.content}</p>
    </article>
  );
}

export async function getStaticProps({ params }) {
  try {
    const post = await getPost(params.slug);
    return { props: { post } };
  } catch (error) {
    return { props: { error: true } };
  }
}

export async function getStaticPaths() {
  const posts = await getAllPosts();
  return {
    paths: posts.map((p) => ({ params: { slug: p.slug } })),
    fallback: true,
  };
}
```

### **Blog Post - App Router**

```typescript
// app/blog/[slug]/page.tsx
export default async function Post({ params }) {
  const post = await getPost(params.slug);

  return (
    <article>
      <h1>{post.title}</h1>
      <p>{post.content}</p>
    </article>
  );
}

// app/blog/[slug]/loading.tsx
export default function Loading() {
  return <div>Loading...</div>;
}

// app/blog/[slug]/error.tsx
("use client");
export default function Error() {
  return <div>Error</div>;
}

export async function generateStaticParams() {
  const posts = await getAllPosts();
  return posts.map((p) => ({ slug: p.slug }));
}
```

**¿Notas la diferencia?** App Router es más limpio y separado ✨

---

## 🚀 Conclusión

**App Router** es el futuro de Next.js:

- 🎯 Más simple y moderno
- ⚡ Mejor rendimiento
- 🧩 Componentes de servidor por defecto
- 📦 Menos JavaScript al cliente
- 🔄 Layouts que persisten

**Tu proyecto usa App Router**, ¡así que estás usando lo mejor! 🎉
