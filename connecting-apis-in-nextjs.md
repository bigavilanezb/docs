# 🌐 Guía Completa: Conectar APIs en Next.js

## 📚 Fuente Oficial
Basado en la documentación oficial de Next.js:
- [Fetching Data](https://nextjs.org/docs/app/getting-started/fetching-data)
- [fetch API Reference](https://nextjs.org/docs/app/api-reference/functions/fetch)

---

## 🎯 Tres formas de conectar APIs en Next.js

### 1️⃣ **Server Components** (Recomendado - Server-Side)
### 2️⃣ **Client Components** (Client-Side con hooks)
### 3️⃣ **Route Handlers** (API Routes internas)

---

## 1️⃣ Server Components - Fetching en el Servidor

### ✅ Ventajas:
- Mejor SEO
- Más rápido (no envía JavaScript al cliente)
- Acceso directo a bases de datos
- Datos frescos en cada request

### 📝 Ejemplo básico:

```typescript
// app/page.tsx
export default async function Page() {
  // Fetch directo en el componente
  const res = await fetch('https://api.example.com/data')
  const data = await res.json()
  
  return (
    <div>
      <h1>Datos de la API</h1>
      <pre>{JSON.stringify(data, null, 2)}</pre>
    </div>
  )
}
```

### 🎨 Ejemplo con tu proyecto Dragon Ball:

```typescript
// app/page.tsx
interface Character {
  id: number
  name: string
  ki: string
  race: string
  image: string
}

export default async function Home() {
  const res = await fetch('https://dragonball-api.com/api/characters')
  const data = await res.json()
  const characters: Character[] = data.items
  
  return (
    <main className="p-8">
      <h1 className="text-4xl font-bold mb-8">Personajes de Dragon Ball</h1>
      <div className="grid grid-cols-3 gap-4">
        {characters.map((character) => (
          <div key={character.id} className="border p-4 rounded">
            <img src={character.image} alt={character.name} />
            <h2 className="text-xl font-bold">{character.name}</h2>
            <p>Raza: {character.race}</p>
            <p>Ki: {character.ki}</p>
          </div>
        ))}
      </div>
    </main>
  )
}
```

---

## 🔄 Opciones de Caché con fetch()

Next.js extiende el `fetch()` nativo con opciones de caché:

### **1. Cache: 'force-cache' (Por defecto)**
Cachea la respuesta indefinidamente:

```typescript
const res = await fetch('https://api.example.com/data', {
  cache: 'force-cache' // Cachea para siempre
})
```

### **2. Cache: 'no-store'**
Sin caché, datos frescos siempre:

```typescript
const res = await fetch('https://api.example.com/data', {
  cache: 'no-store' // Sin caché, siempre fresco
})
```

### **3. Revalidate**
Cachea pero revalida cada X segundos:

```typescript
const res = await fetch('https://api.example.com/data', {
  next: { revalidate: 3600 } // Revalida cada hora (3600 segundos)
})
```

---

## 🎯 Ejemplo completo con manejo de errores:

```typescript
// app/characters/page.tsx
interface Character {
  id: number
  name: string
  image: string
}

async function getCharacters(): Promise<Character[]> {
  try {
    const res = await fetch('https://dragonball-api.com/api/characters', {
      next: { revalidate: 3600 }, // Cachea 1 hora
    })
    
    if (!res.ok) {
      throw new Error(`Error ${res.status}: ${res.statusText}`)
    }
    
    const data = await res.json()
    return data.items
  } catch (error) {
    console.error('Error fetching characters:', error)
    return [] // Retorna array vacío en caso de error
  }
}

export default async function CharactersPage() {
  const characters = await getCharacters()
  
  if (characters.length === 0) {
    return <div>No se pudieron cargar los personajes</div>
  }
  
  return (
    <div>
      <h1>Personajes</h1>
      <div className="grid">
        {characters.map((character) => (
          <div key={character.id}>
            <h2>{character.name}</h2>
          </div>
        ))}
      </div>
    </div>
  )
}
```

---

## 2️⃣ Client Components - Fetching en el Cliente

### ✅ Cuándo usar:
- Datos que cambian con interacción del usuario
- Componentes interactivos (botones, formularios)
- Datos específicos del usuario
- No necesitas SEO

### 📝 Ejemplo con useEffect:

```typescript
// app/components/characters-client.tsx
'use client' // 👈 Obligatorio para Client Components

import { useState, useEffect } from 'react'

interface Character {
  id: number
  name: string
  image: string
}

export default function CharactersClient() {
  const [characters, setCharacters] = useState<Character[]>([])
  const [loading, setLoading] = useState(true)
  const [error, setError] = useState<string | null>(null)
  
  useEffect(() => {
    async function fetchCharacters() {
      try {
        const res = await fetch('https://dragonball-api.com/api/characters')
        
        if (!res.ok) {
          throw new Error('Error al cargar datos')
        }
        
        const data = await res.json()
        setCharacters(data.items)
      } catch (err) {
        setError(err instanceof Error ? err.message : 'Error desconocido')
      } finally {
        setLoading(false)
      }
    }
    
    fetchCharacters()
  }, [])
  
  if (loading) return <div>Cargando...</div>
  if (error) return <div>Error: {error}</div>
  
  return (
    <div>
      {characters.map((character) => (
        <div key={character.id}>{character.name}</div>
      ))}
    </div>
  )
}
```

### 🎨 Ejemplo con búsqueda interactiva:

```typescript
'use client'

import { useState } from 'react'

export default function SearchCharacters() {
  const [query, setQuery] = useState('')
  const [results, setResults] = useState([])
  const [loading, setLoading] = useState(false)
  
  const handleSearch = async () => {
    if (!query) return
    
    setLoading(true)
    try {
      const res = await fetch(
        `https://dragonball-api.com/api/characters?name=${query}`
      )
      const data = await res.json()
      setResults(data.items)
    } catch (error) {
      console.error('Error:', error)
    } finally {
      setLoading(false)
    }
  }
  
  return (
    <div>
      <input
        type="text"
        value={query}
        onChange={(e) => setQuery(e.target.value)}
        placeholder="Buscar personaje..."
      />
      <button onClick={handleSearch}>Buscar</button>
      
      {loading && <p>Buscando...</p>}
      
      <div>
        {results.map((char: any) => (
          <div key={char.id}>{char.name}</div>
        ))}
      </div>
    </div>
  )
}
```

---

## 🔥 SWR - Librería recomendada para Client-Side

SWR (Stale-While-Revalidate) es una librería de Vercel para fetching de datos:

### **Instalación:**
```bash
pnpm add swr
```

### **Ejemplo con SWR:**

```typescript
'use client'

import useSWR from 'swr'

// Fetcher function
const fetcher = (url: string) => fetch(url).then((res) => res.json())

export default function CharactersWithSWR() {
  const { data, error, isLoading } = useSWR(
    'https://dragonball-api.com/api/characters',
    fetcher,
    {
      revalidateOnFocus: false, // No revalidar al volver a la pestaña
      revalidateOnReconnect: true, // Revalidar al reconectar
    }
  )
  
  if (isLoading) return <div>Cargando...</div>
  if (error) return <div>Error al cargar datos</div>
  
  return (
    <div>
      {data.items.map((character: any) => (
        <div key={character.id}>{character.name}</div>
      ))}
    </div>
  )
}
```

### ✅ Ventajas de SWR:
- Caché automático
- Revalidación automática
- Reintentos automáticos
- Polling (actualización periódica)
- Optimistic UI
- Paginación y scroll infinito

---

## 3️⃣ Route Handlers - API Routes Internas

Útil cuando necesitas:
- Ocultar API keys
- Procesar datos antes de enviarlos al cliente
- Conectar con bases de datos
- Autenticación

### 📝 Crear un Route Handler:

**Archivo: `app/api/characters/route.ts`**

```typescript
import { NextResponse } from 'next/server'

export async function GET() {
  try {
    const res = await fetch('https://dragonball-api.com/api/characters')
    const data = await res.json()
    
    return NextResponse.json(data)
  } catch (error) {
    return NextResponse.json(
      { error: 'Error al obtener datos' },
      { status: 500 }
    )
  }
}
```

### 🔒 Con API Key oculta:

```typescript
// app/api/characters/route.ts
import { NextResponse } from 'next/server'

export async function GET() {
  const apiKey = process.env.DRAGON_BALL_API_KEY // Variable de entorno
  
  try {
    const res = await fetch('https://dragonball-api.com/api/characters', {
      headers: {
        'Authorization': `Bearer ${apiKey}`,
      },
    })
    
    if (!res.ok) {
      throw new Error('API request failed')
    }
    
    const data = await res.json()
    return NextResponse.json(data)
  } catch (error) {
    return NextResponse.json(
      { error: 'Failed to fetch data' },
      { status: 500 }
    )
  }
}
```

### 📞 Consumir desde el cliente:

```typescript
'use client'

import { useEffect, useState } from 'react'

export default function Characters() {
  const [data, setData] = useState(null)
  
  useEffect(() => {
    fetch('/api/characters') // Tu API interna
      .then(res => res.json())
      .then(data => setData(data))
  }, [])
  
  if (!data) return <div>Loading...</div>
  
  return <div>{/* Renderiza data */}</div>
}
```

---

## 📦 Métodos HTTP en Route Handlers

```typescript
// app/api/characters/route.ts
import { NextResponse } from 'next/server'

// GET
export async function GET(request: Request) {
  return NextResponse.json({ message: 'GET' })
}

// POST
export async function POST(request: Request) {
  const body = await request.json()
  return NextResponse.json({ message: 'POST', data: body })
}

// PUT
export async function PUT(request: Request) {
  const body = await request.json()
  return NextResponse.json({ message: 'PUT', data: body })
}

// DELETE
export async function DELETE(request: Request) {
  return NextResponse.json({ message: 'DELETE' })
}
```

---

## 🎨 Ejemplo completo: API de Dragon Ball

### **Estructura del proyecto:**

```
app/
├── api/
│   └── characters/
│       └── route.ts          # API Route interna
├── characters/
│   └── page.tsx              # Server Component
└── components/
    └── search-characters.tsx # Client Component
```

### **1. Route Handler (API interna):**

```typescript
// app/api/characters/route.ts
import { NextResponse } from 'next/server'

export async function GET(request: Request) {
  const { searchParams } = new URL(request.url)
  const name = searchParams.get('name')
  
  try {
    const url = name
      ? `https://dragonball-api.com/api/characters?name=${name}`
      : 'https://dragonball-api.com/api/characters'
    
    const res = await fetch(url)
    const data = await res.json()
    
    return NextResponse.json(data)
  } catch (error) {
    return NextResponse.json(
      { error: 'Error fetching characters' },
      { status: 500 }
    )
  }
}
```

### **2. Server Component (listado):**

```typescript
// app/characters/page.tsx
interface Character {
  id: number
  name: string
  ki: string
  race: string
  image: string
}

async function getCharacters(): Promise<Character[]> {
  const res = await fetch('https://dragonball-api.com/api/characters', {
    next: { revalidate: 3600 }, // Cachea 1 hora
  })
  
  if (!res.ok) {
    throw new Error('Failed to fetch')
  }
  
  const data = await res.json()
  return data.items
}

export default async function CharactersPage() {
  const characters = await getCharacters()
  
  return (
    <main className="p-8">
      <h1 className="text-4xl font-bold mb-8">
        Personajes de Dragon Ball
      </h1>
      <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
        {characters.map((character) => (
          <div key={character.id} className="border rounded-lg p-4">
            <img
              src={character.image}
              alt={character.name}
              className="w-full h-48 object-cover rounded"
            />
            <h2 className="text-xl font-bold mt-2">{character.name}</h2>
            <p className="text-gray-600">Raza: {character.race}</p>
            <p className="text-gray-600">Ki: {character.ki}</p>
          </div>
        ))}
      </div>
    </main>
  )
}
```

### **3. Client Component (búsqueda):**

```typescript
// app/components/search-characters.tsx
'use client'

import { useState } from 'react'

export default function SearchCharacters() {
  const [query, setQuery] = useState('')
  const [results, setResults] = useState<any[]>([])
  const [loading, setLoading] = useState(false)
  
  const handleSearch = async (e: React.FormEvent) => {
    e.preventDefault()
    if (!query.trim()) return
    
    setLoading(true)
    try {
      const res = await fetch(`/api/characters?name=${query}`)
      const data = await res.json()
      setResults(data.items || [])
    } catch (error) {
      console.error('Error:', error)
    } finally {
      setLoading(false)
    }
  }
  
  return (
    <div className="p-8">
      <form onSubmit={handleSearch} className="mb-6">
        <input
          type="text"
          value={query}
          onChange={(e) => setQuery(e.target.value)}
          placeholder="Buscar personaje..."
          className="border p-2 rounded mr-2"
        />
        <button
          type="submit"
          className="bg-blue-500 text-white px-4 py-2 rounded"
        >
          Buscar
        </button>
      </form>
      
      {loading && <p>Buscando...</p>}
      
      <div className="grid grid-cols-3 gap-4">
        {results.map((char) => (
          <div key={char.id} className="border p-4 rounded">
            <h3>{char.name}</h3>
          </div>
        ))}
      </div>
    </div>
  )
}
```

---

## 🔐 Variables de Entorno

### **Archivo: `.env.local`**

```bash
# API Keys (servidor only)
DRAGON_BALL_API_KEY=tu-api-key-secreta

# URLs públicas (cliente + servidor)
NEXT_PUBLIC_API_URL=https://dragonball-api.com/api
```

### **Uso en código:**

```typescript
// Server Component o Route Handler (ambas funcionan)
const apiKey = process.env.DRAGON_BALL_API_KEY

// Client Component (solo las NEXT_PUBLIC_*)
const apiUrl = process.env.NEXT_PUBLIC_API_URL
```

---

## 📊 Tabla comparativa

| Método | Dónde usar | SEO | Performance | Uso típico |
|--------|-----------|-----|-------------|-----------|
| **Server Component** | Servidor | ✅ Excelente | ⚡ Muy rápido | Listados, páginas estáticas |
| **Client Component** | Cliente | ❌ Limitado | 🐢 Más lento | Búsquedas, interactividad |
| **Route Handler** | Servidor (API) | N/A | ⚡ Rápido | Proxy de APIs, autenticación |
| **SWR** | Cliente | ❌ Limitado | ⚡ Rápido (caché) | Dashboards, datos en tiempo real |

---

## 💡 Mejores prácticas

### ✅ DO:
- Usa **Server Components** por defecto
- Cachea con `revalidate` para datos semi-estáticos
- Usa **Route Handlers** para ocultar API keys
- Maneja errores con try/catch
- Valida datos con Zod o similares
- Usa **SWR** para Client Components con datos dinámicos

### ❌ DON'T:
- No expongas API keys en Client Components
- No hagas fetch en useEffect si puedes usar Server Components
- No uses `cache: 'no-store'` innecesariamente (más lento)
- No olvides manejar estados de loading y error

---

## 🚀 Recursos adicionales

- [Documentación oficial de fetching](https://nextjs.org/docs/app/getting-started/fetching-data)
- [SWR Documentation](https://swr.vercel.app/)
- [Route Handlers](https://nextjs.org/docs/app/building-your-application/routing/route-handlers)

---

## 🎯 Recomendación para tu proyecto Dragon Ball:

```typescript
// Usa Server Components para el listado principal
// app/page.tsx - Server Component
export default async function Home() {
  const res = await fetch('https://dragonball-api.com/api/characters', {
    next: { revalidate: 3600 } // Cachea 1 hora
  })
  const data = await res.json()
  
  return (
    <div>
      {/* Lista de personajes */}
      <SearchCharacters /> {/* Client Component para búsqueda */}
    </div>
  )
}
```

¡Así aprovechas lo mejor de ambos mundos! 🌟