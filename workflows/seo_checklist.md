# Workflow — Checklist SEO Completo para Implementação

## Fase 1 — Fundação (Dia 1)

### 1.1 robots.txt
- [ ] Arquivo existe em `/robots.txt`
- [ ] Não bloqueia JS, CSS, imagens
- [ ] Inclui `Sitemap:` com URL completa
- [ ] Bloqueia `/admin/`, `/api/`, `/login/`
- [ ] Teste: `https://search.google.com/search-console/robots-tester`

### 1.2 Sitemap XML
- [ ] `sitemap.xml` existe e está acessível
- [ ] Enviado no Google Search Console
- [ ] Inclui `<lastmod>` para URLs dinâmicas
- [ ] Não inclui páginas com `noindex`
- [ ] Não inclui páginas com canonical diferente
- [ ] Validado em: `https://www.xml-sitemaps.com/validate-xml-sitemap.html`

### 1.3 Google Search Console
- [ ] Propriedade verificada (domínio ou URL prefix)
- [ ] Sitemap enviado
- [ ] Sem erros críticos no relatório de cobertura

---

## Fase 2 — Conteúdo e Meta Tags (Dia 2)

### Para cada página:
- [ ] `<title>` único, 50-60 chars, keyword no início
- [ ] `<meta description>` único, 120-160 chars, com CTA
- [ ] `<link rel="canonical">` definido
- [ ] `<meta robots>` correto (index/noindex)
- [ ] Open Graph: og:title, og:description, og:image, og:url
- [ ] og:image tem 1200×630px mínimo
- [ ] Twitter Card: twitter:card, twitter:title, twitter:image
- [ ] `<html lang="pt-BR">` definido

### Estrutura HTML:
- [ ] Exatamente 1 `<h1>` por página
- [ ] Hierarquia h1 → h2 → h3 sem pular níveis
- [ ] `<main>`, `<nav>`, `<footer>` usados semanticamente
- [ ] Links internos com `<a href>` real
- [ ] Nenhum link dependente só de `onClick`

### Imagens:
- [ ] Alt text em todas as imagens não-decorativas
- [ ] `loading="lazy"` em imagens below-the-fold
- [ ] `fetchpriority="high"` no hero image
- [ ] `width` e `height` definidos em todas as imagens
- [ ] Formato WebP ou AVIF para melhor compressão

---

## Fase 3 — Dados Estruturados (Dia 3)

- [ ] JSON-LD de Organization ou LocalBusiness na home
- [ ] BreadcrumbList em páginas internas
- [ ] FAQPage em páginas de perguntas frequentes
- [ ] Article em posts de blog
- [ ] Produto + Review em páginas de produto (e-commerce)
- [ ] Testado no: `https://search.google.com/test/rich-results`
- [ ] Sem erros no relatório de dados estruturados do GSC

---

## Fase 4 — Performance e Core Web Vitals (Dia 4-5)

### LCP < 2.5s:
- [ ] Hero image em WebP
- [ ] `<link rel="preload">` para hero image
- [ ] CDN configurado para assets estáticos
- [ ] TTFB < 800ms (medir no PageSpeed Insights)
- [ ] `font-display: swap` para web fonts

### CLS < 0.1:
- [ ] Todas imagens com `width` e `height`
- [ ] Fontes com `font-display: swap`
- [ ] Espaço reservado para anúncios/banners
- [ ] Sem injeção de conteúdo above-the-fold

### INP < 200ms:
- [ ] JS pesado com `defer` ou `async`
- [ ] Long tasks quebradas em chunks
- [ ] React: sem re-renders desnecessários (useMemo, useCallback)

---

## Fase 5 — Auditoria Final

```bash
# Lighthouse via terminal
npx lighthouse https://seusite.com --view

# Ou via Chrome DevTools > Lighthouse > Generate report
```

**Scores mínimos recomendados:**
| Categoria | Mínimo | Ótimo |
|-----------|--------|-------|
| Performance | 70 | 90+ |
| Accessibility | 85 | 95+ |
| Best Practices | 90 | 100 |
| SEO | 90 | 100 |

---

## Passo a Passo Específico — React/Vite SPA

```
1. Instalar react-helmet-async
2. Envolver App com <HelmetProvider>
3. Criar componente SEO.tsx reutilizável
4. Aplicar <SEO> em cada rota/página
5. Adicionar robots.txt em /public/
6. Gerar sitemap.xml estático ou dinâmico em /public/
7. Verificar alt em todas as imagens
8. Verificar links com <a href> válido
9. Executar Lighthouse e corrigir alertas
10. Enviar sitemap no Google Search Console
```

## Passo a Passo Específico — Next.js App Router

```
1. Configurar metadata base em app/layout.tsx
2. Adicionar metadata específica em cada page.tsx
3. Criar app/sitemap.ts (geração automática)
4. Criar app/robots.ts (geração automática)
5. Implementar JSON-LD via <script type="application/ld+json">
6. Verificar Open Graph com og:debugger do Facebook
7. Executar Lighthouse
8. Enviar sitemap no Google Search Console
```
