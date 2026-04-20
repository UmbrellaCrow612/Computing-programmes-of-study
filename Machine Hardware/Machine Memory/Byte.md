
Related knowledge:

- [[Bit]]

## What Are Bytes?

A **byte** is a `group of 8 bits`. It's the standard unit for measuring computer memory and storage.

| Term     | Definition              | Analogy                        |
| -------- | ----------------------- | ------------------------------ |
| **Bit**  | Smallest unit (0 or 1)  | A single light switch (on/off) |
| **Byte** | 8 bits grouped together | 8 light switches in a row      |

### Why 8 Bits?

The byte became standard because:

- **8 is a power of 2** (2³ = 8)  computers work in binary
- **Enough combinations**  8 bits can represent 256 different values (2⁸)
- **Perfect for text**  covers all English letters, numbers, and symbols

### What Can One Byte Store?

| Value Range            | Example Use                         |
| ---------------------- | ----------------------------------- |
| **0 to 255**           | Whole numbers                       |
| **One character**      | 'A', '7', '\$' (ASCII/UTF-8)        |
| **Small colour value** | One shade of red, green, or blue    |
| **8 Boolean flags**    | 8 true/false values packed together |

## Example

| File/Item              | Size   | What It Means       |
| ---------------------- | ------ | ------------------- |
| Text message character | 1 byte | 'H' = `01001000`    |
| Small image            | 50 KB  | 50,000 bytes        |
| MP3 song               | 5 MB   | 5,000,000 bytes     |
| RAM in a laptop        | 8 GB   | 8,000,000,000 bytes |

### Signed vs Unsigned Bytes

| Type         | Range       | How It Works                                  |
| ------------ | ----------- | --------------------------------------------- |
| **Unsigned** | 0 to 255    | All 8 bits used for value                     |
| **Signed**   | -128 to 127 | Leftmost bit is sign (0=positive, 1=negative) |

### Character Encoding: ASCII and Beyond

| Encoding           | Bytes per Character | Coverage                              |
| ------------------ | ------------------- | ------------------------------------- |
| **ASCII**          | 1 byte              | 128 English characters                |
| **Extended ASCII** | 1 byte              | 256 characters (adds accents/symbols) |
| **UTF-8**          | 1-4 bytes           | All world languages, emojis           |
| **UTF-16**         | 2-4 bytes           | Alternative Unicode encoding          |


### Memory Addressing

The **byte is the smallest addressable unit** — you cannot request a single bit from memory:

```plain
Memory address → Points to 1 byte (8 bits)
0x0000 → [byte 0]
0x0001 → [byte 1]
0x0002 → [byte 2]
```

This is why Booleans typically use 1 byte even though they only need 1 bit.

## Units of Measurement

| Unit            | Size        | Real-World Equivalent |
| --------------- | ----------- | --------------------- |
| 1 Byte (B)      | 8 bits      | One character         |
| 1 Kilobyte (KB) | 1,024 bytes | Half page of text     |
| 1 Megabyte (MB) | 1,024 KB    | Small photo/MP3       |
| 1 Gigabyte (GB) | 1,024 MB    | 30 minutes of video   |
| 1 Terabyte (TB) | 1,024 GB    | 250,000 photos        |

## Exam-Style Questions

**KS3:** _How many different values can be stored in one byte?_  
**Answer:** 256 (2⁸)

**KS4:** _Convert the signed byte `11111110` to decimal._  
**Answer:** -2 (using two's complement)