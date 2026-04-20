- [[Data Types]]
## 1. The Core Concept: What is an Array?

A **Variable** is like a single box. An **Array** is like a **row of lockers** or a **train of carriages**. It allows you to store multiple pieces of data under a single name.

- **Definition:** An array is a data structure that holds a collection of items (elements), usually of the same data type.
    
- **Why use them?** Imagine a game with 100 players. Instead of creating 100 variables (`player1`, `player2`, etc.), you create one array called `players`.
    

---

## 2. Key Terminology

To master arrays, students must understand these three terms:

1. **Element:** An individual item stored in the array.
    
2. **Index:** The "address" or position of an element.
    
    - **CRITICAL:** In programming, we almost always start counting at **0**.
        
3. **Length:** The total number of items in the array.
    

### The "Off-By-One" Rule

Because we start at 0, the index of the **last** item is always **Length - 1**.

> **Example:** In an array of 5 items, the indexes are `0, 1, 2, 3, 4`.

---

## 3. Basic Operations (CRUD)

Most exam boards require students to know how to perform these actions:

|**Action**|**Example Logic (Pseudocode)**|**Result**|
|---|---|---|
|**Create**|`fruits = ["Apple", "Banana", "Cherry"]`|A new array is born.|
|**Read**|`print(fruits[0])`|Outputs "Apple".|
|**Update**|`fruits[1] = "Blueberry"`|"Banana" is replaced.|
|**Length**|`len(fruits)`|Returns 3.|

---

## 4. Iterating Through Arrays (KS4)

The most powerful thing about arrays is using a **FOR Loop** to look at every item automatically. This is called **traversing**.

**Python Example:**

Python

```
high_scores = [85, 92, 78, 99]

for score in high_scores:
    print("The score is:", score)
```

---

## 5. 2D Arrays (The Grid)

For KS4/GCSE, students need to understand **Two-Dimensional Arrays**. Think of this as an array _inside_ an array, or a **spreadsheet/coordinate grid**.

- To access a value, you need two coordinates: `array[row][column]`.
    
- **Analogy:** A cinema seating plan or a Tic-Tac-Toe board.
    

**Example:**

Python

```
# A 3x3 Grid
board = [
    ["X", "O", "X"],
    ["O", "X", "O"],
    ["X", " ", "O"]
]

print(board[0][1]) # Accesses Row 0, Column 1 -> Outputs "O"
```

---

## 6. Classroom Activity: "The Human Array"

1. Line up 5 students at the front of the class.
    
2. Give each student a piece of paper with a "Value" (e.g., a random number).
    
3. **The Index Challenge:** Ask the class: "Who is at index 0?" "Who is at index 4?"
    
4. **The Update:** Tell the student at index 2 to swap their paper with a new value.
    
5. **The Search:** Ask a student to "loop" through the line (start at 0 and move one by one) to find the highest number.
    

---

## 7. Common Pitfalls to Watch For

- **Out of Bounds Error:** Trying to access an index that doesn't exist (e.g., `fruits[10]` when the list only has 3 items).
    
- **Mixing Data Types:** While Python allows it, many languages (like C# or Java) require all items in an array to be the same type (e.g., all Integers).
    
- **Confusing Index vs. Value:** Students often confuse the _position_ (Index 2) with the _data_ inside it ("Cherry").
    

Would you like a set of pseudocode exercises for your students to practice searching and sorting these arrays?