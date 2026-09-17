# Manifesto de Ferramentas — Catálogo de Integrações

Lista das categorias de integração comuns num organismo Claude Code, e como
instalar cada tipo. Nenhum ID de conta, token ou nome de cliente vai aqui — isso
é catálogo de **capacidade**, não de configuração real.

Existem três formas de conectar uma ferramenta ao Claude Code. Saber qual é qual
evita confusão na hora de instalar:

## 1. Conectores claude.ai (gerenciados pela Anthropic)

Ativados em **claude.ai → configurações → conectores** (ou `/mcp` numa sessão
interativa do Claude Code). Não precisam de token manual — o fluxo OAuth roda
pelo navegador. Exemplos comuns: Gmail, Google Calendar, Google Drive, ClickUp,
Canva, Slack, Notion, Supabase, Make.

**Instalação:** abrir claude.ai → Connectors → escolher o serviço → autorizar.
Depois disso, as ferramentas `mcp__claude_ai_<Serviço>__*` ficam disponíveis em
qualquer sessão da mesma conta.

## 2. Servidores MCP locais (rodam na sua máquina)

Configurados em `.mcp.json` na raiz do projeto, ou via `claude mcp add` no
terminal. Precisam de um executável ou pacote instalado localmente, e a
credencial fica em variável de ambiente — **nunca dentro do `.mcp.json` versionado**.

Exemplo de formato (sem valores reais):

```json
{
  "mcpServers": {
    "nome-do-servidor": {
      "command": "caminho/pro/executavel",
      "env": {
        "ALGUMA_CHAVE": "${ALGUMA_CHAVE}"
      }
    }
  }
}
```

Referencie a variável de ambiente (`${VAR}`) em vez do valor literal, e defina o
valor real só no seu `.env` local ou nas variáveis de ambiente do sistema.

Exemplos comuns desse tipo: Google Ads API (via biblioteca própria + MCP wrapper),
Playwright (browser automation), servidores MCP de VPS/hosting.

## 3. CLIs e scripts próprios

Ferramentas que não são MCP — rodam via `Bash`/`PowerShell` chamando um script ou
CLI instalado (ex: `ffmpeg`, bibliotecas Python, scripts Node de automação).
Documentar cada uma numa skill (`.agents/skills/<nome>/SKILL.md`) explicando como
invocar e quais variáveis de ambiente ela espera.

---

## Checklist ao adicionar uma integração nova

1. A credencial vai para `.env` (nunca para `.mcp.json`, `settings.json` ou
   dentro de uma skill).
2. Adicione o nome da variável em `.env.example` (sem valor).
3. Se for MCP local, use `${VAR}` no `.mcp.json`.
4. Rode o hook de `pre-commit` (`git commit` de teste) antes de confiar que está
   seguro.
5. Documente numa skill o que a integração faz e como usá-la — não documente a
   credencial em lugar nenhum além do `.env`.
