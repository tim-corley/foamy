# Binary Tree

A version of a binary tree is the **Binary Search Tree**, which has a specific set of rules around how/where nodes are added.

- Example: https://codepen.io/beaucarnes/pen/ryKvEQ?editors=0011
- collection of ordered nodes
- a node without children is a leaf node
- node can only have a max of 2 children
- order by:
  - each left sub-tree is **less** than (or equal to) the parent node
  - each right sub-tree is **greater** than (or equal to) the parent node
- a balanced tree is more efficient to search
- a tree is balanced if the max-height - the min-height <= 1
- there is a way to balance a tree while adding nodes (see: "red black tree", "b tree")
- root node has a height of 0
- **min-height**: the number of levels from the root node to the first leaf node without 2 children
- **max-hieght**: the number of levels from the root node to the furthest/last node
- 3 variations of **Depth First Search**
  - in-order: explore most left node to right most node
  - pre-order: explore from root nodes
  - post-order: explore from leaf nodes
- **Breadth First Search**: explore nodes at each level
- binary search is executed in logarithmic time (`O(log(n))`) since half the tree can be discarded for each round of search/traversal
