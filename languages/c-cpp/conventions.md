# C/C++ Coding Conventions

## 1. General Principles

- Prefer simple, explicit, readable, and maintainable code.
- Follow the C or C++ standard configured by the project.
- Avoid unnecessary abstractions, inheritance, templates, and dependencies.
- Keep changes focused. Do not refactor unrelated code.
- Preserve existing public interfaces and behavior unless explicitly requested.

## 2. Naming Conventions

| Element | Convention | Example |
|---|---|---|
| Files | `snake_case` | `motor_control.cpp` |
| Functions | `snake_case` | `read_encoder()` |
| Variables | `snake_case` | `motor_speed` |
| Struct fields | `snake_case` | `timestamp_us` |
| Namespaces | `snake_case` | `esp_link` |
| C++ classes | `PascalCase` | `MotorController` |
| C structs and typedefs | `snake_case_t` | `motor_state_t` |
| Enums | `PascalCase` or `snake_case_t` | `MotorState`, `motor_state_t` |
| Macros | `UPPER_SNAKE_CASE` | `MAX_BUFFER_SIZE` |
| Constants | `UPPER_SNAKE_CASE` | `WL_HEADER_SIZE` |

- Use descriptive names without unnecessary abbreviations.
- Prefix related APIs consistently when useful, especially in C.
- Include units in identifiers when relevant, such as `_ms`, `_us`, `_rad`, `_deg`.

## 3. Formatting

- Use the repository `.clang-format` configuration.
- Indent with 4 spaces, never tabs.
- Use braces for control-flow statements.
- Do not manually align or reformat code against the formatter.
- Use blank lines to separate logical operations.
- Avoid excessive blank lines or visual decoration.

## 4. Headers and Source Files

- Use `.h` for C headers and `.hpp` for C++ headers.
- Use `.c` for C implementations and `.cpp` for C++ implementations.
- Place public declarations in headers.
- Place nontrivial implementations in source files.
- Use header guards or `#pragma once` consistently within a project.
- Minimize header dependencies; include only what is needed.
- Keep internal functions and data private to their implementation.

## 5. Functions

- Give each function one clear responsibility.
- Prefer short functions with explicit inputs and outputs.
- Validate external inputs and handle failure conditions.
- Prefer early returns to deeply nested control flow.
- Avoid hidden side effects and unnecessary global state.
- Use `const` wherever appropriate.
- Document public function contracts using the Doxygen convention.

## 6. Data Structures and Types

- Use fixed-width integer types for hardware interfaces, binary protocols, and persisted formats.
- Use `std::size_t` or `size_t` for memory sizes and buffer lengths.
- Prefer `enum class` in C++ when type safety is useful.
- Prefer explicit initialization.
- Avoid unnecessary type casts.
- Do not depend on compiler-specific structure padding or alignment for external data formats.
- Avoid unions or bitfields for wire serialization unless their representation is explicitly controlled and verified.

## 7. Memory and Ownership

- Make resource ownership explicit.
- Prefer automatic storage and RAII in C++.
- Avoid unnecessary dynamic allocation, especially in real-time paths.
- Check buffer bounds before reading or writing.
- Avoid dangling pointers and invalid references.
- Release resources on all relevant failure paths.
- Use raw pointers for non-owning access when their lifetime contract is clear.

## 8. Error Handling

- Never silently discard errors.
- Use return values, error codes, or another consistent project-defined mechanism.
- Prefer explicit failure handling in embedded code.
- Do not use exceptions in environments where they are disabled.
- Keep error handling predictable and easy to trace.
- Avoid aborting the program for recoverable errors.

## 9. Concurrency and Embedded Systems

- Keep interrupt handlers short and deterministic.
- Avoid blocking operations and dynamic allocation in critical paths.
- Protect shared state using appropriate synchronization.
- Do not assume `volatile` provides thread synchronization.
- Respect hardware initialization and shutdown sequences.
- Preserve watchdogs, fault handling, and hardware safety constraints.
- Clearly distinguish hardware-facing code from application logic.

## 10. Binary Protocols

- Define field sizes, byte order, and valid ranges explicitly.
- Encode and decode multi-byte fields explicitly.
- Do not transmit raw C/C++ structs directly.
- Validate packet lengths and integrity before accessing payloads.
- Handle malformed and incomplete frames safely.
- Do not change protocol contracts without explicit approval.

## 11. Documentation

Follow `doxygen.md` for C/C++ documentation requirements.

- Document public APIs, contracts, units, ownership, and failure conditions.
- Explain non-obvious logic and important design decisions.
- Avoid comments that repeat the code.
- Keep documentation consistent with implementation.

## 12. Testing

- Add or update tests for changed behavior.
- Verify normal, boundary, and failure cases.
- Test serialization and parsing against known byte sequences.
- Run the configured formatter and relevant tests when possible.
- Do not claim successful verification without executing it.