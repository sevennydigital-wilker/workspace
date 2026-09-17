# Inventário do que está instalado (só nomes — sem conteúdo, sem credencial)

Isto é um retrato do que existe hoje no projeto de origem: nomes de skills e
nomes de MCPs/conectores. Não vem junto o conteúdo de nenhuma skill (é onde mora
o processo/negócio específico de quem montou) nem nenhuma credencial. Use como
checklist do que existe/pode existir — recrie cada peça do zero conforme sua
necessidade, seguindo `MANIFESTO-FERRAMENTAS.md` e `.agents/skills/_exemplo-skill/`.

## Skills instaladas (`.agents/skills/`)

Núcleo do organismo:
- `_homodeus` — filtros de raciocínio e protocolo de comunicação entre skills

Skills de negócio/operação (nomes — conteúdo não incluso, é específico do negócio de origem):
- `analista-trafego`, `aprendizado`, `arquiteto-lp`, `auditor-criativos`,
  `briefing-criativo-imob`, `campanha-imob`, `capcut`, `carrossel-imob`,
  `carrossel-viral`, `cfo`, `ciberseguranca`, `comparador`, `debug-sistematico`,
  `demanda`, `dev-nova-antares`, `dwc`, `engenheiro-n8n`, `estrategia`, `flux`,
  `forja`, `google-ads`, `guardiao-verba`, `head-analise`, `historiador`,
  `maestro`, `negocio`, `nonstop-drive`, `organizador-criativos`, `orion`,
  `plano-tecnico`, `protetor`, `qa-nova-altair`, `secretaria`, `sentinela`,
  `sevenny-site`, `veo3-imob`, `verificacao`, `video-vendas`, `xerife`

Skills utilitárias (genéricas, sem lógica de negócio — mais fáceis de recriar):
- `defuddle` — extrair conteúdo limpo de páginas web
- `json-canvas`, `obsidian-bases`, `obsidian-cli`, `obsidian-markdown` — trabalhar
  com arquivos do Obsidian
- `webapp-testing` — testar app web local via Playwright

## MCPs / conectores usados no projeto de origem

**Conectores claude.ai** (ativados em claude.ai → Connectors, sem instalação local):
Canva, ClickUp, Gmail, Google Calendar, Google Drive, Higgsfield, Make, Spotify,
Tactiq, Claude Docs, Meta Ads*, Notion*, Supabase*, WordPress.com*, ElevenLabs*,
n8n*, S&P Global*
> *precisam de autorização/upgrade antes de funcionar — não vêm "prontos" só
> por aparecer na lista.

**MCP local** (`.mcp.json`, executável próprio + variável de ambiente):
- `google-ads` — biblioteca Google Ads API + credencial OAuth própria

**Ferramentas de browser/automação:**
- `chrome-devtools`, `playwright` — automação e inspeção de navegador

**Configurados mas não essenciais** (dependem de infraestrutura própria de quem
montou — VPS, DNS): `hostinger-dns`, `hostinger-vps`, `clickmax`, `capcut` (MCP).

---

Para recriar qualquer peça desta lista: use `MANIFESTO-FERRAMENTAS.md` (como
conectar cada tipo) e `.agents/skills/_exemplo-skill/SKILL.md` (como estruturar
uma skill nova, com o SEU processo — não uma cópia do processo de outra pessoa).
