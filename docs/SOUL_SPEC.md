# ClawSouls Package Spec

Latest version: **v0.2** ([SOUL_SPEC_v0.2.md](./SOUL_SPEC_v0.2.md))

## Version History

| Version | Date | Description |
|---------|------|-------------|
| [v0.2](./SOUL_SPEC_v0.2.md) | 2026-02-13 | Add STYLE.md, examples, modes, interpolation |
| [v0.1](./SOUL_SPEC_v0.1.md) | 2026-02-12 | Initial spec: clawsoul.json, file structure, categories, CLI, security |

---

## Roadmap

### v0.3 Planned Features

Aligned with Anthropic's Skill design patterns ("The Complete Guide to Building Skills for Claude", Jan 2026).

#### 3-Level Progressive Disclosure

Adopt the same layered information architecture used by Anthropic Skills:

| Level | Purpose | Soul Spec |
|-------|---------|-----------|
| 1. Quick scan | Minimal metadata for discovery/filtering | `clawsoul.json` (lightweight) |
| 2. Full read | Complete persona definition | SOUL.md body |
| 3. Deep dive | Extended references and examples | Linked files (STYLE.md, IDENTITY.md, examples/) |

This reduces token cost — agents load only the detail level they need.

#### New Fields

- **`compatibility`**: Environment requirements (minimum model, platform constraints, required extensions)
- **`allowed-tools`**: Tool access restrictions — explicitly declare which tools a soul expects or permits (e.g., `["browser", "exec", "web_search"]`)

#### Soul + Skill Bundle Support

Enable packaging a Soul with recommended Anthropic Skills, creating complete agent profiles that define both persona (WHO) and capabilities (WHAT).
