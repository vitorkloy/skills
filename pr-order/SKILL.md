---
name: pr-order
description: 'Sugerir a melhor ordem de merge das PRs abertas com base no estado do repositório. Ativa com /pr-order.'
disable-model-invocation: true
allowed-tools:
  - Bash(gh pr list *)
  - Bash(gh pr view *)
  - Bash(git *)
---

# Ordem de merge das PRs abertas

Sugere a ordem de merge. Não faz merge. Não faz commit. Não troca de branch. Não edita outros skills.

## Coleta

Rode nesta ordem:

```bash
gh repo view --json nameWithOwner

gh pr list --state open --limit 30 --json number,title,author,isDraft,mergeable,reviewDecision,baseRefName,headRefName,additions,deletions,labels,createdAt,closingIssuesReferences

git status -sb
git log -15 --oneline
```

Só esse estado local. Não baixe o diff de cada PR. Não faça checkout de branch.

Se o `gh` falhar (sem remote, sem auth), uma frase em português com o motivo exato. Sem tabela inventada.

Se não houver PR aberta que não seja draft, uma frase, sem tabela. Se só houver drafts, cite-os nessa frase. Draft não está pronto para merge e não entra na tabela.

`gh pr view` só se faltar o corpo para checar dependência. Não use para puxar diff.

## Ordem

Aplique nesta ordem. A primeira regra que decidir vence.

1. Pule drafts. Liste-os só se o usuário ficaria sem nada, em uma frase, fora da tabela.
2. Texto ou label `DO NOT MERGE` ou `do-not-merge` vai por último, ou sai da tabela com uma nota. Nunca recomende merge desses primeiro.
3. PR com base `main` ou `master` vem antes de PR cuja base é o branch de outra PR aberta. Empilhadas: o pai primeiro.
4. Se a PR A fecha uma issue da qual o título ou o corpo da PR B depende, A vem primeiro. Use `closingIssuesReferences`. Não invente dependência.
5. PR aprovada (`reviewDecision` APPROVED) e `MERGEABLE` vem antes de PR em conflito, bloqueada ou aguardando review, quando mexem na mesma área. Correção pequena aprovada, da qual as outras dependem, vem primeiro.
6. PR com `mergeable` `CONFLICTING` vem depois das limpas que se sobrepõem a ela, para o conflito ser resolvido uma vez.
7. Bugfix e release antes de feature; feature antes de chore e docs, salvo dependência em contrário.
8. Se duas PRs empatam, prefira a que bate com o branch atual (`git status -sb`) ou com os últimos commits (`git log`).

Não diga para mergear PR que o GitHub marca DRAFT, CONFLICTING ou BLOCKED como se estivesse pronta. O estado real vai na coluna Estado:

- `pronta` — MERGEABLE e aprovada, ou MERGEABLE sem bloqueio
- `conflito` — mergeable CONFLICTING
- `aguardando review` — review pendente
- `bloqueada` — BLOCKED ou DO NOT MERGE
- `empilhada em #n` — a base é o branch da PR #n

## Saída

Só um título curto e uma tabela Markdown. Sem bloco de código. Sem URL solta. Escape `|` nas células. No máximo 30 linhas.

| Ordem | PR | Título | Estado | Motivo |
|---|---|---|---|---|
| 1 | [#12](https://github.com/owner/repo/pull/12) | Corrige carga vazia | pronta | Aprovada e MERGEABLE; base main |
| 2 | [#18](https://github.com/owner/repo/pull/18) | Tela Escritório | empilhada em #12 | Base é o branch da #12 |

A célula PR é `[#número](https://github.com/<owner>/<repo>/pull/<número>)` com o `nameWithOwner` real. Ordem é 1, 2, 3.

Motivo é uma frase curta: por que esta posição (base, dependência, review, conflito ou branch atual). Sem evidência, escreva `sem vínculo no código`.
