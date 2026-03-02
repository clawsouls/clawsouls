# Changelog

All notable changes to the Soul Spec will be documented in this file.

## [0.5.1] - 2026-02-28

### Added
- `safety.laws` section — Asimov-inspired hierarchical safety laws for embodied agents
  - Priority-based law system (0 = highest, humanity protection → self-preservation)
  - Each law includes `id`, `priority`, `law` text, and optional `override` conditions
- SoulScan rules SEC100–SEC102 for safety law validation
  - SEC100: Warn if embodied soul missing `safety.laws`
  - SEC101: Warn if embodied soul missing critical (priority ≤ 1) safety laws
  - SEC102: Error if persona files contradict declared safety laws

## [0.5.0] - 2026-02-15

### Added
- `environment` field for embodied agent context (indoor, outdoor, mixed, any)
- `interactionMode` array (voice, gesture, touch-screen, text, haptic)
- `hardwareConstraints` object (mobility, sensors, actuators, compute, battery)
- `safety.physical` object (maxSpeed, emergencyStop, collisionAvoidance, softExterior)
- Progressive disclosure: minimal soul.json works, advanced fields optional
- Fallback instructions support for graceful degradation
- Cross-modal persona consistency validation

## [0.4.0] - 2026-01-20

### Added
- `specVersion` field required in soul.json
- Namespace format: `owner/name` for package identification
- License allowlist enforcement (MIT, Apache-2.0, CC-BY-4.0, etc.)

### Changed
- `specVersion` is now mandatory — packages without it are rejected

## [0.3.0] - 2025-12-01

### Added
- Initial public Soul Spec release
- Core fields: name, version, description, license, tags
- SOUL.md and IDENTITY.md persona file conventions
- Basic SoulScan security scanning (prompt injection, secrets, XSS)
