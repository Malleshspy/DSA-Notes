# # 📌 1. What is an Array?

### 🔹 Definition
An **array** is a contiguous block of memory that stores elements of the same data type, accessed using an **index**.

### 🔹 Indexing
- 0-based in most programming languages  
  → first element at index **0**, last at index **n-1**
- Random access: `arr[i]` in **O(1)** time

### 🔹 Key Properties
- **Fixed size** (low-level view)
- **Elements stored back-to-back in memory**
- **Fast read by index**, but **slower insert/delete in the middle**

---

# 📌 2. Time & Space Complexities (Very Important for Interviews)

Let **n = number of elements**

| Operation | Time Complexity |
|----------|------------------|
| Access `arr[i]` | **O(1)** |
| Update `arr[i] = x` | **O(1)** |
| Search (Unsorted — Linear) | **O(n)** |
| Search (Binary — Sorted) | **O(log n)** |
| Insert at end (static array) | **O(n)** |
| Insert at end (dynamic array) | **Amortized O(1)** |
| Insert in middle | **O(n)** |
| Delete from middle | **O(n)** |

> ⚠️ Insert/Delete in middle = **O(n)** because elements must be shifted to maintain continuous memory.

---

# 📌 3. When to Use Arrays

Use **arrays** when:
✔ You need **fast random access by index**  
✔ Size is **known or predictable**  
✔ You want **cache-friendly and simple structure**  
✔ Data is mostly processed **sequentially**, but random access may also be needed

Avoid arrays when:
❌ Frequent **insert/delete in the middle** → prefer **Linked List / Dynamic DS**

---



## 4. Basic Patterns on Arrays

### 4.1 Traversal Template

**Forward:**
```cpp
for (int i = 0; i < n; i++) {
    // use arr[i]
}
```

**Reverse:**
```cpp
for (int i = n - 1; i >= 0; i--) {
    // use arr[i]
}
```

---

### 4.2 Linear Search (Unsorted)
```cpp
int index = -1;
for (int i = 0; i < n; i++) {
    if (arr[i] == target) {
        index = i;
        break;
    }
}
return index;
```

---

### 4.3 Binary Search (Sorted Array)
Always sorted ascending (or descending) and no rotation.
```cpp
int l = 0, r = n - 1;
while (l <= r) {
    int mid = l + (r - l) / 2;   // safe mid formula
    if (arr[mid] == target) return mid;
    else if (arr[mid] < target) l = mid + 1;
    else r = mid - 1;
}
return -1;
```
## 5. Array Rotation – The Main Pain Point 🌀
Rotating an array = shift its elements cyclically by **k** positions.

---

### 5.1 Types of Rotation

| Type | Example (n = 5, k = 2) |
|------|------------------------|
| Right rotation by k | `[1, 2, 3, 4, 5] → [4, 5, 1, 2, 3]` |
| Left rotation by k | `[1, 2, 3, 4, 5] → [3, 4, 5, 1, 2]` |

#### Index formula (very helpful)
| Rotation | New Index Formula |
|----------|-------------------|
| Right rotation | `(i + k) % n` |
| Left rotation | `(i - k + n) % n` |

Always reduce k:
k = k % n;


---

### 5.2 Naive Method (Using Extra Array) – O(n) Time, O(n) Space
Right rotate by k:
```cpp
k = k % n;
int temp[n];
for (int i = 0; i < n; i++) {
    int newIndex = (i + k) % n;
    temp[newIndex] = arr[i];
}
// copy temp back
for (int i = 0; i < n; i++)
    arr[i] = temp[i];
```
📝 Easy to remember, but **uses extra memory**.

---

### 5.3 Reversal Algorithm – O(n) Time, O(1) Space (Most Asked in Interviews)

Right rotation by k:

#### Steps:
1. Reverse entire array  

2. Reverse first k elements  
3. Reverse last n − k elements  

Example: `[1, 2, 3, 4, 5, 6, 7]`, `k = 3`

Reverse whole  → [7, 6, 5, 4, 3, 2, 1]

Reverse first 3 → [5, 6, 7, 4, 3, 2, 1]

Reverse last 4  → [5, 6, 7, 1, 2, 3, 4]

#### Code pattern:
```cpp
void reverse(int arr[], int start, int end) {
    while (start < end) {
        swap(arr[start], arr[end]);
        start++;
        end--;
    }
}

void rotateRight(int arr[], int n, int k) {
    k = k % n;
    reverse(arr, 0, n - 1);
    reverse(arr, 0, k - 1);
    reverse(arr, k, n - 1);
}
```

---

### Left rotate by k using reversal:

#### Steps:
1. Reverse first k elements  

2. Reverse last n − k elements  
3. Reverse whole array  

```cpp
void rotateLeft(int arr[], int n, int k) {
    k = k % n;
    reverse(arr, 0, k - 1);
    reverse(arr, k, n - 1);
    reverse(arr, 0, n - 1);
}
```

---
### 5.4 Juggling Algorithm (Concept Only)
- Uses the idea of **GCD(n, k)** to move elements in **cycles**
- **O(n)** time, **O(1)** space
- Harder to implement; **Reversal Algorithm is preferred in interviews**

---

### 5.5 Common Pitfalls in Rotation Problems
❗ Not doing `k = k % n` → wrong for large k  
❗ Confusing **left vs right rotation**  
❗ Off-by-one errors in `reverse()` function (`start < end` vs `<=`)  
❗ For 0-based indexing, be careful with ranges:

| Portion | Index range |
|--------|-------------|
| First k elements | `0 to k-1` |
| Last n-k elements | `k to n-1` |

---

### 5.6 Problems Based on Rotation (Must Practice)
Write these names in your notes:

- Rotate array by k steps (left & right)
- **Search in a rotated sorted array**
- **Find pivot / rotation count in rotated sorted array**
- **Check if one array is a rotation of another**
- **Rotate a matrix (2D array) by 90°**
- **Find minimum element in rotated sorted array**

---

## 6. Important Array Patterns for Interviews

---

### 6.1 Prefix Sum
📌 Idea: Precompute cumulative sums to answer range queries quickly.

> `prefix[i] = sum of elements from 0 to i`

Range sum from **l to r**:
```
prefix[r] - prefix[l - 1]     // handle l = 0 separately
```

Use when:
- “Sum of subarray from i to j”
- “Count subarrays with a target sum”
- “Range updates / range queries”

---

### 6.2 Two Pointers
Use **two indices** to process array from both ends or within the array.

Examples:
- Check if array is **palindrome**
- Find **pair with given sum in sorted array**
- Partition **negatives and positives**
- Remove duplicates from sorted array
- Container with most water (LeetCode)

Template → sorted array pair sum:
```cpp
int i = 0, j = n - 1;
while (i < j) {
    int sum = arr[i] + arr[j];
    if (sum == X) return true;
    else if (sum < X) i++;
    else j--;
}
return false;
```
### 6.3 Sliding Window
Used for **subarrays with contiguous elements**.

- **Fixed size window (size k):** max/min subarray sum, averages, max fruits, etc.
- **Variable size window:** longest/shortest subarray satisfying a condition (sum/characters/unique values)

#### Fixed window sum template:
```cpp
int windowSum = 0;

// first window
for (int i = 0; i < k; i++)
    windowSum += arr[i];
int best = windowSum;

// slide the window
for (int i = k; i < n; i++) {
    windowSum += arr[i] - arr[i - k];
    best = max(best, windowSum);
}
```

---

### 6.4 Frequency Counting
Use an **extra array or hashmap** to count occurrences of values.

✔ Useful for:
- Element appearing more than **n/2 times** (majority)
- Check if **two arrays are permutations** of each other
- **Count occurrences** / duplicate frequency

---

### 6.5 Binary Search Variants on Arrays
Binary search is not only for "find target". It has **many variations** on sorted or rotated arrays:

- Find **first occurrence**
- Find **last occurrence**
- **Count occurrences** of target
- Find **peak element**
- **Search in rotated sorted array**
- Minimum element in rotated sorted array
- Binary search on **answer space** (painters partition, shipping days, aggressive cows)

---

## 7. Common Mistakes with Arrays in Interviews

❌ Forgetting **edge cases**  
- Empty array → `n = 0`  
- Single element → `n = 1`  
- Rotation problems → `k = 0`, `k = n`, `k > n`

❌ Using extra space when **in-place** solution is required  
❌ Applying **binary search on an unsorted array**  
❌ Integer overflow in binary search mid calculation

✔ Use:

mid = l + (r - l) / 2;


---

## 8. Quick Checklist Before You Say “Done” in an Interview

Before final answer, ensure you thought about:

🔹 Is the array **sorted** → binary search / two pointers  
🔹 **Rotation** involved?  
🔹 Can I use **prefix sum** or **sliding window**?  
🔹 Edge cases: empty, duplicates, one element, large k  
🔹 Time complexity + space complexity mentioned clearly  

---

## 9. Real-Life Applications of Arrays

- **Circular buffers** (audio, video streaming, queues)
- **Round-robin task scheduling**
- **Look-up tables** (frequency of characters)
- **Image processing** (2D matrix of pixels)
- **Game boards** (tic-tac-toe / chess stored as matrices)

---

## 🔥 10. Small Summary for Last-Minute Revision (Cheat Sheet)


Array = contiguous memory + same data type + O(1) index access

Rotation:
k = k % n

Right Rotate → Reverse All → Reverse first k → Reverse last n-k

Left Rotate  → Reverse first k → Reverse last n-k → Reverse All

Important patterns:
Prefix Sum
Two Pointers
Sliding Window
Binary Search Variants

Always ask:
Sorted?
Rotated?
Subarray?
Frequency?


---

