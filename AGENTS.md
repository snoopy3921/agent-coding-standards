# AGENTS.md

## Purpose

This repository provides reusable coding standards and development guidelines for Codex across multiple programming languages.

## Instructions

- Read the applicable language conventions before writing or modifying code.
- Follow the repository's formatting and documentation standards.
- Prefer simple, explicit, maintainable implementations.
- Make minimal, focused changes. Avoid unnecessary abstractions and unrelated refactoring.
- Preserve existing APIs, ABIs, binary protocols, hardware contracts, and behavior unless explicitly requested otherwise.
- Document public APIs and handle errors explicitly.
- Build and run relevant tests when possible. Never claim unexecuted tests passed.

## Standards

| Scope | Reference |
|---|---|
| C / C++ | `languages/c-cpp/conventions.md` |
| C / C++ documentation | `languages/c-cpp/doxygen.md` |
| C / C++ formatting | `languages/c-cpp/.clang-format` |
| Architecture | `guidelines/architecture.md` |
| Testing | `guidelines/testing.md` |
| Documentation | `guidelines/documentation.md` |

For Python, Rust, and other languages, use their corresponding standards under `languages/` when available.

## Workflow

1. Inspect relevant code and interfaces.
2. Read applicable conventions.
3. Implement the smallest correct change.
4. Format and test affected files.
5. Report changes and verification results.