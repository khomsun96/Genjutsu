# genjutsu

A Claude Code plugin that casts illusions for your codebase (mock APIs, realistic fixtures, test stubs) and dispels the ones that leak into production.

## Install

```
/plugin marketplace add khomsun96/Genjutsu
/plugin install genjutsu@genjutsu
```

Then restart Claude Code (or run `/reload-plugins`) so the commands load.

## What you get

| Piece | Name | What it does |
|---|---|---|
| Command | `/genjutsu:mock-api <spec or description>` | Builds a runnable mock server using the project's own stack |
| Command | `/genjutsu:fixtures <model> [count]` | Generates realistic, constraint-respecting fixture or seed data |
| Command | `/genjutsu:stub <dependency>` | Creates a configurable test double and one example test |
| Command | `/genjutsu:dispel [path]` | Read-only sweep for mocks and fake data reachable in production |
| Agent | `illusionist` | Read-only specialist used by `dispel` |
| Skill | `mock-data` | Rules for fake data that looks real but is safe |

Everything genjutsu generates is tagged `genjutsu:mock`, which is how `dispel` tells intended mocks from leaks.

## Layout

```
genjutsu/
├── .claude-plugin/marketplace.json     # makes this repo a marketplace
└── plugins/genjutsu/
    ├── .claude-plugin/plugin.json      # plugin manifest
    ├── commands/                       # slash commands
    ├── agents/illusionist.md
    └── skills/mock-data/SKILL.md
```

## Developing

Test locally without pushing:

```
/plugin marketplace add ./path/to/genjutsu
/plugin install genjutsu@genjutsu
```

Bump `version` in both `plugin.json` and `marketplace.json` when you release, then users run `/plugin marketplace update genjutsu`.

## License

MIT
