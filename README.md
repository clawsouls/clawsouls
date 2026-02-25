# ClawSouls

AI agent persona sharing platform

> 🧠 *"When you change your AI's soul, you don't just change the AI. You change yourself."*
>
> Read [The Soul Thesis](https://clawsouls.ai/en/manifesto)

ClawSouls is an open-spec platform for shareable AI agent personas. 80+ curated souls. One command to install. Built for OpenClaw, works with any SOUL.md-compatible agent. Apache 2.0.

While Anthropic Skills define **what** an agent can do, Souls define **who** it is when it does it.

## 🤝 Multi-Platform

ClawSouls auto-detects your agent framework — no configuration needed.

| Platform | Directory | Status |
|----------|-----------|--------|
| OpenClaw | `~/.openclaw/workspace/` | ✅ Auto-detected |
| ZeroClaw | `~/.zeroclaw/workspace/` | ✅ Auto-detected |
| Clawdbot | `~/.clawdbot/workspace/` | ✅ Auto-detected |
| Moltbot  | `~/.moltbot/workspace/`  | ✅ Auto-detected |
| Moldbot  | `~/.moldbot/workspace/`  | ✅ Auto-detected |
| Custom   | Any path                 | ✅ `--workspace` / `--platform` |

```bash
# Override if needed
clawsouls --platform zeroclaw use surgical-coder
clawsouls --workspace ~/my-agent/workspace use surgical-coder
clawsouls platform   # check detected platform
```

## What is a Soul?

A Soul is a set of markdown files that give an AI agent a consistent personality, voice, and behavior.

```
my-soul/
├── soul.json       # metadata & config
├── SOUL.md         # core personality
├── IDENTITY.md     # name, emoji, vibe
├── AGENTS.md       # behavioral guidelines
├── STYLE.md        # writing voice & tone
├── HEARTBEAT.md    # periodic check items
└── README.md       # documentation
```

No code. No API keys. No vendor lock-in. Just text files that any AI can read.

## ⚡ Quick Start

```bash
# Install a soul
npx clawsouls install clawsouls/surgical-coder

# Apply it to your workspace
npx clawsouls use clawsouls/surgical-coder

# Restart your agent — done!
openclaw gateway restart
```

Or visit [clawsouls.ai](https://clawsouls.ai) to browse the gallery.

## Create Your Own

```bash
# Scaffold a new soul
npx clawsouls init my-soul

# For robotics/embodied agents, use --spec 0.5
npx clawsouls init my-robot --spec 0.5

# Edit the files, then publish
npx clawsouls publish ./my-soul/
```

Get your publish token at [clawsouls.ai/dashboard](https://clawsouls.ai/en/dashboard).

## Sample Souls

| Soul | Personality | Use Case |
|------|-------------|----------|
| [Surgical Coder](https://clawsouls.ai/en/souls/clawsouls/surgical-coder) 🧠 | Disciplined, minimal, goal-driven | Precise coding |
| [DevOps Veteran](https://clawsouls.ai/en/souls/clawsouls/devops-veteran) 🔧 | Experienced, opinionated | Infrastructure |
| [GameDev Mentor](https://clawsouls.ai/en/souls/clawsouls/gamedev-mentor) 🎮 | Warm, encouraging | Game development |
| [Minimalist](https://clawsouls.ai/en/souls/clawsouls/minimalist) ⚡ | Extremely concise | Quick Q&A |
| [Brad](https://clawsouls.ai/en/souls/clawsouls/brad) 🅱️ | Formal, professional | Development partner |

**79+ souls** available — browse all at [clawsouls.ai](https://clawsouls.ai).

## ⚠️ Spec Version Compatibility

> **v0.5 souls with `environment: "physical"`** include hardware, sensor, and safety fields intended for embodied agents (robots, IoT). Text-only agents (OpenClaw, ChatGPT, Claude) will safely ignore these fields — but the LLM may still interpret physical descriptions in `SOUL.md` as persona context. If you're using a physical soul with a text agent, set `environment: "virtual"` in `soul.json` or add fallback instructions in `SOUL.md`: *"In text-only environments, omit physical action descriptions."*

## Soul Spec

Open standard. LLM-agnostic. Platform-portable.

- [Soul Spec v0.4](docs/soul-spec-v0.4.md) — Latest
- [Soul Spec v0.3](docs/soul-spec-v0.3.md)

## Links

- 🌐 [clawsouls.ai](https://clawsouls.ai) — Browse & install souls
- 📜 [The Soul Thesis](https://clawsouls.ai/en/manifesto) — Our manifesto
- 📄 [Research Paper](https://doi.org/10.5281/zenodo.18758910) — "Soul-Driven Interaction Design" (Lee, 2026)
- 📦 [npm: clawsouls](https://www.npmjs.com/package/clawsouls) — CLI
- 📄 [License Guide](https://clawsouls.ai/en/licenses) — Allowed licenses
- 🐙 [GitHub](https://github.com/clawsouls) — All repositories

## License

Apache 2.0 — see [LICENSE](LICENSE)

## Disclaimer

ClawSouls is an independent, community-driven platform. Not affiliated with or endorsed by OpenClaw.
