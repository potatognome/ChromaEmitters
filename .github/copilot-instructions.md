# Copilot Instructions — ChromaEmitters (Device Output Layer)

# Copilot Instructions - ChromaEmitters

Scope: this file applies only to the ChromaEmitters project.

Rules:
- Keep ChromaEmitters focused on emitter/device output concerns.
- Do not duplicate colour model logic from Core/Chromaspace or animation logic from Core/Chromagrams.
- Use config/ChromaEmitters_CONFIG.json as the primary config and config/emitters.d for overrides.
- Keep paths portable and workspace-relative. Do not introduce machine-specific absolute paths.
- Prefer imports and references that work when the workspace root is dev_local on any device.
- Enabled emitters
- Device IPs
- Authentication tokens
- Transition speeds
- Device‑specific parameters
Example
{
  "emitters": {
    "tapo_led": {
      "enabled": true,
      "device_ip": "192.168.1.50",
      "transition_ms": 50
    },
    "terminal": {
      "enabled": true
    }
  }
}



6. Override Directory
config/emitters.d/


Files inside may be:
- JSON (preferred)
- YAML (allowed for user‑authored overrides)
Overrides must merge deterministically using tUilKit’s config loader.

7. tUilKit Integration
Copilot must ensure:
- All config loading uses tUilKit’s deterministic loader
- All emitter actions use tUilKit structured logging
- All errors are audit‑friendly
- All emitter metadata is exposed to tUilKit for introspection

8. Adding New Emitters
Copilot must follow this workflow:
- Create a new emitter folder under:
src/chromaemitters/<device>/
- Implement an emitter class extending EmitterInterface
- Register it with @register_emitter
- Add a config schema (YAML)
- Add default config to ChromaEmitters_CONFIG.json
- Add tests under tests/
This ensures:
- Clean modularity
- Registry‑driven discovery
- Deterministic configuration
- Easy future expansion

9. Testing Requirements
Copilot must scaffold:
- Emitter initialization tests
- Frame rendering tests
- Config loading tests
- Registry registration tests
- Device mock tests (no real hardware required)

10. Summary
ChromaEmitters is the device output layer of Chromaspace.
It must:
- Register emitters with the Chromacore Registry
- Use ChromaEmitters_CONFIG.json as the primary config file
- Integrate with tUilKit for config + logging
- Keep emitters modular and extensible
- Support workspace‑mode and project‑root‑mode path resolution
- Provide a clean path for adding new devices
This ensures a scalable, deterministic, hardware‑agnostic output pipeline for the entire Chromaspace ecosystem.
