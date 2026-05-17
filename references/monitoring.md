# Monitoramento e Auditoria SEO — Google Search Console

## Configuração do Google Search Console

1. Acesse: https://search.google.com/search-console/
2. Adicione propriedade → escolha **Domain** (cobre www + não-www + HTTP/HTTPS)
3. Verifique via DNS TXT record (mais confiável)
4. Envie o sitemap: Sitemaps → Adicionar sitemap

## Relatórios Essenciais

### Desempenho (Performance)
- **Impressões**: quantas vezes apareceu no Google
- **Cliques**: quantas vezes foi clicado
- **CTR**: taxa de clique (cliques/impressões)
- **Posição média**: ranking médio no SERP

**Como usar:** Filtre por página, depois por query. Páginas com CTR baixo mesmo com boa posição precisam de title/description mais atraentes.

### Cobertura (Coverage)
- **Válido**: indexado normalmente ✅
- **Válido com aviso**: indexado mas com problemas
- **Excluído**: não indexado (pode ser intencional)
- **Erro**: problemas que impedem indexação ❌

**Erros comuns:**
| Erro | Causa | Solução |
|------|-------|---------|
| Página com redirecionamento | Sitemap aponta para URL redirecionada | Atualizar sitemap |
| Enviado e bloqueado pelo robots.txt | Sitemap inclui URL bloqueada | Remover do sitemap |
| Página não encontrada (404) | URL quebrada | Corrigir ou redirecionar |
| Soft 404 | Página retorna 200 mas não tem conteúdo | Adicionar conteúdo ou retornar 404 real |
| Crawled - currently not indexed | Google rastreou mas não indexou | Melhorar qualidade do conteúdo |

### Core Web Vitals no GSC
- **Dados de campo** (CrUX): experiência real dos usuários
- **Dados de laboratório** (Lighthouse): simulação controlada
- Priorize corrigir páginas com status "Ruim" (vermelho)

## Lighthouse — Auditoria Local

```bash
# Instalar globalmente
npm install -g lighthouse

# Auditar uma página
lighthouse https://seusite.com --view

# Apenas métricas de performance
lighthouse https://seusite.com --only-categories=performance

# Salvar relatório JSON
lighthouse https://seusite.com --output=json --output-path=./report.json
```

## Ferramentas de Auditoria

| Ferramenta | Gratuita | Melhor para |
|------------|----------|------------|
| Google Search Console | ✅ | Dados reais, erros de indexação |
| PageSpeed Insights | ✅ | Core Web Vitals campo + lab |
| Lighthouse (Chrome) | ✅ | Auditoria completa local |
| Screaming Frog (free) | ✅ (até 500 URLs) | Auditoria técnica em escala |
| Ahrefs Webmaster Tools | ✅ (limitado) | Backlinks, erros técnicos |
| Google Rich Results Test | ✅ | Validação JSON-LD |

## Checklist Mensal de Monitoramento

- [ ] Verificar relatório de Cobertura — novos erros?
- [ ] Verificar Core Web Vitals — alguma página piorou?
- [ ] Verificar relatório de Desempenho — queda de impressões?
- [ ] Verificar Dados Estruturados — erros de schema?
- [ ] Verificar Sitemaps — processado com sucesso?
- [ ] Rodar Lighthouse nas principais páginas
- [ ] Verificar Search Console Messages — avisos manuais?
