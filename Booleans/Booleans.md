Related knowledge:

- [[Byte]]

# What is a Boolean ? 

> A value that is either True or False  nothing else

Computers make decisions by asking yes/no questions. A Boolean is how we store the answer. It can only ever be one of two things: True or False. Think of a light switch it's either on or off, never both.

Booleans appear everywhere in everyday life.

Each of these is a Boolean question, the answer is always True or False:

- Is it raining ?
- Is the player alive ?
- Is the score greater than 10 ?

## Representation on a machine

| Boolean | Binary | Voltage State |
| ------- | ------ | ------------- |
| `true`  | `1`    | HIGH          |
| `false` | `0`    | LOW           |

### Memory Storage: The Smallest Addressable Unit

| Aspect                       | Details                                                                                             |
| ---------------------------- | --------------------------------------------------------------------------------------------------- |
| **Minimum addressable unit** | **1 byte** (8 bits)                                                                                 |
| **Boolean storage**          | Typically uses **1 full byte** per Boolean                                                          |
| **Why?**                     | Memory is byte-addressable; addressing individual bits would require complex bit-masking operations |

### Programming Language Implementations

| Language                  | Boolean Storage                    | Notes                                                         |
| ------------------------- | ---------------------------------- | ------------------------------------------------------------- |
| **C/C++**                 | `bool`: 1 byte; can use bit-fields | `std::vector<bool>` packs 8 bools per byte                    |
| **TypeScript/JavaScript** | Implementation-dependent           | V8 engine uses tagged pointers; booleans are immediate values |
| **Python**                | 28+ bytes per bool                 | Objects with overhead; `True`/`False` are singletons          |
| **Java**                  | 1 byte (`boolean`)                 | Arrays use 1 byte per element                                 |
| **Rust**                  | 1 byte (`bool`)                    | Can use bit-flags for packing                                 |

### Boolean Operations at the Hardware Level

| Operation | Machine Instruction | How It Works                           |
| --------- | ------------------- | -------------------------------------- |
| **AND**   | `AND` opcode        | Bitwise: `1 AND 1 = 1`, else `0`       |
| **OR**    | `OR` opcode         | Bitwise: `0 OR 0 = 0`, else `1`        |
| **NOT**   | `NOT`/`XOR` with 1  | Flips all bits                         |
| **XOR**   | `XOR` opcode        | `1 XOR 1 = 0`, `0 XOR 0 = 0`, else `1` |
