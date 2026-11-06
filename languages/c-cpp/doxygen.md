# C/C++ Doxygen Conventions

## 1. General Rules

- Use Doxygen-compatible comments for public APIs.
- Use `/** ... */` for documentation blocks.
- Write documentation in English.
- Keep descriptions concise, precise, and technically accurate.
- Document behavior and contracts rather than repeating implementation details.
- Place API documentation in header files.
- Do not duplicate documentation in implementation files.
- Keep comments synchronized with code changes.

## 2. Documentation Requirements

| Element | Requirement |
|---|---|
| Public functions | Required |
| Public classes and structs | Required |
| Public enums | Required |
| Public macros | Required when behavior is non-obvious |
| Public constants | Required when meaning or units are unclear |
| Private functions | Optional |
| Local variables | Not required |

## 3. Doxygen Tags

Use the following tags when applicable:

| Tag | Purpose |
|---|---|
| `@brief` | Short description |
| `@param` | Function parameter |
| `@tparam` | Template parameter |
| `@return` | Return value |
| `@retval` | Specific return code |
| `@note` | Important information |
| `@warning` | Safety or critical constraints |
| `@pre` | Preconditions |
| `@post` | Postconditions |
| `@see` | Related APIs |
| `@deprecated` | Deprecated APIs |

Do not add unnecessary tags to trivial declarations.

## 4. Function Documentation

Document parameters, return values, error conditions, and relevant constraints.

```cpp
/**
 * @brief Encodes a binary protocol frame.
 *
 * @param type Message type identifier.
 * @param sequence Frame sequence number.
 * @param payload Pointer to the input payload.
 * @param payload_length Payload length in bytes.
 * @param output Destination buffer.
 * @param output_capacity Destination buffer capacity in bytes.
 * @param output_length Receives the encoded frame length in bytes.
 *
 * @retval true Frame encoded successfully.
 * @retval false Invalid arguments or insufficient buffer capacity.
 *
 * @note No dynamic memory is allocated.
 * @pre Input and output buffers must not overlap.
 */
bool encode_frame(uint8_t type, uint16_t sequence, const uint8_t *payload,
                  uint16_t payload_length, uint8_t *output,
                  std::size_t output_capacity, std::size_t *output_length);
```

For pointer parameters, specify nullability and ownership when relevant.

## 5. Struct and Class Documentation

Document the purpose of the type and important field semantics.

```cpp
/**
 * @brief Represents a decoded protocol frame header.
 *
 * @note This structure is not the serialized wire representation.
 */
struct frame_header_t {
    uint8_t type;             /**< Message type identifier. */
    uint16_t payload_length;  /**< Payload length in bytes. */
    uint16_t sequence;        /**< Frame sequence number. */
};
```

Avoid documenting obvious fields unless their meaning, units, or constraints matter.

## 6. Enum Documentation

```cpp
/**
 * @brief Operating states of a motor controller.
 */
enum class MotorState : uint8_t {
    Disabled, /**< Motor output is disabled. */
    Enabled,  /**< Motor accepts control commands. */
    Fault     /**< Motor requires fault recovery. */
};
```

Document enum values when they define externally visible behavior.

## 7. Constants and Macros

Use brief inline Doxygen comments for constants whose meaning is not immediately clear.

```cpp
constexpr uint32_t CONTROL_TIMEOUT_MS = 100; /**< Maximum command age in milliseconds. */
```

For function-like macros, document parameters and side effects when necessary.

Prefer `constexpr` constants and inline functions over macros in C++ when appropriate.

## 8. Error and Safety Documentation

Use `@warning` for behavior that may affect hardware or system safety.

```cpp
/**
 * @brief Enables motor output.
 *
 * @retval true Motor output was enabled.
 * @retval false Safety conditions were not satisfied.
 *
 * @warning The caller must ensure that the actuator is initialized.
 */
bool enable_motor();
```

Document error codes, recovery requirements, and failure side effects when applicable.

## 9. Units and Ranges

Always specify units for physical quantities when they are not unambiguous.

```cpp
/**
 * @brief Sets the motor velocity target.
 *
 * @param velocity_rad_s Target angular velocity in radians per second.
 * @return True if accepted; otherwise false.
 */
bool set_velocity(float velocity_rad_s);
```

Document valid ranges and special values when relevant.

## 10. Implementation Comments

Implementation files should contain comments only when they clarify:

- Non-obvious algorithms.
- Hardware constraints.
- Timing or concurrency requirements.
- Workarounds and their reasons.
- Safety-critical decisions.

Avoid unnecessary comments such as:

```cpp
// Increment counter
counter++;
```

## 11. Documentation Quality Checklist

Before completing a change:

- Public API documentation is present.
- All documented parameters match the declarations.
- Return values and error behavior are accurate.
- Units, valid ranges, and pointer ownership are clear.
- Safety-critical constraints are documented.
- No obsolete or duplicated comments remain.