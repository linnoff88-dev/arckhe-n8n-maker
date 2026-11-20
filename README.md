# n8n-maker â€” Skills de n8n para Claude Code

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="48" />
  <p><strong>Arckhé AI</strong></p>
</div>


**ðŸ‡§ðŸ‡· [PortuguÃªs](README.md) Â· ðŸ‡ºðŸ‡¸ [English](README.en.md) Â· ðŸ‡ªðŸ‡¸ [EspaÃ±ol](README.es.md)**

Conjunto de **7 skills** que ensinam o Claude Code a construir, configurar, validar e
depurar workflows do **n8n**. Ficam em `.claude/skills/` e carregam sozinhas quando o
assunto aparece na conversa â€” nÃ£o precisa invocar nada Ã  mÃ£o.

## ðŸ“– Guia de uso

Guia completo (landing + passo a passo): **https://inematds.github.io/n8n-maker/guia/**

> Antes eram skills globais (`~/.claude/skills/`). Foram movidas para dentro deste
> projeto para ficarem versionadas junto com o trabalho de n8n.

---

## As skills

| Skill | Para que serve | Quando dispara |
|---|---|---|
| **n8n-workflow-patterns** | Os 5 padrÃµes arquiteturais comprovados: webhook, integraÃ§Ã£o HTTP/API, banco de dados, AI agent e tarefas agendadas | Desenhar/estruturar um workflow novo |
| **n8n-node-configuration** | ConfiguraÃ§Ã£o *operation-aware*: campos obrigatÃ³rios, dependÃªncias entre propriedades, nÃ­veis de detalhe do `get_node` | Configurar um node especÃ­fico |
| **n8n-expression-syntax** | Sintaxe `{{ }}`, variÃ¡veis `$json` / `$node`, dados de webhook e os erros clÃ¡ssicos | Escrever ou corrigir expressÃµes |
| **n8n-code-javascript** | Code node em JS: `$input` / `$json` / `$node`, `$helpers.httpRequest`, `DateTime`, modos do node | Escrever JS dentro do n8n |
| **n8n-code-python** | Code node em Python (beta): `_input` / `_json`, biblioteca padrÃ£o e limitaÃ§Ãµes | Escrever Python dentro do n8n |
| **n8n-validation-expert** | Ler e resolver erros de validaÃ§Ã£o, perfis de validaÃ§Ã£o, falsos positivos | Um `validate_*` reclamou |
| **n8n-mcp-tools-expert** | Uso eficiente das ferramentas do MCP `n8n-mcp`: busca de nodes, validaÃ§Ã£o, gestÃ£o de workflows, biblioteca de ~2.700 templates | Operar o n8n via MCP |

Cada pasta traz o `SKILL.md` (o que o Claude lÃª primeiro) mais arquivos de
referÃªncia carregados sob demanda â€” `ERROR_CATALOG.md`, `COMMON_PATTERNS.md`,
`DATA_ACCESS.md`, `FALSE_POSITIVES.md` etc. Isso mantÃ©m o contexto leve: sÃ³ o
detalhe necessÃ¡rio entra.

---

## Estrutura

O conteÃºdo real das skills mora em `skills/` (versionado, fÃ¡cil de achar);
`.claude/skills/` guarda apenas symlinks para lÃ¡, que Ã© de onde o Claude Code
carrega. Uma fonte sÃ³, sem cÃ³pia duplicada.

```
n8n-maker/
â”œâ”€â”€ README.md
â”œâ”€â”€ .claude/skills/              â†’ symlinks para ../../skills/*
â””â”€â”€ skills/
        â”œâ”€â”€ n8n-code-javascript/     SKILL.md + BUILTIN_FUNCTIONS, COMMON_PATTERNS,
        â”‚                            DATA_ACCESS, ERROR_PATTERNS
        â”œâ”€â”€ n8n-code-python/         SKILL.md + STANDARD_LIBRARY, COMMON_PATTERNS,
        â”‚                            DATA_ACCESS, ERROR_PATTERNS
        â”œâ”€â”€ n8n-expression-syntax/   SKILL.md + COMMON_MISTAKES, EXAMPLES
        â”œâ”€â”€ n8n-mcp-tools-expert/    SKILL.md + SEARCH_GUIDE, VALIDATION_GUIDE,
        â”‚                            WORKFLOW_GUIDE
        â”œâ”€â”€ n8n-node-configuration/  SKILL.md + DEPENDENCIES, OPERATION_PATTERNS
        â”œâ”€â”€ n8n-validation-expert/   SKILL.md + ERROR_CATALOG, FALSE_POSITIVES
        â””â”€â”€ n8n-workflow-patterns/   SKILL.md + webhook_processing,
                                     http_api_integration, database_operations,
                                     ai_agent_workflow, scheduled_tasks
```

---

## Como usar

1. Abra o Claude Code **dentro desta pasta** (`cd ~/projetos/n8n-maker`). Skills em
   `.claude/skills/` valem sÃ³ para este projeto.
   (o carregamento vem dos symlinks em `.claude/skills/`).
2. PeÃ§a o que quer em portuguÃªs mesmo: *"monta um workflow que recebe um webhook,
   valida o payload e grava no Postgres"*.
3. O Claude puxa a skill certa sozinho â€” `n8n-workflow-patterns` para o desenho,
   `n8n-node-configuration` na hora de configurar, `n8n-validation-expert` quando a
   validaÃ§Ã£o reclamar.

Para usar em qualquer projeto, copie (ou faÃ§a symlink) as pastas de volta para
`~/.claude/skills/`.

### Fluxo tÃ­pico

```
desenhar (workflow-patterns)
   â†’ configurar nodes (node-configuration)
   â†’ expressÃµes e Code nodes (expression-syntax, code-javascript)
   â†’ validar e corrigir (validation-expert)   â† 2-3 voltas Ã© o normal
   â†’ publicar/gerenciar via MCP (mcp-tools-expert)
```

### Combinando com o MCP n8n

A skill `n8n-mcp-tools-expert` pressupÃµe o servidor MCP **n8n-mcp** conectado â€” Ã©
ele que dÃ¡ busca de nodes, validaÃ§Ã£o de configuraÃ§Ã£o, biblioteca de templates e
deploy de workflows. Sem o MCP as outras seis continuam Ãºteis: viram guia de
sintaxe, padrÃµes e depuraÃ§Ã£o.

---

## LicenÃ§a / origem

Skills de uso interno INEMA, mantidas neste repositÃ³rio.

---

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="32" />
  <p><strong>Arckhé AI</strong></p>
</div>