---
title: "Post-order DFS - Alien Dictionary"
date: 2026-03-22
categories:
  - DSA
tags:
  - Algorithms
  - DFS
  - Graph
  - Topological Sort
---

## What is DFS?

**DFS (Depth-First Search)** is a graph/tree traversal algorithm that explores as far as possible along each branch before backtracking.

Starting from a node, DFS keeps going deeper into neighbors until it hits a dead end, then backtracks and explores the next unvisited neighbor.

```
Graph:  A → B → D
            ↓
            C → E

DFS from A: A → B → D (backtrack) → C → E
```

There are three ways to visit nodes during DFS depending on **when you process the current node**:

| Order | When to process | Use case |
|---|---|---|
| Pre-order | Before visiting children | Copy a tree, prefix expressions |
| In-order | Between left and right child | BST sorted output |
| **Post-order** | **After visiting all children** | **Topological sort, dependency resolution** |

## Related Problems by DFS Order

### Pre-order — "Copy a tree, prefix expressions"

- **[LeetCode 144 - Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/)**
  Classic pre-order traversal: process the node before visiting its children.

- **[LeetCode 105 - Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)**
  Uses the fact that the first element of a pre-order sequence is always the root.

### In-order — "BST sorted output"

- **[LeetCode 98 - Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)**
  In-order traversal of a valid BST must produce a strictly increasing sequence.

- **[LeetCode 230 - Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)**
  In-order traversal visits BST nodes in sorted order — the k-th visited node is the answer.


---

## Post-order DFS

In **Post-order DFS**, a node is processed only **after all of its descendants have been fully visited**.

```
Tree:     A
         / \
        B   C
       / \
      D   E

Post-order traversal: D → E → B → C → A
```

The key idea: **a node is added to the result only when there is nothing left to explore from it.**

This naturally encodes a "dependency finished" signal — you record a node only after everything it depends on is already recorded.

---

## What is Topological Sort?

**Topological sort** is an ordering of nodes in a **directed acyclic graph (DAG)** such that for every directed edge `u → v`, node `u` appears before node `v` in the ordering.

```
Graph:  A → C
        ↓   ↓
        B → D

Valid topological order: A → B → C → D
                      or A → C → B → D
```

Think of it as scheduling tasks with dependencies — you can't start a task until all tasks it depends on are finished.

### Key constraints

- The graph must be **directed** (edges have a direction).
- The graph must be **acyclic** — if there's a cycle, no valid ordering exists.

```
Cycle:  A → B → C → A   ← impossible to order!
```

### Why does Alien Dictionary require topological sort?

The alien dictionary gives us a set of **"must come before"** rules between characters. For example:

```
t → f  means: t must appear before f in the alien alphabet
w → e  means: w must appear before e
```

These rules form a directed graph. Finding the alien alphabet order = finding a valid topological order of that graph.

- If the rules are consistent (no cycles) → a valid alien alphabet exists.
- If there's a cycle (e.g., `a → b → a`) → the input is invalid, return `""`.

This is exactly what topological sort solves.

---

## Why Post-order DFS is perfect for Alien Dictionary

### The Problem

Given a list of words sorted in an alien language's lexicographic order, find the character ordering of that language.

```
Input:  ["wrt", "wrf", "er", "ett", "rftt"]
Output: "wertf"
```

### Building the Graph

By comparing adjacent words, we can extract ordering rules between characters:

```
"wrt" vs "wrf"  →  t comes before f  (t → f)
"wrf" vs "er"   →  w comes before e  (w → e)
"er"  vs "ett"  →  r comes before t  (r → t)
"ett" vs "rftt" →  e comes before r  (e → r)
```

This gives us a **directed graph** where an edge `u → v` means character `u` must come before `v`.

```
w → e → r → t → f
```

### Why Post-order DFS?

We need a **topological ordering** — an order where every node appears before the nodes it points to.

Post-order DFS gives us exactly this, in reverse:

- When we finish DFS on a node, all nodes reachable from it have already been visited and added to the result.
- So the node we just finished must come **before** all of them in the final order.
- Reversing the post-order result gives a valid topological sort.

```java
public class Solution {
    private Map<Character, Set<Character>> adj;
    private Map<Character, Boolean> visited; // true = visiting, false = visited
    private List<Character> result;

    public String alienOrder(String[] words) {
        adj = new HashMap<>();
        visited = new HashMap<>();
        result = new ArrayList<>();

        // Initialize adjacency list with all unique characters
        for (String word : words)
            for (char c : word.toCharArray())
                adj.putIfAbsent(c, new HashSet<>());

        // Build graph by comparing adjacent words
        for (int i = 0; i < words.length - 1; i++) {
            String w1 = words[i], w2 = words[i + 1];
            int minLen = Math.min(w1.length(), w2.length());
            if (w1.length() > w2.length() && w1.substring(0, minLen).equals(w2))
                return ""; // invalid order
            for (int j = 0; j < minLen; j++) {
                if (w1.charAt(j) != w2.charAt(j)) {
                    adj.get(w1.charAt(j)).add(w2.charAt(j));
                    break;
                }
            }
        }

        // Post-order DFS on every node
        for (char c : adj.keySet())
            if (dfs(c)) return ""; // cycle detected

        Collections.reverse(result);
        StringBuilder sb = new StringBuilder();
        for (char c : result) sb.append(c);
        return sb.toString();
    }

    private boolean dfs(char c) {
        if (visited.containsKey(c))
            return visited.get(c); // true = cycle detected

        visited.put(c, true); // mark as visiting

        for (char neighbor : adj.get(c))
            if (dfs(neighbor)) return true;

        visited.put(c, false);  // mark as visited
        result.add(c);          // post-order: add after all children done
        return false;
    }
}
```

### Why not Pre-order?

In pre-order, we add a node **before** exploring its neighbors. But at that point, we don't yet know if any of its descendants form a cycle, and we haven't confirmed all dependencies are resolved. Post-order guarantees that by the time we record a node, the full subtree beneath it is clean and complete.

---

## Summary

- **DFS** explores depth-first, backtracking when stuck.
- **Post-order DFS** records a node only after all its dependencies are resolved.
- In the **Alien Dictionary** problem, post-order DFS on the character graph gives a reverse topological order — reversing it yields the valid alien alphabet.

---

