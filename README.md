# Final-Data-and-Algor

## Introduction

This project implements and compares two fundamental data structures: a Sorted Linked List (linear) and a B-Tree (hierarchical). The core requirement was to manage a dataset of 5,000 random integers and maintain them in descending order (largest to smallest) throughout the entire process. This report confirms the implementation details and verifies the correctness of the final structure.

## Implementation Details

## Sorted Linked List (Insertion Sort)

The linked list was fully implemented from scratch using custom Node and SortedLinkedList classes.

Data Generation: 5,000 random integers (range 1 to 50,000) were created using a custom LCG (CustomRandom class) and a fixed seed (123456L) to ensure data reproducibility in data.txt.

Sorting Method: The insertDescending() method functions as an Insertion Sort. Each element is inserted by traversing the list to find its position that maintains the descending order of the list.

Complexity: The overall time complexity for constructing the fully sorted list is $\mathcal{O}(N^2)$.

## B-Tree Construction and Logic

The B-Tree structure was implemented from scratch using array-based nodes (BTreeNode) to mimic disk block structures.

Minimum Degree ($t$): $t=5$ was chosen.

Node Capacity: Each node holds a maximum of $2t-1 = 9$ keys and $2t = 10$ children. The B-Tree structure stores keys in sorted arrays within each node block, with pointers (references) linking to child nodes.

Justification for $t=5$: This high degree maximizes the branching factor, which significantly reduces the tree's height, optimizing retrieval speed for large datasets (disk access is minimized).

Descending Order Adaptation: All core B-Tree operations (insertion, splitting, search) were logically inverted to maintain the descending order of keys within the node blocks.

## Output and Verification

## Sorted Linked List Snippet

The following snippet verifies that the Insertion Sort successfully maintained descending order.

--- Sorted Linked List Snippet (for Report - DESCENDING) ---
First 20 numbers (Largest):
49989 49983 49957 49954 49950 49947 49947 49941 49938 49931 49912 49900 49896 49895 49877 49871 49867 49864 49860 49859 
...
Last 20 numbers (Smallest):
109 108 107 106 103 103 98 96 85 80 73 66 62 57 56 31 29 20 12 11 
------------------------------------------------



## B-Tree Traversal Verification

The B-Tree's traverse() method uses a reverse in-order traversal to output keys in the required descending sequence to tree_traversal.txt.

Snippet from tree_traversal.txt (Confirmed Descending Order):

49989
49983
49957
49954
...
106
103
103



## B-Tree Search Results

The search function was tested using three keys dynamically located within the tree structure:

Key 40001: Found in the root node. Result: FOUND.

Key 111: Found deep in a leaf node (along the smallest value path). Result: FOUND.

Key 50001: Guaranteed to be missing (outside the data range). Result: NOT FOUND.

## Challenges & Conclusion

## Main Challenges

Adapting the B-Tree's logic for descending order storage required careful modification of its core algorithms:

Insertion Logic: The descent path was reversed. If a new key is greater than the current node key, the insertion must proceed to the left child (the subtree containing larger values).

Node Splitting: After a split, the new key must be routed to the correct resulting sibling node (the one holding the smaller values), which is the right sibling in this descending arrangement.

Traversal: The final output relied on a custom reverse in-order traversal pattern (traversing $C_n, K_{n-1}, C_{n-1}, \dots$) to ensure the descending key order.

## Comparative Analysis

The project demonstrates the functional differences and performance trade-offs between the two structures:

Sorting Cost:

Linked List: $\mathcal{O}(N^2)$ (Sorting is tied to insertion).

B-Tree: $\mathcal{O}(N \cdot \log_t N)$ (Insertion maintains balance).

Search Time:

Linked List: $\mathcal{O}(N)$ (Linear scan required).

B-Tree: $\mathcal{O}(\log_t N)$ (Optimized for fast retrieval/I/O).

Best Use Case:

Linked List: Small, memory-resident datasets.

B-Tree: Large datasets stored on secondary memory (disk).

## Conclusion:

While the Linked List efficiently served as a pipeline for initial ordering, the B-Tree provides superior scalability and performance. Through its high branching factor ($t=5$) and successful adaptation for descending order, the B-Tree structure is confirmed as the highly efficient choice for quick retrieval from large data volumes.
