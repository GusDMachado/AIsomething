# Resume AI

Step by step

🚀 Passo a passo para rodar o projeto em 1 dia

🧰 1. Instale as ferramentas básicas (se ainda não fez) no seu computador:

npm install -g pnpm

npm install -g vercel


No diretório do projeto (novo ou clonado do GitHub):

pnpm install

🧠 2. Crie a estrutura de pastas

Se ainda não criou, use isso como base:

/app

  /api
  
    - gerarRelatorio.ts
    
    - gerarRespostas.ts
    
    - listarHistorico.ts
    
    - salvarResposta.ts
    
  /dashboard
  
    - page.tsx
    
  /login
  
    - page.tsx
    
/components

  - HistoricoDeRespostas.tsx
    
  - Formulario.tsx
    
  - Relatorio.tsx
    
  - Resultado.tsx
    
/lib

  - openai.ts
    
  - auth.ts
    
/middleware.ts

🔐 3. Configure Clerk para autenticação

Acesse Clerk.com → crie projeto.

Copie as chaves da API.

Crie o arquivo .env.local:

CLERK_PUBLISHABLE_KEY=pk_...

CLERK_SECRET_KEY=sk_...

NEXT_PUBLIC_CLERK_FRONTEND_API=...

No middleware.ts:

import { authMiddleware } from "@clerk/nextjs"

export default authMiddleware({
  publicRoutes: ["/login"]
})

export const config = {
  matcher: ["/((?!_next|.*\\..*).*)"],
}

🧪 4. Teste o login

Crie uma tela de login simples (/login/page.tsx), ou use o componente pronto do Clerk:

import { SignIn } from "@clerk/nextjs"

export default function LoginPage() {
  return (
    <div className="flex justify-center items-center h-screen">
      <SignIn />
    </div>
  )
}

🧩 5. Construa a dashboard real (componentes que já temos)

Em /dashboard/page.tsx:

import HistoricoDeRespostas from '@/components/HistoricoDeRespostas'

import Formulario from '@/components/Formulario'

import Relatorio from '@/components/Relatorio'

import Resultado from '@/components/Resultado'

export default function DashboardPage() {
  return (
    <div className="p-6 space-y-8 max-w-4xl mx-auto">
      <h1 className="text-2xl font-bold">Copiloto de IA para Processos Seletivos</h1>
      <Formulario />
      <Relatorio />
      <Resultado />
      <HistoricoDeRespostas />
    </div>
  )
}

📡 6. Configure a OpenAI API

Crie uma conta em OpenAI.

Crie uma API Key.

Coloque no .env.local:

OPENAI_API_KEY=sk-...

Em /lib/openai.ts:

import OpenAI from 'openai'

export const openai = new OpenAI({
  apiKey: process.env.OPENAI_API_KEY
})

💬 7. Teste os fluxos

✅ Upload do edital (simulado com textarea por enquanto).

✅ Geração de relatório.

✅ Geração de resposta a partir do currículo e relatório.

✅ Refinamento.

✅ Histórico aparecendo na dashboard.

☁️ 8. Suba no GitHub e deploy na Vercel (opcional)

Crie um repositório no GitHub.

Faça push:

git init

git add .

git commit -m "first commit"

git remote add origin https://github.com/seuuser/seurepo.git

git push -u origin main

Vá para vercel.com, conecte ao GitHub e faça deploy do repositório.

✅ Checklist Final de um Frontend “real”

Item	Status

Autenticação	✅

Upload/Edital	✅ (simulado)

Relatório IA	✅

Respostas IA	✅

Refinamento	✅

Histórico	✅

Integração dos componentes	🟡

Estilização / UX	🟡

Deploy	🔲
