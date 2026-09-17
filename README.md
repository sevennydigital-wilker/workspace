# Homodeus Starter Kit

Kit de instalação para montar um organismo Claude Code no mesmo padrão do Homodeus:
CLAUDE.md com protocolos, skills organizadas em `.agents/skills/`, segundo cérebro
em Obsidian e proteção contra vazamento de credencial.

Este repositório **não contém** nenhum dado de cliente, token, senha ou conteúdo
de negócio de quem montou o kit. É só o esqueleto + instruções.

---

## O que você vai instalar

1. **Claude Code** (CLI) — o motor
2. **Git** — versionamento e proteção de segredo via hooks
3. **Obsidian** — o segundo cérebro (memória de longo prazo fora da conversa)
4. **Este repositório** — como projeto Claude Code, com CLAUDE.md, skills e hooks já prontos
5. **MCPs (opcional)** — integrações externas (ClickUp, Google Drive, etc.) conforme sua necessidade

---

## Passo 1 — Instalar o Claude Code

```bash
npm install -g @anthropic-ai/claude-code
```

Confirme:

```bash
claude --version
```

Se não tiver Node.js instalado, instale primeiro (https://nodejs.org, versão LTS).

---

## Passo 2 — Instalar o Git e configurar a blindagem de credencial

O maior risco de um projeto de IA agêntica é subir uma chave de API pro GitHub sem
querer. Este kit já vem com um hook de `pre-commit` que bloqueia isso — mas ele só
funciona depois de ativado.

1. Instale o Git (https://git-scm.com) se ainda não tiver.
2. Depois de clonar este repositório (Passo 4), ative os hooks locais:

```bash
git config core.hooksPath .claude/hooks
chmod +x .claude/hooks/pre-commit
```

3. Teste: crie um arquivo com uma string parecida com uma chave de API e tente commitar.
   O commit deve ser recusado. Se não for, revise `.claude/hooks/pre-commit` antes de continuar.

**Regra de ouro:** nenhuma credencial jamais entra em um arquivo versionado.
Credenciais vivem em `.env` (que está no `.gitignore`) ou em variável de ambiente do
sistema. Veja `.env.example` para o formato.

---

## Passo 3 — Instalar o Obsidian (segundo cérebro)

O Obsidian é a memória de longo prazo do organismo — fora da janela de contexto da
conversa. O Claude Code lê e escreve nele via caminho de arquivo (não precisa de
plugin nem de API).

1. Baixe o Obsidian: https://obsidian.md
2. Crie um vault novo (pasta local, ex: `meu-nome/vault-segundo-cerebro/`)
3. Dentro do vault, crie esta estrutura de pastas (adapte os nomes ao seu contexto):

```
vault-segundo-cerebro/
  📚 Base de Conhecimento/      ← conhecimento permanente, por tema
  📋 Reuniões/                  ← uma nota por reunião/brainstorm
  🤖 Operação/
    Log de Decisões.md          ← log de ações relevantes (append-only)
  Estratégias/
    [PROJETO]/                  ← uma pasta por projeto/cliente
  [PROJETO OU CLIENTE]/         ← pasta por cliente/contexto recorrente
```

4. Anote o caminho absoluto do vault — você vai usar esse caminho no seu `CLAUDE.md`
   pessoal (Passo 5) para o Claude Code saber onde procurar.

> Não existe automação obrigatória aqui. O vínculo Claude Code ↔ Obsidian é só:
> "aqui está o caminho da pasta, leia e escreva arquivos `.md` nela".

---

## Passo 4 — Clonar/copiar este repositório

```bash
git clone <url-deste-repositorio> meu-homodeus
cd meu-homodeus
```

Ou, se recebeu como zip: extraia e rode `git init` dentro da pasta.

Estrutura que vem no kit:

```
homodeus-starter-kit/
  README.md                        ← este arquivo
  CLAUDE.md.example                ← protocolo global, GENÉRICO (copie e adapte)
  .env.example                     ← nomes de variáveis, sem valores reais
  .gitignore                       ← já bloqueia .env, credenciais, exports de vault
  MANIFESTO-FERRAMENTAS.md         ← catálogo de integrações comuns + como habilitar cada uma
  .claude/
    settings.json.example          ← permissões e hooks, genérico
    hooks/
      pre-commit                   ← bloqueia commit com padrão de segredo
  .agents/
    skills/
      _exemplo-skill/
        SKILL.md                   ← modelo de skill (copie esta pasta pra criar as suas)
```

---

## Passo 5 — Montar o seu CLAUDE.md

1. Copie `CLAUDE.md.example` para `CLAUDE.md` (na raiz do projeto, ou em
   `~/.claude/CLAUDE.md` se quiser que valha em todo projeto seu).
2. Substitua todos os `[PLACEHOLDER]` pelo seu contexto real: seu nome, o nome do
   seu negócio/organismo, o caminho do seu vault Obsidian, suas regras específicas.
3. Releia os protocolos incluídos (Regra #0, Protocolo Nuclear, Honestidade Radical,
   Log de Ações) — eles são o "sistema operacional" do organismo. Ajuste o que não
   fizer sentido pro seu caso, mas **não remova o Protocolo Nuclear e a regra de
   credencial nunca sobe pro Git** — são as duas camadas de segurança do kit.

---

## Passo 6 — Configurar `.env` e `settings.json`

```bash
cp .env.example .env
# edite .env com suas credenciais reais — este arquivo NUNCA é commitado
cp .claude/settings.json.example .claude/settings.json
```

Edite `.claude/settings.json` conforme os MCPs/ferramentas que for habilitar
(veja `MANIFESTO-FERRAMENTAS.md`).

---

## Passo 7 — Criar suas próprias skills

Skills ficam em `.agents/skills/<nome-da-skill>/SKILL.md`. Use
`.agents/skills/_exemplo-skill/` como modelo: copie a pasta, renomeie, e escreva o
processo que quer que o organismo siga sempre que aquele tipo de tarefa aparecer.

Skills são o lugar certo para documentar **processo repetível** — não para guardar
dado de cliente ou credencial.

---

## Passo 8 — Testar

```bash
cd meu-homodeus
claude
```

Peça pra ele ler o `CLAUDE.md` e confirmar que entendeu os protocolos. Teste o
gatilho do Protocolo Nuclear pedindo pra ele "apagar" algum arquivo de teste — ele
deve pedir as 3 confirmações antes de agir.

---

## O que NUNCA vai neste repositório (nem em nenhum outro)

- `.env` ou qualquer variante
- Tokens, chaves de API, senhas, segredo de cliente OAuth, chave de role de serviço (Supabase)
- Dados reais de cliente (nomes, contratos, campanhas, números)
- Conteúdo do vault Obsidian em si (o vault fica local, fora do Git)
- Chaves privadas (`.pem`, `.key`, `id_rsa`, `*.json` de service account)

Se alguma dessas coisas vazar mesmo assim: rotacione a credencial imediatamente
(trocar a chave, não só apagar o arquivo) e limpe do histórico do Git.
