---
name: issue-order
description: 'Analisar issues abertas e sugerir a ordem de implementação com base no estado atual do código. Ativa com /issue-order.'
disable-model-invocation: true
allowed-tools:
  - Bash(gh issue list *)
  - Bash(gh pr list *)
  - Bash(git *)
---

# Ordem de implementação das issues

Analisa as issues abertas e sugere a ordem de implementação com base no código atual.

## Coleta

```bash
gh repo view --json nameWithOwner

gh issue list --state open --limit 30 --json number,title,labels,createdAt,body,assignees

gh pr list --state open --limit 20 --json number,title,headRefName,closingIssuesReferences

git log -15 --oneline

git status -sb
```

Estado local e barato. Não clone. Não leia a árvore inteira. Se o título apontar com clareza para um diretório, leia só a listagem desse diretório.

Exige `gh` autenticado num repositório git. Use o `nameWithOwner` real. Não invente issues, dependências ou código que você não viu. Não faça commit.

Se `gh` falhar por falta de remote ou erro de autenticação, uma frase em português com o motivo exato. Sem tabela inventada. Se não houver issues abertas, uma frase e sem tabela.

## Ordem

1. Faça primeiro o trabalho que a branch atual e os commits recentes já começaram, antes de áreas novas sem relação.
2. Issue já citada por um PR aberto vem depois das issues sem PR, salvo se esse PR estiver bloqueado. Marque `PR #n` na coluna Estado. Não peça para reimplementar.
3. alta (bug, fix, incident, blocker, priority/high, priority/critical, P0, P1) antes de média, antes de baixa. Um bug pequeno que bloqueia uma feature passa na frente dessa feature.
4. baixa (docs, chore, question, good first issue, priority/low, P3) por último, salvo se desbloquear algo acima.
5. Dependências: se a issue A cita a issue B ou "depends on", B vem primeiro.
6. Se o vínculo com o código não estiver claro, escreva `sem vínculo no código` na célula Motivo.

Compare labels e título sem diferenciar maiúsculas.

**alta** — bug, fix, incident, blocker, `priority/high`, `priority/critical`, `P0`, `P1`.

**baixa** — docs, chore, question, good first issue, `priority/low`, `P3`. Só se não for alta.

**média** — o restante.

## Formato

Responda só com um título curto e uma tabela Markdown. Sem cerca de código (o link precisa ser clicável). Sem URL solta. Sem resumo extra. Escape `|` nas células. Máximo de 30 linhas.

```markdown
## Ordem de implementação

| Ordem | Issue | Título | Estado | Motivo |
|---|---|---|---|---|
| 1 | [#120](https://github.com/owner/repo/issues/120) | Login quebra após refresh | sem PR | Branch atual já mexe em auth; bug bloqueia o filtro. |
| 2 | [#88](https://github.com/owner/repo/issues/88) | Filtro na lista de pedidos | sem PR | Depende da #120. |
| 3 | [#40](https://github.com/owner/repo/issues/40) | Atualizar o README | PR #12 | Baixa e já coberta pelo PR #12. |
```

A coluna Issue é sempre `[#número](https://github.com/<owner>/<repo>/issues/<número>)`.

Ordem é 1, 2, 3.

Estado é `PR #n` quando um PR aberto referencia a issue, ou `sem PR`.

Motivo é uma frase curta: por que esta posição, dado a branch atual, os commits recentes, os PRs abertos ou uma dependência. Cite o número do PR quando existir.
