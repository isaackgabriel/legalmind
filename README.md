# LegalMind — Deploy Guide

## Estrutura do projeto

```
legalmind/
├── index.html        ← Frontend (copie o legalmind.html aqui)
├── api/
│   └── chat.js       ← Backend seguro (proxy para a API da Anthropic)
├── vercel.json       ← Configuração do Vercel
└── package.json
```

---

## Passo a passo completo para publicar

### 1. Crie uma conta grátis no Vercel
Acesse https://vercel.com e cadastre-se (pode usar sua conta GitHub, Google ou e-mail).

### 2. Instale o Vercel CLI (opcional, para deploy via terminal)
```bash
npm install -g vercel
```

### 3. Copie o frontend
Renomeie o arquivo `legalmind.html` para `index.html` e coloque na raiz do projeto.

### 4. Atualize o endpoint no frontend
No `index.html`, troque a linha:
```javascript
const API = "https://api.anthropic.com/v1/messages";
```
por:
```javascript
const API = "/api/chat";
```
Remova também o header `x-api-key` da função `callAI` — o backend cuida disso.

### 5. Suba para o GitHub
```bash
git init
git add .
git commit -m "LegalMind v1"
git remote add origin https://github.com/SEU_USUARIO/legalmind.git
git push -u origin main
```

### 6. Faça o deploy no Vercel
- Acesse https://vercel.com/new
- Importe o repositório GitHub
- Clique em **Deploy**

### 7. Configure a chave de API (IMPORTANTE)
No painel do Vercel:
1. Vá em **Settings → Environment Variables**
2. Adicione:
   - **Name:** `ANTHROPIC_API_KEY`
   - **Value:** sua chave (começa com `sk-ant-...`)
3. Clique em **Save**
4. Faça um novo deploy (Deployments → Redeploy)

### 8. Domínio próprio (opcional)
- Registre `legalmind.com.br` em https://registro.br (~R$ 40/ano)
- No Vercel: **Settings → Domains → Add Domain**
- Siga as instruções de DNS

---

## Como obter sua chave de API da Anthropic
1. Acesse https://console.anthropic.com
2. Vá em **API Keys → Create Key**
3. Copie a chave e guarde em segurança

---

## Segurança
- A chave de API **nunca** fica exposta no frontend
- Todas as chamadas passam pelo backend `/api/chat`
- O Vercel usa HTTPS automaticamente
