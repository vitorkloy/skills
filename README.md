# Skills pessoais do Cursor

Skills de uso próprio no Cursor: uma voz curta para as respostas e quatro comandos de triagem no GitHub (PRs e issues abertas, prioridade e ordem de trabalho).

## Skills

| Skill | Comando | O que faz |
|---|---|---|
| caveman | `/caveman` | Responde curto, fato técnico intacto, sem cerimônia. Fica ativo a sessão inteira até `stop caveman` ou `normal mode`. |
| pr-list | `/pr-list` | Lista até 30 PRs abertos (sem draft) numa tabela, da prioridade alta para a baixa. |
| issue-list | `/issue-list` | Lista até 30 issues abertas numa tabela, da prioridade alta para a baixa. |
| issue-order | `/issue-order` | Sugere a ordem de implementação das issues abertas a partir do código, da branch e dos PRs abertos. Não faz commit. |
| pr-order | `/pr-order` | Sugere a ordem de merge das PRs abertas. Não faz merge, commit nem troca de branch. Draft fica de fora da tabela. |

`/caveman status` só informa se o modo está ligado. `/caveman ultra` e `/caveman wenyan` não usam esta skill.

## Como usar

Copie a pasta da skill para `~/.cursor/skills/<nome>/`. No Windows: `C:\Users\<voce>\.cursor\skills\`.

Os comandos `/` dependem de `disable-model-invocation: true` no `SKILL.md`. Estas skills já vêm com isso. Abra um chat novo de Agent e digite `/`.

`/pr-list`, `/issue-list`, `/issue-order` e `/pr-order` precisam do GitHub CLI (`gh`) autenticado, dentro de um clone que tenha remote no GitHub.

## Formato

Cada skill de GitHub responde com um título curto e uma tabela Markdown. O número da issue ou da PR é um link clicável. Sem URL solta e sem bloco de código em volta da tabela.

- `/pr-list`: `#`, Título, Issue, Prioridade (`alta`, `média` ou `baixa`; tipo no título depois da vírgula, como `média, bug`).
- `/issue-list`: `#`, Título, Prioridade (nível e, se houver, labels reais).
- `/issue-order`: Ordem, Issue, Título, Estado (`PR #n` ou `sem PR`), Motivo.
- `/pr-order`: Ordem, PR, Título, Estado (`pronta`, `conflito`, `aguardando review`, `bloqueada` ou `empilhada em #n`), Motivo.
