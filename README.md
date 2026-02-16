# ClawSouls

AI agent persona sharing platform

> 🧠 *"When you change your AI's soul, you don't just change the AI. You change yourself."*
>
> Read [The Soul Thesis](https://clawsouls.ai/en/manifesto)

ClawSouls is an open registry of shareable personas for AI agents. 79+ curated souls. One command to install. Open spec (Apache 2.0).

While Anthropic Skills define **what** an agent can do, Souls define **who** it is when it does it.

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

## Soul Spec

Open standard. LLM-agnostic. Platform-portable.

- [Soul Spec v0.3](docs/soul-spec-v0.3.md) — Latest
- [Soul Spec v0.2](docs/soul-spec-v0.2.md)
- [Soul Spec v0.1](docs/soul-spec-v0.1.md)

## Links

- 🌐 [clawsouls.ai](https://clawsouls.ai) — Browse & install souls
- 📜 [The Soul Thesis](https://clawsouls.ai/en/manifesto) — Our manifesto
- 📄 [Research Paper](https://doi.org/10.5281/zenodo.18661656) — "Soul-Driven Interaction Design" (Lee, 2026)
- 📦 [npm: clawsouls](https://www.npmjs.com/package/clawsouls) — CLI
- 📄 [License Guide](https://clawsouls.ai/en/licenses) — Allowed licenses
- 🐙 [GitHub](https://github.com/clawsouls) — All repositories

## License

Apache 2.0 — see [LICENSE](LICENSE)

## Disclaimer

ClawSouls is an independent, community-driven platform. Not affiliated with or endorsed by OpenClaw.
