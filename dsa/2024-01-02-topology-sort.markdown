---
layout: post
title: "Topology Sort - Directed Graph (Kahn's Algorithm)"
comments: true
keywords: "dsa"
date: 2024-01-02 16:41:00 +05:30
tags: dsa 
---

### Problem Statement

In Directed Acyclic Graph, find the topology sort. That is if a -> b, then in the answer list a should appear before b.

### Code

```python
class Solution:
    
    #Function to return list containing vertices in Topological order.
    def topoSort(self, V, adj):
        # Code here
        
        l = len(adj)
        
        indegree = [0]*l
        
        for index, value in enumerate(adj):
            for val in value:
                indegree[val] += 1
                

        topo = []
        
        for i in range(len(indegree)):
            if indegree[i] == 0:
                topo.append(i)
                
        ans = []
        while topo:
            node = topo.pop()
            ans.append(node)
            
            for n in adj[node]:
                indegree[n] -= 1
                if indegree[n] == 0:
                    topo.append(n)
        
        return ans


```

### Useful Links

[TakeuForward YT Explanation](https://www.youtube.com/watch?v=73sneFXuTEg&ab_channel=takeUforward)
[GFG practice Link](https://www.geeksforgeeks.org/problems/topological-sort/1)


