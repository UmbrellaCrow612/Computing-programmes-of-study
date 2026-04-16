
A `bit` (short for binary digit) is the smallest unit of data in a computer. It's like an atom, you can't break it down further.

A bit has only two possible values:

- `0` (off / false)
- `1` (on / true)

Think of it like a light switch, it's either OFF or ON. That's it!
## Why Only 0 and 1?

Computers are made of electronic circuits with tiny switches called transistors. These switches only understand two states:

- No electricity = 0
- Electricity flowing = 1

This is called binary a number system with just two digits (0 and 1), unlike our normal decimal system which uses ten digits (0-9).

## KS3 Level: Building Up from Bits

Bits → Bytes

| Term         | Size           | What It Can Store               |
| ------------ | -------------- | ------------------------------- |
| **1 bit**    | 1 binary digit | 0 or 1 (yes/no)                 |
| **1 nibble** | 4 bits         | One hexadecimal digit           |
| **1 byte**   | **8 bits**     | One character (like 'A' or '7') |

Key fact to remember: `8 bits` = `1 byte`

A byte can represent 256 different values (0 to 255) because:
- 2⁸ = 256 possible combinations

### Real-World Examples

| Storage        | Approximate Size            |
| -------------- | --------------------------- |
| A text message | ~1-2 KB (1,000-2,000 bytes) |
| A photo        | ~2-5 MB (millions of bytes) |
| A song         | ~3-5 MB                     |
| A movie        | ~1-4 GB (billions of bytes) |

### Binary Numbers (KS3)

Here's how we count in binary vs decimal:

| Decimal | Binary |
| ------- | ------ |
| 0       | 0      |
| 1       | 1      |
| 2       | 10     |
| 3       | 11     |
| 4       | 100    |
| 5       | 101    |
| 6       | 110    |
| 7       | 111    |
| 8       | 1000   |

**Pattern:** When you run out of digits (just 0 and 1), you add another place value — just like going from 9 to 10 in decimal!

## KS4 Level: Deeper Understanding

### Binary Place Values

Each position in a binary number represents a **power of 2**:


```txt
128  64  32  16   8   4   2   1    ← Place values (2⁷ to 2⁰)
  0   1   0   1   0   1   1   0    ← Binary: 01010110 = 86 in decimal
```

Calculation: 64 + 16 + 4 + 2 = 86

### Converting Decimal to Binary

To convert 45 to binary:

1. Find the largest power of 2 that fits: **32** (2⁵)
2. 45 - 32 = 13
3. Next: **8** (2³) fits in 13
4. 13 - 8 = 5
5. Next: **4** (2²) fits in 5
6. 5 - 4 = 1
7. Next: **1** (2⁰) fits

Result: 32 + 8 + 4 + 1 = 45 → `00101101` in binary

### Negative Numbers (Two's Complement)

Computers need to represent negative numbers too. In **two's complement** (most common method):

- The **leftmost bit** indicates the sign (1 = negative, 0 = positive)
- To make a number negative: **invert all bits and add 1**

Example: Represent -5 in 8-bit two's complement

- +5 = 00000101
- Invert: 11111010
- Add 1: **11111011** = -5

### Data Types & Bit Usage

| Data Type | Bits Used          | Range/Values    |
| --------- | ------------------ | --------------- |
| Boolean   | 1 bit              | true/false      |
| Char      | 8 or 16 bits       | One character   |
| Integer   | 16, 32, or 64 bits | Whole numbers   |
| Float     | 32 or 64 bits      | Decimal numbers |

### Why Powers of 2?

Computer memory and storage use powers of 2 because of binary:

| Term            | Exact Value               | Approximate |
| --------------- | ------------------------- | ----------- |
| 1 KB (Kilobyte) | 2¹⁰ = 1,024 bytes         | ~1,000      |
| 1 MB (Megabyte) | 2²⁰ = 1,048,576 bytes     | ~1 million  |
| 1 GB (Gigabyte) | 2³⁰ = 1,073,741,824 bytes | ~1 billion  |
| 1 TB (Terabyte) | 2⁴⁰ bytes                 | ~1 trillion |


## Quick Check Questions

### KS3:

- How many bits in a byte? **(8)**
- What are the two values a bit can have? **(0 and 1)**
- What does binary 1010 equal in decimal? **(10)**

### KS4:

- Convert decimal 25 to binary **(11001)**
- What is 11111111 in decimal if unsigned? **(255)**
- What is the largest positive number in 8-bit two's complement? **(127)**