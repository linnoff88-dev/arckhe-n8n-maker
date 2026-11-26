ï»¿# n8n-maker ê¢â¬â Skills de n8n para Claude Code

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="48" />
  <p><strong>Arckhé AI</strong></p>
</div>


**ê°Å¸â¡Â§ê°Å¸â¡Â· [PortuguêÂªs](README.md) êÂ· ê°Å¸â¡Âºê°Å¸â¡Â¸ [English](README.en.md) êÂ· ê°Å¸â¡Âªê°Å¸â¡Â¸ [EspaêÂ±ol](README.es.md)**

Conjunto de **7 skills** que ensinam o Claude Code a construir, configurar, validar e
depurar workflows do **n8n**. Ficam em `.claude/skills/` e carregam sozinhas quando o
assunto aparece na conversa ê¢â¬â nêÂ£o precisa invocar nada êÂ  mêÂ£o.

## ê°Å¸ââ Guia de uso

Guia completo (landing + passo a passo): **https://linnoff88-dev.github.io/arckhe-/guia/**

> Antes eram skills globais (`~/.claude/skills/`). Foram movidas para dentro deste
> projeto para ficarem versionadas junto com o trabalho de n8n.

---

## As skills

| Skill | Para que serve | Quando dispara |
|---|---|---|
| **n8n-workflow-patterns** | Os 5 padrêÂµes arquiteturais comprovados: webhook, integraêÂ§êÂ£o HTTP/API, banco de dados, AI agent e tarefas agendadas | Desenhar/estruturar um workflow novo |
| **n8n-node-configuration** | ConfiguraêÂ§êÂ£o *operation-aware*: campos obrigatêÂ³rios, dependêÂªncias entre propriedades, nêÂ­veis de detalhe do `get_node` | Configurar um node especêÂ­fico |
| **n8n-expression-syntax** | Sintaxe `{{ }}`, variêÂ¡veis `$json` / `$node`, dados de webhook e os erros clêÂ¡ssicos | Escrever ou corrigir expressêÂµes |
| **n8n-code-javascript** | Code node em JS: `$input` / `$json` / `$node`, `$helpers.httpRequest`, `DateTime`, modos do node | Escrever JS dentro do n8n |
| **n8n-code-python** | Code node em Python (beta): `_input` / `_json`, biblioteca padrêÂ£o e limitaêÂ§êÂµes | Escrever Python dentro do n8n |
| **n8n-validation-expert** | Ler e resolver erros de validaêÂ§êÂ£o, perfis de validaêÂ§êÂ£o, falsos positivos | Um `validate_*` reclamou |
| **n8n-mcp-tools-expert** | Uso eficiente das ferramentas do MCP `n8n-mcp`: busca de nodes, validaêÂ§êÂ£o, gestêÂ£o de workflows, biblioteca de ~2.700 templates | Operar o n8n via MCP |

Cada pasta traz o `SKILL.md` (o que o Claude lêÂª primeiro) mais arquivos de
referêÂªncia carregados sob demanda ê¢â¬â `ERROR_CATALOG.md`, `COMMON_PATTERNS.md`,
`DATA_ACCESS.md`, `FALSE_POSITIVES.md` etc. Isso mantêÂ©m o contexto leve: sêÂ³ o
detalhe necessêÂ¡rio entra.

---

## Estrutura

O conteêÂºdo real das skills mora em `skills/` (versionado, fêÂ¡cil de achar);
`.claude/skills/` guarda apenas symlinks para lêÂ¡, que êÂ© de onde o Claude Code
carrega. Uma fonte sêÂ³, sem cêÂ³pia duplicada.

```
n8n-maker/
ê¢âÅê¢ââ¬ê¢ââ¬ README.md
ê¢âÅê¢ââ¬ê¢ââ¬ .claude/skills/              ê¢â â symlinks para ../../skills/*
ê¢ââê¢ââ¬ê¢ââ¬ skills/
        ê¢âÅê¢ââ¬ê¢ââ¬ n8n-code-javascript/     SKILL.md + BUILTIN_FUNCTIONS, COMMON_PATTERNS,
        ê¢ââ                            DATA_ACCESS, ERROR_PATTERNS
        ê¢âÅê¢ââ¬ê¢ââ¬ n8n-code-python/         SKILL.md + STANDARD_LIBRARY, COMMON_PATTERNS,
        ê¢ââ                            DATA_ACCESS, ERROR_PATTERNS
        ê¢âÅê¢ââ¬ê¢ââ¬ n8n-expression-syntax/   SKILL.md + COMMON_MISTAKES, EXAMPLES
        ê¢âÅê¢ââ¬ê¢ââ¬ n8n-mcp-tools-expert/    SKILL.md + SEARCH_GUIDE, VALIDATION_GUIDE,
        ê¢ââ                            WORKFLOW_GUIDE
        ê¢âÅê¢ââ¬ê¢ââ¬ n8n-node-configuration/  SKILL.md + DEPENDENCIES, OPERATION_PATTERNS
        ê¢âÅê¢ââ¬ê¢ââ¬ n8n-validation-expert/   SKILL.md + ERROR_CATALOG, FALSE_POSITIVES
        ê¢ââê¢ââ¬ê¢ââ¬ n8n-workflow-patterns/   SKILL.md + webhook_processing,
                                     http_api_integration, database_operations,
                                     ai_agent_workflow, scheduled_tasks
```

---

## Como usar

1. Abra o Claude Code **dentro desta pasta** (`cd ~/projetos/n8n-maker`). Skills em
   `.claude/skills/` valem sêÂ³ para este projeto.
   (o carregamento vem dos symlinks em `.claude/skills/`).
2. PeêÂ§a o que quer em portuguêÂªs mesmo: *"monta um workflow que recebe um webhook,
   valida o payload e grava no Postgres"*.
3. O Claude puxa a skill certa sozinho ê¢â¬â `n8n-workflow-patterns` para o desenho,
   `n8n-node-configuration` na hora de configurar, `n8n-validation-expert` quando a
   validaêÂ§êÂ£o reclamar.

Para usar em qualquer projeto, copie (ou faêÂ§a symlink) as pastas de volta para
`~/.claude/skills/`.

### Fluxo têÂ­pico

```
desenhar (workflow-patterns)
   ê¢â â configurar nodes (node-configuration)
   ê¢â â expressêÂµes e Code nodes (expression-syntax, code-javascript)
   ê¢â â validar e corrigir (validation-expert)   ê¢â Â 2-3 voltas êÂ© o normal
   ê¢â â publicar/gerenciar via MCP (mcp-tools-expert)
```

### Combinando com o MCP n8n

A skill `n8n-mcp-tools-expert` pressupêÂµe o servidor MCP **n8n-mcp** conectado ê¢â¬â êÂ©
ele que dêÂ¡ busca de nodes, validaêÂ§êÂ£o de configuraêÂ§êÂ£o, biblioteca de templates e
deploy de workflows. Sem o MCP as outras seis continuam êÂºteis: viram guia de
sintaxe, padrêÂµes e depuraêÂ§êÂ£o.

---

## LicenêÂ§a / origem

Skills de uso interno ARCKHÉ, mantidas neste repositêÂ³rio.

---

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="32" />
  <p><strong>Arckhé AI</strong></p>
</div>