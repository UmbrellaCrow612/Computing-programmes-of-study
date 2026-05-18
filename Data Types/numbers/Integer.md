To represent a number in code, we use data types that hold numeric values.

One such data type is the **integer**.

## What Is an Integer?

> An integer is zero, a positive whole number, or a negative whole number.

In other words, an integer is a **whole number** - not a fraction or decimal. Integers can be negative, zero, or positive, but they **cannot** contain fractional parts.

## When to Use Integers

Use an integer when you need to store a whole number (positive, negative, or zero).

**Examples:**
- Someone's age
- A year of birth
- Item count
- Temperature in whole degrees

## Signed vs. Unsigned Integers

Integers can be **signed** or **unsigned**:

| Type                 | Description                                  |
| -------------------- | -------------------------------------------- |
| **Signed** (default) | Can hold positive, negative, and zero values |
| **Unsigned**         | Can hold only positive values and zero       |

Most programming languages use signed integers by default.

## When to Use Signed vs. Unsigned

For most programming tasks, use the default **signed** integers.

Use **unsigned** integers only when you have a specific reason to restrict values to non-negative numbers. Common use cases include:

- **Database fields** that should never be negative (e.g., quantity in stock, auto-increment IDs)
- **Memory-sensitive applications** where you need the extra positive range (since unsigned types can store larger positive values)
- **Bit manipulation** and low-level systems programming

Using unsigned integers where negatives don't make sense can also help catch logic errors early, as attempting to store a negative value will trigger an [[Errors & exceptions]].