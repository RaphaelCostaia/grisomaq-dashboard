# Painel de Demandas — GRISOMAQ

Página web que mostra as demandas de RH atendidas pelo assistente no WhatsApp.
Lê os dados de um endpoint do n8n. Sem a URL configurada, exibe dados de exemplo.

```
.
├─ index.html    # o painel
├─ Dockerfile    # empacota como site estático (nginx)
└─ nginx.conf
```

## Deploy no EasyPanel
1. Subir este repositório no GitHub.
2. EasyPanel → **Create Service → App** → Source **GitHub** → este repositório.
3. Deploy (detecta o `Dockerfile`) → adicionar domínio na **porta 80**.
4. No login do painel, em "Configurar servidor", colar a URL do endpoint de leitura
   (`https://SEU-N8N/webhook/grisomaq-dashboard`) e entrar com a senha.

## Painel operacional — o que o n8n precisa ter
O painel usa **3 endpoints** no mesmo n8n (o painel deriva os outros dois a partir da URL de leitura):

| Endpoint | Workflow | Função |
|---|---|---|
| `/webhook/grisomaq-dashboard` | `dashboard-api.json` | métricas, filtros (`?dias=&setor=`), KPIs, admissões |
| `/webhook/grisomaq-atendimento` | `dashboard-atendimento.json` | detalhe + histórico da conversa |
| `/webhook/grisomaq-acao` | `dashboard-acao.json` | ações: status / responsável / resolver (grava Postgres + planilha) |

Nos **três** workflows, use a **mesma senha** no nó **"Chave de acesso (EDITAR)"** — é a senha do login.
Rode também `sql/dashboard-ops.sql` no banco. Todos já retornam o cabeçalho CORS.

## Recursos do painel
Login · filtros por período/setor · KPIs com comparativo · gráficos · **carga por responsável** ·
**bloco de admissões** · fila com **busca** e **exportar CSV** · **detalhe lateral com a conversa** ·
**ações** (mudar status, atribuir responsável, resolver) · alternar tema claro/escuro · auto-atualização (60s) ·
modo demonstração (para apresentar sem senha).
