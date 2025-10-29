# 📍 Geria Geoloc - Sistema de Confirmação de Localização

Aplicação web para confirmação de localização GPS de cuidadores via WhatsApp.

## 🎯 Funcionalidades

- ✅ Captura de localização GPS do dispositivo
- ✅ Interface responsiva e moderna
- ✅ Validação de permissões
- ✅ Feedback visual de sucesso/erro
- ✅ Integração com API backend
- ✅ Redirecionamento automático para WhatsApp

## 🚀 Deploy

### Pré-requisitos

- Conta no GitHub
- Conta no Cloudflare
- Domínio configurado no GoDaddy

### Passo 1: Configurar Repositório GitHub

```bash
cd geria-geoloc
git init
git add .
git commit -m "Initial commit: Location confirmation page"
git remote add origin https://github.com/pbrandaoquorum/geria-geoloc.git
git push -u origin main
```

### Passo 2: Deploy no Cloudflare Pages

1. Acesse: https://dash.cloudflare.com
2. Vá em **Workers & Pages**
3. Clique em **Create application** → **Pages**
4. Conecte seu repositório GitHub: `pbrandaoquorum/geria-geoloc`
5. Configurações:
   - **Project name**: `geria-geoloc`
   - **Production branch**: `main`
   - **Build command**: (deixe vazio)
   - **Build output directory**: `public`
6. Clique em **Save and Deploy**

### Passo 3: Configurar DNS no GoDaddy

1. Acesse GoDaddy → Meus Domínios
2. Selecione `quorumsaude.com.br`
3. Vá em **Gerenciar DNS**
4. Adicione um registro **CNAME**:
   - **Tipo**: CNAME
   - **Nome**: `location`
   - **Valor**: `geria-geoloc.pages.dev` (ou o valor fornecido pelo Cloudflare)
   - **TTL**: 600 segundos
5. Salve as alterações

### Passo 4: Configurar Custom Domain no Cloudflare

1. No projeto Cloudflare Pages, vá em **Custom domains**
2. Clique em **Set up a custom domain**
3. Digite: `location.quorumsaude.com.br`
4. Cloudflare verificará o DNS automaticamente
5. Aguarde propagação (5-10 minutos)

### Passo 5: Atualizar URL da API

Após fazer deploy do backend, edite `public/index.html`:

**Procure por:**
```javascript
const API_ENDPOINT = 'https://abc123xyz.execute-api.sa-east-1.amazonaws.com/Prod/confirm-location';
```

**Substitua pela URL real** da sua API Gateway.

## 🧪 Teste Local

Para testar localmente:

```bash
# Instalar servidor HTTP simples
python3 -m http.server 8000 --directory public

# Ou usar npx
npx serve public
```

Acesse: `http://localhost:8000?scheduleId=test-123`

## 📋 Estrutura do Projeto

```
geria-geoloc/
├── public/
│   └── index.html          # Página principal (HTML + CSS + JS)
├── wrangler.toml           # Configuração Cloudflare
├── .gitignore              # Arquivos ignorados pelo Git
└── README.md               # Este arquivo
```

## 🔧 Configuração da API

A página espera receber um `scheduleId` via query parameter:

```
https://location.quorumsaude.com.br?scheduleId=ABC123
```

E faz uma requisição POST para:

```
POST /confirm-location
Content-Type: application/json

{
  "scheduleId": "ABC123",
  "latitude": -23.550520,
  "longitude": -46.633308,
  "accuracy": 10.5,
  "timestamp": "2024-10-29T12:34:56.789Z"
}
```

## 🔐 Segurança

- ✅ HTTPS obrigatório (fornecido pelo Cloudflare)
- ✅ CORS configurado no backend
- ✅ Validação de parâmetros no frontend
- ✅ Timeout de 10 segundos para geolocalização
- ✅ Tratamento de erros de permissão

## 🆘 Troubleshooting

### Erro: "Link inválido"
- Verifique se a URL contém o parâmetro `scheduleId`
- Exemplo correto: `?scheduleId=123`

### Erro: "Geolocalização não suportada"
- Use um navegador moderno (Chrome, Safari, Firefox)
- Verifique se está acessando via HTTPS

### Erro: "Permissão negada"
- Permita acesso à localização nas configurações do navegador
- No iOS: Ajustes → Safari → Localização
- No Android: Configurações → Apps → Chrome → Permissões

### Erro de conexão com API
- Verifique se a URL da API está correta no `index.html`
- Teste o endpoint diretamente com curl
- Verifique logs no CloudWatch

## 📊 Monitoramento

### Logs do Navegador
Abra o Console (F12) para ver logs detalhados:
- Carregamento da página
- Obtenção de localização
- Requisições à API
- Erros e exceções

### CloudWatch (Backend)
Verifique os logs da Lambda `ConfirmLocationFunction`:
- Requisições recebidas
- Atualizações no DynamoDB
- Erros de processamento

## 🔄 Atualizações

Para atualizar a página:

```bash
# Fazer alterações em public/index.html
git add .
git commit -m "Descrição das alterações"
git push origin main
```

O Cloudflare Pages fará deploy automático.

## 📞 Suporte

Em caso de problemas:
1. Verifique os logs do navegador (Console)
2. Teste o endpoint da API com curl
3. Verifique configuração DNS
4. Consulte documentação do backend

## 📄 Licença

Uso interno - Quorum Saúde

---

**Desenvolvido por**: Quorum Saúde  
**Versão**: 1.0.0  
**Data**: Outubro 2024

