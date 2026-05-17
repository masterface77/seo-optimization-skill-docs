# SEO para SPAs — React, Next.js e Vite

## O Problema com SPAs e SEO

SPAs (Single Page Applications) renderizam conteúdo via JavaScript no client-side. O Googlebot executa JS, mas com atraso. Isso significa que:

- Meta tags geradas pelo JS podem não ser lidas imediatamente
- Links dinâmicos podem não ser rastreados no primeiro crawl
- O conteúdo pode aparecer vazio para rastreadores que não executam JS

## Solução 1 — Next.js (App Router) — Recomendado

```tsx
// app/cardiologia/page.tsx
import type { Metadata } from 'next'

// SEO automático via Metadata API
export const metadata: Metadata = {
  title: 'Cardiologia | Centro Médico Fraga Maia',
  description: 'Especialistas em cardiologia em Feira de Santana. Agende sua consulta.',
  keywords: ['cardiologia', 'feira de santana', 'médico coração'],
  openGraph: {
    title: 'Cardiologia | Centro Médico Fraga Maia',
    description: 'Especialistas em cardiologia em Feira de Santana.',
    url: 'https://seusite.com/cardiologia',
    images: [
      {
        url: 'https://seusite.com/og-cardiologia.jpg',
        width: 1200,
        height: 630,
        alt: 'Cardiologia no Centro Médico Fraga Maia',
      },
    ],
    locale: 'pt_BR',
    type: 'website',
  },
  twitter: {
    card: 'summary_large_image',
    title: 'Cardiologia | Centro Médico Fraga Maia',
    description: 'Especialistas em cardiologia em Feira de Santana.',
    images: ['https://seusite.com/og-cardiologia.jpg'],
  },
  alternates: {
    canonical: 'https://seusite.com/cardiologia',
  },
  robots: {
    index: true,
    follow: true,
  },
}

export default function CardiologiaPage() {
  return <main>...</main>
}
```

```tsx
// app/layout.tsx — Metadata base (herdada por todas as páginas)
export const metadata: Metadata = {
  metadataBase: new URL('https://seusite.com'),
  title: {
    default: 'Centro Médico Fraga Maia',
    template: '%s | Centro Médico Fraga Maia',
  },
  description: 'Centro médico em Feira de Santana com especialistas em cardiologia, ortopedia e clínica geral.',
}
```

## Solução 2 — React (Vite/CRA) com react-helmet-async

```bash
npm install react-helmet-async
```

```tsx
// main.tsx — configuração global
import { HelmetProvider } from 'react-helmet-async'

ReactDOM.createRoot(document.getElementById('root')!).render(
  <HelmetProvider>
    <App />
  </HelmetProvider>
)
```

```tsx
// components/SEO.tsx — componente reutilizável
import { Helmet } from 'react-helmet-async'

interface SEOProps {
  title: string
  description: string
  canonical: string
  ogImage?: string
}

export function SEO({ title, description, canonical, ogImage }: SEOProps) {
  const siteName = 'Centro Médico Fraga Maia'
  const fullTitle = `${title} | ${siteName}`
  const defaultImage = 'https://seusite.com/og-default.jpg'

  return (
    <Helmet>
      <title>{fullTitle}</title>
      <meta name="description" content={description} />
      <link rel="canonical" href={canonical} />
      <meta property="og:title" content={fullTitle} />
      <meta property="og:description" content={description} />
      <meta property="og:url" content={canonical} />
      <meta property="og:image" content={ogImage ?? defaultImage} />
      <meta property="og:type" content="website" />
      <meta property="og:locale" content="pt_BR" />
      <meta name="twitter:card" content="summary_large_image" />
      <meta name="twitter:title" content={fullTitle} />
      <meta name="twitter:description" content={description} />
      <meta name="twitter:image" content={ogImage ?? defaultImage} />
    </Helmet>
  )
}

// Uso nas páginas:
function CardiologiaPage() {
  return (
    <>
      <SEO
        title="Cardiologia"
        description="Especialistas em cardiologia em Feira de Santana. Agende sua consulta."
        canonical="https://seusite.com/cardiologia"
        ogImage="https://seusite.com/og-cardiologia.jpg"
      />
      <main>...</main>
    </>
  )
}
```

## Sitemap e robots.txt em Vite

```
public/
├── robots.txt      ← copiado automaticamente para /
└── sitemap.xml     ← copiado automaticamente para /
```

## Sitemap dinâmico no Next.js

```tsx
// app/sitemap.ts
import { MetadataRoute } from 'next'

export default async function sitemap(): Promise<MetadataRoute.Sitemap> {
  // Busca posts do banco de dados
  const posts = await fetch('https://api.seusite.com/posts').then(r => r.json())

  const postUrls = posts.map((post: any) => ({
    url: `https://seusite.com/blog/${post.slug}`,
    lastModified: new Date(post.updatedAt),
    changeFrequency: 'weekly' as const,
    priority: 0.7,
  }))

  return [
    {
      url: 'https://seusite.com',
      lastModified: new Date(),
      changeFrequency: 'weekly',
      priority: 1,
    },
    {
      url: 'https://seusite.com/cardiologia',
      lastModified: new Date(),
      changeFrequency: 'monthly',
      priority: 0.8,
    },
    ...postUrls,
  ]
}
```
