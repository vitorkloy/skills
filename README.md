# Skills

Skills para agentes de código (Claude Code, Cursor, Codex). Cada pasta tem um `SKILL.md`.

Para instalar no Claude Code, copie as pastas que quiser para `~/.claude/skills/` (todas as sessões) ou `.claude/skills/` (só um projeto).

## Skills próprias

| Skill | O que faz |
|---|---|
| [caveman](caveman) | Respostas curtas, sem enrolação, mantendo todo o conteúdo técnico |
| [issue-list](issue-list) | Lista as issues abertas numa tabela por prioridade |
| [issue-order](issue-order) | Sugere a ordem de implementação das issues abertas |
| [pr-list](pr-list) | Lista os PRs abertos numa tabela por prioridade |
| [pr-order](pr-order) | Sugere a ordem de merge dos PRs abertos |
| [web-interface-guidelines](web-interface-guidelines) | Revisa UI contra as Web Interface Guidelines da Vercel, com arquivo:linha |

## Skills de design de terceiros

Cópias das skills originais, sem alterações, cada uma com a licença do autor na própria pasta. Para pegar versões novas, atualize a partir do repositório de origem.

### Direção e qualidade visual

| Skill | O que faz | Origem | Licença |
|---|---|---|---|
| [frontend-design](frontend-design) | Escolhe uma direção visual clara antes de escrever código | [anthropics/skills](https://github.com/anthropics/skills/tree/main/skills/frontend-design) | Apache-2.0 |
| [impeccable](impeccable) | Planeja, critica, refina e anima interfaces numa skill só | [pbakaus/impeccable](https://github.com/pbakaus/impeccable) | Apache-2.0 |
| [taste-skill](taste-skill) | Controles de variação, movimento e densidade, com checagem antes de entregar | [Leonxlnx/taste-skill](https://github.com/Leonxlnx/taste-skill) | MIT |
| [hallmark](hallmark) | Temas, estruturas de página e checklist de qualidade | [Nutlope/hallmark](https://github.com/Nutlope/hallmark) | MIT |
| [ui-ux-pro-max](ui-ux-pro-max) | Paletas, pares de fontes e regras de UX sob demanda | [nextlevelbuilder/ui-ux-pro-max-skill](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) | MIT |
| [hue](hue) | Transforma uma marca numa skill de linguagem visual própria | [dominikmartn/hue](https://github.com/dominikmartn/hue) | MIT |
| [extract-design-md](extract-design-md) | Extrai tokens e padrões de um código para um DESIGN.md (requer o MCP do Stitch) | [google-labs-code/stitch-skills](https://github.com/google-labs-code/stitch-skills/tree/main/plugins/stitch-design/skills/extract-design-md) | Apache-2.0 |
| [shadcn](shadcn) | Adiciona e atualiza componentes no padrão shadcn/ui | [shadcn-ui/ui](https://github.com/shadcn-ui/ui/tree/main/skills/shadcn) | MIT |
| [interface-design](interface-design) | Dashboards e painéis admin com hierarquia de verdade | [Dammyjay93/interface-design](https://github.com/Dammyjay93/interface-design) | MIT |
| [better-typography](better-typography) | Escala tipográfica, entrelinha, largura de linha e carregamento de fontes | [jakubkrehel/skills](https://github.com/jakubkrehel/skills/tree/main/skills/better-typography) | MIT |
| [refactoring-ui](refactoring-ui) | Revisão de hierarquia, espaçamento e profundidade baseada no livro Refactoring UI | [edisonmbli/refactoring-ui-skill](https://github.com/edisonmbli/refactoring-ui-skill) | MIT |

### Movimento, 3D e acabamento

| Skill | O que faz | Origem | Licença |
|---|---|---|---|
| [emil-design-eng](emil-design-eng) | Easing, durações e springs segundo Emil Kowalski | [emilkowalski/skill](https://github.com/emilkowalski/skill/tree/main/skills/emil-design-eng) | MIT |
| [gsap-scrolltrigger](gsap-scrolltrigger) | Guia oficial de pinning, scrub e cleanup do ScrollTrigger | [greensock/gsap-skills](https://github.com/greensock/gsap-skills/tree/main/skills/gsap-scrolltrigger) | MIT |
| [motion-design](motion-design) | Tabelas de duração e easing da LottieFiles | [lottiefiles/motion-design-skill](https://github.com/lottiefiles/motion-design-skill) | MIT |
| [shader-dev](shader-dev) | Técnicas de shader no estilo ShaderToy, de SDFs a fluidos | [MiniMax-AI/skills](https://github.com/MiniMax-AI/skills/tree/main/skills/shader-dev) | MIT |
| [build-threejs-scroll-worlds](build-threejs-scroll-worlds) | Um mundo 3D em Three.js guiado pelo scroll nativo | [MengTo/Skills](https://github.com/MengTo/Skills/tree/main/agent-skills/web-design/build-threejs-scroll-worlds) | MIT |
| [diagram-design](diagram-design) | Diagramas editoriais em HTML e SVG | [cathrynlavery/diagram-design](https://github.com/cathrynlavery/diagram-design) | MIT |
| [frontend-slides](frontend-slides) | Apresentações HTML animadas, exportáveis para PPTX | [zarazhangrui/frontend-slides](https://github.com/zarazhangrui/frontend-slides) | MIT |

### Só link (não copiadas)

| Skill | Por quê | Onde |
|---|---|---|
| Craftwork | Sem licença para redistribuir; exige MCP, login OAuth e plano pago | [craftwork.design/SKILL.md](https://craftwork.design/SKILL.md) |

A `web-interface-guidelines` acima foi reescrita aqui porque o repositório original ([vercel-labs/agent-skills](https://github.com/vercel-labs/agent-skills)) não tem licença. Ela busca as regras de [vercel-labs/web-interface-guidelines](https://github.com/vercel-labs/web-interface-guidelines), que é MIT.
