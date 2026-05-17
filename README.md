# 🔍 SEO Optimization — Skill Completa para Google Search

Uma **skill para IA (Claude CLI / Antigravity / Windsurf)** especializada em otimização de SEO baseada nos fundamentos oficiais do Google Search, Core Web Vitals, dados estruturados e boas práticas para sites modernos — incluindo SPAs, React, Next.js e Vite.

## 📦 Como instalar esta Skill no Claude CLI

### Método 1 — Instalar como plugin (recomendado)

```bash
claude plugin install https://github.com/masterface77/seo-optimization-skill-docs
```

### Método 2 — Adicionar como marketplace

```bash
claude marketplace add https://github.com/masterface77/seo-optimization-skill-docs
```

### Método 3 — Via URL raw (Windsurf / Antigravity)

Adicione nas configurações de Rules do seu assistente:

```
https://raw.githubusercontent.com/masterface77/seo-optimization-skill-docs/main/SKILL.md
```

### Método 4 — Clone local

```bash
git clone https://github.com/masterface77/seo-optimization-skill-docs.git
```

---

## 📚 Conteúdo da Skill

| Tópico | Arquivo | Descrição |
|--------|---------|-----------|
| **Skill Principal** | `SKILL.md` | Núcleo com robots.txt, sitemap, meta tags, JSON-LD e checklist |
| **Rastreabilidade** | `references/crawling_indexing.md` | Googlebot, robots.txt, sitemap, indexação |
| **Conteúdo e Meta** | `references/content_meta.md` | Title, description, Open Graph, Twitter Cards |
| **Dados Estruturados** | `references/structured_data.md` | Schema.org, JSON-LD, Rich Results, FAQ |
| **SEO Técnico** | `references/technical_seo.md` | Core Web Vitals, LCP, CLS, INP, HTTPS |
| **SEO para SPAs** | `references/spa_seo.md` | React, Next.js, Vite, react-helmet, SSR/SSG |
| **Monitoramento** | `references/monitoring.md` | Google Search Console, Lighthouse, erros |
| **Workflow** | `workflows/seo_checklist.md` | Passo a passo de implementação completa |

---

## 🎯 Quando a Skill é ativada

O assistente usa esta skill automaticamente quando você menciona:

- `SEO`, `otimização de busca`, `search engine optimization`
- `Google Search`, `Googlebot`, `indexação`
- `robots.txt`, `sitemap.xml`
- `meta tags`, `title`, `meta description`
- `Core Web Vitals`, `LCP`, `CLS`, `INP`
- `dados estruturados`, `Schema.org`, `JSON-LD`, `Rich Results`
- `Open Graph`, `Twitter Cards`
- `Google Search Console`, `GSC`
- `canonical URL`, `conteúdo duplicado`
- `SEO para React`, `Next.js SEO`, `Vite SEO`

---

## 🔧 Compatibilidade

```yaml
frameworks: [react, next.js, vite, nuxt, astro, html-puro, rails]
tools: [google-search-console, lighthouse, pagespeed-insights, screaming-frog]
```

---

## 📋 Tópicos Cobertos

### 🕷️ Rastreabilidade e Indexação
- Configuração segura do `robots.txt`
- Sitemap XML com suporte a imagens e vídeos
- Sitemap Index para sites grandes
- Crawl Budget e otimização de rastreamento
- Status HTTP corretos (301, 302, 304, 404, 410)

### 📝 Conteúdo e Tags Meta
- Tags `<title>` únicas e descritivas (50-60 chars)
- Meta descriptions com CTA (120-160 chars)
- Canonical URLs para evitar conteúdo duplicado
- Open Graph para Facebook, LinkedIn, WhatsApp
- Twitter Cards (summary_large_image)
- Hreflang para sites multilíngues

### 🏗️ Estrutura HTML Semântica
- Hierarquia correta de headings (H1 → H2 → H3)
- Tags semânticas: `<main>`, `<article>`, `<section>`, `<nav>`, `<footer>`
- Links internos com `<a href>` (compatível com Googlebot)
- Alt text em imagens: descritivo e com contexto
- Imagens: `loading="lazy"`, `fetchpriority`, `width`/`height`

### 📊 Dados Estruturados (Schema.org)
- JSON-LD para Organization, LocalBusiness, MedicalClinic
- BreadcrumbList para navegação
- FAQPage para Rich Results
- Article para posts de blog
- Product, Review, Event, HowTo

### ⚡ Core Web Vitals
- **LCP** (Largest Contentful Paint) < 2.5s: preload, WebP, CDN
- **CLS** (Cumulative Layout Shift) < 0.1: width/height em imagens
- **INP** (Interaction to Next Paint) < 200ms: otimização de JS
- Preconnect e preload de recursos críticos
- Font display swap para web fonts

### ⚛️ SEO para SPAs e React
- `react-helmet-async` para meta tags dinâmicas
- Next.js: `<Head>`, `metadata` API (App Router)
- SSR e SSG: quando usar cada abordagem
- Pré-renderização para Googlebot
- `robots.txt` e sitemap em `public/`

### 📈 Monitoramento e Auditoria
- Google Search Console: configuração e leitura de relatórios
- Lighthouse: análise de performance e SEO
- PageSpeed Insights: métricas de campo (CrUX)
- Screaming Frog: auditoria técnica completa
- Correção de erros de cobertura e indexação

---

## 🚀 Quick Start — Checklist de Implementação

```
1. [ ] robots.txt configurado (não bloqueia JS/CSS)
2. [ ] Sitemap.xml criado e enviado ao GSC
3. [ ] <title> único e otimizado em cada página
4. [ ] <meta description> único em cada página
5. [ ] <link rel="canonical"> em todas as páginas
6. [ ] 1 único <h1> por página
7. [ ] Alt text em todas as imagens
8. [ ] JSON-LD de dados estruturados
9. [ ] Open Graph e Twitter Cards
10.[ ] Core Web Vitals verificados no Lighthouse
11.[ ] Google Search Console conectado
12.[ ] HTTPS com HSTS configurado
```

---

## 👤 Autor

**Levi Reis** — Criado como material de referência para desenvolvimento web com SEO profissional e boas práticas do Google Search.

---

## 📄 Licença

MIT License — Livre para uso, modificação e distribuição.
