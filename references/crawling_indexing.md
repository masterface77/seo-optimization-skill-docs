# Rastreabilidade e Indexação — Referência Completa

## robots.txt — Regras Avançadas

```
# Bloqueia rastreadores maliciosos (não afeta SEO)
User-agent: AhrefsBot
Disallow: /

User-agent: SemrushBot
Disallow: /

# Configuração segura para Googlebot
User-agent: Googlebot
Allow: /
# Permite scripts e estilos (NUNCA bloqueie isso!)
Allow: /*.js$
Allow: /*.css$
Allow: /*.png$
Allow: /*.jpg$
Allow: /*.webp$

# Bloqueia seções sem valor de SEO
User-agent: *
Disallow: /admin/
Disallow: /login/
Disallow: /api/
Disallow: /cart/
Disallow: /*?sort=
Disallow: /*?filter=
Disallow: /search?q=

Sitemap: https://seusite.com/sitemap.xml
```

## Como o Googlebot Rastreia — Sequência

1. **Descobre URLs** via sitemap, links internos, backlinks
2. **Verifica robots.txt** — obedece as regras de Allow/Disallow
3. **Faz requisição HTTP** da página
4. **Renderiza JavaScript** (Googlebot executa JS com delay)
5. **Extrai links** e adiciona à fila de rastreamento
6. **Avalia conteúdo** e passa para indexação

> ⚠️ O Googlebot renderiza JS, mas com atraso de horas a dias. Use SSR/SSG para conteúdo crítico.

## Status HTTP Corretos para SEO

| Status | Significado | Impacto SEO |
|--------|-------------|-------------|
| `200 OK` | Página existe e está ok | ✅ Indexa normalmente |
| `301 Moved Permanently` | Redirecionamento definitivo | ✅ Passa link equity |
| `302 Found` | Redirecionamento temporário | ⚠️ Não transfere equity |
| `304 Not Modified` | Conteúdo não mudou (cache) | ✅ Economiza crawl budget |
| `404 Not Found` | Página não existe | Desindexada após tempo |
| `410 Gone` | Removida permanentemente | ✅ Desindexação mais rápida |
| `503 Service Unavailable` | Fora do ar temporariamente | ⚠️ Retry automático |

> 🚨 **Soft 404**: retornar status 200 para página "não encontrada" — NUNCA faça isso. Confunde o Google e desperdiça crawl budget.

## Crawl Budget

O crawl budget é a quantidade de URLs que o Googlebot rastreia no seu site em um período. Para otimizá-lo:

- Remova URLs duplicadas com canonical ou noindex
- Corrija erros 404 e 500
- Evite parâmetros de URL desnecessários
- Use `<link rel="canonical">` consistentemente
- Não deixe páginas com conteúdo thin (< 300 palavras) indexáveis
