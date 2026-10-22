---
name: issue-list
description: 'Listar issues abertas numa tabela de prioridade. Ativa com "mostrar issues", "issues abertas", "issues pendentes" e o comando /issue-list.'
disable-model-invocation: true
allowed-tools:
  - Bash(gh issue list *)
---

# Listar issues abertas com prioridade

Lista as issues abertas do repositório atual e classifica cada uma.

## Uso

```bash
gh repo view --json nameWithOwner

gh issue list --state open --limit 30 --json number,title,labels,createdAt,author,assignees
```

Exige `gh` autenticado dentro de um repositório git. Use o `nameWithOwner` real na URL. Não invente issues. Se a lista vier vazia, responda numa frase que não há issues abertas e não imprima tabela.

## Formato de exibição

Responda só com um título curto e uma tabela Markdown. Sem cerca de código (o link precisa ser clicável). Sem URL solta. Sem resumo extra.

Escape `|` no título.

Ordem: alta, depois média, depois baixa. No mesmo nível, o número maior vem primeiro. Máximo de 30 issues abertas.

```markdown
## Issues abertas

| # | Título | Prioridade |
|---|---|---|
| [#120](https://github.com/owner/repo/issues/120) | Login quebra após refresh | alta, bug |
| [#88](https://github.com/owner/repo/issues/88) | Filtro na lista de pedidos | média, enhancement / ui |
| [#40](https://github.com/owner/repo/issues/40) | Atualizar o README | baixa, docs |
```

A coluna `#` é sempre `[#número](https://github.com/<owner>/<repo>/issues/<número>)`.

A coluna Prioridade é curta. Começa com o nível (`alta`, `média` ou `baixa`). Se houver labels reais que justificam o nível, escreva-os depois, separados por vírgula ou ` / `. Exemplos: `alta`, `média, bug`, `média, enhancement / ui`, `baixa`.

## Prioridade

Compare labels e título sem diferenciar maiúsculas. O primeiro nível que casar vale.

**alta** — label ou título indica bug, fix, incident, blocker, ou `priority/high`, `priority/critical`, `P0`, `P1`.

**baixa** — label ou título indica docs, chore, question, good first issue, ou `priority/low`, `P3`. Só se não for alta.

**média** — enhancement, feat, feature, ui, ou issue normal sem label. É o padrão quando nada acima casa.

## Observações

- Só issues com `--state open`, no máximo 30
- A URL usa o `nameWithOwner` real
- A tabela sai em Markdown puro, fora de bloco de código
