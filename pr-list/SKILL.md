---
name: pr-list
description: 'Exibir PRs abertos com ranking de prioridade. Ativa com "mostrar PRs", "PRs abertos", "PRs pendentes".'
disable-model-invocation: true
allowed-tools:
  - Bash(gh pr list *)
---

# Exibir PRs abertos com ranking de prioridade

Exibe a lista de PRs abertos do repositório atual com priorização.

## Uso

```bash
# Solicitar ao Claude
"Exibir lista de PRs abertos com priorização"
```

## Exemplo básico

```bash
# Obtém informações do repositório
gh repo view --json nameWithOwner | jq -r '.nameWithOwner'

# Obtém informações de PRs abertos e solicita ao Claude
gh pr list --state open --draft=false --json number,title,author,createdAt,additions,deletions,reviews,closingIssuesReferences --limit 30

"Monte uma única tabela Markdown. O número de cada PR é um link clicável. Não cole URL solta."
```

## Formato de exibição

Responda só com um título curto e uma tabela Markdown. Sem árvore, sem resumo de duas linhas, sem URL fora do link.

Ordem das linhas: alta, depois média, depois baixa. Dentro do mesmo nível, o número maior vem primeiro.

Escape `|` no título. Não envolva a tabela em bloco de código, senão o link não abre.

```markdown
## PRs abertos

| # | Título | Issue | Prioridade |
|---|---|---|---|
| [#747](https://github.com/owner/repo/pull/747) | Efeito padronizado de deleção em partículas | [#120](https://github.com/owner/repo/issues/120) | alta |
| [#697](https://github.com/owner/repo/pull/697) | Falha de carga aparece como "vazio" | — | média, bug |
| [#689](https://github.com/owner/repo/pull/689) | Chat: tela Escritório | [#88](https://github.com/owner/repo/issues/88), [#90](https://github.com/owner/repo/issues/90) | baixa |
```

A coluna `#` usa sempre `[#número](url)`. A URL é `https://github.com/<owner>/<repo>/pull/<número>`, com o `nameWithOwner` real.

A coluna Issue lista `closingIssuesReferences`. Cada issue é `[#número](https://github.com/<owner>/<repo>/issues/<número>)`. Várias issues na mesma célula, separadas por vírgula. Sem issue vinculada, use `—`. Não invente vínculo.

A coluna Prioridade usa `alta`, `média` ou `baixa`. Se o título tiver um tipo (`fix`, `feat`, `bug`, `ui`), acrescente depois da vírgula, como `média, bug`. Se for DO NOT MERGE, escreva `baixa, DNM`.

## Critérios de determinação de prioridade

**Alta Prioridade**

- `fix:` Correção de bug
- `release:` Trabalho de release

**Prioridade Média**

- `feat:` Nova funcionalidade
- `update:` Melhoria de funcionalidade
- Outros PRs normais

**Baixa Prioridade**

- PRs contendo DO NOT MERGE
- Draft com PRs de `test:`, `build:`, `perf:`

## Observações

- Requer GitHub CLI (`gh`)
- Exibe apenas PRs no estado aberto (exclui Draft)
- Exibe máximo de 30 PRs
- A URL do PR usa o `nameWithOwner` real do repositório
- A tabela sai em Markdown puro, para o número do PR e da issue ficarem clicáveis
- A coluna Issue vem de `closingIssuesReferences`. Sem referência, a célula é `—`
