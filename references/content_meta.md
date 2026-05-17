# Conteúdo e Tags Meta — Referência Completa

## Title Tags — Boas Práticas

```
Formato: [Keyword Principal] | [Marca] — [Diferencial/Localização]

✅ BOM:  "Cardiologista em Feira de Santana | Dr. João Silva"
✅ BOM:  "Comprar iPhone 15 Pro Max | TechStore — Entrega Rápida"
❌ RUIM: "Início" (genérico, sem keyword)
❌ RUIM: "Centro Médico - Cardiologia - Ortopedia - Clínica Geral - Neurologia" (keyword stuffing)
❌ RUIM: "Bem-vindo ao nosso site!" (zero valor SEO)
```

**Regras:**
- 50-60 caracteres (Google trunca em ~60)
- Keyword mais importante no início
- Único para cada página — nunca o mesmo em 2 páginas
- Nome da marca no final (economy de caracteres)

## Meta Descriptions

```
Formato: [Benefício principal]. [CTA] + [Keyword localizada].

✅ BOM:  "Cardiologistas certificados em Feira de Santana. 
          Agende sua consulta online e cuide do seu coração."
✅ BOM:  "iPhone 15 Pro Max com até 12x sem juros e entrega em 24h. 
          Compre agora na TechStore e receba amanhã."
❌ RUIM: Copiar o início do texto da página
❌ RUIM: > 160 caracteres (truncado no SERP)
❌ RUIM: Repetir a mesma description em várias páginas
```

## Canonical URLs — Casos Comuns

```html
<!-- Página principal -->
<link rel="canonical" href="https://seusite.com/cardiologia">

<!-- Com parâmetros de UTM (canonical aponta para URL limpa) -->
<!-- URL visitada: /cardiologia?utm_source=google&utm_medium=cpc -->
<link rel="canonical" href="https://seusite.com/cardiologia">

<!-- Paginação: cada página tem seu canonical -->
<!-- /blog?page=2 -->
<link rel="canonical" href="https://seusite.com/blog?page=2">

<!-- Versão mobile (se separado de desktop) -->
<!-- m.seusite.com/cardiologia -->
<link rel="canonical" href="https://seusite.com/cardiologia">
<link rel="alternate" media="only screen and (max-width: 640px)"
      href="https://m.seusite.com/cardiologia">
```

## Open Graph — Imagens

| Tipo | Tamanho recomendado | Mínimo |
|------|--------------------|----|
| og:image padrão | 1200×630px | 600×315px |
| og:image quadrado | 1080×1080px | 400×400px |
| Twitter large card | 1200×628px | 600×314px |

**Dicas para imagem OG:**
- Formato JPG ou PNG (WebP tem suporte limitado em alguns crawlers)
- Tamanho máximo: 5MB
- Texto na imagem: máximo 20% da área
- Inclua o logo ou nome da marca

## Hreflang para Sites Multilíngues

```html
<!-- Para site em PT-BR e EN -->
<link rel="alternate" hreflang="pt-BR" href="https://seusite.com/pt/cardiologia">
<link rel="alternate" hreflang="en"    href="https://seusite.com/en/cardiology">
<link rel="alternate" hreflang="x-default" href="https://seusite.com/cardiologia">
```
