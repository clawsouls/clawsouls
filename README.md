# ClawSouls

AI agent persona sharing platform

> 🧠 *"Give your AI a soul."*

ClawSouls is a persona (Soul) marketplace for [OpenClaw](https://github.com/openclaw/openclaw) agents. While Skills define "what an agent can do", Souls define "how it does it".

## Overview

- **Browse & Install Souls** — Community-made AI personas
- **Create & Share** — Build your own Soul and share it
- **Premium Market** — High-quality Soul packs by experts

## What is a Soul?

A Soul package defines an AI persona with 4 files:

| File | Purpose |
|------|---------|
| `SOUL.md` | Personality, principles, communication style |
| `IDENTITY.md` | Name, emoji, avatar |
| `AGENTS.md` | Behavior rules, workflow |
| `HEARTBEAT.md` | Periodic check items |

Same LLM, completely different persona depending on the Soul.

## Quick Start

```bash
# Install a soul
npx clawsouls install brad

# Activate it
npx clawsouls use brad

# Restart your OpenClaw session — done!
```

## Sample Souls

| Soul | Personality | Use Case |
|------|-------------|----------|
| [Brad](https://clawsouls.ai/souls/brad) 🅱️ | Formal, autonomous, concise | Development partner |
| [DevOps Veteran](https://clawsouls.ai/souls/devops-veteran) 🔧 | Experienced, opinionated | Infrastructure management |
| [GameDev Mentor](https://clawsouls.ai/souls/gamedev-mentor) 🎮 | Warm, encouraging | Game development mentor |
| [Minimalist](https://clawsouls.ai/souls/minimalist) ⚡ | Extremely concise | Quick Q&A |
| [Code Reviewer](https://clawsouls.ai/souls/code-reviewer) 🔍 | Thorough, constructive | Code review |

Browse all at [clawsouls.ai](https://clawsouls.ai).

## Links

- 🌐 [clawsouls.ai](https://clawsouls.ai) — Browse souls
- 📦 [CLI (npm)](https://www.npmjs.com/package/clawsouls) — Install & manage
- 📦 [Soul Spec](docs/SOUL_SPEC.md) — Create your own soul
- 🐙 [GitHub Org](https://github.com/clawsouls) — All repositories

## License

Open source parts: Apache 2.0 — see [LICENSE.md](LICENSE.md)
