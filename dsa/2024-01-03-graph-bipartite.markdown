---
layout: post
title: "Is Graph Bipartite?"
comments: true
keywords: "dsa"
date: 2024-01-03 16:41:00 +05:30
tags: dsa 
---

### Problem Statement

A graph is bipartite if the nodes can be partitioned into two independent sets A and B such that every edge in the graph connects a node in set A and a node in set B.  
Return true if and only if it is bipartite.

### Code

#### BFS

```python
class Solution:
    def isBipartite(self, graph: List[List[int]]) -> bool:
        
        l = len(graph)

        arr = [-1]*l

        for i in range(l):

            if arr[i] == -1 and graph[i]:
                arr[i] = 0

                stack = [i]

                while stack:
                    node = stack.pop(0)
                    child_col = 0 if arr[node] == 1 else 1

                    for child in graph[node]:
                        if arr[child] == -1:
                            arr[child] = child_col
                            stack.append(child)
                        elif arr[child] == arr[node]:
                            return False
                
        return True


```

#### DFS

```python
sys.setrecursionlimit(1000000)
class Solution:
    def isBipartite(self, graph: List[List[int]]) -> bool:
        
        def dfs(i, value):
            if len(graph[i]) > 0:
                arr[i] = value
            
                for child in graph[i]:

                    if arr[child] == 0:
                        if not dfs(child, -value):
                            return False
                    elif arr[child] == value:
                        return False

            return True


        l = len(graph)
        arr = [0]*l
        for i in range(l):
            if arr[i] == 0:
                if not dfs(i, 1):
                    return False       
                
        return True
```

### Useful Links

[Leetcode Problem](https://leetcode.com/problems/is-graph-bipartite/)
[TakeuForward YT Explanation | BFS](https://www.youtube.com/watch?v=-vu34sct1g8&ab_channel=takeUforward)
[TakeuForward YT Explanation | DFS](https://www.youtube.com/watch?v=KG5YFfR0j8A&ab_channel=takeUforward)


