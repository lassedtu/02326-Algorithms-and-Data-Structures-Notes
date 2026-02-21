# Searching
> Given a sorted array ´A´ and number ´x´, determine if ´x´ appears in the array.

## Linear search

### Algorithm Breakdown
- Start at the beginning of the array.
- Iterate through each element `A[i]` of the array.
- Compare `A[i]` with the target value `x`.
	- If `A[i] = x`, return `true` and stop.
- If the end of the array is reached without finding `x`, return `false` and stop.

``` c
#include <stdbool.h> // For bool type
#include <stddef.h>  // For size_t

bool linearSearch(const int A[], int x, size_t n) {
    // Iterate through each element of the array
    for (size_t i = 0; i < n; i++) {
        // Compare A[i] with the target value x
        if (A[i] == x) {
            // If A[i] = x, return true and stop.
            return true;
        }
    }
    // If the end of the array is reached without finding x, return false and stop.
    return false;
}
```

### Analysis
- **Best Case**: O(1) - The target element `x` is found at the first position of the array.
- **Worst Case**: O(n) - The target element `x` is found at the last position of the array, or `x` is not present in the array. In both scenarios, the algorithm has to iterate through all `n` elements.
- **Average Case**: O(n) - On average, the algorithm will check about half of the elements.

## Binary Search

### Algorithm Breakdown
- Compare `x` to middle entry `m` in ´A´
	- if `A[m]= x` return `true` and stop
	- if `A[m] < x` continue recursively on the right half
	- if `A[m] > x` continue recursively on the left half
- If array size $\leq$ 0 return `false` and stop

``` c
#include <stdbool.h> // For bool type
#include <stddef.h>  // For size_t

bool binarySearch(const int A[], int x, int low, int high) {
    // If array size <= 0 (or search range is empty), return false and stop.
    if (low > high) {
        return false;
    }

    // Calculate the middle index
    int mid = low + (high - low) / 2;

    // Compare x to middle entry A[m]
    if (A[mid] == x) {
        // if A[m] = x return true and stop.
        return true;
    } else if (A[mid] < x) {
        // if A[m] < x continue recursively on the right half.
        return binarySearch(A, x, mid + 1, high);
    } else { // A[mid] > x
        // if A[m] > x continue recursively on the left half.
        return binarySearch(A, x, low, mid - 1);
    }
}
```

### Analysis
- **Time Complexity**: O(log n)
    - Binary search repeatedly divides the search interval in half. This logarithmic behavior means that the number of comparisons grows very slowly with the size of the array. For an array of size `n`, the maximum number of comparisons is approximately $\log_2 n$.

---
# Sorting
> Given array `A[0..n-1]` return array `B[0..n-1]` with same values as `A` but in sorted order.
## Insertion sort

### Algorithm Breakdown
- Start with unsorted array `A`
- Proceed left-to-right in `n` rounds
- Round `i`:
	- Subarray `A[0..i-1]` is sorted
	- Insert `A[i]` into `A[0..i-1]` to make `A[0..i]` sorted

``` java
public class InsertionSort {

    public static void insertionSort(int[] A) {
        // Proceed left-to-right in n rounds
        for (int i = 1; i < A.length; i++) {
            // A[0..i-1] is sorted
            int currentElement = A[i];
            int j = i - 1;

            // Insert A[i] (currentElement) into A[0..i-1]
            // Shift elements of A[0..i-1], that are greater than currentElement,
            // to one position ahead of their current position
            while (j >= 0 && A[j] > currentElement) {
                A[j + 1] = A[j];
                j--;
            }
            A[j + 1] = currentElement; /* Place currentElement 
                                          in its correct position */
            // Now A[0..i] is sorted
        }
    }
}
```

### Analysis
- **Best Case**: O(n) - When the array is already sorted. The inner `while` loop condition `A[j] > currentElement` will almost always be false, resulting in only `n-1` comparisons and no shifts.
- **Worst Case**: O(n^2) - When the array is sorted in reverse order. For each element `A[i]`, the inner `while` loop has to shift all `i` preceding elements. This leads to a sum of operations $1 + 2 + ... + (n-1)$, which is approximately $n^2/2$.
- **Average Case**: O(n^2) - On average, the inner loop will perform about half the maximum number of shifts and comparisons.

## Merge sort
> Recursive sorting via merging sorted subarrays.

### Algorithm Breakdown (Merge)
- Scan both arrays left-to-right. In each step:
	- Insert smallest of the two entries in new array
	- Move forward in array with smallest entry
	- Repeat until input arrays are exhausted

### Analysis (Merge)
- **Time Complexity**: O(n) - Where `n` is the total number of elements in the two arrays being merged. The merge operation involves a single pass through all elements of both input arrays.

### Algorithm Breakdown (Merge Sort)
- If $|A| \leq 1$, return `A`
- Otherwise:
	- Split `A` into halves
	- Sort each half recursively
	- Merge the two halves

``` Python

def merge(left, right):
    result = []
    i = 0  # Pointer for left array
    j = 0  # Pointer for right array

    # Scan both arrays left-to-right. In each step:
    # Insert smallest of the two entries in new array
    # Move forward in array with smallest entry
    while i < len(left) and j < len(right):
        if left[i] < right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1

    # Repeat until input arrays are exhausted
    # Append any remaining elements from left or right (if one array is longer)
    result.extend(left[i:])
    result.extend(right[j:])
    return result

def merge_sort(A):
    # If |A| <= 1, return A
    if len(A) <= 1:
        return A

    # Otherwise:
    # Split A into halves
    mid = len(A) // 2
    left_half = A[:mid]
    right_half = A[mid:]

    # Sort each half recursively
    left_half = merge_sort(left_half)
    right_half = merge_sort(right_half)

    # Merge the two halves
    return merge(left_half, right_half)

```

### Analysis
- **Time Complexity**: O(n log n)
    - Merge sort is a classic example of a divide and conquer algorithm.
    - The recurrence relation for merge sort is $T(n) = 2T(n/2) + O(n)$.
        - $2T(n/2)$ represents the time taken to recursively sort the two halves of the array.
        - $O(n)$ represents the time taken to merge the two sorted halves.
    - This recurrence relation resolves to O(n log n), which is consistent across best, worst, and average cases, making merge sort a very stable sorting algorithm in terms of performance.

# Divide and Conquer
- ﻿﻿**Merge sort is example of a divide and conquer algorithm, an algorithmic design paradigm**
	- ﻿﻿Divide. Split problem into subproblems
	- ﻿﻿Conquer. Solve subproblems recursively
	- ﻿﻿Combine. Combine solution for subproblem to a solution for problem
- ﻿﻿**Merge sort**:
	- ﻿﻿Divide. Split array into halves
	- ﻿﻿Conquer. Sort each half
	- ﻿﻿Combine. Merge halves