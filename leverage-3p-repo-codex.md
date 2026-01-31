You are modifying an existing Rust project to integrate the InputBot library from:
https://github.com/obv-mikhail/InputBot

Goal
- Use InputBot to handle global keyboard and mouse hotkeys and to simulate input events.
- Expose these capabilities through our existing input abstraction instead of sprinkling InputBot calls everywhere.

Project context
- Project root: <PROJECT_ROOT>
- Main crate: <CRATE_NAME>
- Our input abstraction:
  - Trait: <PATH::TO::InputServiceTrait>
  - Current implementations live in: <src/input/*.rs or similar>
- Target OSes: Windows 10+ and Linux (Debian/Ubuntu-based) with X11. No macOS support required for now.

Dependency strategy
- Do NOT add InputBot as a Git submodule or vendor the source manually.
- Pull it as a Cargo dependency from crates.io and pin the version for reproducibility:
  
  In Cargo.toml:
    [dependencies]
    inputbot = "=0.6.0"

- Additionally, document the exact InputBot version in our README and in a third-party notices file:
  - README section: "Input dependencies"
  - File: docs/THIRD_PARTY.md

Artifacts and APIs to reuse from InputBot
- Use the public APIs from the crate root:
  - KeybdKey
  - MouseButton
  - KeySequence
  - inputbot::handle_input_events
- Follow the event model shown in the InputBot README and examples:
  - One-time setup of bindings (KeybdKey::bind, MouseButton::bind)
  - Single global event loop via inputbot::handle_input_events(false)
- Do NOT copy code out of `examples/`; adapt patterns but call the library through its public API.

Integration boundaries
- Create a new module dedicated to InputBot:
  - Path: src/input/inputbot_backend.rs
- Implement a single, well-defined backend type there that plugs into our abstraction:
  - Struct name: InputBotBackend
  - Implement trait: <PATH::TO::InputServiceTrait>
- Rules:
  - All direct InputBot calls (KeybdKey::*, MouseButton::*, handle_input_events, etc.) must live only in `inputbot_backend.rs`.
  - Other parts of the codebase must depend only on the trait, never on InputBot types.
  - If new methods are needed on the trait, design them in terms of generic “input events” instead of InputBot-specific types.

Platform, permissions, and environment expectations
- InputBot is cross-platform for Windows and Linux. We only target:
  - Windows: standard desktop environment.
  - Linux: Debian/Ubuntu with X11, not Wayland.
- On Linux, ensure that the build and runtime assumptions match the upstream README:
  - Use system packages: libx11-dev, libxtst-dev, libudev-dev, libinput-dev.
  - Note in comments and docs that running with global input access may require elevated permissions (e.g., sudo with libinput).
- Do NOT introduce non-portable OS APIs outside `inputbot_backend.rs`.
- Provide a compile-time or runtime check that:
  - Gracefully disables InputBot functionality on unsupported platforms (e.g., headless servers, no display).
  - Surfaces a clear error message or log line, not a panic.

License and provenance
- InputBot is MIT-licensed. Respect this:
  - Do not copy large chunks of source from the InputBot repo into our project.
  - Rely on the published crate and its public APIs instead.
- Add an entry to docs/THIRD_PARTY.md:
  - Name: InputBot
  - URL: https://github.com/obv-mikhail/InputBot
  - License: MIT
  - Version: 0.6.0
- In Cargo.toml, add a comment next to the dependency noting:
  - Why we’re using InputBot.
  - Link to the upstream repo.

Behavior, failure modes, and fallbacks
- InputBot may not function correctly in:
  - Headless environments.
  - Containers without access to a display or input devices.
- Implement a capability check during startup of InputBotBackend:
  - If the environment is clearly unsupported, log a warning and disable global hotkeys instead of crashing.
  - Expose a boolean or status enum from InputBotBackend that tells the rest of the app whether global input is available.
- Design the rest of the app so that:
  - When InputBot is unavailable, features that depend on global hooks are either hidden or no-ops with clear user feedback.
  - The app remains functional for non-input-bot-dependent paths.

Testing and validation
- Add tests or test harnesses to exercise the integration:
  - Unit tests for InputBotBackend to verify:
    - Correct wiring between our trait methods and InputBot bindings.
    - That the feature-flag / capability detection logic returns expected values in mocked environments.
  - Integration test (where feasible) that simulates:
    - Registering one or more hotkeys.
    - Triggering the associated callbacks in a controlled setup (e.g., by abstracting over InputBot so that parts can be mocked).
- Wire these tests into the existing CI:
  - Ensure tests that require real input devices are either:
    - Marked with a feature flag (e.g., `--features inputbot_integration_tests`).
    - Or annotated in a way that lets CI skip them if running in an unsupported environment.

Refactoring expectations
- If our existing input system already has an implementation (e.g., a stub or different backend), do the following:
  - Keep the existing implementation as a fallback.
  - Introduce a simple runtime switch or configuration flag:
    - `InputProvider = "inputbot" | "noop"` (or similar).
- Ensure that:
  - The choice of backend is configured in exactly one place (e.g., configuration module or main.rs).
  - Switching providers does not require code changes, only config changes.

Deliverables
- Updated Cargo.toml with pinned InputBot dependency and comments.
- New module: src/input/inputbot_backend.rs implementing <PATH::TO::InputServiceTrait>.
- Minimal refactoring of the rest of the codebase to route global hotkey behavior through the trait instead of direct platform calls.
- Tests added/updated:
  - Unit tests for InputBotBackend.
  - Integration or harness tests wired into CI with clear feature flags.
- Documentation updates:
  - README section describing InputBot usage, supported platforms, and permission notes.
  - docs/THIRD_PARTY.md entry for InputBot.

Respond with:
- A summary of the changes you will make.
- The relevant code diffs or new files.
- Any assumptions you made that should be confirmed about the project structure, trait definitions, or target platforms.

---

You are modifying an existing Rust project to integrate the InputBot library from:
https://github.com/obv-mikhail/InputBot

Goal
- Use InputBot to handle global keyboard and mouse hotkeys and to simulate input events.
- Expose these capabilities through our existing input abstraction instead of sprinkling InputBot calls everywhere.

Project context
- Project root: <PROJECT_ROOT>
- Main crate: <CRATE_NAME>
- Our input abstraction:
  - Trait: <PATH::TO::InputServiceTrait>
  - Current implementations live in: <src/input/*.rs or similar>
- Target OSes: Windows 10+ and Linux (Debian/Ubuntu-based) with X11. No macOS support required for now.

Dependency strategy
- Do NOT add InputBot as a Git submodule or vendor the source manually.
- Pull it as a Cargo dependency from crates.io and pin the version for reproducibility:
  
  In Cargo.toml:
    [dependencies]
    inputbot = "=0.6.0"

- Additionally, document the exact InputBot version in our README and in a third-party notices file:
  - README section: "Input dependencies"
  - File: docs/THIRD_PARTY.md

Artifacts and APIs to reuse from InputBot
- Use the public APIs from the crate root:
  - KeybdKey
  - MouseButton
  - KeySequence
  - inputbot::handle_input_events
- Follow the event model shown in the InputBot README and examples:
  - One-time setup of bindings (KeybdKey::bind, MouseButton::bind)
  - Single global event loop via inputbot::handle_input_events(false)
- Do NOT copy code out of `examples/`; adapt patterns but call the library through its public API.

Integration boundaries
- Create a new module dedicated to InputBot:
  - Path: src/input/inputbot_backend.rs
- Implement a single, well-defined backend type there that plugs into our abstraction:
  - Struct name: InputBotBackend
  - Implement trait: <PATH::TO::InputServiceTrait>
- Rules:
  - All direct InputBot calls (KeybdKey::*, MouseButton::*, handle_input_events, etc.) must live only in `inputbot_backend.rs`.
  - Other parts of the codebase must depend only on the trait, never on InputBot types.
  - If new methods are needed on the trait, design them in terms of generic “input events” instead of InputBot-specific types.

Platform, permissions, and environment expectations
- InputBot is cross-platform for Windows and Linux. We only target:
  - Windows: standard desktop environment.
  - Linux: Debian/Ubuntu with X11, not Wayland.
- On Linux, ensure that the build and runtime assumptions match the upstream README:
  - Use system packages: libx11-dev, libxtst-dev, libudev-dev, libinput-dev.
  - Note in comments and docs that running with global input access may require elevated permissions (e.g., sudo with libinput).
- Do NOT introduce non-portable OS APIs outside `inputbot_backend.rs`.
- Provide a compile-time or runtime check that:
  - Gracefully disables InputBot functionality on unsupported platforms (e.g., headless servers, no display).
  - Surfaces a clear error message or log line, not a panic.

License and provenance
- InputBot is MIT-licensed. Respect this:
  - Do not copy large chunks of source from the InputBot repo into our project.
  - Rely on the published crate and its public APIs instead.
- Add an entry to docs/THIRD_PARTY.md:
  - Name: InputBot
  - URL: https://github.com/obv-mikhail/InputBot
  - License: MIT
  - Version: 0.6.0
- In Cargo.toml, add a comment next to the dependency noting:
  - Why we’re using InputBot.
  - Link to the upstream repo.

Behavior, failure modes, and fallbacks
- InputBot may not function correctly in:
  - Headless environments.
  - Containers without access to a display or input devices.
- Implement a capability check during startup of InputBotBackend:
  - If the environment is clearly unsupported, log a warning and disable global hotkeys instead of crashing.
  - Expose a boolean or status enum from InputBotBackend that tells the rest of the app whether global input is available.
- Design the rest of the app so that:
  - When InputBot is unavailable, features that depend on global hooks are either hidden or no-ops with clear user feedback.
  - The app remains functional for non-input-bot-dependent paths.

Testing and validation
- Add tests or test harnesses to exercise the integration:
  - Unit tests for InputBotBackend to verify:
    - Correct wiring between our trait methods and InputBot bindings.
    - That the feature-flag / capability detection logic returns expected values in mocked environments.
  - Integration test (where feasible) that simulates:
    - Registering one or more hotkeys.
    - Triggering the associated callbacks in a controlled setup (e.g., by abstracting over InputBot so that parts can be mocked).
- Wire these tests into the existing CI:
  - Ensure tests that require real input devices are either:
    - Marked with a feature flag (e.g., `--features inputbot_integration_tests`).
    - Or annotated in a way that lets CI skip them if running in an unsupported environment.

Refactoring expectations
- If our existing input system already has an implementation (e.g., a stub or different backend), do the following:
  - Keep the existing implementation as a fallback.
  - Introduce a simple runtime switch or configuration flag:
    - `InputProvider = "inputbot" | "noop"` (or similar).
- Ensure that:
  - The choice of backend is configured in exactly one place (e.g., configuration module or main.rs).
  - Switching providers does not require code changes, only config changes.

Deliverables
- Updated Cargo.toml with pinned InputBot dependency and comments.
- New module: src/input/inputbot_backend.rs implementing <PATH::TO::InputServiceTrait>.
- Minimal refactoring of the rest of the codebase to route global hotkey behavior through the trait instead of direct platform calls.
- Tests added/updated:
  - Unit tests for InputBotBackend.
  - Integration or harness tests wired into CI with clear feature flags.
- Documentation updates:
  - README section describing InputBot usage, supported platforms, and permission notes.
  - docs/THIRD_PARTY.md entry for InputBot.

Respond with:
- A summary of the changes you will make.
- The relevant code diffs or new files.
- Any assumptions you made that should be confirmed about the project structure, trait definitions, or target platforms.

