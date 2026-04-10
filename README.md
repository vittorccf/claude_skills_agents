# Claude Code Toolkit

Colecao pessoal de skills e agentes customizados para o [Claude Code](https://docs.anthropic.com/en/docs/claude-code).

Um lugar central para versionar e organizar as skills que eu crio, para nao perder nada entre maquinas ou projetos.

---

Personal collection of custom skills and agents for [Claude Code](https://docs.anthropic.com/en/docs/claude-code).

A central place to version-control and organize the skills I build, so nothing gets lost across machines or projects.

## Estrutura / Structure

```
skills/          — Skills customizadas / Custom skills (SKILL.md + resources)
.agents/         — Skills de agentes instaladas / Installed agent skills (managed by Claude Code)
```

## Skills

| Skill | Descricao / Description |
|-------|-------------------------|
| **read-only** | Ativa modo somente-leitura — permite que o Claude analise e explore um projeto sem modificar nenhum arquivo. Ideal para sessoes com `--dangerously-skip-permissions` onde voce quer leitura total sem risco de escrita. |
| | Enforces read-only mode — lets Claude analyze and explore a project without modifying any files. Ideal for `--dangerously-skip-permissions` sessions where you want full read access with zero write risk. |

## Uso / Usage

Para usar uma skill deste repo em qualquer projeto, aponte o Claude Code para o caminho da skill:

To use a skill from this repo in any project, point Claude Code to the skill path:

```bash
claude --skill-path /path/to/this/repo/skills/read-only
```

Ou copie a pasta da skill para o diretorio `.claude/skills/` do seu projeto.

Or copy the skill folder into your project's `.claude/skills/` directory.

## Adicionando novas skills / Adding new skills

Crie uma nova pasta em `skills/` com um arquivo `SKILL.md`:

Create a new folder under `skills/` with a `SKILL.md` file:

```
skills/
  my-new-skill/
    SKILL.md
    scripts/      (opcional / optional)
    references/   (opcional / optional)
```

Veja a [documentacao de skills do Claude Code](https://docs.anthropic.com/en/docs/claude-code/skills) para o formato completo.

See the [Claude Code skills docs](https://docs.anthropic.com/en/docs/claude-code/skills) for the full format.
