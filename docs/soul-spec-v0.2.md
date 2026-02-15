# ClawSouls Package Spec v0.2

## soul.json

Metadata file for a Soul package.

```json
{
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
| `name` | string | Unique identifier (kebab-case) |
| `displayName` | string | Display name |
| `version` | semver | Version |
| `description` | string | One-line description (max 160 chars) |
| `author` | object | Creator info |
| `license` | string | SPDX license identifier |
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

### STYLE.md (Optional, New in v0.2)
Writing style guide. Defines *how* the persona communicates.

Contents:
- **Sentence structure** — Short/long, simple/complex, fragments allowed?
- **Vocabulary** — Preferred words, banned words, jargon level
- **Tone** — Formal/casual, warm/dry, direct/diplomatic
- **Formatting** — Emoji usage, markdown style, list preference
- **Rhythm** — Pacing, paragraph length, punctuation habits
- **Anti-patterns** — Specific phrases or patterns to never use

Example:
```markdown
# STYLE.md

## Sentence Structure
Short sentences. Fragments welcome. Never start with "I think" — just state it.

## Vocabulary
- Say "ship" not "deploy"
- Say "broken" not "suboptimal"
- No corporate speak: "synergy", "leverage", "circle back"

## Tone
Direct. Opinionated. Occasional dry humor. Never apologetic.

## Anti-patterns
- ❌ "That's a great question!"
- ❌ "I'd be happy to help with that."
- ❌ "Some might argue..."
```

### HEARTBEAT.md (Optional)
Periodic background task configuration.

### examples/ Directory (Optional, New in v0.2)
Calibration material for voice matching.

#### examples/good-outputs.md
Curated examples that demonstrate the voice done right. The agent should match this tone, structure, and personality.

#### examples/bad-outputs.md
Anti-patterns — what the persona should *never* sound like. Helps the agent avoid generic AI assistant voice.

Example:
```markdown
# Bad Outputs

## Generic Assistant
❌ "Sure! I'd be happy to help you with that. Here are some options:"
Why it's bad: Servile, no personality, could be anyone.

## Over-qualified
❌ "While there are many perspectives on this, some might say..."
Why it's bad: This persona has opinions. Use them.

## Breaking Character
❌ "As an AI, I don't have personal opinions, but..."
Why it's bad: Never break character. You ARE this persona.
```

---

## Interaction Modes (New in v0.2)

Souls can declare supported modes. The agent adapts its behavior per mode.

| Mode | Description |
|------|-------------|
| `default` | Standard interaction. Match STYLE.md voice. |
| `chat` | Conversational, exploratory, can be longer. Push back, disagree, have takes. |
| `tweet` | Short, punchy. Single idea. No hashtags/emojis unless in STYLE.md. |
| `essay` | Long-form, more nuance, structured thinking. Same voice, more room. |
| `idea` | Generate novel ideas. Contrarian but defensible. Thesis → reasoning → implications. |
| `code` | Code-focused. Terse explanations, opinionated on patterns/tools. |
| `mentor` | Teaching mode. Patient but not condescending. Socratic when appropriate. |

Custom modes can be defined in SOUL.md. The `modes` array in soul.json declares which modes the soul supports.

---

## Interpolation Strategy (New in v0.2)

When asked about topics not explicitly covered in SOUL.md, the agent needs a strategy.

| Strategy | Behavior |
|----------|----------|
| `bold` | Extrapolate freely from worldview. Prefer interesting takes over safe ones. |
| `cautious` | Extrapolate from adjacent positions. Flag uncertainty in-character. |
| `strict` | Only respond to explicitly covered topics. Redirect others in-character. |

**Source Priority (all strategies):**
1. Explicit positions in SOUL.md → use directly
2. Covered in examples/ → reference for grounding
3. Adjacent to known positions → extrapolate from worldview
4. Completely novel → depends on strategy setting

---

## Category System

```
work/
  engineering/frontend
  engineering/backend
  engineering/fullstack
  engineering/gamedev
  devops
  data
  pm
  writing
creative/
  design
  storytelling
  music
education/
  programming
  language
  science
lifestyle/
  assistant
  health
  cooking
enterprise/
  support
  onboarding
  review
```

---

## CLI Commands

```bash
# Install a soul
clawsouls install senior-devops-engineer

# Search for souls
clawsouls search "game dev"

# List installed souls
clawsouls list

# Apply a soul to current agent
clawsouls use senior-devops-engineer

# Restore previous soul
clawsouls restore

# Create a new soul package
clawsouls init

# Publish a soul
clawsouls publish
```

---

## Installation Behavior

When `clawsouls install <name>` runs:

1. Download package from ClawSouls registry
2. Save to `~/.openclaw/souls/<name>/`
3. On `clawsouls use <name>`:
   - SOUL.md → copy to workspace
   - IDENTITY.md → copy to workspace
   - AGENTS.md → merge into workspace (preserve user settings)
   - STYLE.md → copy to workspace (if exists)
   - examples/ → copy to workspace (if exists)
   - USER_TEMPLATE.md → copy to USER.md only if USER.md doesn't exist
   - avatar → copy to workspace
4. Backup existing files to `~/.openclaw/souls/_backup/`

### Protected Files (Never Overwritten)
- USER.md
- MEMORY.md
- TOOLS.md
- memory/*.md

---

## Security Considerations

- Soul packages must contain only markdown files and images (no executable code)
- AGENTS.md external action rules require user confirmation before applying
- Automatic scan on publish (prompt injection detection)
- Report & flagging system
- STYLE.md and examples/ are instruction-only, no code execution
- Interpolation strategy limits hallucination scope

---

## Changelog

### v0.2 (2026-02-13)
- Added `files.style` — STYLE.md for writing style guides
- Added `examples` — good/bad output calibration files
- Added `modes` — interaction mode declarations
- Added `interpolation` — strategy for uncovered topics
- Added source priority rules
- Translated spec to English
- Expanded file descriptions with examples

### v0.1 (2026-02-12)
- Initial spec: soul.json, file structure, categories, CLI, security
