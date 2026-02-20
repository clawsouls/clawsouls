# ClawSouls Package Spec

Latest version: **v0.4** ([soul-spec-v0.4.md](./soul-spec-v0.4.md))

## Version History

| Version | Date | Status | Description |
|---------|------|--------|-------------|
| [v0.4](./soul-spec-v0.4.md) | 2026-02-20 | **Current** | Multi-framework compatibility, allowedTools, recommendedSkills, progressive disclosure, soul lifecycle |
| [v0.3](./soul-spec-v0.3.md) | 2026-02-16 | Supported | specVersion field, soul.json rename, license allowlist |
| [v0.2](./soul-spec-v0.2.md) | 2026-02-13 | Internal | STYLE.md, examples, modes, interpolation |
| [v0.1](./soul-spec-v0.1.md) | 2026-02-12 | Internal | Initial spec prototype |

> **Note**: v0.1 and v0.2 were internal development specs used during early prototyping. They are not supported for new publications. The registry requires **v0.3 or higher**.

---

## Design Decisions (v0.4)

Transparent record of what changed and why, based on internal review (2026-02-20).

### Why deprecate `modes` and `interpolation`?

Both fields were introduced in v0.2 as theoretical features — "supported interaction modes" and "interpolation strategy for uncovered topics." After 8 days of production use and 80+ published souls:

- **Zero frameworks consume these fields.** No runtime (OpenClaw, Clawdbot, ZeroClaw) reads or acts on `modes` or `interpolation`.
- **Zero soul creators used them meaningfully.** Most souls either omit them or copy the example values.
- **Spec surface cost.** Every unused field adds cognitive load for creators and validation complexity for tools.

**Decision**: Deprecated in v0.4. If a runtime implements mode-switching in the future, the fields can be re-introduced with actual semantics.

### Why rename `skills` → `recommendedSkills`?

The v0.2 `skills: string[]` had two problems:

1. **No version constraints.** A soul depending on `github` skill v2.0 features would silently break with v1.0.
2. **No required/optional semantics.** Is `github` essential or nice-to-have? No way to express this.

`recommendedSkills` (object array) solves both. Backward compatibility is preserved — tools accept the legacy `string[]` format.

### Why add `compatibility.frameworks`?

ClawSouls positions itself as "for any SOUL.md-compatible agent." The `frameworks` field makes this explicit:

- **Discovery**: Registry can filter "souls that work with Cursor" or "souls optimized for OpenClaw."
- **Positioning**: Reinforces that Soul Spec is framework-agnostic, not locked to one vendor.
- **Practical**: Some souls use framework-specific features (e.g., OpenClaw heartbeats). Declaring this helps users choose.

### Why add `allowedTools`?

Security transparency. A "writing assistant" soul that requests `exec` and `browser` access is suspicious. `allowedTools` enables:

- SoulScan cross-validation (declared vs. actual tool usage in SOUL.md/AGENTS.md)
- User-facing trust signals on the registry
- Future: framework-enforced tool sandboxing

### Why add `disclosure.summary`?

Token economics. Loading a full SOUL.md (often 2-5KB) just to display a card in a marketplace is wasteful. `disclosure.summary` gives agents and UIs a self-contained persona hint without parsing markdown.

### Why add `deprecated` / `supersededBy`?

Soul lifecycle management. As creators iterate, old versions need clear retirement paths. Without this, abandoned souls accumulate in the registry with no signal to users.

---

## Minimum Version Policy

The ClawSouls registry enforces **specVersion ≥ 0.3** for all new publications.

- `v0.3` and `v0.4` souls are accepted.
- `v0.1` and `v0.2` souls are rejected at publish time with a migration guide.
- Tools SHOULD warn if `specVersion` is missing but MUST NOT reject during read (backward compatibility for local use).

---

## Roadmap (Post-v0.4)

- **Runtime mode support**: If a framework implements mode-switching, re-introduce `modes` with defined semantics
- **Soul + Skill bundles**: Package a Soul with recommended Skills for one-click complete agent setup
- **Signed souls**: Cryptographic signature for tamper-proof distribution
- **Dependency resolution**: Auto-install `recommendedSkills` with version resolution
