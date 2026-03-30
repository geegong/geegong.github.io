---
title: "BFS - Binary Tree Level Order Traversal"
date: 2026-03-27
categories:
  - DSA
tags:
  - Algorithms
  - BFS
  - Tree
  - Queue
---

## The Problem

**[LeetCode 102 - Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal)**

Given the root of a binary tree, return the node values **level by level** from left to right.

```
Input:
        3
       / \
      9  20
        /  \
       15   7

Output: [[3], [9, 20], [15, 7]]
```

Each inner list represents one level of the tree. The challenge is to visit nodes **in the correct order** and **group them by depth**.

---

## What is BFS?

**BFS (Breadth-First Search)** is a traversal algorithm that explores nodes **level by level** — visiting all neighbors at the current depth before moving deeper.

```
Tree:       3
           / \
          9  20
            /  \
           15   7

BFS order:  3 → 9 → 20 → 15 → 7
```

Unlike DFS which dives deep first, BFS spreads wide — it processes every node at depth `d` before touching any node at depth `d+1`.

The key data structure that makes this possible is a **queue** (FIFO). Every time you visit a node, you enqueue its children. When you dequeue a node, you're guaranteed it's the next one in level order.

---

## Why BFS fits this problem perfectly

This problem asks for nodes **grouped by level**. That's exactly the pattern BFS produces naturally:

- All depth-0 nodes first → `[3]`
- All depth-1 nodes next → `[9, 20]`
- All depth-2 nodes last → `[15, 7]`

The only extra step beyond plain BFS is capturing the **size of the queue at the start of each level**, so we know which nodes belong to the same group.

---

## Approaching the Problem Step by Step

### Step 1 — Seed the queue with the root

```
Queue: [3]
Result: []
```

### Step 2 — At each level, snapshot the queue size

When we enter a new level, the queue contains **exactly the nodes at that level** (and nothing else yet). We snapshot `size = queue.size()` and loop that many times — this isolates one level's worth of work.

```
Level 0:  size = 1  →  dequeue 3, enqueue 9 and 20
          currentLevel = [3]
          Queue: [9, 20]
          Result: [[3]]
```

### Step 3 — Repeat until the queue is empty

```
Level 1:  size = 2  →  dequeue 9 (no children), dequeue 20 (enqueue 15, 7)
          currentLevel = [9, 20]
          Queue: [15, 7]
          Result: [[3], [9, 20]]

Level 2:  size = 2  →  dequeue 15, dequeue 7 (no children)
          currentLevel = [15, 7]
          Queue: []
          Result: [[3], [9, 20], [15, 7]]
```

Queue is empty → done.

---

## The Code

```java
public List<List<Integer>> levelOrder(TreeNode root) {
    List<List<Integer>> result = new ArrayList<>();
    if (root == null) return result;

    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);

    while (!queue.isEmpty()) {
        int size = queue.size();           // snapshot: nodes at this level
        List<Integer> currentLevel = new ArrayList<>();

        for (int i = 0; i < size; i++) {
            TreeNode node = queue.poll();
            currentLevel.add(node.val);

            if (node.left != null)  queue.offer(node.left);
            if (node.right != null) queue.offer(node.right);
        }

        result.add(currentLevel);
    }

    return result;
}
```

### Why `LinkedList` for the queue?

In Java, `Queue` is an interface — you can't instantiate it directly. You need a concrete class that implements it. `LinkedList` is the most common choice because:

- It implements both `Queue` and `Deque`, giving you `offer()`, `poll()`, and `peek()` out of the box.
- Insertions and removals at both ends are **O(1)** — exactly what a queue needs.
- `ArrayDeque` is another valid option and is slightly faster in practice (no node allocation overhead), but `LinkedList` is more commonly seen in interview solutions.

```
Queue<TreeNode> queue = new LinkedList<>();
//    ↑ interface     ↑ concrete implementation
```

This is the standard Java pattern: program to the interface (`Queue`), instantiate with the implementation (`LinkedList`).

### Why `size = queue.size()` is the key line

Without snapshotting the size, you'd mix nodes from different levels into the same group as the queue grows during iteration. The snapshot freezes the boundary: "these `size` nodes belong to the current level — everything enqueued after belongs to the next."

---

## Complexity

| | |
|---|---|
| Time | O(n) — every node is enqueued and dequeued exactly once |
| Space | O(n) — the queue holds at most the widest level of the tree |

---

## Summary

- **BFS** explores a tree level by level using a queue.
- The trick for grouping nodes by level is to **snapshot `queue.size()` at the start of each iteration** — this acts as a boundary between levels.
- This pattern generalizes to many BFS problems: shortest path in a grid, word ladder, zigzag traversal, and more.
