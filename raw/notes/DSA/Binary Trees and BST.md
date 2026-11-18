---
title: "Binary Trees & Binary Search Trees"
source: "https://algomap.io/lessons/binary-trees"
author:
published:
created: 2026-08-01
description: "AlgoMap.io - Free roadmap for learning data structures and algorithms (DSA). Master Arrays, Strings, Hashmaps, 2 Pointers, Stacks & Queues, Linked Lists, Binary Search, Sliding Window, Trees, Heaps & Priority Queues, Recursion, Backtracking, Graph Theory, Dynamic Programming, and Bit Manipulation."
tags:
  - "clippings"
---
Links To Code:

![](https://www.youtube.com/watch?v=EPwWrs8OtfI)

```cpp
// Binary Search - Greg Hogg DSA Course Materials Lecture 7

 

#include <iostream>

#include <vector>

 

// Traditional Binary Search - O(log n) time, O(1) space

bool binarySearch(const std::vector<int>& arr, int target) {

    int L = 0;

    int R = arr.size() - 1;

 

    while (L <= R) {

        int M = L + (R - L) / 2;

        if (arr[M] == target) {

            return true;

        } else if (target < arr[M]) {

            R = M - 1;

        } else {

            L = M + 1;

        }

    }

    return false;

}

 

// Condition-based Binary Search - O(log n) time, O(1) space

int binarySearchCondition(const std::vector<bool>& arr) {

    int L = 0;

    int R = arr.size() - 1;

 

    while (L < R) {

        int M = L + (R - L) / 2;

        if (arr[M]) {

            R = M;

        } else {

            L = M + 1;

        }

    }

    return L;

}

 

int main() {

    std::vector<int> A = {-3, -1, 0, 1, 4, 7};

    int target = 8;

    bool result = binarySearch(A, target);

    std::cout << "Is " << target << " in the array? " << (result ? "Yes" : "No") << std::endl;

 

    std::vector<bool> B = {false, false, false, false, false, true, true};

    int conditionResult = binarySearchCondition(B);

    std::cout << "First true element index: " << conditionResult << std::endl;

 

    return 0;

}
```

```java
// Binary Trees and Binary Search Trees - Greg Hogg DSA Course Materials Lecture 8

 

// Binary Tree Functions

public class Main {

    public static void main(String[] args) {

        TreeNode A = new TreeNode(1);

        TreeNode B = new TreeNode(2);

        TreeNode C = new TreeNode(3);

        TreeNode D = new TreeNode(4);

        TreeNode E = new TreeNode(5);

        TreeNode F = new TreeNode(10);

 

        A.left = B;

        A.right = C;

        B.left = D;

        B.right = E;

        C.left = F;

 

        System.out.println("Root Node: " + A);

 

        // Recursive Pre Order Traversal (DFS)

        System.out.println("Pre Order Traversal:");

        preOrder(A);

 

        // Recursive In Order Traversal (DFS)

        System.out.println("In Order Traversal:");

        inOrder(A);

 

        // Iterative Pre Order Traversal (DFS)

        System.out.println("Iterative Pre Order Traversal:");

        preOrderIterative(A);

 

        // Level Order Traversal (BFS)

        System.out.println("Level Order Traversal:");

        levelOrder(A);

 

        // Search for a value in the tree

        int target = 11;

        boolean found = search(A, target);

        System.out.println("Value " + target + " found in tree: " + found);

    }

 

    static class TreeNode {

        int val;

        TreeNode left, right;

 

        TreeNode(int val) {

            this.val = val;

        }

 

        public String toString() {

            return Integer.toString(val);

        }

    }

 

    // Recursive Pre Order Traversal (DFS)

    public static void preOrder(TreeNode node) {

        if (node == null) return;

        System.out.println(node);

        preOrder(node.left);

        preOrder(node.right);

    }

 

    // Recursive In Order Traversal (DFS)

    public static void inOrder(TreeNode node) {

        if (node == null) return;

        inOrder(node.left);

        System.out.println(node);

        inOrder(node.right);

    }

 

    // Iterative Pre Order Traversal (DFS)

    public static void preOrderIterative(TreeNode node) {

        if (node == null) return;

        java.util.Stack<TreeNode> stack = new java.util.Stack<>();

        stack.push(node);

 

        while (!stack.isEmpty()) {

            TreeNode current = stack.pop();

            System.out.println(current);

 

            if (current.right != null) stack.push(current.right);

            if (current.left != null) stack.push(current.left);

        }

    }

 

    // Level Order Traversal (BFS)

    public static void levelOrder(TreeNode node) {

        if (node == null) return;

        java.util.Queue<TreeNode> queue = new java.util.LinkedList<>();

        queue.add(node);

 

        while (!queue.isEmpty()) {

            TreeNode current = queue.poll();

            System.out.println(current);

 

            if (current.left != null) queue.add(current.left);

            if (current.right != null) queue.add(current.right);

        }

    }

 

    // Search for a value in the tree (DFS)

    public static boolean search(TreeNode node, int target) {

        if (node == null) return false;

        if (node.val == target) return true;

        return search(node.left, target) || search(node.right, target);

    }

}

 

 

 

// Binary Search Trees:

 

public class Main {

    public static void main(String[] args) {

        TreeNode A2 = new TreeNode(5);

        TreeNode B2 = new TreeNode(1);

        TreeNode C2 = new TreeNode(8);

        TreeNode D2 = new TreeNode(-1);

        TreeNode E2 = new TreeNode(3);

        TreeNode F2 = new TreeNode(7);

        TreeNode G2 = new TreeNode(9);

 

        A2.left = B2;

        A2.right = C2;

        B2.left = D2;

        B2.right = E2;

        C2.left = F2;

        C2.right = G2;

 

        System.out.println("BST Root Node: " + A2);

 

        // In Order Traversal (DFS)

        System.out.println("BST In Order Traversal:");

        inOrder(A2);

 

        // Search in BST

        int target = -1;

        boolean found = searchBST(A2, target);

        System.out.println("Value " + target + " found in BST: " + found);

    }

 

    // Node class for the Binary Search Tree

    static class TreeNode {

        int val;

        TreeNode left, right;

 

        TreeNode(int val) {

            this.val = val;

        }

 

        public String toString() {

            return Integer.toString(val);

        }

    }

 

    // In Order Traversal (DFS)

    public static void inOrder(TreeNode node) {

        if (node == null) return;

        inOrder(node.left);

        System.out.println(node);

        inOrder(node.right);

    }

 

    // Search in BST - O(log n) time, O(log n) space

    public static boolean searchBST(TreeNode node, int target) {

        if (node == null) return false;

        if (node.val == target) return true;

        if (target < node.val) return searchBST(node.left, target);

        else return searchBST(node.right, target);

    }

}
```

## Summary

**Binary trees** are hierarchical data structures where each node has at most two children—left and right. A **binary search tree (BST)** is a specialized form where the left child is less than the node, and the right is greater. They are used in searching, sorting, and hierarchical modeling of data like directories, decision trees, and parsers.

### Binary Trees & Binary Search Trees

A **binary tree** is a fundamental data structure composed of nodes, where each node can have at most two children—commonly referred to as the left and right child. These structures are useful for representing hierarchical relationships and enabling efficient search and traversal algorithms.

### Binary Trees

Binary trees serve as the basis for many more advanced structures such as heaps, expression trees, and search trees. Key operations include depth-first traversal (in-order, pre-order, post-order) and breadth-first traversal (level-order). They are ideal for problems that require ordered and recursive data access.

### Binary Search Trees (BST)

A **binary search tree** is a binary tree where the left subtree contains values less than the parent node, and the right subtree contains values greater than the parent node. This ordering enables fast search, insert, and delete operations in average `O(log n)` time, though performance can degrade to `O(n)` in unbalanced trees.

### Common Operations

- **Insert/Search/Delete:** `O(log n)` average
- **Traversal:** In-order for sorted output, pre/post-order for structural operations

### Conclusion

Binary trees and BSTs are crucial to mastering tree-based recursion and divide-and-conquer strategies. They form the backbone of efficient searching and are widely used in compilers, databases, and file systems.

---

## Binary Trees: Concepts, Structure, and Algorithms

### What Is a Binary Tree?

A **Binary Tree** is a hierarchical data structure composed of nodes. Each node contains a value and can have at most two children: a **left** child and a **right** child. These child nodes are connected via references (or pointers), which may point to another node or be **null** (or `None`) if no child exists.

Binary trees are a specialized form of a directed graph and are fundamental to many algorithmic techniques in computer science.

### Key Terminology

- **Node:** The fundamental unit of a binary tree, storing a value and pointers to its children.
- **Root:** The topmost node of the tree. All other nodes descend from this node.
- **Left/Right Child:** The two potential children of any node, accessed through the left and right pointers.
- **Null (None):** Indicates the absence of a child node.
- **Leaf:** A node with no children; its height is 1.
- **Parent:** The node directly above a given node in the tree structure.
- **Children:** The nodes directly below a given node.

### Types of Binary Trees

- **Complete Binary Tree:** All levels are fully filled except possibly the last, which is filled from left to right.
- **Perfect Binary Tree:** All internal nodes have two children, and all leaf nodes are at the same level.
- **Binary Search Tree (BST):** A binary tree with an ordering property: for any node, values in the left subtree are smaller, and values in the right subtree are larger. This property holds recursively across the tree and enables efficient searching.

### Binary Tree Representation

Binary trees can be implemented in different ways:

- **Linked Structure:** Each node is an object containing its value, and references to its left and right children.
- **Array Representation:** Using 1-based indexing, the node at index `i` has its left child at index `2*i` and its right child at `2*i + 1`. Nulls are represented by out-of-bound indices or special null values.

### Height of a Binary Tree

The **height** of a binary tree is defined as the longest path from the root node to any leaf node, counted in terms of nodes. Even individual subtrees have their own height, and a **leaf** node has a height of 1.

### Tree Traversal Techniques

### Depth-First Search (DFS)

DFS explores as deep as possible along each branch before backtracking. It is implemented using a **stack** — either explicitly in iterative approaches or implicitly via the recursive call stack. DFS has three primary traversal orders:

- **Pre-order:** Visit the current node, then traverse the left subtree, followed by the right subtree.
- **In-order:** Traverse the left subtree, visit the node, then traverse the right subtree. This results in sorted values in a Binary Search Tree.
- **Post-order:** Traverse the left subtree, then the right subtree, and finally visit the node.

### Breadth-First Search (BFS)

BFS, or **Level Order Traversal**, explores the tree level by level from top to bottom. It uses a **queue** to track nodes at each level. BFS is especially useful when the tree needs to be processed in layers or when searching for the shortest path.

### Common Binary Tree Algorithms and Complexities

Several algorithms operate on binary trees, especially searches and traversals. The efficiency of these algorithms depends on the structure of the tree.

### Searching in a General Binary Tree

- **Time Complexity:** `O(N)` in the worst case — all nodes must be visited.
- **Space Complexity:** `O(N)` — due to the call stack in DFS or queue in BFS.

### Searching in a Binary Search Tree (BST)

- **Time Complexity (Balanced BST):** `O(log N)` — halves the search space at each step.
- **Time Complexity (Unbalanced BST):** `O(N)` — resembles a linked list in the worst case.
- **Space Complexity:**
	- `O(log N)` for a balanced tree (height of the tree).
		- `O(N)` if the tree is unbalanced.

### Traversal Complexities (DFS and BFS)

- **Time Complexity:** `O(N)` — all nodes are visited once.
- **Space Complexity:** `O(N)` — maximum size of the call stack or queue in worst-case scenarios.