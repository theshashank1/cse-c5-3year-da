# NumPy Practice — In-Class + Take-Home
### Companion to NumPy_Lecture_Notes.md and NumPy_Student_Notes.md

Two sets here, for two different moments:
- **In-Class Practice** — short, fast, meant to be solved in pairs during the session itself, right after the matching topic is taught. No answers shown inline (keeps students thinking instead of scrolling); full answer key at the end for you to reveal on the board.
- **Take-Home Practice** — longer, mixed-topic, meant to be attempted alone after class. Answers are collapsed under each question so students can self-check immediately without flipping to the end.

---

## PART 1 — In-Class Practice

Use these as pair-exercises, 3–5 minutes each, right after teaching the matching section. Don't hand out the whole sheet at once — reveal one block at a time so students can't jump ahead.

### Block A — Creating Arrays (after Section 2)
1. Convert the list `[10, 20, 30, 40]` into a NumPy array.
2. Convert `[[1,2],[3,4],[5,6]]` into a NumPy array. What shape is it?
3. What's the difference between printing a plain list of lists and printing the NumPy array made from it?

### Block B — Array Generators (after Section 3)
4. Generate every multiple of 5 from 0 to 50 using `arange`.
5. Create a 4x4 array of all zeros.
6. Create 7 evenly spaced numbers between 0 and 100 using `linspace`.
7. Create a 3x3 identity matrix.
8. In one sentence — when would you reach for `linspace` instead of `arange`?

### Block C — Random Numbers (after Section 4)
9. Generate 6 random numbers between 0 and 1.
10. Generate a 3x3 grid of random numbers from a normal distribution.
11. Generate 5 random whole numbers between 50 and 100.
12. True or false: `randn` can produce a negative number. Why or why not?

### Block D — Attributes & Methods (after Section 5)
13. Create a 1-D array of 16 numbers and reshape it into a 4x4 grid.
14. Given `arr = np.random.randint(0, 100, 15)`, find both the largest value and its index position.
15. What does `.shape` return for a 3x4 array? What about `.dtype`?
16. Why does `np.arange(10).reshape(3, 3)` throw an error?

### Block E — 1D Indexing & Broadcasting (after Sections 6–7)
17. From `arr = np.arange(0, 20)`, slice out just the values from index 5 to index 12.
18. Set the last 4 elements of a 10-element array to 0 in a single line.
19. Add 10 to every element of an array in one line — no loop.
20. `slice_of_arr = arr[2:6]` then `slice_of_arr[:] = 0` — does the original `arr` change? Why?

### Block F — 2D Indexing (after Section 8)
21. Given a 4x4 array of numbers 0–15, grab the value in row 2, column 3 — using comma notation.
22. From that same array, grab the bottom-right 2x2 corner.
23. Grab the entire second row.
24. Grab the entire third column (all rows, just column index 2).

### Block G — Fancy Indexing (after Section 9)
25. From a 6x6 array, select rows 0, 2, and 4 using fancy indexing.
26. Select rows 5, 1, and 3 — in that exact order — from the same array.

### Block H — Boolean Selection (after Section 10)
27. From `arr = np.arange(1, 21)`, select only the values greater than 10.
28. From the same array, select only values divisible by 3.
29. Select values that are both greater than 5 **and** less than 15.
30. What's wrong with writing `arr[arr > 5 and arr < 15]`? What's the fix?

### Block I — Operations (after Section 11)
31. Multiply an array of 1–10 by itself, element by element.
32. Compute the square of every element in one line, without a loop.
33. What does NumPy return for `np.array([1,0,2]) / np.array([0,0,2])`? Which positions give `nan`, which give `inf`, and why?
34. Compute the natural log of `np.arange(1, 6)`.

---

### Answer Key — In-Class Practice (for you, not the board)

```python
# 1
np.array([10, 20, 30, 40])

# 2
np.array([[1,2],[3,4],[5,6]])   # shape: (3, 2)

# 3 — talking point, no code: the array prints aligned in columns; NumPy
# already treats it as a structured grid, not just nested Python lists.

# 4
np.arange(0, 51, 5)

# 5
np.zeros((4, 4))

# 6
np.linspace(0, 100, 7)

# 7
np.eye(3)

# 8 — talking point: arange when you know the step size you want;
# linspace when you know exactly how many points you want.

# 9
np.random.rand(6)

# 10
np.random.randn(3, 3)

# 11
np.random.randint(50, 101, 5)

# 12 — True. randn samples from a normal distribution centered at 0,
# so roughly half the values it produces will be negative.

# 13
arr = np.arange(16)
arr.reshape(4, 4)

# 14
arr = np.random.randint(0, 100, 15)
arr.max()
arr.argmax()

# 15
arr = np.zeros((3, 4))
arr.shape     # (3, 4)
arr.dtype     # dtype('float64') for zeros, dtype('int64') for an int array

# 16 — 10 elements can't be reshaped into 3x3 (9 slots); the reshape
# target's total element count must exactly match the original.

# 17
arr = np.arange(0, 20)
arr[5:13]

# 18
arr = np.arange(10)
arr[-4:] = 0

# 19
arr + 10

# 20 — Yes, arr changes too. A slice is a view into the same underlying
# data, not a separate copy — use .copy() to avoid this.

# 21
arr2d = np.arange(16).reshape(4, 4)
arr2d[2, 3]

# 22
arr2d[2:, 2:]

# 23
arr2d[1]        # or arr2d[1, :]

# 24
arr2d[:, 2]

# 25
arr2d = np.arange(36).reshape(6, 6)
arr2d[[0, 2, 4]]

# 26
arr2d[[5, 1, 3]]

# 27
arr = np.arange(1, 21)
arr[arr > 10]

# 28
arr[arr % 3 == 0]

# 29
arr[(arr > 5) & (arr < 15)]

# 30 — Python's `and` isn't defined element-wise for arrays and throws
# an error. Fix: use `&` with each condition wrapped in parentheses:
# arr[(arr > 5) & (arr < 15)]

# 31
arr = np.arange(1, 11)
arr * arr

# 32
arr ** 2

# 33
# array([inf, nan, 1.])
# Position 0: 1/0 → inf (nonzero divided by zero)
# Position 1: 0/0 → nan (undefined — not a number)
# Position 2: 2/2 → 1.0 (ordinary division)

# 34
np.log(np.arange(1, 6))
```

---

## PART 2 — Take-Home Practice

20 mixed-topic questions to attempt alone, without looking at the lecture notes first. Answers are collapsed under each one — try the question fully before revealing it.

**1. Create a 1-D array containing every whole number from 1 to 30.**
<details><summary>Show answer</summary>

```python
np.arange(1, 31)
```
</details>

**2. Create a 6x6 array of all ones, then reshape nothing — just confirm its `.shape`.**
<details><summary>Show answer</summary>

```python
arr = np.ones((6, 6))
arr.shape     # (6, 6)
```
</details>

**3. Generate 15 evenly spaced numbers between -5 and 5.**
<details><summary>Show answer</summary>

```python
np.linspace(-5, 5, 15)
```
</details>

**4. Create a 5x5 identity matrix, then check its `.dtype`.**
<details><summary>Show answer</summary>

```python
arr = np.eye(5)
arr.dtype     # dtype('float64')
```
</details>

**5. Generate a 4x4 grid of random numbers from a standard normal distribution, then find the single smallest value in the whole grid.**
<details><summary>Show answer</summary>

```python
arr = np.random.randn(4, 4)
arr.min()
```
</details>

**6. Generate 20 random integers between 1 and 6 (simulating dice rolls), then count how many of them are exactly 6, using boolean selection.**
<details><summary>Show answer</summary>

```python
rolls = np.random.randint(1, 7, 20)
sixes = rolls[rolls == 6]
len(sixes)
```
</details>

**7. Create a 1-D array of 30 numbers and reshape it into a 6x5 grid. Why would `reshape(6, 6)` fail here?**
<details><summary>Show answer</summary>

```python
arr = np.arange(30).reshape(6, 5)
# reshape(6, 6) would fail because 6*6 = 36, but arr only has 30
# elements — reshape can't invent or drop data, the counts must match.
```
</details>

**8. From a random array of 25 integers between 0 and 100, find both the max value and the index position where it occurs.**
<details><summary>Show answer</summary>

```python
arr = np.random.randint(0, 100, 25)
arr.max()
arr.argmax()
```
</details>

**9. From `arr = np.arange(0, 30)`, slice out every element from index 10 to the end.**
<details><summary>Show answer</summary>

```python
arr = np.arange(0, 30)
arr[10:]
```
</details>

**10. Take a slice of an array, set all its values to 0, and explain in one sentence why the original array also changes.**
<details><summary>Show answer</summary>

```python
arr = np.arange(0, 10)
s = arr[2:6]
s[:] = 0
arr
# The original changes because a slice is a view into the same
# underlying data, not an independent copy.
```
</details>

**11. Add 50 to every element of a 1-D array of 10 numbers, in a single line.**
<details><summary>Show answer</summary>

```python
arr = np.arange(10)
arr + 50
```
</details>

**12. Build a 5x5 array of numbers 0–24. Grab the value at row 3, column 4.**
<details><summary>Show answer</summary>

```python
arr = np.arange(25).reshape(5, 5)
arr[3, 4]
```
</details>

**13. From that same 5x5 array, grab the bottom two rows entirely.**
<details><summary>Show answer</summary>

```python
arr[3:]
```
</details>

**14. From that same 5x5 array, grab the top-left 2x2 corner.**
<details><summary>Show answer</summary>

```python
arr[:2, :2]
```
</details>

**15. From a 7x7 array (numbers 0–48), use fancy indexing to select rows 6, 0, and 3, in that exact order.**
<details><summary>Show answer</summary>

```python
arr = np.arange(49).reshape(7, 7)
arr[[6, 0, 3]]
```
</details>

**16. From `arr = np.arange(1, 51)`, select only the values that are multiples of 7.**
<details><summary>Show answer</summary>

```python
arr = np.arange(1, 51)
arr[arr % 7 == 0]
```
</details>

**17. From the same array, select values that are less than 10 OR greater than 40.**
<details><summary>Show answer</summary>

```python
arr[(arr < 10) | (arr > 40)]
```
</details>

**18. Create an array of 1–10 and compute both its square root and its natural log in two separate lines.**
<details><summary>Show answer</summary>

```python
arr = np.arange(1, 11)
np.sqrt(arr)
np.log(arr)
```
</details>

**19. Create `np.array([4, 0, 9, 0])` and divide it by `np.array([2, 0, 3, 0])`. Predict the output before running it, then explain each position.**
<details><summary>Show answer</summary>

```python
a = np.array([4, 0, 9, 0])
b = np.array([2, 0, 3, 0])
a / b
# array([2., nan, 3., nan])
# Position 0: 4/2 = 2.0 — ordinary division
# Position 1: 0/0 = nan — undefined, both sides are zero
# Position 2: 9/3 = 3.0 — ordinary division
# Position 3: 0/0 = nan — same as position 1
```
</details>

**20. Without running any code — in your own words, explain why `arr[arr > 5 and arr < 20]` throws an error, and rewrite it correctly.**
<details><summary>Show answer</summary>

```python
# Python's `and` checks the truthiness of two whole objects at once,
# not element-by-element — NumPy arrays with more than one element
# can't be reduced to a single True/False, so it errors.
# Correct version, using & with each condition parenthesized:
arr[(arr > 5) & (arr < 20)]
```
</details>

---

**One line to leave students with:** if you can look at any of these 20 questions and immediately know *which section* it belongs to before writing a line of code, you've actually learned the material — not just memorized the syntax.
