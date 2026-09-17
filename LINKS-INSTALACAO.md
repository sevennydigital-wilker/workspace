# Links de Instalação

Links diretos pra cada peça da base. Onde a integração é um "conector" do
claude.ai (não um pacote local), não existe link de "instalar" — é autorizar
pela interface, então o link é o de configuração, não de download.

## Base (instalar sempre)

| Ferramenta | Link | Observação |
|---|---|---|
| Node.js (LTS) | https://nodejs.org | pré-requisito do Claude Code |
| Claude Code (CLI) | https://docs.claude.com/en/docs/claude-code | docs oficiais; instalar com `npm install -g @anthropic-ai/claude-code` |
| Claude Code (repo/issues) | https://github.com/anthropics/claude-code | reportar bug, ver changelog |
| Git | https://git-scm.com | necessário pro hook de proteção de credencial |
| Obsidian | https://obsidian.md | segundo cérebro |

## MCP servers com repositório próprio (instalação local)

| MCP | Repositório | Observação |
|---|---|---|
| Playwright MCP | https://github.com/microsoft/playwright-mcp | automação de navegador |
| Chrome DevTools MCP | https://github.com/ChromeDevTools/chrome-devtools-mcp | inspeção de página, performance, rede |

Ambos se registram com `claude mcp add` — ver instruções de cada repositório
(o comando exato muda conforme a versão).

## Conectores claude.ai (autorizar pela interface, sem instalar nada local)

Ativar em: **https://claude.ai/settings/connectors** (ou dentro do Claude Code,
comando `/mcp`, numa sessão interativa).

| Serviço | Site oficial (pra criar conta, se ainda não tiver) |
|---|---|
| ClickUp | https://clickup.com |
| Google Drive / Gmail / Calendar | https://myaccount.google.com |
| Canva | https://www.canva.com |
| Make | https://www.make.com |
| Notion | https://www.notion.so |
| Supabase | https://supabase.com |
| WordPress.com | https://wordpress.com |
| ElevenLabs | https://elevenlabs.io |
| n8n | https://n8n.io (self-host) ou https://n8n.cloud |
| Tactiq | https://tactiq.io |
| Spotify | https://www.spotify.com |
| Higgsfield | https://higgsfield.ai |

## Serviços com API própria (MCP local, precisa de credencial em `.env`)

| Serviço | Onde gerar a credencial |
|---|---|
| Google Ads API | https://ads.google.com/aw/apicenter (developer token) + https://console.cloud.google.com (OAuth) |
| Meta (Graph API / Meta Ads) | https://developers.facebook.com/apps |
| Z-API (WhatsApp) | https://www.z-api.io |

---

**Lembrete:** nenhum desses links substitui o cuidado com credencial — depois de
criar a conta/token em qualquer um desses serviços, o valor vai só pro `.env`
local (nunca pro `.mcp.json`, `settings.json` ou qualquer arquivo versionado).
Veja `.env.example` e o hook `.claude/hooks/pre-commit`.
