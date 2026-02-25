# ClawSouls Package Spec v0.5

## soul.json

```json
{
  "specVersion": "0.5",
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
    "models": ["anthropic/*", "openai/*"],
    "frameworks": ["openclaw", "clawdbot", "zeroclaw", "cursor"]
  },
  "allowedTools": ["browser", "exec", "web_search", "github"],
  "recommendedSkills": [
    { "name": "github", "version": ">=1.0.0", "required": false },
    { "name": "healthcheck", "required": true }
  ],
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
  "disclosure": {
    "summary": "Infrastructure-obsessed DevOps engineer with strong CI/CD opinions."
  },
  "deprecated": false,
  "repository": "https://github.com/clawsouls/souls"
}
```

---

## Changes from v0.3

### New Fields

| Field | Type | Description |
|-------|------|-------------|
| `compatibility.frameworks` | string[] | Compatible agent frameworks (e.g., `"openclaw"`, `"clawdbot"`, `"zeroclaw"`, `"cursor"`) |
| `compatibility.minTokenContext` | number | Minimum context window (tokens) needed to load the full soul |
| `allowedTools` | string[] | Tools this soul expects or permits (e.g., `["browser", "exec"]`) |
| `recommendedSkills` | object[] | Recommended skills with version and required/optional flag |
| `disclosure.summary` | string | One-line summary for Level 1 progressive disclosure (max 200 chars) |
| `deprecated` | boolean | Whether this soul is deprecated |
| `supersededBy` | string | `owner/name` of the replacement soul (used with `deprecated: true`) |

### Deprecated Fields

| Field | Status | Reason | Migration |
|-------|--------|--------|-----------|
| `modes` | **Deprecated** | No framework currently consumes this field. Declared since v0.2 but never implemented in any runtime. Removing to reduce spec surface. | Remove from soul.json. If needed in future, will be re-introduced with runtime support. |
| `interpolation` | **Deprecated** | Same as `modes` — no runtime implementation exists. Theoretical feature without practical adoption. | Remove from soul.json. |
| `skills` | **Deprecated** | Replaced by `recommendedSkills` which supports version constraints and required/optional semantics. | Migrate `"skills": ["a", "b"]` → `"recommendedSkills": [{"name": "a"}, {"name": "b"}]`. Tools accept both formats for backward compatibility. |

### Enhanced Fields

| Field | Change | Reason |
|-------|--------|--------|
| `compatibility.openclaw` | Now validated by SoulScan + CLI install | Was declared but never checked. v0.4 adds actual version comparison. |
| `compatibility.models` | Remains optional, hint-only | Cannot be enforced (user chooses their model), but useful for discovery and recommendations. Warning-level in SoulScan. |

---

## Required Fields

| Field | Type | Description |
|-------|------|-------------|
| `specVersion` | string | Spec version. Valid: `"0.3"`, `"0.4"`, `"0.5"` |
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
| `compatibility.openclaw` | string | Minimum OpenClaw version (semver range) |
| `compatibility.models` | string[] | Recommended models (glob patterns) |
| `compatibility.frameworks` | string[] | Compatible agent frameworks |
| `compatibility.minTokenContext` | number | Minimum context window in tokens |
| `allowedTools` | string[] | Expected/permitted tools |
| `recommendedSkills` | object[] | Skills with `name`, `version?`, `required?` |
| `files.identity` | string | Path to IDENTITY.md |
| `files.agents` | string | Path to AGENTS.md |
| `files.heartbeat` | string | Path to HEARTBEAT.md |
| `files.style` | string | Path to STYLE.md |
| `files.userTemplate` | string | Path to USER template |
| `files.avatar` | string | Path to avatar image |
| `examples` | object | Calibration examples (`good`, `bad`) |
| `disclosure.summary` | string | One-line summary for quick-scan discovery (max 200 chars) |
| `deprecated` | boolean | Mark soul as deprecated |
| `supersededBy` | string | Replacement soul (`owner/name`) |
| `repository` | string | Source repository URL |

---

## Progressive Disclosure

v0.4 formalizes the 3-level progressive disclosure pattern, aligned with Anthropic's Skill design:

| Level | Purpose | What to Load |
|-------|---------|-------------|
| **Level 1 — Quick Scan** | Discovery, filtering, marketplace browsing | `soul.json` only (`disclosure.summary` for instant context) |
| **Level 2 — Full Read** | Agent loads persona for active use | `SOUL.md` + `IDENTITY.md` |
| **Level 3 — Deep Dive** | Extended behavior, calibration, style | `AGENTS.md`, `STYLE.md`, `HEARTBEAT.md`, `examples/` |

**Rationale**: Token budgets matter. A marketplace listing doesn't need AGENTS.md. An agent switching between souls benefits from Level 1 caching. Progressive disclosure reduces cost without losing depth.

The `disclosure.summary` field provides a self-contained persona hint that agents can use without parsing SOUL.md.

---

## Multi-Framework Compatibility

The `compatibility.frameworks` field declares which agent frameworks this soul works with.

Known framework identifiers:
- `openclaw` — OpenClaw (Claude Code, etc.)
- `clawdbot` — Clawdbot
- `zeroclaw` — ZeroClaw
- `cursor` — Cursor
- `windsurf` — Windsurf
- `continue` — Continue.dev

**Semantics**: If omitted, the soul is assumed compatible with any SOUL.md-consuming framework. If specified, it's a recommendation — not a hard restriction.

**Rationale**: ClawSouls positions itself as "for any SOUL.md-compatible agent." This field makes that explicit at the spec level, enabling framework-specific filtering on the registry.

---

## Allowed Tools

The `allowedTools` field declares which tools a soul expects to function properly.

```json
"allowedTools": ["browser", "exec", "web_search", "github"]
```

**Semantics**:
- **Informational**: Frameworks are not required to enforce this. It's a transparency signal.
- **SoulScan integration**: SoulScan can cross-reference `allowedTools` with actual tool usage in AGENTS.md/SOUL.md to detect undeclared tool expectations or excessive tool requests.
- **Security angle**: A "writing assistant" soul requesting `exec` and `browser` is suspicious. SoulScan flags this.

---

## Recommended Skills

Replaces the v0.3 `skills: string[]` field.

```json
"recommendedSkills": [
  { "name": "github", "version": ">=1.0.0", "required": false },
  { "name": "healthcheck", "required": true }
]
```

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| `name` | string | Yes | Skill identifier |
| `version` | string | No | Semver range constraint |
| `required` | boolean | No | Default `false`. If `true`, the soul may not function properly without this skill. |

**Backward compatibility**: Tools MUST accept the legacy `"skills": ["a", "b"]` format, treating each entry as `{ "name": "a", "required": false }`.

---

## Soul Lifecycle

### Deprecation

```json
{
  "deprecated": true,
  "supersededBy": "TomLeeLive/senior-devops-v2"
}
```

- Registry shows a deprecation banner
- CLI `install` warns but doesn't block
- `supersededBy` links to the replacement (optional)

---

## Allowed Licenses

Same as v0.3. Permissive licenses only:

- `Apache-2.0`, `MIT`, `BSD-2-Clause`, `BSD-3-Clause`
- `CC-BY-4.0`, `CC0-1.0`, `ISC`, `Unlicense`

Copyleft (`GPL-*`, `AGPL-*`, `LGPL-*`) and restrictive Creative Commons (`CC-BY-NC-*`, `CC-BY-ND-*`) are blocked.

---

## File Descriptions

Same as v0.3. See [Soul Spec v0.3 — File Descriptions](./soul-spec-v0.3.md#file-descriptions).

---

## Embodied Agents (Robotics / IoT)

Soul Spec extends naturally to embodied agents — robots, IoT devices, and physical AI systems that interact with the real world. The same persona package that defines a chatbot's personality can define a robot's interaction character.

### New Optional Fields

| Field | Type | Description |
|-------|------|-------------|
| `environment` | string | Deployment context. Values: `"virtual"` (default), `"embodied"`, `"hybrid"` |
| `interactionMode` | string | Primary interaction modality. Values: `"text"`, `"voice"`, `"multimodal"`, `"gesture"` |
| `hardwareConstraints` | object | Physical hardware capabilities and limitations |
| `safety.physical` | object | Physical safety rules for embodied agents |

### Environment Field

```json
{
  "environment": "embodied"
}
```

- `"virtual"` — Text/chat-based agent (default, backward compatible)
- `"embodied"` — Physical robot, kiosk, or IoT device
- `"hybrid"` — Operates in both virtual and physical contexts

If omitted, defaults to `"virtual"`. Existing souls are unaffected.

### Interaction Mode

```json
{
  "interactionMode": "voice"
}
```

Declares the primary interaction modality. Useful for:
- Registry filtering ("show me voice-first souls")
- Framework adaptation (voice-first = shorter responses, simpler vocabulary)
- SoulScan validation (voice-first soul shouldn't reference "click here")

### Hardware Constraints

```json
{
  "hardwareConstraints": {
    "hasDisplay": true,
    "hasSpeaker": true,
    "hasMicrophone": true,
    "hasCamera": true,
    "mobility": "mobile",
    "manipulator": false
  }
}
```

| Property | Type | Description |
|----------|------|-------------|
| `hasDisplay` | boolean | Screen available for visual output |
| `hasSpeaker` | boolean | Audio output capability |
| `hasMicrophone` | boolean | Audio input capability |
| `hasCamera` | boolean | Visual perception capability |
| `mobility` | string | `"stationary"`, `"mobile"`, `"limited"` |
| `manipulator` | boolean | Can physically manipulate objects |

**Semantics**: Informational only. Frameworks use these hints to adapt behavior (e.g., skip visual references on a speaker-only device). Not enforced.

### Physical Safety

```json
{
  "safety": {
    "physical": {
      "contactPolicy": "no-contact",
      "emergencyProtocol": "alert_operator",
      "operatingZone": "indoor",
      "maxSpeed": "0.5m/s"
    }
  }
}
```

| Property | Type | Description |
|----------|------|-------------|
| `contactPolicy` | string | `"no-contact"`, `"gentle-contact"`, `"full-contact"` |
| `emergencyProtocol` | string | Action on emergency: `"stop"`, `"alert_operator"`, `"return_home"` |
| `operatingZone` | string | `"indoor"`, `"outdoor"`, `"both"` |
| `maxSpeed` | string | Maximum movement speed (informational) |

**Rationale**: Physical safety is fundamentally different from prompt injection defense. A robot soul that permits physical contact must declare it explicitly. SoulScan can flag embodied souls without safety declarations.

### Platform Identifiers for Robotics

The `compatibility.frameworks` field now includes robotics platforms:

- `ros2` — Robot Operating System 2
- `isaac` — NVIDIA Isaac
- `webots` — Cyberbotics Webots
- `gazebo` — Open Robotics Gazebo

```json
{
  "compatibility": {
    "frameworks": ["openclaw", "ros2"]
  }
}
```

### Example: Care Companion Robot

```json
{
  "specVersion": "0.5",
  "name": "care-companion",
  "displayName": "Care Companion",
  "version": "1.0.0",
  "description": "Gentle elderly care companion with patience and warmth.",
  "author": { "name": "RoboticsLab", "github": "robotics-lab" },
  "license": "Apache-2.0",
  "tags": ["care", "elderly", "companion", "robot", "embodied"],
  "category": "robotics/care",
  "environment": "embodied",
  "interactionMode": "voice",
  "hardwareConstraints": {
    "hasDisplay": true,
    "hasSpeaker": true,
    "hasMicrophone": true,
    "hasCamera": true,
    "mobility": "mobile",
    "manipulator": false
  },
  "safety": {
    "physical": {
      "contactPolicy": "gentle-contact",
      "emergencyProtocol": "alert_operator",
      "operatingZone": "indoor",
      "maxSpeed": "0.3m/s"
    }
  },
  "compatibility": {
    "frameworks": ["ros2", "openclaw"],
    "models": ["anthropic/*", "openai/*"]
  },
  "files": {
    "soul": "SOUL.md",
    "identity": "IDENTITY.md"
  },
  "disclosure": {
    "summary": "Patient, warm elderly care companion for indoor mobile robots."
  }
}
```

### Sensor Schema

For detailed hardware description beyond boolean flags, souls can declare sensor capabilities:

```json
{
  "sensors": {
    "lidar": { "type": "2D", "range": "12m", "fov": 360 },
    "camera": { "type": "RGB-D", "resolution": "1280x720", "fps": 30 },
    "microphone": { "type": "array", "channels": 4 },
    "imu": true,
    "touchSensors": ["chest", "head"]
  }
}
```

| Property | Type | Description |
|----------|------|-------------|
| `sensors` | object | Sensor capabilities map |
| `sensors.[name]` | boolean \| object | `true` for presence-only, object for details |
| `sensors.[name].type` | string | Sensor variant |
| `sensors.[name].range` | string | Detection range |
| `sensors.[name].fov` | number | Field of view in degrees |

**Semantics**: Informational. Helps frameworks and LLMs understand what the robot can perceive, enabling appropriate behavioral adaptation (e.g., don't reference visual cues for a robot without camera).

### Actuator Capabilities

Extends the basic `manipulator: boolean` with structured actuator descriptions:

```json
{
  "actuators": {
    "locomotion": { "type": "differential-drive", "maxSpeed": "1.0m/s" },
    "arm": { "type": "6DOF", "payload": "2kg", "reach": "0.5m" },
    "gripper": { "type": "parallel", "force": "10N" },
    "head": { "dof": 2, "range": { "pan": 180, "tilt": 60 } },
    "expression": { "type": "LED-matrix", "resolution": "8x8" }
  }
}
```

| Property | Type | Description |
|----------|------|-------------|
| `actuators` | object | Actuator capabilities map |
| `actuators.locomotion` | object | Movement system |
| `actuators.arm` | object | Manipulator arm specs |
| `actuators.gripper` | object | End-effector specs |
| `actuators.head` | object | Head movement (pan/tilt) |
| `actuators.expression` | object | Facial/emotional display hardware |

**Rationale**: A persona designed for a robot with expressive LED eyes behaves differently than one for a voice-only speaker. Actuator declarations let the LLM adapt behavioral output to physical capabilities.

### ROS2 Integration Pattern

For `ros2` framework compatibility, Soul Spec maps to ROS2 concepts:

```
soul.json          → ROS2 package manifest (package.xml)
SOUL.md            → System prompt for LLM node
IDENTITY.md        → Robot namespace / TF frame identity
safety.physical    → Safety controller parameters
sensors            → Sensor topic subscriptions
actuators          → Action server capabilities
```

**Recommended ROS2 node structure:**
```
/robot_soul_loader       — Reads soul package, configures LLM
/robot_personality_node  — Publishes personality-aware responses
/safety_monitor          — Enforces safety.physical constraints
```

Soul packages can be distributed via both ClawSouls registry and ROS2 package managers. The `soul.json` manifest provides all metadata needed for either ecosystem.

### Backward Compatibility

All embodied fields are optional. Existing virtual souls require zero changes. The `environment` field defaults to `"virtual"` when omitted.

### Academic References

This extension is informed by recent research demonstrating that consistent robot personality significantly improves interaction quality and task performance:

- "LLM-based Robot Personality Simulation and Cognitive System" (Nature Scientific Reports, 2025)
- "Robots with Attitudes: Influence of LLM-Driven Robot Personalities" (arXiv 2512.06910, 2025)
- "Making Social Robots Adaptable by a Marketplace for Interaction Characters" (Frontiers in Robotics and AI, 2025)
- "ROS-LLM: A ROS Framework for Embodied AI with Task Feedback" (arXiv 2406.19741, 2024)

---

## Security Considerations

Same as v0.3, with additions:

- **`allowedTools` cross-validation**: SoulScan checks if declared tools match actual tool usage in persona files.
- **`recommendedSkills` audit**: Excessive required skills may indicate dependency on specific system access.
- **Framework spoofing**: `compatibility.frameworks` is self-declared and not verified. Trust but verify via SoulScan.
- **Embodied safety audit**: SoulScan flags embodied souls (`environment: "embodied"`) that lack `safety.physical` declarations. Physical agents without explicit safety rules are a risk.
- **Contact policy validation**: Souls with `contactPolicy: "full-contact"` require explicit justification in SOUL.md. SoulScan warns on missing rationale.

---

## Changelog

### v0.5 (2026-02-24)
- Added Embodied Agents section (`environment`, `interactionMode`, `hardwareConstraints`, `safety.physical`)
- Added robotics platform identifiers (`ros2`, `isaac`, `webots`, `gazebo`)
- SoulScan embodied safety audit rules (contact policy validation)
- Academic references for robotics persona research (4 papers)

### v0.4 (2026-02-20)
- Added `compatibility.frameworks` for multi-framework support
- Added `compatibility.minTokenContext` for token budget hints
- Added `allowedTools` for tool transparency
- Added `recommendedSkills` (object[]) replacing `skills` (string[])
- Added `disclosure.summary` for progressive disclosure Level 1
- Added `deprecated` / `supersededBy` for soul lifecycle
- Deprecated `modes`, `interpolation` (no runtime implementation)
- Deprecated `skills` (replaced by `recommendedSkills`)
- `compatibility.openclaw` now actively validated by SoulScan + CLI

### v0.3 (2026-02-16)
- Added `specVersion` field (required for new souls)
- Renamed `clawsoul.json` → `soul.json`
- Publish confirmation requirement (CLI + web)
- License allowlist enforcement

### v0.2 (2026-02-13) — *Internal development spec*
- Added STYLE.md, examples, modes, interpolation, skills
- **Note**: v0.2 was an internal iteration. Not supported for new publications.

### v0.1 (2026-02-12) — *Internal development spec*
- Initial spec: soul.json, file structure, categories, CLI, security
- **Note**: v0.1 was the initial internal prototype. Not supported for new publications.
