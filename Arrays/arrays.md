# 📌 **Arrays — Full Interview Notes**

---

## 🔹 **1. What is an Array?**
An **array** is a contiguous block of memory that stores elements of the same data type, accessed using an **index**.

### 🔸 **Indexing**
- 0-based in most languages  
  → first element at index **0**, last at index **n-1**
- Random access: `arr[i]` in **O(1)** time

### 🔸 **Key Properties**
- **Fixed size** (low-level view)
- **Elements stored back-to-back in memory**
- **Fast read by index**, but **slow insert/delete in the middle**

---

## 🔹 **2. Time & Space Complexities (Very Important)**
Let **n = number of elements**

| Operation | Time Complexity |
|----------|------------------|
| Access `arr[i]` | **O(1)** |
| Update `arr[i] = x` | **O(1)** |
| Search (Linear) | **O(n)** |
| Search (Binary, Sorted) | **O(log n)** |
| Insert at end (static arr) | **O(n)** |
| Insert at end (dynamic arr) | **Amortized O(1)** |
| Insert in middle | **O(n)** |
| Delete from middle | **O(n)** |

> ⚠️ Insert/Delete in middle = **O(n)** because elements must shift to maintain continuous memory.

---

## 🔹 **3. When to Use Arrays**
Use arrays when:
✔ Need **fast random access by index**  
✔ Size is **known or limited**  
✔ Need **sequential + random access**  
✔ Want **cache-friendly layout and low memory overhead**

Avoid when:
❌ Frequent insert/delete in the middle → use **LinkedList** or other DS

---

## 🔹 **4. Basic Patterns on Arrays**

### 🟢 **4.1 Traversal Templates**
Forward:
```cpp
for (int i = 0; i < n; i++) {
    // arr[i]
}
Reverse:

cpp
Copy code
for (int i = n - 1; i >= 0; i--) {
    // arr[i]
}
🟢 4.2 Linear Search (Unsorted)
cpp
Copy code
for (int i = 0; i < n; i++)
    if (arr[i] == target)
        return i;
🟢 4.3 Binary Search (Sorted Only)
cpp
Copy code
int l = 0, r = n - 1;
while (l <= r) {
    int mid = l + (r - l) / 2;
    if (arr[mid] == target) return mid;
    else if (arr[mid] < target) l = mid + 1;
    else r = mid - 1;
}
🔹 5. Array Rotation — Most Confusing Topic 😵‍💫
Rotate = shift array elements cyclically by k positions.

🔸 Right Rotation
csharp
Copy code
[1, 2, 3, 4, 5], k = 2 → [4, 5, 1, 2, 3]
🔸 Left Rotation
csharp
Copy code
[1, 2, 3, 4, 5], k = 2 → [3, 4, 5, 1, 2]
🔹 Index Formula (Super Important)
Rotation Type	New Index Formula
Right	(i + k) % n
Left	(i - k + n) % n

Always normalize:

cpp
Copy code
k = k % n;
⭐ 5.2 Naive Method – Extra Array (Easy, but O(n) space)
Right rotation:

cpp
Copy code
k = k % n;
int temp[n];
for (int i = 0; i < n; i++)
    temp[(i + k) % n] = arr[i];
copy temp to arr;
⭐ 5.3 Reversal Algorithm – O(n) Time, O(1) Space (Most Asked)
Right rotation by k:

pgsql
Copy code
1️⃣ Reverse whole array  
2️⃣ Reverse first k elements  
3️⃣ Reverse last n-k elements
Example:

mathematica
Copy code
[1,2,3,4,5,6,7], k=3
→ Reverse whole → [7,6,5,4,3,2,1]
→ Reverse first 3 → [5,6,7,4,3,2,1]
→ Reverse last 4 → [5,6,7,1,2,3,4]
Code:

cpp
Copy code
void reverse(int arr[], int l, int r) {
    while (l < r) swap(arr[l++], arr[r--]);
}

void rotateRight(int arr[], int n, int k) {
    k %= n;
    reverse(arr, 0, n-1);
    reverse(arr, 0, k-1);
    reverse(arr, k, n-1);
}
Left rotation variant:

cpp
Copy code
void rotateLeft(int arr[], int n, int k) {
    k %= n;
    reverse(arr, 0, k-1);
    reverse(arr, k, n-1);
    reverse(arr, 0, n-1);
}
🔹 5.4 Juggling Algorithm (Concept Only)
Uses GCD(n, k) and moves elements in cycles

O(n) time, O(1) space

Harder, rarely required; Reversal Method is preferred

❗ Common Pitfalls in Rotation
Mistake	Fix
Not reducing k	k = k % n
Confusing left vs right	Remember formulas
Wrong reverse indices	0 → k-1, k → n-1

🔹 6. High-Level Array Patterns
Pattern	Use-Cases
Prefix Sum	Range sum queries
Two Pointers	Pairs / sorted arrays / palindrome
Sliding Window	Fixed/variable subarray processing
Frequency Count	Majority, permutations, duplicates
Binary Search Variants	First/last, peak, rotated sorted array

🔹 7. Common Mistakes in Interviews
❌ Using binary search on unsorted array
❌ Missing edge cases (n = 0, 1, duplicate values)
❌ Thinking rotation without k % n
❌ Forgetting integer overflow →
✔ use mid = l + (r - l) / 2;

🔹 8. Quick Interview Checklist
Before final answer, ask mentally:
🔸 Sorted? → Two pointers / binary search
🔸 Subarray? → Sliding window / prefix sum
🔸 Rotated? → Reversal / pivot logic
🔸 Large k? → k = k % n
🔸 Time & Space complexity mentioned?

🟢 9. Real-Life Applications of Arrays
Circular buffers & round-robin scheduling

Audio/video streaming ring buffers

Lookup tables & hash-map internal arrays

Image matrices (2D arrays)

Game boards (chess, sudoku)

🎯 10. Last-Minute Cheat Sheet
mathematica
Copy code
Array = contiguous memory + same type + O(1) index access
Rotation →
    Right: Reverse All → Reverse first k → Reverse last n-k
    Left : Reverse first k → Reverse last n-k → Reverse All
Key patterns →
    Prefix → Subarray sums
    Two Pointers → Sorted, pairs, palindrome
    Sliding Window → Continuous subarrays
    Binary Search Variants → Sorted / rotated arrays