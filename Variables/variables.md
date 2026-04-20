## 1. The Core Concepts

In programming, we need to store data so the computer can use it later. We do this using **Identifiers** (names) that point to a location in the computer's memory.

### What is a Variable?

A **Variable** is a named memory location used to store data that **can change** while the program is running.

- **Analogy:** Think of a variable as a **labelled cardboard box**. You can put a value inside it, but you can also take that value out and replace it with something else at any time.

### What is a Constant?

A **Constant** is a named memory location used to store data that **cannot change** once the program has started.

- **Analogy:** Think of a constant as a **glass display case**. Once the value is placed inside and the door is locked, it stays exactly as it is for the rest of the program.

## 2. Key Differences at a Glance

| **Feature**             | **Variable**                            | **Constant**                        |
| ----------------------- | --------------------------------------- | ----------------------------------- |
| **Value Change**        | Can be updated during execution.        | Remains fixed during execution.     |
| **Purpose**             | To track changing data (e.g., a score). | To store permanent data (e.g., Pi). |
| **Example**             | `user_score = 10`                       | `PI = 3.142`                        |
| **Naming (Convention)** | Often camelCase or snake_case.          | Often written in ALL_CAPS.          |
|                         |                                         |                                     |

## 3. Assignment: Giving Values a Name

We use the **Assignment Operator** ($=$) to store a value inside a variable or constant.

- **Syntax:** `identifier = value`
- **Note:** In computer science, $=$ doesn't mean "is equal to" like in math; it means **"set the value on the left to be the result of the right."**
    

> **Example in Python:**
> 
> Python
> 
> ```
> player_name = "Alex"  # Variable: The name could change later
> MAX_LIVES = 3         # Constant: The maximum lives allowed stays the same
> ```

## 4. Why Use Constants? (KS4 Focus)

Students often ask: _"Why not just use variables for everything?"_ Using constants is a mark of a "robust" programmer for three reasons:

1. **Readability:** It is easier to understand what `VAT_RATE` means than just seeing the number `0.2` scattered throughout a program.
2. **Safety:** If you accidentally try to write code that changes a constant, the computer will throw an error, preventing bugs.
3. **Efficiency:** If the value needs to change (e.g., the tax rate goes up next year), you only have to change it in **one place** at the top of your code.
## 5. Check Your Understanding

### Task A: Spot the Type

Look at the following data items for a racing game. Decide if they should be stored as a **Variable** or a **Constant**:

1. The number of laps completed by the player.
2. The value of Gravity ($9.81$).
3. The player’s current speed.
4. The name of the game ("Super Turbo Racer").

### Task B: Code Repair (Python)

The following code has a logic error. A programmer tried to change a constant. What will happen?

Python

```
PI = 3.14
radius = 5

# The programmer tries to update PI by mistake
PI = 4.0 

area = PI * (radius ** 2)
print(area)
```

---

## Quick Reference Summary

- **Variable:** Use when data is dynamic (Score, Time, Level).
- **Constant:** Use when data is static (Gravity, Math constants, Settings).
- **Identifier:** The unique name you give to your variable or constant.