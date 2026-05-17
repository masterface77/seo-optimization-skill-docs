---
name: seo-optimization
description: >
  Skill especializada em otimização de SEO baseada nos fundamentos do Google Search.
  Cobre rastreabilidade, indexação, conteúdo semântico, Core Web Vitals, dados estruturados,
  SEO técnico, performance, SPAs/React, Next.js, robots.txt, sitemap.xml, meta tags,
  Schema.org, Open Graph, Twitter Cards, canonical URLs, links internos, auditorias e
  monitoramento com Google Search Console. Use SEMPRE que o usuário mencionar SEO,
  otimização para motores de busca, indexação, Google Search, robots.txt, sitemap,
  meta tags, Core Web Vitals, dados estruturados, Schema.org, Open Graph, rastreamento
  Googlebot ou qualquer tarefa relacionada a visibilidade em buscadores.
compatibility:
  frameworks: [react, next.js, vite, nuxt, astro, html-puro]
  tools: [google-search-console, lighthouse, pagespeed-insights, screaming-frog]
triggers:
  - seo
  - otimização de busca
  - indexação
  - google search
  - robots.txt
  - sitemap
  - meta tags
  - core web vitals
  - schema.org
  - open graph
  - rastreamento
  - googlebot
  - pagerank
  - serp
---

# SEO Optimization — Skill Completa para Google Search

## ÍNDICE DE REFERÊNCIAS

> Para tarefas específicas, leia o arquivo de referência correspondente:

| Tópico | Arquivo | Quando ler |
|--------|---------|-----------|
| Rastreabilidade e Indexação | `references/crawling_indexing.md` | robots.txt, sitemap, Googlebot |
| Conteúdo e Tags Meta | `references/content_meta.md` | title, description, OG, Twitter Cards |
| Dados Estruturados | `references/structured_data.md` | Schema.org, JSON-LD, Rich Results |
| SEO Técnico e Performance | `references/technical_seo.md` | Core Web Vitals, CLS, LCP, FID |
| SEO para SPAs e React | `references/spa_seo.md` | Next.js, Vite, react-helmet, SSR |
| Monitoramento e Auditoria | `references/monitoring.md` | GSC, Lighthouse, erros de indexação |
| Workflow Passo a Passo | `workflows/seo_checklist.md` | Checklist completo para implementação |

---

## PRINCÍPIOS FUNDAMENTAIS DE SEO

### 1. Rastreabilidade — robots.txt

```
# robots.txt — localização: /public/robots.txt ou raiz do domínio

# Permite acesso total ao Googlebot (padrão recomendado)
User-agent: Googlebot
Allow: /

# Permite acesso total a todos os robôs
User-agent: *
Allow: /

# NUNCA bloqueie JS, CSS ou imagens — o Googlebot precisa renderizar a página
# ERRADO:  Disallow: /static/
# ERRADO:  Disallow: *.js$
# CORRETO: deixar Allow: / para todos os recursos necessários à renderização

# Bloqueia áreas administrativas e APIs internas (não precisam de indexação)
User-agent: *
Disallow: /admin/
Disallow: /api/
Disallow: /dashboard/
Disallow: /_next/static/  # Next.js internals

# Referência ao sitemap (obrigatório!)
Sitemap: https://seusite.com/sitemap.xml
Sitemap: https://seusite.com/sitemap-images.xml
```

---

### 2. Sitemap XML

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9"
        xmlns:image="http://www.google.com/schemas/sitemap-image/1.1">

  <!-- Página principal — maior prioridade -->
  <url>
    <loc>https://seusite.com/</loc>
    <lastmod>2025-01-15</lastmod>
    <changefreq>weekly</changefreq>
    <priority>1.0</priority>
  </url>

  <!-- Página com imagem para Google Imagens -->
  <url>
    <loc>https://seusite.com/sobre</loc>
    <lastmod>2025-01-10</lastmod>
    <changefreq>monthly</changefreq>
    <priority>0.8</priority>
    <image:image>
      <image:loc>https://seusite.com/images/equipe.jpg</image:loc>
      <image:caption>Equipe de profissionais da empresa</image:caption>
      <image:title>Sobre nós</image:title>
    </image:image>
  </url>

  <!-- Blog/artigos — frequência alta -->
  <url>
    <loc>https://seusite.com/blog/como-funciona-seo</loc>
    <lastmod>2025-01-20</lastmod>
    <changefreq>weekly</changefreq>
    <priority>0.7</priority>
  </url>

</urlset>
```

**Sitemap Index (para sites grandes):**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<sitemapindex xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <sitemap>
    <loc>https://seusite.com/sitemap-pages.xml</loc>
    <lastmod>2025-01-20</lastmod>
  </sitemap>
  <sitemap>
    <loc>https://seusite.com/sitemap-blog.xml</loc>
    <lastmod>2025-01-20</lastmod>
  </sitemap>
  <sitemap>
    <loc>https://seusite.com/sitemap-images.xml</loc>
    <lastmod>2025-01-20</lastmod>
  </sitemap>
</sitemapindex>
```

---

### 3. Meta Tags Essenciais

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <!-- CHARSET: sempre UTF-8, primeiro elemento do head -->
  <meta charset="UTF-8">

  <!-- VIEWPORT: obrigatório para mobile-first indexing do Google -->
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <!-- TITLE: único por página, 50-60 caracteres, keyword no início -->
  <!-- Formato: "Keyword Principal | Nome do Site - Localização" -->
  <title>Centro Médico Fraga Maia - Cardiologia | Feira de Santana, BA</title>

  <!-- META DESCRIPTION: 120-160 chars, inclua CTA e keyword -->
  <meta name="description"
        content="Cardiologia de alta precisão no Centro Médico Fraga Maia, Feira de Santana. Agende sua consulta e cuide do seu coração com especialistas certificados.">

  <!-- CANONICAL: evita conteúdo duplicado — SEMPRE defina em cada página -->
  <link rel="canonical" href="https://seusite.com/cardiologia">

  <!-- ROBOTS: controle fino de indexação por página -->
  <!-- noindex: não indexa | nofollow: não segue links | noarchive: sem cache -->
  <meta name="robots" content="index, follow">
  <!-- Para páginas que NÃO devem ser indexadas: -->
  <!-- <meta name="robots" content="noindex, nofollow"> -->

  <!-- OPEN GRAPH (Facebook, LinkedIn, WhatsApp) -->
  <meta property="og:type"        content="website">
  <meta property="og:title"       content="Centro Médico Fraga Maia - Cardiologia">
  <meta property="og:description" content="Cardiologia de alta precisão em Feira de Santana.">
  <meta property="og:url"         content="https://seusite.com/cardiologia">
  <meta property="og:image"       content="https://seusite.com/images/og-cardiologia.jpg">
  <meta property="og:image:width"  content="1200">
  <meta property="og:image:height" content="630">
  <meta property="og:locale"      content="pt_BR">
  <meta property="og:site_name"   content="Centro Médico Fraga Maia">

  <!-- TWITTER CARDS -->
  <meta name="twitter:card"        content="summary_large_image">
  <meta name="twitter:title"       content="Centro Médico Fraga Maia - Cardiologia">
  <meta name="twitter:description" content="Cardiologia de alta precisão em Feira de Santana.">
  <meta name="twitter:image"       content="https://seusite.com/images/og-cardiologia.jpg">
  <!-- <meta name="twitter:site" content="@seutwitter"> -->

  <!-- FAVICON moderno -->
  <link rel="icon" type="image/svg+xml" href="/favicon.svg">
  <link rel="apple-touch-icon" href="/apple-touch-icon.png">

  <!-- PRECONNECT para recursos externos críticos (melhora LCP) -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

  <!-- PRELOAD do recurso mais importante above-the-fold -->
  <link rel="preload" as="image" href="/images/hero.webp">
</head>
```

---

### 4. Estrutura HTML Semântica

```html
<body>
  <!-- HEADER: nav principal — links com <a href> (nunca onClick puro) -->
  <header>
    <nav aria-label="Navegação principal">
      <a href="/">Início</a>
      <a href="/especialidades">Especialidades</a>
      <a href="/sobre">Sobre Nós</a>
      <a href="/contato">Contato</a>
    </nav>
  </header>

  <main>
    <!-- H1: ÚNICO por página, contém a keyword principal -->
    <h1>Cardiologia de Alta Precisão em Feira de Santana</h1>

    <!-- ARTIGO principal com hierarquia de headings -->
    <article>
      <h2>Por que escolher o Centro Médico Fraga Maia?</h2>
      <p>Texto rico em palavras-chave relacionadas, sem keyword stuffing...</p>

      <h2>Nossos Especialistas</h2>
      <h3>Dr. João Silva — Cardiologista Intervencionista</h3>
      <p>...</p>

      <h2>Localização e Horários</h2>

      <!-- IMAGENS: sempre com alt descritivo e loading="lazy" para imagens fora da viewport -->
      <figure>
        <img
          src="/images/cardiologista.webp"
          alt="Dr. João Silva examinando paciente com estetoscópio no Centro Médico Fraga Maia"
          width="800"
          height="600"
          loading="lazy"
          decoding="async"
        >
        <figcaption>Dr. João Silva, Cardiologista Intervencionista</figcaption>
      </figure>

      <!-- IMAGEM hero (above-the-fold): NÃO use loading="lazy" -->
      <img
        src="/images/hero.webp"
        alt="Fachada do Centro Médico Fraga Maia em Feira de Santana"
        width="1200"
        height="600"
        fetchpriority="high"
      >
    </article>
  </main>

  <!-- FOOTER: links internos relevantes e dados de contato -->
  <footer>
    <address>
      Centro Médico Fraga Maia<br>
      Rua Exemplo, 123 — Feira de Santana, BA<br>
      <a href="tel:+557512345678">(75) 1234-5678</a><br>
      <a href="mailto:contato@fragamaia.com.br">contato@fragamaia.com.br</a>
    </address>
  </footer>
</body>
```

---

### 5. Dados Estruturados — JSON-LD

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "MedicalClinic",
  "name": "Centro Médico Fraga Maia",
  "description": "Centro médico especializado em cardiologia, ortopedia e clínica geral em Feira de Santana, BA.",
  "url": "https://seusite.com",
  "telephone": "+55-75-1234-5678",
  "email": "contato@fragamaia.com.br",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "Rua Exemplo, 123",
    "addressLocality": "Feira de Santana",
    "addressRegion": "BA",
    "postalCode": "44000-000",
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
      "dayOfWeek": ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday"],
      "opens": "08:00",
      "closes": "18:00"
    }
  ],
  "medicalSpecialty": ["Cardiology", "Orthopedics"],
  "priceRange": "$$",
  "image": "https://seusite.com/images/fachada.jpg",
  "sameAs": [
    "https://www.facebook.com/centromedico",
    "https://www.instagram.com/centromedico"
  ]
}
</script>

<!-- Breadcrumb para páginas internas -->
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "BreadcrumbList",
  "itemListElement": [
    {
      "@type": "ListItem",
      "position": 1,
      "name": "Início",
      "item": "https://seusite.com"
    },
    {
      "@type": "ListItem",
      "position": 2,
      "name": "Especialidades",
      "item": "https://seusite.com/especialidades"
    },
    {
      "@type": "ListItem",
      "position": 3,
      "name": "Cardiologia",
      "item": "https://seusite.com/especialidades/cardiologia"
    }
  ]
}
</script>

<!-- FAQ para aparecer como Rich Result -->
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "O Centro Médico Fraga Maia atende planos de saúde?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Sim, atendemos os principais convênios como Unimed, Bradesco Saúde e SulAmérica."
      }
    },
    {
      "@type": "Question",
      "name": "Como agendar uma consulta?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Você pode agendar pelo telefone (75) 1234-5678, WhatsApp ou pelo nosso site."
      }
    }
  ]
}
</script>
```

---

## CHECKLIST RÁPIDO DE SEO

```
✅ robots.txt não bloqueia JS, CSS ou imagens
✅ Sitemap.xml enviado no Google Search Console
✅ <title> único, 50-60 chars, keyword no início
✅ <meta description> único, 120-160 chars, com CTA
✅ <link rel="canonical"> em todas as páginas
✅ Apenas 1 <h1> por página com keyword principal
✅ Hierarquia correta: h1 → h2 → h3
✅ Alt em todas as imagens não-decorativas
✅ Links internos com <a href> real (não onClick puro)
✅ JSON-LD de dados estruturados implementado
✅ Open Graph e Twitter Cards configurados
✅ Core Web Vitals: LCP < 2.5s, CLS < 0.1, INP < 200ms
✅ Mobile-first: viewport meta, fontes legíveis, tap targets
✅ HTTPS em produção com HSTS
✅ Sem soft 404 (páginas não encontradas retornando 200)
✅ Redirecionamentos: máximo 2 saltos por cadeia
✅ Google Search Console conectado e sem erros críticos
```

---

## QUANDO LER OS ARQUIVOS DE REFERÊNCIA

- **Configurar rastreamento?** → `references/crawling_indexing.md`
- **Meta tags, OG, Twitter Cards?** → `references/content_meta.md`
- **Schema.org, JSON-LD, Rich Results?** → `references/structured_data.md`
- **Core Web Vitals, LCP, CLS, INP?** → `references/technical_seo.md`
- **SEO em React/Next.js/Vite?** → `references/spa_seo.md`
- **Monitorar com Google Search Console?** → `references/monitoring.md`
- **Implementação passo a passo?** → `workflows/seo_checklist.md`
