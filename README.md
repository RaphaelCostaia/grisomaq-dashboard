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
Veja o passo a passo completo no chat / documentação. Resumo:
1. Subir este repositório no GitHub.
2. EasyPanel → **Create Service → App** → Source **GitHub** → este repositório.
3. Deploy (detecta o `Dockerfile`) → adicionar domínio na **porta 80**.
4. No painel, colar a URL do endpoint do n8n (`https://SEU-N8N/webhook/grisomaq-dashboard`).

> No n8n, o workflow `dashboard-api` precisa estar importado e **ativo** (ele libera o CORS).
