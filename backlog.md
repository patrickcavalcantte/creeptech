# Backlog — Creep.tech

## Features

### Tradução automática para inglês
Publicar automaticamente uma versão em inglês a cada novo post ou projeto.

**Arquitetura planejada:**
- Hugo multilíngue (`pt-br` + `en`) configurado no `hugo.toml`
- GitHub Actions detecta arquivos `.md` novos/alterados no push
- Chama API de tradução e salva `meu-post.en.md` automaticamente
- Hugo builda as duas versões (`/posts/...` e `/en/posts/...`)

**Pendente:** escolher API de tradução (DeepL recomendado — free tier 500k chars/mês)

---

### Google Search Console — verificar propriedade
Cadastro iniciado em https://search.google.com/search-console com a URL `https://creeptech.com.br`.

**Pendente:** aguardar propagação do DNS e então:
1. Voltar no Search Console e clicar em **Verificar** (método: Tag HTML)
2. Após verificar, ir em **Sitemaps** e cadastrar `sitemap.xml`

---

### JARVIS — intent "publicar post"
Você escreve o post manualmente, fala pro JARVIS publicar e ele faz o git por você.

**Fluxo:**
1. Você termina de escrever o `.md` em `content/posts/`
2. Fala: *"JARVIS, publica o blog"* (ou aperta um botão na interface)
3. JARVIS roda via Node.js `child_process`: `git add`, `git commit -m "novo post"`, `git push`
4. GitHub Actions faz o deploy automaticamente

**Implementação:** nova intent no JARVIS BOLCHEVIQUE (`/publish` ou intent `publicar_blog`) usando `child_process.exec` apontando pro diretório do Creep.tech

---

### JARVIS — módulo Creep.tech Manager
Expandir o JARVIS para gerenciar todo o ecossistema Creep.tech: site + Instagram.

**Intents planejadas:**
- `publicar_blog` — commit/push do post escrito manualmente (ver item acima)
- `publicar_instagram` — envia arte pronta para o Instagram do @creep__tech automaticamente
- `status_creeptech` — mostra últimos posts publicados no site e no Instagram

**Instagram — como funciona:**
- Usar a **Instagram Graph API** (oficial da Meta)
- Requer: conta Instagram Professional (gratuito) + Facebook Business + app aprovado na Meta
- JARVIS envia a imagem + legenda via API e agenda ou publica na hora

**Fluxo do Instagram:**
1. Você cria a arte (Figma, Canva, etc.) e salva localmente
2. Fala: *"JARVIS, publica essa arte no Instagram com a legenda X"*
3. JARVIS faz upload via Graph API e publica

**Pendente:**
- [ ] Criar app no Meta for Developers (gratuito) em https://developers.facebook.com
- [ ] Conectar o Instagram @creep__tech ao app e gerar token de acesso
- [ ] Implementar a intent no JARVIS

**Obs:** conta @creep__tech já é Professional ✅
