# 🚀 Guia Rápido de Deploy

## ✅ Pré-requisitos

- [x] Projeto criado em `/Users/pedro/geria/geria-geoloc`
- [ ] Backend deployado (URL da API)
- [ ] Repositório GitHub criado
- [ ] Conta Cloudflare ativa

## 📋 Passo a Passo

### 1. Atualizar URL da API

**IMPORTANTE**: Antes de fazer deploy, atualize a URL da API!

Edite `public/index.html`, linha 222:

```javascript
const API_ENDPOINT = 'https://SUA_URL_REAL.execute-api.sa-east-1.amazonaws.com/Prod/confirm-location';
```

### 2. Criar Repositório no GitHub

```bash
cd /Users/pedro/geria/geria-geoloc

# Inicializar Git
git init

# Adicionar arquivos
git add .

# Commit inicial
git commit -m "Initial commit: Location confirmation page"

# Adicionar remote (substitua se necessário)
git remote add origin https://github.com/pbrandaoquorum/geria-geoloc.git

# Push
git push -u origin main
```

### 3. Deploy no Cloudflare Pages

1. Acesse: https://dash.cloudflare.com
2. **Workers & Pages** → **Create application** → **Pages**
3. **Connect to Git** → Selecione `pbrandaoquorum/geria-geoloc`
4. Configurações:
   ```
   Project name: geria-geoloc
   Production branch: main
   Build command: (vazio)
   Build output directory: public
   ```
5. **Save and Deploy**
6. Aguarde ~1 minuto

### 4. Configurar DNS (GoDaddy)

1. GoDaddy → Meus Domínios → `quorumsaude.com.br`
2. **Gerenciar DNS**
3. **Adicionar** → **CNAME**:
   ```
   Tipo: CNAME
   Nome: location
   Valor: geria-geoloc.pages.dev
   TTL: 600
   ```
4. **Salvar**

### 5. Custom Domain (Cloudflare)

1. Projeto Cloudflare → **Custom domains**
2. **Set up a custom domain**
3. Digite: `location.quorumsaude.com.br`
4. **Activate domain**
5. Aguarde verificação (~5-10 min)

### 6. Testar

**URL temporária** (disponível imediatamente):
```
https://geria-geoloc.pages.dev?scheduleId=test-123
```

**URL final** (após DNS propagar):
```
https://location.quorumsaude.com.br?scheduleId=test-123
```

## ✅ Checklist Final

- [ ] URL da API atualizada no `index.html`
- [ ] Push para GitHub concluído
- [ ] Deploy no Cloudflare bem-sucedido
- [ ] DNS configurado no GoDaddy
- [ ] Custom domain ativado no Cloudflare
- [ ] Teste com URL temporária OK
- [ ] Teste com URL final OK
- [ ] Teste end-to-end com WhatsApp OK

## 🧪 Comandos de Teste

### Testar localmente:
```bash
cd /Users/pedro/geria/geria-geoloc
python3 -m http.server 8000 --directory public
# Abrir: http://localhost:8000?scheduleId=test-123
```

### Testar API diretamente:
```bash
curl -X POST https://SUA_URL_REAL.execute-api.sa-east-1.amazonaws.com/Prod/confirm-location \
  -H "Content-Type: application/json" \
  -d '{
    "scheduleId": "test-123",
    "latitude": -23.550520,
    "longitude": -46.633308,
    "accuracy": 10,
    "timestamp": "2024-10-29T12:00:00.000Z"
  }'
```

### Verificar DNS:
```bash
nslookup location.quorumsaude.com.br
```

## 🔄 Atualizações Futuras

Para atualizar a página:

```bash
cd /Users/pedro/geria/geria-geoloc

# Editar arquivos...

git add .
git commit -m "Descrição da mudança"
git push origin main
```

Deploy automático em ~1 minuto! 🎉

## 🆘 Problemas Comuns

### "Link inválido"
- Adicione `?scheduleId=XXX` na URL

### "Geolocalização não suportada"
- Use HTTPS (obrigatório para geolocalização)
- Use navegador moderno

### "Erro ao confirmar"
- Verifique URL da API no código
- Verifique CORS no backend
- Veja logs no CloudWatch

### DNS não resolve
- Aguarde até 24h para propagação
- Use URL temporária enquanto isso

---

**Tempo estimado total**: 15-20 minutos  
**Dificuldade**: Fácil  
**Resultado**: Sistema funcionando! 🚀

