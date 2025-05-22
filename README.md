# Implementing Algorithms Based On "CLRS" in JavaScript

## Comparison-based Sorts

### Bubble Sort

#### 📌 Overview

**Bubble Sort** is a simple comparison-based sorting algorithm. It repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order. This process is repeated until the list is sorted.

#### 💡 Implementation

```js
const bubbleSort = (array) => {
  let length = array.length
  for (let i = 0; i < length - 1; i++) {
    for (let j = 0; j < length - i - 1; j++) {
      if (array[j] > array[j + 1]) {
        //swapping two number
        [array[j], array[j + 1]] = [array[j + 1], array[j]]
      }
    }
  }
  return array
}
```

#### ⚙️ How It Works

1. Compare the first two adjacent elements.
2. Swap them if they are in the wrong order.
3. Move to the next pair and repeat until the end of the array.
4. After each pass, the largest unsorted element **"bubbles up"** to its correct position.
5. Repeat the process for the remaining unsorted part of the array.

#### ⏱️ Time and Space Complexities

| Case         | Time Complexity | Description                                                                |
| ------------ | --------------- | -------------------------------------------------------------------------- |
| Best Case    | O(n)            | The array is already sorted; only one pass needed without any swaps.       |
| Average Case | O(n²)           | Elements are in random order; multiple passes and swaps are needed.        |
| Worst Case   | O(n²)           | The array is sorted in reverse order; maximum number of comparisons/swaps. |

- **Space Complexity**: O(1) – In-place sorting, no additional memory used.
- **Stable**: ✅ Yes – Equal elements retain their original order.
- **In-place**: ✅ Yes – Uses only constant extra space.

---

### Insertion Sort

#### 📌 Overview

**Insertion Sort** is a simple, intuitive sorting algorithm that builds the final sorted array one item at a time. It works well for **small datasets** and is especially **efficient when the input is already partially sorted**.

#### 💡 Implementation

```js
const insertionSort = (array) => {
  for (let i = 1; i < array.length; i++) {
    let key = array[i]
    let j = i - 1
    while (j >= 0 && array[j] > key) {
      array[j + 1] = array[j]
      j--
    }
    array[j + 1] = key
  }
  return array
}
```

#### ⚙️ How It Works

1. Start with the second element as the "key".
2. Compare it with elements to its left.
3. Shift all larger elements one position to the right.
4. Insert the key into its correct position.
5. Repeat for all elements in the array.

#### ⏱️ Time and Space Complexities

| Case         | Time Complexity | Description                                                                     |
| ------------ | --------------- | ------------------------------------------------------------------------------- |
| Best Case    | O(n)            | The array is already sorted; only one comparison per element.                   |
| Average Case | O(n²)           | Elements are in random order; each new element is compared with many before it. |
| Worst Case   | O(n²)           | The array is sorted in reverse order; each new element goes to the beginning.   |

- **Space Complexity**: O(1) – In-place sorting, no extra memory needed.
- **Stable**: ✅ Yes – Maintains the relative order of equal elements.
- **In-place**: ✅ Yes – Only uses constant memory for operations.

---

### Selection Sort

#### 📌 Overview

**Selection Sort** is a simple comparison-based sorting algorithm. It divides the array into a sorted and unsorted region and repeatedly selects the smallest (or largest) element from the unsorted region, placing it at the end of the sorted region.

#### 💡 Implementation

```js
const selectionSort = (array) => {
  const n = array.length

  for (let i = 0; i < n - 1; i++) {
    let minIndex = i
    for (let j = i + 1; j < n; j++) {
      if (array[j] < array[minIndex]) {
        minIndex = j
      }
    }

    if (minIndex !== i) {
      [array[i], array[minIndex]] = [array[minIndex], array[i]]
    }
  }

  return array
}
```

#### ⚙️ How It Works

1. Start from the first element.
2. Find the minimum element in the unsorted part of the array.
3. Swap it with the first unsorted element.
4. Repeat for the remaining elements.

#### ⏱️ Time and Space Complexities

| Case         | Time Complexity | Description                                                            |
| ------------ | --------------- | ---------------------------------------------------------------------- |
| Best Case    | O(n²)           | Even if the array is sorted, it still does n² comparisons.             |
| Average Case | O(n²)           | Always performs the same number of comparisons regardless of order.    |
| Worst Case   | O(n²)           | Occurs when the array is sorted in reverse; still does n² comparisons. |

- **Space Complexity**: O(1) – In-place sorting.
- **Stable**: ❌ No – Swapping can change the relative order of equal elements.
- **In-place**: ✅ Yes – Requires constant extra memory.

---

### Merge Sort

#### 📌 Overview

**Merge Sort** is a **Divide and Conquer** algorithm. It divides the input array into two halves, recursively sorts them, and then merges the sorted halves. It guarantees O(n log n) performance and is widely used due to its predictable efficiency.

#### 💡 Implementation

```js
const mergeSort = (array) => {
  if (array.length < 2) return array
  const mid = Math.floor(array.length / 2)
  const left = mergeSort(array.slice(0, mid))
  const right = mergeSort(array.slice(mid))
  return merge(left, right)
}
const merge = (left, right) => {
  let result = []
  while (left.length && right.length) {
    if (left[0] < right[0]) {
      result.push(left.shift())
    } else {
      result.push(right.shift())
    }
  }
  return [...result, ...left, ...right]
}
```

#### ⚙️ How It Works

1. Divide the array into two halves.
2. Recursively sort each half.
3. Merge the two sorted halves into one sorted array.
4. Continue until the entire array is sorted.

#### ⏱️ Time and Space Complexities

| Case         | Time Complexity | Description                                                     |
| ------------ | --------------- | --------------------------------------------------------------- |
| Best Case    | O(n log n)      | All elements are already sorted; merge steps still required.    |
| Average Case | O(n log n)      | Standard case; always divides array and merges.                 |
| Worst Case   | O(n log n)      | Occurs in all scenarios; merge sort consistently performs well. |

- **Space Complexity**: O(n) – Extra space is required for the merging process.
- **Stable**: ✅ Yes – Maintains the relative order of equal elements.
- **In-place**: ❌ No – Requires additional memory.

---

### Quick Sort

#### 📌 Overview

**Quick Sort** is a highly efficient **Divide and Conquer** sorting algorithm. It selects a "pivot" element, partitions the array into elements less than and greater than the pivot, and recursively sorts the partitions. It is commonly used in practice due to its speed and in-place sorting capability.

#### 💡 Implementation

```js
const partition = (arr, low, high) => {
  let pivot = arr[high]
  let i = low - 1

  for (let j = low; j <= high - 1; j++) {
    if (arr[j] < pivot) {
      i++
      [arr[i], arr[j]] = [arr[j], arr[i]]
    }
  }

  [arr[i + 1], arr[high]] = [arr[high], arr[i + 1]]
  return i + 1
}

const quickSort = (arr, low, high) => {
  if (low >= high) return
  let pi = partition(arr, low, high)

  quickSort(arr, low, pi - 1)
  quickSort(arr, pi + 1, high)
}
quickSort(arr, 0, arr.length - 1)
```

#### ⚙️ How It Works

1. Choose a pivot (e.g., first, last, middle, or random element).
2. Partition the array so that:
   - Elements < pivot go to the left.
   - Elements > pivot go to the right.
3. Recursively apply the same logic to the left and right subarrays.
4. Continue until the base case is reached (subarray has 0 or 1 element).

#### ⏱️ Time and Space Complexities

| Case         | Time Complexity | Description                                                                     |
| ------------ | --------------- | ------------------------------------------------------------------------------- |
| Best Case    | O(n log n)      | The pivot divides the array into nearly equal parts.                            |
| Average Case | O(n log n)      | On average, the pivot balances the partitions fairly well.                      |
| Worst Case   | O(n²)           | Occurs when the pivot is always the smallest or largest (e.g., already sorted). |

- **Space Complexity**: O(log n) – Due to recursive stack calls (in-place).
- **Stable**: ❌ No – May change the relative order of equal elements.
- **In-place**: ✅ Yes – Does not require additional arrays.

---

### Tree Sort

#### 📌 Overview

**Tree Sort** is a sorting algorithm that builds a **Binary Search Tree (BST)** from the elements of the input list, then performs an **in-order traversal** of the BST to retrieve elements in sorted order.

#### 💡 Implementation

```js
class TreeNode {
  constructor(value) {
    this.value = value
    this.left = null
    this.right = null
  }
}

const insertNode = (root, value) => {
  if (!root) return new TreeNode(value)

  if (value < root.value) {
    root.left = insertNode(root.left, value)
  } else {
    root.right = insertNode(root.right, value)
  }
  return root
}
const inOrderTraversal = (node, result) => {
  if (node) {
    inOrderTraversal(node.left, result)
    result.push(node.value)
    inOrderTraversal(node.right, result)
  }
}

const treeSort = (array) => {
  let root = null
  for (const num of array) {
    root = insertNode(root, num)
  }

  const sorted = []
  inOrderTraversal(root, sorted)
  return sorted
}
```

#### ⚙️ How It Works

1. Insert each element into a Binary Search Tree (BST).
2. Perform in-order traversal of the BST.
3. Collect the elements during traversal to get the sorted array.

#### ⏱️ Time and Space Complexities

| Case         | Time Complexity | Description                                               |
| ------------ | --------------- | --------------------------------------------------------- |
| Best Case    | O(n log n)      | Balanced BST; each insert and traversal is log(n).        |
| Average Case | O(n log n)      | On average, trees are reasonably balanced.                |
| Worst Case   | O(n²)           | Unbalanced BST (e.g., sorted input leads to skewed tree). |

- **Space Complexity**: O(n) – Extra space for the tree.
- **Stable**: ❌ No – Relative order of equal elements may change.
- **In-place**: ❌ No – Requires additional memory for the tree structure.

---

### Heap Sort

#### 📌 Overview

**Heap Sort** is a comparison-based sorting algorithm that uses a **Binary Heap** (usually a Max-Heap). It repeatedly extracts the maximum element from the heap and rebuilds the heap until the array is sorted.

#### 💡 Implementation

```js
const heapify = (array, n, i) => {
  let largest = i
  let left = 2 * i + 1
  let right = 2 * i + 2

  if (left < n && array[left] > array[largest]) {
    largest = left
  }
  if (right < n && array[right] > array[largest]) {
    largest = right
  }

  if (largest !== i) {
    ;[array[i], array[largest]] = [array[largest], array[i]]
    heapify(array, n, largest)
  }
}

const heapSort = (array) => {
  let n = array.length

  for (let i = Math.floor(n / 2) - 1; i >= 0; i--) {
    heapify(array, n, i)
  }

  for (let i = n - 1; i > 0; i--) {
    [array[0], array[i]] = [array[i], array[0]]
    heapify(array, i, 0)
  }
  return array
}
```

#### ⚙️ How It Works

1. Build a **Max Heap** from the input array.
2. Swap the root (largest element) with the last item.
3. Reduce heap size and heapify the root.
4. Repeat until heap size is 1.

#### ⏱️ Time and Space Complexities

| Case         | Time Complexity | Description                                                |
| ------------ | --------------- | ---------------------------------------------------------- |
| Best Case    | O(n log n)      | Heapify is always log(n), even if input is already sorted. |
| Average Case | O(n log n)      | Consistently log(n) for each of n elements.                |
| Worst Case   | O(n log n)      | Performs the same regardless of input distribution.        |

- **Space Complexity**: O(1) – Sorting is done in-place.
- **Stable**: ❌ No – Order of equal elements may not be preserved.
- **In-place**: ✅ Yes – No additional memory needed.

---

## Non-Comparison-based Sorts

## ✅ Covered

- [x] Bubble Sort
- [x] Insertion Sort
- [x] Merge Sort
- [x] Quick Sort
- [x] Selection Sort
- [x] Tree Sort
- [x] Heap Sort

---

## 📌 To-Do Next

- [ ] Radix Sort
- [ ] Counting Sort
- [ ] Bucket Sort
