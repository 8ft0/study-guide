# Priority Queue Operations

#### Problem Statement

You are required to implement a simple priority queue using a list of operations. A priority queue is a data structure where each element has a priority assigned to it. Elements with higher priority are dequeued before elements with lower priority. If two elements have the same priority, they are dequeued in the order they were enqueued.

You need to implement a class `PriorityQueue` with the following methods:

1. `insert(element: int, priority: int) -> None`: Inserts an element with the given priority into the priority queue.
2. `extract_max() -> int`: Removes and returns the element with the highest priority. If two elements have the same priority, return the one that was inserted first. If the queue is empty, return -1.
3. `peek() -> int`: Returns the element with the highest priority without removing it from the queue. If the queue is empty, return -1.

#### Input

- A list of operations, where each operation is either:
  - `["insert", element, priority]`: Insert the element with the given priority.
  - `["extract_max"]`: Remove and return the element with the highest priority.
  - `["peek"]`: Return the element with the highest priority without removing it.

#### Output

- For `extract_max` and `peek` operations, return the respective results in a list in the order they were performed.

#### Example

```python
operations = [
    ["insert", 10, 2],
    ["insert", 5, 1],
    ["insert", 15, 3],
    ["extract_max"],
    ["peek"],
    ["extract_max"],
    ["extract_max"],
    ["peek"]
]

result = process_operations(operations)
# result should be: [15, 10, 10, 5, -1]
```

#### Constraints

- The number of operations will be between 1 and 10^5.
- The value of `element` and `priority` will be integers between -10^9 and 10^9.

### Reference Solution

```python
import heapq
from typing import List, Union

class PriorityQueue:
    def __init__(self):
        self.heap = []
        self.counter = 0  # To keep track of the order of insertion

    def insert(self, element: int, priority: int) -> None:
        heapq.heappush(self.heap, (-priority, self.counter, element))
        self.counter += 1

    def extract_max(self) -> int:
        if not self.heap:
            return -1
        return heapq.heappop(self.heap)[2]

    def peek(self) -> int:
        if not self.heap:
            return -1
        return self.heap[0][2]

def process_operations(operations: List[List[Union[str, int]]]) -> List[int]:
    pq = PriorityQueue()
    results = []
    
    for operation in operations:
        if operation[0] == "insert":
            pq.insert(operation[1], operation[2])
        elif operation[0] == "extract_max":
            results.append(pq.extract_max())
        elif operation[0] == "peek":
            results.append(pq.peek())
    
    return results

# Example usage
operations = [
    ["insert", 10, 2],
    ["insert", 5, 1],
    ["insert", 15, 3],
    ["extract_max"],
    ["peek"],
    ["extract_max"],
    ["extract_max"],
    ["peek"]
]

print(process_operations(operations))  # Output: [15, 10, 10, 5, -1]
```

#### Explanation

1. **PriorityQueue Class**:
   - `__init__`: Initialize an empty heap and a counter to keep track of the insertion order.
   - `insert`: Push a tuple containing negative priority (to simulate max-heap), counter, and element into the heap.
   - `extract_max`: Pop and return the element with the highest priority from the heap. Return -1 if the heap is empty.
   - `peek`: Return the element with the highest priority without removing it from the heap. Return -1 if the heap is empty.

2. **process_operations Function**:
   - Instantiate the `PriorityQueue` class.
   - Iterate through the operations, calling the appropriate methods on the priority queue and collecting the results for `extract_max` and `peek` operations.