# 🍩 Guía: The Simpsons API en Next.js (Proyecto Open Source)

## 🎯 Objetivo
Conectar **The Simpsons API** (`https://thesimpsonsapi.com/api/`) en tu proyecto Next.js **sin exponer la URL** en el código (para proyectos open source).

## 📡 Endpoints disponibles:
- `https://thesimpsonsapi.com/api/characters` - Personajes
- `https://thesimpsonsapi.com/api/episodes` - Episodios
- `https://thesimpsonsapi.com/api/locations` - Ubicaciones

---

## 🔐 Paso 1: Configurar Variables de Entorno

### **Archivo: `.env.local`** (en la raíz del proyecto)

```bash
# API Base URL - NO usar NEXT_PUBLIC porque queremos ocultarla
SIMPSONS_API_URL=https://thesimpsonsapi.com/api

# Si la API requiere key (actualmente no, pero por si acaso)
# SIMPSONS_API_KEY=tu-api-key
```

### **Archivo: `.env.example`** (para GitHub)

```bash
# The Simpsons API Configuration
SIMPSONS_API_URL=https://thesimpsonsapi.com/api
# SIMPSONS_API_KEY=your-api-key-here
```

### **Archivo: `.gitignore`** (asegúrate que incluye)

```bash
# Variables de entorno
.env*.local
.env
```

---

## 🛡️ Paso 2: Crear Route Handlers (API Routes)

Estos endpoints **ocultan la URL real** y solo exponen rutas internas como `/api/characters`.

### **Estructura del proyecto:**

```
app/
├── api/
│   ├── characters/
│   │   └── route.ts
│   ├── episodes/
│   │   └── route.ts
│   └── locations/
│       └── route.ts
└── ...
```

---

### **1. Route Handler: Characters**

**Archivo: `app/api/characters/route.ts`**

```typescript
import { NextResponse } from 'next/server'

// GET /api/characters
export async function GET(request: Request) {
  const { searchParams } = new URL(request.url)
  const page = searchParams.get('page') || '1'
  
  const apiUrl = process.env.SIMPSONS_API_URL
  
  if (!apiUrl) {
    return NextResponse.json(
      { error: 'API URL not configured' },
      { status: 500 }
    )
  }
  
  try {
    const res = await fetch(`${apiUrl}/characters?page=${page}`, {
      next: { revalidate: 3600 }, // Cachea 1 hora
    })
    
    if (!res.ok) {
      throw new Error(`API responded with status ${res.status}`)
    }
    
    const data = await res.json()
    
    return NextResponse.json(data)
  } catch (error) {
    console.error('Error fetching characters:', error)
    return NextResponse.json(
      { error: 'Failed to fetch characters' },
      { status: 500 }
    )
  }
}
```

---

### **2. Route Handler: Episodes**

**Archivo: `app/api/episodes/route.ts`**

```typescript
import { NextResponse } from 'next/server'

// GET /api/episodes
export async function GET(request: Request) {
  const { searchParams } = new URL(request.url)
  const page = searchParams.get('page') || '1'
  
  const apiUrl = process.env.SIMPSONS_API_URL
  
  if (!apiUrl) {
    return NextResponse.json(
      { error: 'API URL not configured' },
      { status: 500 }
    )
  }
  
  try {
    const res = await fetch(`${apiUrl}/episodes?page=${page}`, {
      next: { revalidate: 3600 },
    })
    
    if (!res.ok) {
      throw new Error(`API responded with status ${res.status}`)
    }
    
    const data = await res.json()
    
    return NextResponse.json(data)
  } catch (error) {
    console.error('Error fetching episodes:', error)
    return NextResponse.json(
      { error: 'Failed to fetch episodes' },
      { status: 500 }
    )
  }
}
```

---

### **3. Route Handler: Locations**

**Archivo: `app/api/locations/route.ts`**

```typescript
import { NextResponse } from 'next/server'

// GET /api/locations
export async function GET(request: Request) {
  const { searchParams } = new URL(request.url)
  const page = searchParams.get('page') || '1'
  
  const apiUrl = process.env.SIMPSONS_API_URL
  
  if (!apiUrl) {
    return NextResponse.json(
      { error: 'API URL not configured' },
      { status: 500 }
    )
  }
  
  try {
    const res = await fetch(`${apiUrl}/locations?page=${page}`, {
      next: { revalidate: 3600 },
    })
    
    if (!res.ok) {
      throw new Error(`API responded with status ${res.status}`)
    }
    
    const data = await res.json()
    
    return NextResponse.json(data)
  } catch (error) {
    console.error('Error fetching locations:', error)
    return NextResponse.json(
      { error: 'Failed to fetch locations' },
      { status: 500 }
    )
  }
}
```

---

## 📦 Paso 3: Consumir las APIs desde componentes

### **Opción A: Server Component (Recomendado para SEO)**

**Archivo: `app/characters/page.tsx`**

```typescript
interface Character {
  _id: number
  name: string
  normalized_name: string
  image_url: string
}

interface ApiResponse {
  docs: Character[]
  total: number
  page: number
  totalPages: number
}

async function getCharacters(page: number = 1): Promise<ApiResponse> {
  // Fetch a TU API interna, no a la API externa
  const baseUrl = process.env.NEXT_PUBLIC_BASE_URL || 'http://localhost:3000'
  const res = await fetch(`${baseUrl}/api/characters?page=${page}`, {
    next: { revalidate: 3600 }, // Cachea 1 hora
  })
  
  if (!res.ok) {
    throw new Error('Failed to fetch characters')
  }
  
  return res.json()
}

export default async function CharactersPage() {
  const data = await getCharacters()
  
  return (
    <main className="p-8">
      <h1 className="text-4xl font-bold mb-8">
        Los Simpsons - Personajes
      </h1>
      
      <div className="grid grid-cols-1 md:grid-cols-3 lg:grid-cols-4 gap-6">
        {data.docs.map((character) => (
          <div 
            key={character._id} 
            className="border rounded-lg p-4 hover:shadow-lg transition"
          >
            <img
              src={character.image_url}
              alt={character.name}
              className="w-full h-48 object-cover rounded mb-3"
            />
            <h2 className="text-xl font-bold">{character.name}</h2>
          </div>
        ))}
      </div>
      
      <div className="mt-8 text-center">
        <p>Página {data.page} de {data.totalPages}</p>
        <p>Total de personajes: {data.total}</p>
      </div>
    </main>
  )
}
```

---

### **Opción B: Client Component (para interactividad)**

**Archivo: `app/components/characters-list.tsx`**

```typescript
'use client'

import { useState, useEffect } from 'react'

interface Character {
  _id: number
  name: string
  normalized_name: string
  image_url: string
}

export default function CharactersList() {
  const [characters, setCharacters] = useState<Character[]>([])
  const [loading, setLoading] = useState(true)
  const [error, setError] = useState<string | null>(null)
  const [page, setPage] = useState(1)
  
  useEffect(() => {
    async function fetchCharacters() {
      setLoading(true)
      try {
        // Llama a TU API interna
        const res = await fetch(`/api/characters?page=${page}`)
        
        if (!res.ok) {
          throw new Error('Error al cargar personajes')
        }
        
        const data = await res.json()
        setCharacters(data.docs)
      } catch (err) {
        setError(err instanceof Error ? err.message : 'Error desconocido')
      } finally {
        setLoading(false)
      }
    }
    
    fetchCharacters()
  }, [page])
  
  if (loading) return <div className="text-center p-8">Cargando...</div>
  if (error) return <div className="text-red-500 p-8">Error: {error}</div>
  
  return (
    <div className="p-8">
      <h1 className="text-4xl font-bold mb-8">Personajes</h1>
      
      <div className="grid grid-cols-4 gap-6">
        {characters.map((character) => (
          <div key={character._id} className="border rounded-lg p-4">
            <img
              src={character.image_url}
              alt={character.name}
              className="w-full h-48 object-cover rounded"
            />
            <h2 className="text-lg font-bold mt-2">{character.name}</h2>
          </div>
        ))}
      </div>
      
      <div className="mt-8 flex justify-center gap-4">
        <button
          onClick={() => setPage(p => Math.max(1, p - 1))}
          disabled={page === 1}
          className="bg-blue-500 text-white px-4 py-2 rounded disabled:opacity-50"
        >
          Anterior
        </button>
        <span className="py-2">Página {page}</span>
        <button
          onClick={() => setPage(p => p + 1)}
          className="bg-blue-500 text-white px-4 py-2 rounded"
        >
          Siguiente
        </button>
      </div>
    </div>
  )
}
```

---

## 🎨 Ejemplo completo: Página con pestañas

**Archivo: `app/page.tsx`**

```typescript
import CharactersTab from './components/characters-tab'
import EpisodesTab from './components/episodes-tab'
import LocationsTab from './components/locations-tab'

export default function Home() {
  return (
    <main className="min-h-screen p-8">
      <header className="mb-8">
        <h1 className="text-5xl font-bold text-yellow-400">
          🍩 The Simpsons API
        </h1>
        <p className="text-gray-600 mt-2">
          Explora personajes, episodios y ubicaciones
        </p>
      </header>
      
      {/* Aquí puedes agregar tabs o secciones */}
      <CharactersTab />
    </main>
  )
}
```

---

## 🔄 Ejemplo con SWR (Recomendado para Client Components)

**Instalación:**
```bash
pnpm add swr
```

**Archivo: `app/components/characters-with-swr.tsx`**

```typescript
'use client'

import useSWR from 'swr'

const fetcher = (url: string) => fetch(url).then((res) => res.json())

export default function CharactersWithSWR() {
  const { data, error, isLoading } = useSWR('/api/characters', fetcher, {
    revalidateOnFocus: false,
    dedupingInterval: 60000, // No re-fetch por 1 minuto
  })
  
  if (isLoading) return <div>Cargando...</div>
  if (error) return <div>Error al cargar datos</div>
  
  return (
    <div className="grid grid-cols-4 gap-4">
      {data.docs.map((character: any) => (
        <div key={character._id} className="border p-4 rounded">
          <img src={character.image_url} alt={character.name} />
          <h3>{character.name}</h3>
        </div>
      ))}
    </div>
  )
}
```

---

## 🚀 Desplegar en Vercel (Open Source)

### **1. Agregar variables de entorno en Vercel:**

1. Ve a tu proyecto en Vercel
2. Settings → Environment Variables
3. Agrega:
   ```
   SIMPSONS_API_URL = https://thesimpsonsapi.com/api
   ```
4. Marca: Production, Preview, Development

### **2. En tu README.md (para colaboradores):**

```markdown
## 🔧 Setup

1. Clona el repositorio:
   ```bash
   git clone https://github.com/tu-usuario/simpsons-app.git
   cd simpsons-app
   ```

2. Instala dependencias:
   ```bash
   pnpm install
   ```

3. Configura variables de entorno:
   ```bash
   cp .env.example .env.local
   ```
   
   Edita `.env.local` y agrega:
   ```bash
   SIMPSONS_API_URL=https://thesimpsonsapi.com/api
   ```

4. Corre el proyecto:
   ```bash
   pnpm run dev
   ```

5. Abre [http://localhost:3000](http://localhost:3000)
```

---

## 📁 Estructura final del proyecto

```
simpsons-app/
├── .env.local                    # ❌ NO subir a Git
├── .env.example                  # ✅ Subir a Git (plantilla)
├── .gitignore                    # ✅ Incluye .env*.local
├── README.md                     # ✅ Instrucciones de setup
├── app/
│   ├── api/
│   │   ├── characters/
│   │   │   └── route.ts         # 🛡️ Proxy de la API
│   │   ├── episodes/
│   │   │   └── route.ts         # 🛡️ Proxy de la API
│   │   └── locations/
│   │       └── route.ts         # 🛡️ Proxy de la API
│   ├── characters/
│   │   └── page.tsx             # 📄 Página de personajes
│   ├── episodes/
│   │   └── page.tsx             # 📄 Página de episodios
│   ├── locations/
│   │   └── page.tsx             # 📄 Página de ubicaciones
│   ├── components/
│   │   ├── characters-list.tsx  # 🎨 Componente
│   │   ├── episodes-list.tsx    # 🎨 Componente
│   │   └── locations-list.tsx   # 🎨 Componente
│   ├── layout.tsx
│   └── page.tsx                 # 🏠 Home
└── package.json
```

---

## 🛡️ Por qué este enfoque es seguro para Open Source

### ✅ Ventajas:

1. **La URL de la API NUNCA aparece en el código del cliente**
   - Solo existe en `.env.local` (ignorado por Git)
   - Solo existe en Route Handlers (servidor)

2. **Cualquiera puede clonar el repo**
   - Usan `.env.example` como plantilla
   - Configuran su propia API URL

3. **Fácil de cambiar la API**
   - Si cambia la URL, solo editas `.env.local`
   - No necesitas cambiar código

4. **Control de caché y rate limiting**
   - Puedes agregar lógica en Route Handlers
   - Proteges la API externa de abuso

---

## 🔒 Ejemplo con Rate Limiting (Opcional)

Si quieres proteger aún más tu API:

**Archivo: `app/api/characters/route.ts`** (con rate limiting)

```typescript
import { NextResponse } from 'next/server'

// Simple rate limiting (en producción usa Redis)
const requestCounts = new Map<string, number>()

export async function GET(request: Request) {
  const ip = request.headers.get('x-forwarded-for') || 'unknown'
  const count = requestCounts.get(ip) || 0
  
  // Máximo 10 requests por minuto
  if (count > 10) {
    return NextResponse.json(
      { error: 'Too many requests' },
      { status: 429 }
    )
  }
  
  requestCounts.set(ip, count + 1)
  setTimeout(() => requestCounts.delete(ip), 60000) // Reset después de 1 min
  
  const apiUrl = process.env.SIMPSONS_API_URL
  
  try {
    const res = await fetch(`${apiUrl}/characters`)
    const data = await res.json()
    return NextResponse.json(data)
  } catch (error) {
    return NextResponse.json(
      { error: 'Failed to fetch' },
      { status: 500 }
    )
  }
}
```

---

## 📊 Tipos TypeScript (Opcional pero recomendado)

**Archivo: `types/simpsons.ts`**

```typescript
export interface Character {
  _id: number
  name: string
  normalized_name: string
  image_url: string
}

export interface Episode {
  _id: number
  name: string
  air_date: string
  episode_number: string
}

export interface Location {
  _id: number
  name: string
  normalized_name: string
  image_url: string
}

export interface ApiResponse<T> {
  docs: T[]
  total: number
  page: number
  totalPages: number
}
```

**Uso:**

```typescript
import { Character, ApiResponse } from '@/types/simpsons'

async function getCharacters(): Promise<ApiResponse<Character>> {
  const res = await fetch('/api/characters')
  return res.json()
}
```

---

## 🎯 Checklist de seguridad para Open Source

- [ ] `.env.local` está en `.gitignore`
- [ ] Creaste `.env.example` con valores placeholder
- [ ] La API URL NO aparece en ningún archivo de código
- [ ] Todos los fetches van a `/api/*` (tus Route Handlers)
- [ ] README.md explica cómo configurar variables de entorno
- [ ] Variables agregadas en Vercel para deployment
- [ ] NO usas `NEXT_PUBLIC_` para URLs que quieres ocultar

---

## 💡 Ventaja adicional: Fácil migración de API

Si en el futuro cambias de API (ej: de Simpsons a Rick and Morty):

1. Cambias solo el `.env.local`:
   ```bash
   SIMPSONS_API_URL=https://rickandmortyapi.com/api
   ```

2. Ajustas los Route Handlers si la estructura de respuesta cambia

3. **El resto del código sigue igual** ✨

---

## 🆘 Troubleshooting

### **Error: "API URL not configured"**

```bash
# Verifica que .env.local existe
ls .env.local

# Verifica el contenido
cat .env.local

# Debe contener:
SIMPSONS_API_URL=https://thesimpsonsapi.com/api
```

### **Error: "Failed to fetch"**

```bash
# Verifica que la API esté funcionando
curl https://thesimpsonsapi.com/api/characters

# Verifica tus Route Handlers
# Abre: http://localhost:3000/api/characters
```

---

## 🚀 Próximos pasos

1. Implementa paginación
2. Agrega búsqueda de personajes
3. Crea páginas de detalle individual
4. Agrega filtros (por temporada, ubicación, etc.)
5. Implementa favoritos (localStorage)

---

**¡Listo para empezar!** 🍩✨

Este enfoque es 100% seguro para proyectos open source en GitHub.