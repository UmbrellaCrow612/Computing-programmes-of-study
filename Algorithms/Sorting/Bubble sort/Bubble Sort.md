
Links: and previous knowledge required:
- [[Data Types]]
- [[Operators & Expressions]]
- [[Booleans]]
- [[For loops]]
- [[variables]]
- [[Arrays]]
- [[Functions]]
- [[IF statements]]
- [[Algorithm]]
- [[Programming language]]
- [[SECONDARY national curriculum Computing KS3 and KS4#Understand several key algorithms that reflect computational thinking]]
- [Slides](https://docs.google.com/presentation/d/e/2PACX-1vTSp8CBPSSGQh9yOuA1sYlANsliD2yVNSj84uk49wxl13vp217cc7azz2d3i0Qjuf4nurp3sN3zmIrU/pub?start=true&loop=true&delayms=10000)

## Learning Objectives

### KS3 Objectives (Ages 11-14)

By the end of this lesson, students will be able to:

| Objective                                                                                                | Level         |
| -------------------------------------------------------------------------------------------------------- | ------------- |
| Explain bubble sort in plain English as a method of sorting by comparing and swapping neighbouring items | Knowledge     |
| Demonstrate how bubble sort works using physical movement or number cards                                | Application   |
| Trace through a bubble sort manually to show how the largest value "bubbles" to the end each pass        | Understanding |
| Count the number of swaps and passes required to sort a small list                                       | Analysis      |
| Write a simple algorithm for bubble sort in pseudocode or plain English                                  | Synthesis     |

### KS4 Objectives (Ages 14-16)

By the end of this lesson, students will be able to:

| Objective                                                                              | Level         |
| -------------------------------------------------------------------------------------- | ------------- |
| Describe bubble sort as an iterative algorithm that makes repeated passes until sorted | Knowledge     |
| Implement bubble sort in code (e.g., JavaScript/Python)                                | Application   |
| Explain why bubble sort has O(n²) time complexity in the worst and average cases       | Understanding |
| Identify the best-case scenario (already sorted list) and its O(n) complexity          | Analysis      |
| Compare bubble sort's efficiency to other sorting algorithms (merge sort, quick sort)  | Evaluation    |

## Timing Guidelines

### KS3 Lesson (50-60 minutes)

| Section              | Time   | Activity                                                       |
| -------------------- | ------ | -------------------------------------------------------------- |
| Introduction         | 5 min  | Hook: "How would you sort these numbers?" — show unsorted list |
| Explanation          | 10 min | Teach the concept using the "bubbling" analogy                 |
| **Practical Demo**   | 15 min | **Card shuffle activity** with students or number cards        |
| Guided Practice      | 15 min | Count the swaps task (worksheet or whiteboard)                 |
| Independent Practice | 10 min | Write the algorithm in plain English                           |
| Plenary              | 5 min  | Review: "When should you use bubble sort?"                     |

### KS4 Lesson (60-70 minutes)

| Section | Time | Activity |
|---------|------|----------|
| Recap/Introduction | 5 min | Quick review: "What's the problem with bubble sort for large datasets?" |
| Explanation | 10 min | Formal definition, passes, swaps, and the `swapped` flag optimisation |
| Practical Demo | 10 min | Card shuffle with focus on counting comparisons and passes |
| Code Implementation | 15 min | Live coding or students implement bubble sort in JavaScript/Python |
| Complexity Analysis | 15 min | Discuss O(n²), best case O(n), compare to other algorithms |
| Discussion & Tasks | 10-15 min | Discussion questions table + "When should you use bubble sort?" |

## Differentiation Tips

| Support                                                     | Challenge                                                          |
| ----------------------------------------------------------- | ------------------------------------------------------------------ |
| Provide partially completed algorithms for the writing task | Ask students to implement the `swapped` optimisation if not shown  |
| Use fewer numbers (5-6) for the card demo                   | Research and present on why bubble sort is rarely used in practice |
| Pair students for the practical demo                        | Modify the code to sort in descending order                        |

# What is bubble sort ?

## KS3

> Bubble sort is a way of sorting a list by repeatedly comparing two neighbouring items and swapping them if they're in the wrong order. You keep doing this until the whole list is sorted.

## KS4

> Bubble sort is a sorting algorithm that works by making repeated passes through a list, comparing each pair of adjacent elements and swapping them if they are in the wrong order. Each pass guarantees that the next largest unsorted value moves into its correct position. The algorithm stops when a full pass completes with no swaps, indicating the list is fully sorted.
# Visual demo

## KS3 & KS4

- [Visual demo](https://www.youtube.com/watch?v=Cq7SMsQBEUw)

# Practical Demo 

## The Card / Number Card Shuffle

**What you need:** 8–10 students, or large number cards (or sticky notes with numbers written on them)
### Setup

Get 8 students to stand in a line, each holding a card with a random number (e.g. 5, 2, 8, 1, 9, 3, 7, 4). Tell the class the goal is to sort them from smallest to largest ,but they can **only compare two neighbours at a time**.
### The Demo

**Round 1 — walk along the line:**

- Start at the left. Compare students 1 & 2 - if the left number is bigger, they **swap places** (physically move).
- Move one step right. Compare students 2 & 3. Swap if needed.
- Keep going to the end of the line.
- Point out: "The biggest number has now **bubbled** to the end!"

**Round 2 — repeat, but stop one early:**

- Do the same again, but this time ignore the last person (already sorted).
- Another large number bubbles to its correct place.

**Keep going** until no swaps happen in a full pass — the line is sorted!
### How to Make it Engaging

- **Sorted students sit down** (or hold up a green card) so the class can visually see the sorted section growing
- **Add a "swap sound"**  students clap when they swap
- **Time it** then ask "how many comparisons did that take?" and discuss efficiency
-  **Ask the class to predict** whether a swap will happen before each comparison

### Discussion Questions KS4

| Question                                                | Concept it teaches                 |
| ------------------------------------------------------- | ---------------------------------- |
| "How many passes did we need?"                          | Understanding iterations           |
| "What's the best case — if the list is already sorted?" | Best case O(n)                     |
| "What if we had 100 students instead of 8?"             | Scalability / O(n²)                |
| "Can you think of a faster way?"                        | Leads into merge sort / quick sort |

# Tasks

## KS3 & KS4

- **Count the swaps**:  How many swaps did it take? 

> Number set: 7 2 1 4 0 3
> Number set: 1  2 4 3 1 3
> Number set: 3 3 4 4 1 1 4

- **Write the steps** Write a set of instructions (an algorithm) for bubble sort in plain English, as if you were explaining it to someone who had never heard of it.

- When should you use bubble sort ?

# Code

## JavaScript

Run the code via node js via cli, for example copy this make a file called `bubble sort.js` paste it in and run it with `node ./bubble sort.js`

```js
function bubbleSort(array) {
  const length = array.length;
  for (let pass = 0; pass < length - 1; pass++) {
    let swapped = false;
    for (let index = 0; index < length - 1 - pass; index++) {
      if (array[index] > array[index + 1]) {
        let temporary = array[index];
        array[index] = array[index + 1];
        array[index + 1] = temporary;
        swapped = true;
      }
    }
    if (!swapped) break;
  }
  return array;
}

// Example
console.log(bubbleSort([5, 2, 8, 1, 9, 3, 7, 4]));
// Output: [1, 2, 3, 4, 5, 7, 8, 9]
```

## Key Vocabulary

| Term       | KS3 definition                          | KS4 definition                                                     |
| ---------- | --------------------------------------- | ------------------------------------------------------------------ |
| Algorithm  | A set of step-by-step instructions      | A precise, finite sequence of instructions to solve a problem      |
| Sorting    | Putting items in order                  | Arranging data into a defined sequence                             |
| Pass       | One trip along the whole list           | One full iteration through the unsorted portion of the list        |
| Swap       | Two items switching places              | Exchanging the position of two adjacent elements                   |
| Comparison | Checking which of two numbers is bigger | Evaluating two elements against a condition                        |
| Efficiency | How fast or slow an algorithm is        | A measure of time/space complexity, expressed using Big O notation |
| O(n²)      | —                                       | The number of operations grows with the square of the input size   |