# [Radix Sort – Data Structures and Algorithms Tutorials](https://www.geeksforgeeks.org/radix-sort/)

Radix Sort is a non-comparative sorting algorithm that works by sorting the elements digit by digit, starting from the least significant digit (LSD) or the most significant digit (MSD). The key idea is to process the digits of the numbers from right to left (or left to right) and sort the numbers based on each digit's place value.

## Radix Sort Algorithm - LSD Approach

**1. Identify the Maximum Number:**
   - Determine the maximum number in the array to figure out the number of digits in the largest number. This helps in deciding the number of passes required.

**2. Initialize Place Value:**
   - Start with the least significant digit (units place) and move to more significant digits (tens, hundreds, etc.).

**3. Perform Stable Sort for Each Digit:**
   - For each digit place, use a stable sorting algorithm (like Counting Sort) to sort the elements based on the current digit.

**4. Repeat Until All Digits Are Processed:**
   - Move to the next digit place and repeat the sorting until all digit places have been processed.

**5. Result:**
   - After processing all digit places, the array will be sorted.

## Example of Radix Sort

Let's sort the array `[170, 45, 75, 90, 802, 24, 2, 66]` using the LSD Radix Sort approach.

**1. Identify Maximum Number:**
   - The maximum number is `802`. It has 3 digits, so we need to perform 3 passes.

**2. Initialize Place Value:**
   - Start with the units place (1s place).

**3. Sort by Units Place (Digit 1):**
   - Extract the units digit of each number.
   - Apply Counting Sort based on the units digit.
   
   After sorting by the units place, the array becomes:
   ```
   [170, 90, 802, 45, 75, 24, 66, 2]
   ```

**4. Sort by Tens Place (Digit 10):**
   - Extract the tens digit of each number.
   - Apply Counting Sort based on the tens digit.

   After sorting by the tens place, the array becomes:
   ```
   [170, 45, 75, 802, 24, 66, 90, 2]
   ```

**5. Sort by Hundreds Place (Digit 100):**
   - Extract the hundreds digit of each number.
   - Apply Counting Sort based on the hundreds digit.

   After sorting by the hundreds place, the array becomes:
   ```
   [2, 24, 45, 66, 75, 90, 170, 802]
   ```

**6. Result:**
   - The array is now fully sorted.

## Radix Sort Implementation in Python

```python
def countingSort(arr, exp):
    n = len(arr)
    output = [0] * n
    count = [0] * 10

    # Calculate count of elements
    for i in range(n):
        index = (arr[i] // exp) % 10
        count[index] += 1

    # Calculate cumulative count
    for i in range(1, 10):
        count[i] += count[i - 1]

    # Place the elements in sorted order
    i = n - 1
    while i >= 0:
        index = (arr[i] // exp) % 10
        output[count[index] - 1] = arr[i]
        count[index] -= 1
        i -= 1

    for i in range(n):
        arr[i] = output[i]

def radixSort(arr):
    # Find the maximum number
    max_val = max(arr)

    # Apply counting sort to sort elements based on place value
    exp = 1
    while max_val // exp > 0:
        countingSort(arr, exp)
        exp *= 10

# Example usage
arr = [170, 45, 75, 90, 802, 24, 2, 66]
radixSort(arr)
print("Sorted array:", arr)
```

## Complexity

- **Time Complexity:** \(O(n \cdot k)\), where \(n\) is the number of elements and \(k\) is the number of digits in the maximum number. Counting Sort is applied \(k\) times.
- **Space Complexity:** \(O(n + k)\), due to the additional space used for counting and output arrays.
