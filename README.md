README (pasos rápidos)

## Requisitos
- Node 18+
- Cuenta en GitHub y Vercel

## 1) Crear proyecto base
npx create-next-app@latest ofertas-battlezone --typescript --eslint --tailwind --app --src-dir --import-alias "@/*"
cd ofertas-battlezone

## 2) Reemplaza/añade los archivos de esta plantilla
Copia el contenido de cada archivo a tu proyecto (mismo path). Si un archivo ya existe, reemplázalo.

## 3) Ejecuta en local
npm run dev

## 4) Deploy en Vercel
- Sube el repo a GitHub
- Entra a vercel.com → Add New → Project → Importa tu repo → Deploy

## 5) Verifica PWA
- Abre la app y revisa en Chrome → Lighthouse → PWA
- En móvil, prueba "Añadir a pantalla de inicio"

---

# package.json (añade los scripts si faltan)
```json
{
  "name": "ofertas-battlezone",
  "version": "1.0.0",
  "private": true,
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint"
  },
  "dependencies": {
    "next": "14.2.5",
    "react": "18.3.1",
    "react-dom": "18.3.1"
  },
  "devDependencies": {
    "@types/node": "20.11.30",
    "@types/react": "18.2.66",
    "@types/react-dom": "18.2.22",
    "autoprefixer": "10.4.19",
    "eslint": "8.57.0",
    "eslint-config-next": "14.2.5",
    "postcss": "8.4.38",
    "tailwindcss": "3.4.3",
    "typescript": "5.4.5"
  }
}


---

tailwind.config.ts

import type { Config } from 'tailwindcss'

const config: Config = {
  content: [
    './src/pages/**/*.{js,ts,jsx,tsx,mdx}',
    './src/components/**/*.{js,ts,jsx,tsx,mdx}',
    './src/app/**/*.{js,ts,jsx,tsx,mdx}',
  ],
  theme: {
    extend: {
      colors: {
        bz: {
          purple: '#5D2F91',
          yellow: '#FFDB00',
          red: '#C3262F',
          black: '#101010'
        }
      },
      boxShadow: {
        soft: '0 10px 30px rgba(0,0,0,0.08)'
      },
      borderRadius: {
        xl2: '1.25rem'
      }
    },
  },
  plugins: [],
}
export default config


---

postcss.config.js

module.exports = {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  },
}


---

src/app/globals.css

@tailwind base;
@tailwind components;
@tailwind utilities;

:root {
  --bz-bg: #0f0f0f;
  --bz-card: #151515;
  --bz-text: #ffffff;
}

html, body {
  background: var(--bz-bg);
  color: var(--bz-text);
}

/* Helpers */
.container-bz { @apply mx-auto max-w-6xl px-4; }
.card { @apply bg-[var(--bz-card)] rounded-2xl shadow-soft border border-white/5; }
.btn { @apply inline-flex items-center justify-center rounded-xl px-4 py-2 font-medium transition; }
.btn-primary { @apply bg-bz.purple text-white hover:opacity-90; }
.badge { @apply rounded-full px-3 py-1 text-xs; }
.badge-hot { @apply bg-red-500/10 text-red-400; }
.badge-new { @apply bg-white/10 text-white/80; }


---

src/app/layout.tsx

import type { Metadata } from 'next'
import './globals.css'

export const metadata: Metadata = {
  title: 'Ofertas Battlezone',
  description: 'Ofertas, descuentos y preventas geek para LATAM',
  manifest: '/manifest.json',
  themeColor: '#5D2F91',
  icons: {
    icon: '/icons/icon-192.png',
    apple: '/icons/icon-192.png',
  },
  openGraph: {
    title: 'Ofertas Battlezone',
    description: 'Ofertas, descuentos y preventas geek para LATAM',
    url: 'https://tu-dominio.com',
    siteName: 'Ofertas Battlezone',
    images: [{ url: '/og.jpg', width: 1200, height: 630 }],
    type: 'website'
  },
  twitter: {
    card: 'summary_large_image',
    title: 'Ofertas Battlezone',
    description: 'Ofertas, descuentos y preventas geek para LATAM',
    images: ['/og.jpg']
  }
}

export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="es">
      <body>{children}</body>
    </html>
  )
}


---

src/app/page.tsx

import Link from 'next/link'
import DealsGrid from '@/components/DealsGrid'

export default function Home() {
  return (
    <main>
      <header className="border-b border-white/10">
        <div className="container-bz py-6 flex items-center justify-between">
          <Link href="/" className="text-xl font-bold">Battlezone <span className="text-bz.yellow">Ofertas</span></Link>
          <nav className="flex gap-3">
            <Link href="/publicar" className="btn btn-primary">Publicar oferta</Link>
          </nav>
        </div>
      </header>

      <section className="container-bz py-6">
        <div className="flex items-center gap-2 mb-4">
          <span className="badge badge-new">Nuevo</span>
          <span className="badge badge-hot">Hot</span>
        </div>
        <DealsGrid />
      </section>

      <footer className="border-t border-white/10">
        <div className="container-bz py-8 text-sm opacity-70">
          © {new Date().getFullYear()} Battlezone LATAM — Hecho con ♥ en México
        </div>
      </footer>
    </main>
  )
}


---

src/components/DealCard.tsx

export type Deal = {
  id: string
  title: string
  url: string
  image: string
  store: 'amazon' | 'aliexpress' | 'mercadolibre' | 'ebay' | string
  category: string
  price_now: number
  price_list?: number
  author?: string
  created_at?: string
}

export default function DealCard({ deal }: { deal: Deal }) {
  const pct = deal.price_list ? Math.max(0, Math.round(100 - (deal.price_now * 100) / deal.price_list)) : null
  return (
    <a href={deal.url} target="_blank" rel="nofollow sponsored" className="card p-3 hover:shadow-xl transition block">
      <div className="aspect-[4/3] overflow-hidden rounded-xl mb-3 bg-black/30">
        <img src={deal.image} alt={deal.title} className="w-full h-full object-cover" />
      </div>
      <h3 className="font-semibold line-clamp-2 mb-2">{deal.title}</h3>
      <div className="flex items-baseline gap-2">
        <span className="text-xl font-bold">${deal.price_now.toLocaleString()}</span>
        {deal.price_list && <span className="line-through text-sm opacity-70">${deal.price_list.toLocaleString()}</span>}
        {pct !== null && <span className="ml-auto badge bg-red-500/10 text-red-400">-{pct}%</span>}
      </div>
      <div className="mt-2 text-xs opacity-70">{deal.store} • {deal.category}</div>
    </a>
  )
}


---

src/components/DealsGrid.tsx

import DealCard, { Deal } from './DealCard'
import { getDeals } from '@/lib/deals'

export default async function DealsGrid() {
  const deals: Deal[] = await getDeals()
  return (
    <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4">
      {deals.map(d => <DealCard key={d.id} deal={d} />)}
    </div>
  )
}


---

src/lib/deals.ts (mock; cámbialo por tu DB/API)

import { Deal } from '@/components/DealCard'

export async function getDeals(): Promise<Deal[]> {
  // Aquí puedes llamar a tu DB (Supabase/Firebase) o a una API.
  // De momento, devolvemos datos mock.
  return [
    {
      id: '1',
      title: 'Lego Star Wars X-Wing — 30% OFF',
      url: 'https://amzn.to/tu-link-afiliado',
      image: '/demo/demo-1.jpg',
      store: 'amazon',
      category: 'Geek Chronicles',
      price_now: 1299,
      price_list: 1899,
      author: 'TheGeekChroniclesBot',
      created_at: new Date().toISOString(),
    },
    {
      id: '2',
      title: 'Funko Pop! Harry Potter — Oferta relámpago',
      url: 'https://amzn.to/tu-link-afiliado',
      image: '/demo/demo-2.jpg',
      store: 'amazon',
      category: 'Coleccionables',
      price_now: 229,
      price_list: 349,
    },
    {
      id: '3',
      title: 'Auriculares Gaming RGB — AliExpress',
      url: 'https://s.click.aliexpress.com/e/tu-link',
      image: '/demo/demo-3.jpg',
      store: 'aliexpress',
      category: 'Home & Tech',
      price_now: 399,
      price_list: 699,
    },
  ]
}


---

src/app/publicar/page.tsx (formulario simple; envía a /api/deals)

'use client'
import { useState } from 'react'

export default function Publicar() {
  const [loading, setLoading] = useState(false)
  const [ok, setOk] = useState<string | null>(null)

  async function onSubmit(e: React.FormEvent<HTMLFormElement>) {
    e.preventDefault()
    setLoading(true)
    setOk(null)
    const data = Object.fromEntries(new FormData(e.currentTarget).entries())
    const res = await fetch('/api/deals', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(data)
    })
    const json = await res.json()
    setLoading(false)
    setOk(json.ok ? 'Enviado para revisión' : 'Error al enviar')
    e.currentTarget.reset()
  }

  return (
    <main className="container-bz py-8">
      <h1 className="text-2xl font-bold mb-4">Publicar oferta</h1>
      <form onSubmit={onSubmit} className="card p-4 grid gap-3">
        <input name="title" placeholder="Título" required className="bg-white/5 rounded-xl px-3 py-2" />
        <input name="url" placeholder="URL de la oferta (afiliado)" required className="bg-white/5 rounded-xl px-3 py-2" />
        <input name="image" placeholder="URL de imagen" className="bg-white/5 rounded-xl px-3 py-2" />
        <div className="grid grid-cols-2 gap-3">
          <input name="price_now" type="number" placeholder="Precio actual" required className="bg-white/5 rounded-xl px-3 py-2" />
          <input name="price_list" type="number" placeholder="Precio de lista (opcional)" className="bg-white/5 rounded-xl px-3 py-2" />
        </div>
        <div className="grid grid-cols-2 gap-3">
          <input name="store" placeholder="Tienda (amazon/aliexpress/ml)" className="bg-white/5 rounded-xl px-3 py-2" />
          <input name="category" placeholder="Categoría" className="bg-white/5 rounded-xl px-3 py-2" />
        </div>
        <button className="btn btn-primary" disabled={loading}>{loading ? 'Enviando…' : 'Enviar'}</button>
        {ok && <p className="text-sm opacity-80">{ok}</p>}
      </form>
    </main>
  )
}


---

src/app/api/deals/route.ts (endpoint demo)

import { NextResponse } from 'next/server'

export async function POST(req: Request) {
  const body = await req.json()
  // TODO: Validar y guardar en DB; por ahora respondemos OK
  console.log('DEAL NUEVA', body)
  return NextResponse.json({ ok: true })
}


---

public/manifest.json (PWA)

{
  "name": "Ofertas Battlezone",
  "short_name": "BZ Ofertas",
  "start_url": "/?source=pwa",
  "scope": "/",
  "display": "standalone",
  "background_color": "#000000",
  "theme_color": "#5D2F91",
  "icons": [
    { "src": "/icons/icon-192.png", "sizes": "192x192", "type": "image/png" },
    { "src": "/icons/icon-512.png", "sizes": "512x512", "type": "image/png" }
  ]
}


---

public/sw.js (Service Worker simple)

const CACHE = 'bz-v1'
const ASSETS = [
  '/',
  '/manifest.json',
  '/icons/icon-192.png',
  '/icons/icon-512.png'
]
self.addEventListener('install', e => {
  e.waitUntil(caches.open(CACHE).then(c => c.addAll(ASSETS)))
})
self.addEventListener('activate', e => {
  e.waitUntil(
    caches.keys().then(keys => Promise.all(keys.filter(k => k !== CACHE).map(k => caches.delete(k))))
  )
})
self.addEventListener('fetch', e => {
  e.respondWith(
    caches.match(e.request).then(r => r || fetch(e.request).catch(() => caches.match('/')))
  )
})


---

src/app/register-sw.tsx (registra el SW)

'use client'
import { useEffect } from 'react'

export default function RegisterSW() {
  useEffect(() => {
    if ('serviceWorker' in navigator) {
      window.addEventListener('load', () => {
        navigator.serviceWorker.register('/sw.js')
      })
    }
  }, [])
  return null
}


---

src/app/(providers)/layout.tsx (inyecta el registro del SW en la home si quieres)

import RegisterSW from '../register-sw'

export default function ProvidersLayout({ children }: { children: React.ReactNode }) {
  return (
    <>
      <RegisterSW />
      {children}
    </>
  )
}


---

public/robots.txt

User-agent: *
Allow: /
Sitemap: https://tu-dominio.com/sitemap.xml


---

next-sitemap.config.js (opcional si instalas next-sitemap)

/** @type {import('next-sitemap').IConfig} */
module.exports = {
  siteUrl: 'https://tu-dominio.com',
  generateRobotsTxt: true,
}


---

vercel.json (headers y ejemplo de redirect)

{
  "headers": [
    {
      "source": "(.*)",
      "headers": [
        { "key": "X-Frame-Options", "value": "SAMEORIGIN" },
        { "key": "X-Content-Type-Options", "value": "nosniff" }
      ]
    },
    {
      "source": "/(.*)\.(jpg|jpeg|png|webp|svg)",
      "headers": [
        { "key": "Cache-Control", "value": "public, max-age=31536000, immutable" }
      ]
    }
  ],
  "redirects": [
    { "source": "/ofertas", "destination": "/", "permanent": true }
  ]
}


---

Notas finales

- Reemplaza /demo/*.jpg por tus imágenes reales.
- Agrega /public/icons/icon-192.png e icon-512.png (puedes generarlas en realfavicongenerator.net).
- Para datos reales, conecta una DB (Supabase) y sustituye src/lib/deals.ts por consultas.
- Añade rel="nofollow sponsored" a links de afiliado (ya está en DealCard).
- Estilos y colores alineados a tu paleta (#5D2F91, #FFDB00, #C3262F, #101010).


