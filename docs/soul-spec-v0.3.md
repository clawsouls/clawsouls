# ClawSouls Package Spec v0.3

## soul.json

Metadata file for a Soul package.

```json
{
  "specVersion": "0.3",
  "name": "senior-devops-engineer",
  "displayName": "Senior DevOps Engineer",
  "version": "1.0.0",
  "description": "Infrastructure-obsessed DevOps engineer with strong opinions on CI/CD, monitoring, and incident response.",
  "author": {
    "name": "TomLee",
    "github": "TomLeeLive"
  },
  "license": "Apache-2.0",
  "tags": ["devops", "infrastructure", "cicd", "monitoring"],
  "category": "work/devops",
  "compatibility": {
    "openclaw": ">=2026.2.0",
    "models": ["anthropic/*", "openai/*"]
  },
  "files": {
    "soul": "SOUL.md",
    "identity": "IDENTITY.md",
    "agents": "AGENTS.md",
    "heartbeat": "HEARTBEAT.md",
    "style": "STYLE.md",
    "userTemplate": "USER_TEMPLATE.md",
    "avatar": "avatar/avatar.png"
  },
  "examples": {
    "good": "examples/good-outputs.md",
    "bad": "examples/bad-outputs.md"
  },
  "modes": ["default", "chat", "tweet", "essay", "idea"],
  "interpolation": "cautious",
  "skills": [
    "github",
    "healthcheck"
  ],
  "repository": "https://github.com/clawsouls/souls"
}
```

---

## Required Fields

| Field | Type | Description |
|-------|------|-------------|
| `specVersion` | string | Spec version this soul targets. Valid: `"0.1"`, `"0.2"`, `"0.3"` |
| `name` | string | Unique identifier (kebab-case) |
| `displayName` | string | Display name |
| `version` | semver | Version |
| `description` | string | One-line description (max 160 chars) |
| `author` | object | Creator info |
| `license` | string | SPDX license identifier (see [Allowed Licenses](#allowed-licenses)) |
| `tags` | string[] | Search tags (max 10) |
| `category` | string | Category path |
| `files.soul` | string | Path to SOUL.md |

## Optional Fields

| Field | Type | Description |
|-------|------|-------------|
| `compatibility.openclaw` | string | Minimum OpenClaw version |
| `compatibility.models` | string[] | Recommended models (glob patterns) |
| `files.identity` | string | Path to IDENTITY.md |
| `files.agents` | string | Path to AGENTS.md |
| `files.heartbeat` | string | Path to HEARTBEAT.md |
| `files.style` | string | Path to STYLE.md |
| `files.userTemplate` | string | Path to USER template |
| `files.avatar` | string | Path to avatar image |
| `examples` | object | Calibration examples |
| `examples.good` | string | Path to good output examples |
| `examples.bad` | string | Path to bad output anti-patterns |
| `modes` | string[] | Supported interaction modes |
| `interpolation` | string | Interpolation strategy for uncovered topics |
| `skills` | string[] | Recommended Skill list |
| `repository` | string | Source repository URL |

---

## specVersion Field

The `specVersion` field declares which version of the ClawSouls spec this soul was built for.

- **Required** for new souls (v0.3+)
- **Backward compatible**: If missing, tools infer the version from file naming conventions:
  - `soul.json` present → assumed v0.3
  - `clawsoul.json` present → assumed v0.2
  - Neither → assumed v0.1
- Valid values: `"0.1"`, `"0.2"`, `"0.3"`
- Tools SHOULD warn if `specVersion` is missing but MUST NOT reject the package (for backward compatibility)

---

## Changes from v0.2

- **Renamed** `clawsoul.json` → `soul.json` (breaking change, with backward compat in tooling)
- **Added** `specVersion` field (required for new souls)
- **Roadmap**: compatibility field, allowed-tools, soul+skill bundles

---

## File Descriptions

### SOUL.md (Required)
The core identity file. Defines who the agent *is*.

Contents:
- **Worldview** — Core beliefs, values, principles
- **Expertise** — Knowledge domains, depth levels
- **Opinions** — Actual positions on topics (not neutral hedging)
- **Personality** — Temperament, humor, quirks
- **Boundaries** — What the persona refuses or avoids

### IDENTITY.md (Optional)
Lightweight identity metadata: name, emoji, avatar path, creature type, vibe.

### AGENTS.md (Optional)
Operational instructions: how the agent behaves in sessions, memory management, safety rules, group chat behavior.

### STYLE.md (Optional)
Writing style guide. Defines *how* the persona communicates.

### HEARTBEAT.md (Optional)
Periodic background task configuration.

### examples/ Directory (Optional)
Calibration material for voice matching (good-outputs.md, bad-outputs.md).

---

## Interaction Modes

Souls can declare supported modes. See v0.2 spec for full mode documentation.

## Interpolation Strategy

When asked about topics not explicitly covered in SOUL.md. See v0.2 spec for details.

## Category System

Same as v0.2.

## CLI Commands

Same as v0.2.

## Security Considerations

Same as v0.2.

---

## Allowed Licenses

The ClawSouls registry only accepts souls with **permissive licenses**:

- `Apache-2.0`, `MIT`, `BSD-2-Clause`, `BSD-3-Clause`
- `CC-BY-4.0`, `CC0-1.0`, `ISC`, `Unlicense`

**Copyleft licenses are not permitted** (`GPL-*`, `AGPL-*`, `LGPL-*`). Additionally, `CC-BY-NC-*` (non-commercial) and `CC-BY-ND-*` (no-derivatives) are blocked because commercial use and modification are core to the soul workflow.

Unknown licenses (not in the allowlist, not matching blocked patterns) will produce a warning but are not rejected.

## Changelog

### v0.3 (2026-02-16)
- Added `specVersion` field (required for new souls)
- Renamed `clawsoul.json` → `soul.json`
- Publish confirmation requirement (CLI + web)
- Platform license disclaimer in Terms of Service
- License allowlist enforcement (permissive only)

### v0.2 (2026-02-13)
- Added STYLE.md, examples, modes, interpolation, skills

### v0.1 (2026-02-12)
- Initial spec: soul.json, file structure, categories, CLI, security
