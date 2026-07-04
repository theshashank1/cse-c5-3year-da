# NumPy Practice —  Take-Home

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
