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
