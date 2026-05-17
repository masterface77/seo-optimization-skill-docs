# SEO Técnico e Core Web Vitals — Referência Completa

## Core Web Vitals 2025 — Métricas e Metas

| Métrica | Boa | Precisa Melhorar | Ruim |
|---------|-----|-----------------|------|
| **LCP** (Largest Contentful Paint) | < 2.5s | 2.5s – 4s | > 4s |
| **INP** (Interaction to Next Paint) | < 200ms | 200ms – 500ms | > 500ms |
| **CLS** (Cumulative Layout Shift) | < 0.1 | 0.1 – 0.25 | > 0.25 |

> ⚠️ O INP substituiu o FID (First Input Delay) desde março de 2024.

---

## Otimizando LCP (Largest Contentful Paint)

O LCP mede o tempo para renderizar o maior elemento visível (geralmente hero image ou H1).

```html
<!-- 1. Preload da imagem hero (MAIS IMPORTANTE) -->
<link rel="preload" as="image" href="/images/hero.webp" fetchpriority="high">

<!-- 2. Imagem hero: NÃO use loading="lazy" -->
<img
  src="/images/hero.webp"
  alt="Descrição do hero"
  width="1200"
  height="600"
  fetchpriority="high"
>

<!-- 3. Preconnect para CDN de imagens -->
<link rel="preconnect" href="https://cdn.seusite.com">

<!-- 4. Preconnect para Google Fonts (antes de carregar) -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
```

```css
/* 5. font-display: swap — evita FOIT (Flash of Invisible Text) */
@font-face {
  font-family: 'Inter';
  src: url('/fonts/inter.woff2') format('woff2');
  font-display: swap;  /* Mostra fallback enquanto carrega */
}
```

**Checklist para bom LCP:**
- [ ] Hero image em formato WebP ou AVIF
- [ ] Imagem hero com `fetchpriority="high"` e sem `loading="lazy"`
- [ ] `<link rel="preload">` para o hero
- [ ] CDN para servir imagens estáticas
- [ ] Servidor com TTFB < 800ms (use cache HTTP)

---

## Otimizando CLS (Cumulative Layout Shift)

O CLS mede quanto os elementos da página "pulam" durante o carregamento.

```html
<!-- SEMPRE defina width e height em imagens -->
<img src="/imagem.webp" alt="..." width="800" height="600" loading="lazy">

<!-- Para imagens responsivas, use aspect-ratio via CSS -->
```

```css
/* Container de imagem com proporção fixa */
.image-container {
  aspect-ratio: 16 / 9;
  width: 100%;
  overflow: hidden;
}

.image-container img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

/* Reservar espaço para anúncios/banners */
.ad-banner {
  min-height: 250px;
  width: 300px;
}

/* Evitar layout shift de fontes */
.heading {
  font-size: clamp(1.5rem, 4vw, 2.5rem);  /* Tamanho fluid */
}
```

**Causas comuns de CLS:**
- Imagens sem `width`/`height`
- Anúncios sem espaço reservado
- Web fonts causando FOUT/FOIT
- Injeção dinâmica de conteúdo above-the-fold

---

## Otimizando INP (Interaction to Next Paint)

```javascript
// Evitar long tasks — dividir processamento pesado
// RUIM: bloqueia a thread principal
function processarListaGrande(lista) {
  lista.forEach(item => processarItem(item));  // Bloqueia por segundos
}

// BOM: usar scheduler para yield entre chunks
async function processarListaGrande(lista) {
  const CHUNK_SIZE = 50;
  for (let i = 0; i < lista.length; i += CHUNK_SIZE) {
    const chunk = lista.slice(i, i + CHUNK_SIZE);
    chunk.forEach(item => processarItem(item));
    // Yield para o browser processar interações
    await new Promise(resolve => setTimeout(resolve, 0));
  }
}

// Adiar scripts não críticos
// HTML:
// <script src="analytics.js" defer></script>
// <script src="chat.js" async></script>
```

---

## HTTPS e Segurança

```nginx
# nginx.conf — HSTS para forçar HTTPS por 1 ano
server {
  listen 443 ssl http2;

  # HSTS: força HTTPS por 1 ano (31536000 segundos)
  add_header Strict-Transport-Security "max-age=31536000; includeSubDomains; preload" always;

  # Redireciona HTTP → HTTPS
  # (configure em server block na porta 80)
}

server {
  listen 80;
  return 301 https://$host$request_uri;
}
```

---

## Redirecionamentos Corretos

```
# Máximo 2 saltos em cadeias de redirect
# RUIM:  /antiga → /intermediaria → /nova-url  (2 hops)
# PIOR:  /a → /b → /c → /d  (3+ hops — prejudica crawl budget)
# BOM:   /antiga → /nova-url  (direto)

# No Next.js (next.config.js):
module.exports = {
  async redirects() {
    return [
      {
        source: '/cardiologia-coracao',
        destination: '/especialidades/cardiologia',
        permanent: true,  // 301
      },
      {
        source: '/blog/:slug*',
        destination: '/artigos/:slug*',
        permanent: true,
      },
    ]
  },
}
```
