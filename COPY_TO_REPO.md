# 📋 Como Copiar para o Repositório Original

## 🎯 Objetivo

Copiar este projeto para o repositório `geria-geoloc` no GitHub.

## ⚠️ ANTES DE COPIAR

**IMPORTANTE**: Atualize a URL da API primeiro!

Edite `public/index.html`, linha 222:

```javascript
const API_ENDPOINT = 'https://SUA_URL_REAL.execute-api.sa-east-1.amazonaws.com/Prod/confirm-location';
```

Para obter a URL real
1. Vá para `/Users/pedro/geria/repo-whatsappMiddleware/whatsappMiddleware`
2. Execute: `sam build && sam deploy`
3. Procure no output por: `ServerlessRestApi: https://...`
4. A URL completa será: `https://XXX.execute-api.sa-east-1.amazonaws.com/Prod/confirm-location`

## 📦 Opção 1: Copiar Arquivos Manualmente

Se você já criou o repositório `geria-geoloc`:

```bash
# Clonar o repositório vazio
cd /Users/pedro/geria
git clone https://github.com/pbrandaoquorum/geria-geoloc.git geria-geoloc-repo

# Copiar arquivos
cp -r geria-geoloc/* geria-geoloc-repo/

# Commit e push
cd geria-geoloc-repo
git add .
git commit -m "Initial commit: Location confirmation page"
git push origin main
```

## 📦 Opção 2: Usar Este Diretório Diretamente

Se ainda NÃO criou o repositório:

```bash
cd /Users/pedro/geria/geria-geoloc

# Inicializar Git
git init

# Adicionar arquivos
git add .

# Commit
git commit -m "Initial commit: Location confirmation page"

# Criar repositório no GitHub primeiro!
# Depois adicionar remote
git remote add origin https://github.com/pbrandaoquorum/geria-geoloc.git

# Push
git push -u origin main
```

## 🔍 Verificar Arquivos

Certifique-se de que estes arquivos estão presentes:

```
✅ public/index.html
✅ wrangler.toml
✅ .gitignore
✅ README.md
✅ DEPLOY.md
✅ PROJECT_SUMMARY.md
✅ COPY_TO_REPO.md (este arquivo)
```

## 🚀 Após Push

1. **Cloudflare Pages**:
   - Conecte o repositório
   - Configure build (vazio) e output (`public`)
   - Deploy automático

2. **DNS (GoDaddy)**:
   - CNAME: `location` → `geria-geoloc.pages.dev`

3. **Custom Domain (Cloudflare)**:
   - Adicione: `location.quorumsaude.com.br`

4. **Teste**:
   - Temporário: `https://geria-geoloc.pages.dev?scheduleId=test`
   - Final: `https://location.quorumsaude.com.br?scheduleId=test`

## ✅ Checklist

- [ ] URL da API atualizada em `public/index.html`
- [ ] Repositório GitHub criado (`pbrandaoquorum/geria-geoloc`)
- [ ] Arquivos copiados/push realizado
- [ ] Cloudflare Pages conectado
- [ ] DNS configurado no GoDaddy
- [ ] Custom domain ativado
- [ ] Teste com URL temporária OK
- [ ] Teste com URL final OK
- [ ] Integração com WhatsApp testada

## 🆘 Problemas?

### Se o repositório já existe com conteúdo:
```bash
git pull origin main --allow-unrelated-histories
git push origin main
```

### Se precisar recriar:
```bash
# Remover .git local
rm -rf .git

# Inicializar novamente
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/pbrandaoquorum/geria-geoloc.git
git push -u origin main -f  # Force push (cuidado!)
```

---

**Localização atual**: `/Users/pedro/geria/geria-geoloc`  
**Destino**: `https://github.com/pbrandaoquorum/geria-geoloc`  
**Domínio final**: `https://location.quorumsaude.com.br`

