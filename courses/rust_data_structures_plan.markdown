# Rust Data Structures Plan

This document outlines a plan for implementing major data structures in Rust, including searching and sorting algorithms, with Rust-specific considerations for ownership, borrowing, and safety.

## Data Structures

### 1. Array (`Vec<T>`)

- **Description**: Dynamic, resizable array from `std::vec::Vec`.
- **Implementation**:

  ```rust
  let mut vec: Vec<i32> = Vec::new();
  vec.push(1); // Add element
  vec[0] = 2; // Update element
  ```
- **Use Case**: Random access, dynamic size.
- **Complexity**: Access O(1), append O(1) amortized, insert/delete O(n).
- **Rust Notes**: Use `Vec` for most array needs; avoid fixed-size arrays (`[T; N]`) for dynamic data.

### 2. Singly Linked List

- **Description**: Nodes with data and a next pointer.
- **Implementation**:

  ```rust
  struct Node<T> {
      data: T,
      next: Option<Box<Node<T>>>,
  }
  struct LinkedList<T> {
      head: Option<Box<Node<T>>>,
  }
  impl<T> LinkedList<T> {
      fn push_front(&mut self, data: T) {
          self.head = Some(Box::new(Node { data, next: self.head.take() }));
      }
  }
  ```
- **Use Case**: Frequent insertions at head/tail.
- **Complexity**: Access O(n), insert/delete O(1) at head.
- **Rust Notes**: Use `Box` for heap allocation; manage ownership carefully.

### 3. Stack

- **Description**: LIFO structure.
- **Implementation**:

  ```rust
  struct Stack<T> {
      items: Vec<T>,
  }
  impl<T> Stack<T> {
      fn push(&mut self, item: T) { self.items.push(item); }
      fn pop(&mut self) -> Option<T> { self.items.pop() }
  }
  ```
- **Use Case**: Undo operations, recursion.
- **Complexity**: Push/pop O(1) amortized.
- **Rust Notes**: `Vec` is ideal; linked list alternative for strict O(1).

### 4. Queue

- **Description**: FIFO structure.
- **Implementation**:

  ```rust
  use std::collections::VecDeque;
  struct Queue<T> {
      items: VecDeque<T>,
  }
  impl<T> Queue<T> {
      fn enqueue(&mut self, item: T) { self.items.push_back(item); }
      fn dequeue(&mut self) -> Option<T> { self.items.pop_front() }
  }
  ```
- **Use Case**: Task scheduling, BFS.
- **Complexity**: Enqueue/dequeue O(1) amortized.
- **Rust Notes**: Use `VecDeque` for efficient front/back operations.

### 5. Binary Search Tree (BST)

- **Description**: Nodes with left/right children, ordered by key.
- **Implementation**:

  ```rust
  struct Node<T> {
      data: T,
      left: Option<Box<Node<T>>>,
      right: Option<Box<Node<T>>>,
  }
  struct BST<T> {
      root: Option<Box<Node<T>>>,
  }
  impl<T: Ord> BST<T> {
      fn insert(&mut self, data: T) {
          // Recursive insertion logic
      }
  }
  ```
- **Use Case**: Ordered data, searching.
- **Complexity**: Search/insert/delete O(h), where h is height (O(log n) balanced, O(n) worst case).
- **Rust Notes**: Use `Box` for recursion; consider `Ord` trait for ordering.

### 6. Binary Heap

- **Description**: Complete binary tree with heap property.
- **Implementation**:

  ```rust
  struct MinHeap<T> {
      items: Vec<T>,
  }
  impl<T: Ord> MinHeap<T> {
      fn push(&mut self, item: T) {
          self.items.push(item);
          self.sift_up(self.items.len() - 1);
      }
      fn sift_up(&mut self, index: usize) { /* Heapify */ }
  }
  ```
- **Use Case**: Priority queues, scheduling.
- **Complexity**: Insert O(log n), extract min/max O(log n).
- **Rust Notes**: Use `Vec` for storage; implement manually or use `std::collections::BinaryHeap`.

### 7. Graph (Adjacency List)

- **Description**: Vertices with edges, stored as adjacency lists.
- **Implementation**:

  ```rust
  use std::collections::HashMap;
  struct Graph {
      adj_list: HashMap<i32, Vec<i32>>,
  }
  impl Graph {
      fn add_edge(&mut self, u: i32, v: i32) {
          self.adj_list.entry(u).or_insert(Vec::new()).push(v);
      }
  }
  ```
- **Use Case**: Networks, pathfinding.
- **Complexity**: Add edge O(1), traverse O(V + E).
- **Rust Notes**: Use `HashMap` for sparse graphs; `Vec` for dense graphs.

### 8. Hash Map (`HashMap<K, V>`)

- **Description**: Key-value pairs with hashing.
- **Implementation**:

  ```rust
  use std::collections::HashMap;
  let mut map: HashMap<String, i32> = HashMap::new();
  map.insert("key".to_string(), 42);
  ```
- **Use Case**: Fast lookups, dictionaries.
- **Complexity**: Insert/search/delete O(1) average, O(n) worst case.
- **Rust Notes**: Use `std::collections::HashMap`; ensure keys implement `Hash` and `Eq`.

### 9. Set (`HashSet<T>` or `BTreeSet<T>`)

- **Description**: Unique elements, unordered or ordered.
- **Implementation**:

  ```rust
  use std::collections::HashSet;
  let mut set: HashSet<i32> = HashSet::new();
  set.insert(42);
  ```
- **Use Case**: Membership testing, deduplication.
- **Complexity**: Insert/search/delete O(1) for `HashSet`, O(log n) for `BTreeSet`.
- **Rust Notes**: Use `HashSet` for speed, `BTreeSet` for ordered iteration.

## Searching Algorithms

### 1. Linear Search

- **Description**: Sequential search for unsorted data.
- **Implementation**:

  ```rust
  fn linear_search<T: PartialEq>(arr: &[T], target: &T) -> Option<usize> {
      arr.iter().position(|x| x == target)
  }
  ```
- **Complexity**: O(n).
- **Use Case**: Small or unsorted arrays/lists.

### 2. Binary Search

- **Description**: Divide-and-conquer for sorted data.
- **Implementation**:

  ```rust
  fn binary_search<T: Ord>(arr: &[T], target: &T) -> Option<usize> {
      let mut left = 0;
      let mut right = arr.len();
      while left < right {
          let mid = left + (right - left) / 2;
          match arr[mid].cmp(target) {
              std::cmp::Ordering::Equal => return Some(mid),
              std::cmp::Ordering::Less => left = mid + 1,
              std::cmp::Ordering::Greater => right = mid,
          }
      }
      None
  }
  ```
- **Complexity**: O(log n).
- **Use Case**: Sorted arrays, BSTs.

### 3. Depth-First Search (DFS)

- **Description**: Recursive or stack-based graph/tree traversal.
- **Implementation**:

  ```rust
  fn dfs(graph: &HashMap<i32, Vec<i32>>, start: i32, visited: &mut HashSet<i32>) {
      if !visited.insert(start) { return; }
      if let Some(neighbors) = graph.get(&start) {
          for &neighbor in neighbors {
              dfs(graph, neighbor, visited);
          }
      }
  }
  ```
- **Complexity**: O(V + E).
- **Use Case**: Pathfinding, cycle detection.

### 4. Breadth-First Search (BFS)

- **Description**: Queue-based graph/tree traversal.
- **Implementation**:

  ```rust
  use std::collections::VecDeque;
  fn bfs(graph: &HashMap<i32, Vec<i32>>, start: i32) -> Vec<i32> {
      let mut visited = HashSet::new();
      let mut queue = VecDeque::new();
      let mut result = Vec::new();
      queue.push_back(start);
      while let Some(node) = queue.pop_front() {
          if visited.insert(node) {
              result.push(node);
              if let Some(neighbors) = graph.get(&node) {
                  for &neighbor in neighbors {
                      queue.push_back(neighbor);
                  }
              }
          }
      }
      result
  }
  ```
- **Complexity**: O(V + E).
- **Use Case**: Shortest path, level-order traversal.

### 5. Hash Table Lookup

- **Description**: Direct access via hashing.
- **Implementation**:

  ```rust
  fn hash_lookup(map: &HashMap<i32, String>, key: i32) -> Option<&String> {
      map.get(&key)
  }
  ```
- **Complexity**: O(1) average.
- **Use Case**: Key-value retrieval.

## Sorting Algorithms

### 1. Bubble Sort

- **Description**: Repeatedly swap adjacent elements if out of order.
- **Implementation**:

  ```rust
  fn bubble_sort<T: Ord>(arr: &mut [T]) {
      for i in 0..arr.len() {
          for j in 0..arr.len() - i - 1 {
              if arr[j] > arr[j + 1] {
                  arr.swap(j, j + 1);
              }
          }
      }
  }
  ```
- **Complexity**: O(n²).
- **Use Case**: Educational, small datasets.

### 2. Quicksort

- **Description**: Partition around pivot, recursively sort subarrays.
- **Implementation**:

  ```rust
  fn quicksort<T: Ord>(arr: &mut [T]) {
      if arr.len() <= 1 { return; }
      let pivot = partition(arr);
      quicksort(&mut arr[..pivot]);
      quicksort(&mut arr[pivot + 1..]);
  }
  fn partition<T: Ord>(arr: &mut [T]) -> usize {
      let pivot = arr.len() - 1;
      let mut i = 0;
      for j in 0..pivot {
          if arr[j] <= arr[pivot] {
              arr.swap(i, j);
              i += 1;
          }
      }
      arr.swap(i, pivot);
      i
  }
  ```
- **Complexity**: O(n log n) average, O(n²) worst case.
- **Use Case**: General-purpose sorting.

### 3. Mergesort

- **Description**: Divide array, sort and merge subarrays.
- **Implementation**:

  ```rust
  fn mergesort<T: Ord + Clone>(arr: &mut [T]) {
      if arr.len() <= 1 { return; }
      let mid = arr.len() / 2;
      let mut left = arr[..mid].to_vec();
      let mut right = arr[mid..].to_vec();
      mergesort(&mut left);
      mergesort(&mut right);
      merge(arr, &left, &right);
  }
  fn merge<T: Ord + Clone>(arr: &mut [T], left: &[T], right: &[T]) {
      let mut i = 0;
      let mut j = 0;
      let mut k = 0;
      while i < left.len() && j < right.len() {
          if left[i] <= right[j] {
              arr[k] = left[i].clone();
              i += 1;
          } else {
              arr[k] = right[j].clone();
              j += 1;
          }
          k += 1;
      }
      while i < left.len() {
          arr[k] = left[i].clone();
          i += 1;
          k += 1;
      }
      while j < right.len() {
          arr[k] = right[j].clone();
          j += 1;
          k += 1;
      }
  }
  ```
- **Complexity**: O(n log n).
- **Use Case**: Stable sorting, large datasets.

### 4. Counting Sort

- **Description**: Count occurrences for integer keys.
- **Implementation**:

  ```rust
  fn counting_sort(arr: &mut [i32], max: i32) {
      let mut counts = vec![0; (max + 1) as usize];
      for &x in arr.iter() {
          counts[x as usize] += 1;
      }
      let mut k = 0;
      for i in 0..=max as usize {
          for _ in 0..counts[i] {
              arr[k] = i as i32;
              k += 1;
          }
      }
  }
  ```
- **Complexity**: O(n + k), where k is range of keys.
- **Use Case**: Small integer ranges.

### 5. Radix Sort

- **Description**: Sort by digits using counting sort.
- **Implementation**:

  ```rust
  fn radix_sort(arr: &mut [u32]) {
      if arr.is_empty() { return; }
      let max = *arr.iter().max().unwrap();
      let mut exp = 1;
      while max / exp > 0 {
          counting_sort_by_digit(arr, exp);
          exp *= 10;
      }
  }
  fn counting_sort_by_digit(arr: &mut [u32], exp: u32) {
      let mut counts = [0; 10];
      let mut output = vec![0; arr.len()];
      for &x in arr.iter() {
          counts[((x / exp) % 10) as usize] += 1;
      }
      for i in 1..10 {
          counts[i] += counts[i - 1];
      }
      for &x in arr.iter().rev() {
          let digit = ((x / exp) % 10) as usize;
          output[counts[digit] - 1] = x;
          counts[digit] -= 1;
      }
      arr.copy_from_slice(&output);
  }
  ```
- **Complexity**: O(nk), where k is number of digits.
- **Use Case**: Large integers, strings.

## Rust-Specific Notes

- **Ownership**: Use `Box` for recursive structures, `Rc`/`Arc` for shared ownership, `RefCell` for interior mutability.
- **Generics**: Implement with `<T: Trait>` (e.g., `Ord`, `PartialEq`, `Hash`) for flexibility.
- **Standard Library**: Leverage `Vec`, `VecDeque`, `HashMap`, `HashSet`, `BTreeMap` for production; custom implementations for learning.
- **Safety**: Avoid `unsafe` code; use Rust’s type system for memory safety.
- **Performance**: Use iterators, minimize allocations, prefer `&[T]` for slices.

## Next Steps

- Implement each data structure with tests (e.g., `#[cfg(test)]`).
- Benchmark algorithms using `criterion.rs`.
- Extend with advanced structures (e.g., AVL trees, graphs with weights).
- Optimize for concurrency using `Arc` and `Mutex`.