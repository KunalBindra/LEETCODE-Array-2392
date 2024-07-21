# LEETCODE-Array-2392
Let's go through a dry run of the `Solution` class, focusing on the `buildMatrix` method and the `topologicalSort` helper method.

### Method: `buildMatrix`
This method aims to build a `k x k` matrix based on row and column conditions, both of which define constraints for the placement of numbers.

**Input:**
- `k`: The dimension of the matrix (i.e., `k x k`).
- `rowConditions`: A list of pairs that define the order constraints for rows.
- `colConditions`: A list of pairs that define the order constraints for columns.

### Steps:
1. **Topological Sorting for Rows:**
   - Call `topologicalSort(rowConditions, k)` to get the topological order for rows.
   - If the returned list is empty, return an empty matrix as the conditions cannot be satisfied.

2. **Topological Sorting for Columns:**
   - Call `topologicalSort(colConditions, k)` to get the topological order for columns.
   - If the returned list is empty, return an empty matrix as the conditions cannot be satisfied.

3. **Build the Matrix:**
   - Initialize a `k x k` matrix `ans` with all zeroes.
   - Create an array `nodeToRowIndex` to map each node to its row index based on the row order.
   - Fill in the matrix `ans` using the column order and the `nodeToRowIndex` mapping.

### Helper Method: `topologicalSort`
This method performs a topological sort on the given conditions to determine the order of elements.

**Steps:**
1. Initialize data structures:
   - `order`: List to store the topological order.
   - `graph`: Adjacency list to represent the graph.
   - `inDegrees`: Array to store the in-degrees of each node.
   - `q`: Queue to process nodes with in-degree of 0.

2. **Build the Graph:**
   - For each condition `(u, v)`, add an edge `u -> v` in the graph and increment the in-degree of `v`.

3. **Topological Sorting:**
   - Add all nodes with in-degree 0 to the queue.
   - Process each node from the queue, adding it to the `order` list and decrementing the in-degree of its neighbors. If a neighbor's in-degree becomes 0, add it to the queue.

4. **Return the Result:**
   - If the size of the `order` list equals `n`, return the `order`. Otherwise, return an empty list.

### Example Dry Run:
Assume:
- `k = 3`
- `rowConditions = [[1, 2], [2, 3]]`
- `colConditions = [[2, 1], [3, 2]]`

1. **Topological Sort for Rows:**
   - Graph: 1 -> 2 -> 3
   - In-degrees: [0, 0, 1, 1]
   - Topological Order: [1, 2, 3]

2. **Topological Sort for Columns:**
   - Graph: 2 -> 1, 3 -> 2
   - In-degrees: [0, 1, 1, 0]
   - Topological Order: [3, 2, 1]

3. **Build the Matrix:**
   - `nodeToRowIndex`: [0, 0, 1, 2]
   - Fill in the matrix using the column order:
     ```
     ans[2][0] = 3
     ans[1][1] = 2
     ans[0][2] = 1
     ```

Final Matrix:
```
[[0, 0, 1],
 [0, 2, 0],
 [3, 0, 0]]
```

### Conclusion
The method correctly constructs the matrix based on the given row and column conditions using topological sorting to determine the valid order of elements.
