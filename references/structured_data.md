# Dados Estruturados — Schema.org e JSON-LD

## Tipos de Rich Results mais Comuns

| Schema Type | Rich Result | Quando usar |
|-------------|-------------|-------------|
| `FAQPage` | Expansão de perguntas no SERP | Página de FAQ |
| `HowTo` | Passos numerados com imagens | Tutoriais |
| `Article` | Thumbnail + data no SERP | Blog posts |
| `Product` | Estrelas + preço no SERP | E-commerce |
| `LocalBusiness` | Mapa + horários | Negócio local |
| `BreadcrumbList` | Caminho no SERP | Todas as páginas internas |
| `Event` | Data + local no SERP | Eventos |
| `Recipe` | Tempo de preparo + estrelas | Receitas |

## LocalBusiness — Negócio Local

```json
{
  "@context": "https://schema.org",
  "@type": "MedicalClinic",
  "name": "Centro Médico Fraga Maia",
  "url": "https://seusite.com",
  "logo": "https://seusite.com/logo.png",
  "image": ["https://seusite.com/fachada.jpg"],
  "description": "Centro médico em Feira de Santana com especialidades em cardiologia e ortopedia.",
  "telephone": "+55-75-1234-5678",
  "email": "contato@fragamaia.com.br",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "Rua Exemplo, 123, Centro",
    "addressLocality": "Feira de Santana",
    "addressRegion": "BA",
    "postalCode": "44001-000",
    "addressCountry": "BR"
  },
  "geo": {
    "@type": "GeoCoordinates",
    "latitude": -12.2664,
    "longitude": -38.9663
  },
  "openingHoursSpecification": [
    {
      "@type": "OpeningHoursSpecification",
      "dayOfWeek": ["Monday","Tuesday","Wednesday","Thursday","Friday"],
      "opens": "08:00",
      "closes": "18:00"
    },
    {
      "@type": "OpeningHoursSpecification",
      "dayOfWeek": "Saturday",
      "opens": "08:00",
      "closes": "12:00"
    }
  ],
  "priceRange": "$$",
  "currenciesAccepted": "BRL",
  "paymentAccepted": "Cash, Credit Card, Health Insurance",
  "hasMap": "https://maps.google.com/?q=Centro+Médico+Fraga+Maia",
  "sameAs": [
    "https://www.facebook.com/fragamaia",
    "https://www.instagram.com/fragamaia"
  ]
}
```

## Article — Blog Post

```json
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "Como funciona a Ecocardiografia e quando fazer o exame",
  "description": "Saiba o que é ecocardiografia, como é feito o exame e quando seu médico pode indicar.",
  "image": {
    "@type": "ImageObject",
    "url": "https://seusite.com/blog/ecocardiografia.jpg",
    "width": 1200,
    "height": 630
  },
  "author": {
    "@type": "Person",
    "name": "Dr. João Silva",
    "url": "https://seusite.com/equipe/dr-joao-silva"
  },
  "publisher": {
    "@type": "Organization",
    "name": "Centro Médico Fraga Maia",
    "logo": {
      "@type": "ImageObject",
      "url": "https://seusite.com/logo.png"
    }
  },
  "datePublished": "2025-01-10T08:00:00-03:00",
  "dateModified": "2025-01-15T10:30:00-03:00",
  "mainEntityOfPage": {
    "@type": "WebPage",
    "@id": "https://seusite.com/blog/ecocardiografia"
  }
}
```

## Como Implementar JSON-LD em React/Next.js

```tsx
// components/JsonLd.tsx
interface JsonLdProps {
  data: Record<string, unknown>
}

export function JsonLd({ data }: JsonLdProps) {
  return (
    <script
      type="application/ld+json"
      dangerouslySetInnerHTML={{ __html: JSON.stringify(data) }}
    />
  )
}

// Uso na página:
export default function CardiologiaPage() {
  const schema = {
    "@context": "https://schema.org",
    "@type": "MedicalClinic",
    "name": "Centro Médico Fraga Maia",
    // ...
  }

  return (
    <>
      <JsonLd data={schema} />
      <main>...</main>
    </>
  )
}
```

## Testando Dados Estruturados

1. **Rich Results Test**: https://search.google.com/test/rich-results
2. **Schema Markup Validator**: https://validator.schema.org/
3. **Google Search Console** → Melhorias → Dados estruturados
