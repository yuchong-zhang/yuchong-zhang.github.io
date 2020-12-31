---
title: "Coding notes"
collection: notes
permalink: /notebook/coding-note
---
1. <b>Python utilities for common data structures</b><br/>
    ~~~ python
    #array
    l=[] #or, l=list()
    l.append(x), l.extend(iterable), l.insert(i, x)
    l.remove(x), l.index(x[, start[, end]]) #remove or return index of the first item==x
    l.pop([i])
    l.sort(key=None, reverse=False) #inplace
    l.clear(), l.count(x), l.reverse(), l.copy()
    #linked list
    class node:
        def __init__(self, val, next, prev):
            self.val=val
            self.next=next
            self.prev=prev #in case of doubly linked list
    #hash set
    s=set()
    s.add(item) #set.uodate() to add multiple items
    s.remove(item), s.discard(item) #If not present, the former will raise errors
    s1.union(s2), s1.difference(s2), s1.intersection(s2)
    s1|s2, s1-s2, s1&s2 #equivalent to the line above
    #hash map
    d={} #equivalently, d=dict()
    d[key] = value
    d.get(key[, default]) #None if default is not given
    d.keys(), d.values(), d.items() #view of keys, values, (key, value) pairs
    del d[key] #similarly, pop(key[, default]), which also returns value
    from collections import defaultdict
    d=defaultdict(list), d=defaultdict(lambda: 1) #dict with default value
    #queue/stack
    from collections import deque #O(1) for all operations
    q=deque(iterable[, maxlen]) #maxlen limits the longest length
    q.append(x), q.pop() #stack
    q.appendleft(x), q.popleft() #queue
    #min heap
    import heapq
    heapq.heapify(heap) #in place, O(n)
    heapq.heappush(heap, item) #O(logN)
    heapq.heappop(heap) #return the smallest item, O(logN)
    ~~~

2. <b>Some common string methods in coding</b><br/>
    ~~~ python
    s='' #or, s=str()
    s.index(val), s.find(val) #if not present, the latter returns -1
    string.join(iterable)
    string.split(separator, maxsplit)
    ~~~

3. <b>Summary of graph algorithms</b><br/>
    <b>BFS</b>: find the shorted path (edge of uniform length), queue implementation, O(m+n) in T\
    <b>DFS</b>: find cycles, topological ordering, stack impementation or recursion, O(m+n) in T\
    <b>Kosaraju's two-pass algorithm</b>: used to find strongly connected components of a directed graph. first DFS on reversed graph G' to determine finishing time f(V), second DFS on original graph G in decreasing order of f(V), O(m+n) in T\
    <b>Dijkstra's algorithm</b>: single source shortest paths (non-negative edge), greedy, O(mlogn) in T with heap implementation\
    <b>Bellman-Ford algorithm</b>: single source shortest paths (general edge, no negative cycles), DP, limit on maxium number of edges to use (adding one iteration to test negative cycles), O(mn) in T, O(n) in S (both for calculation and reconstruction, and the later needs to update the penultimate vertice)   
    <b>Floyed-Warshall algorithm</b>: all-pairs shorted paths (general edge, no negative cycles), DP, limit on sets of vertices to use (checking the diagonal of last iteration for negative cycles), O(n<sup>3</sup>) in T\
    <b>Johnson'algorithm</b>: all-pairs shorted paths (general edge, no negative cycles), one invocation of Bellman-Ford algorithm to transform the orginal graph G into a reweighted G' (non-negative edge), and then n invocations of Dijkstra's algorithm. O(mnlogn)\

4. <b>Master method for Divide & Conquer running time analysis</b><br/>
    T(n)<=aT(n/b)+O(n<sup>d</sup>)\
    where a = number of recursive calls (>=1), b = input size shrinkage factor (>1) and d = exponent in running time of "combine step" (>=0)\
    There are three cases:\
    T(n) = O(n<sup>d</sup>logn) if a=b<sup>d</sup>  
    T(n) = O(n<sup>d</sup>) if a<b<sup>d</sup>  
    T(n) = O(n<sup>log<sub>b</sub>a</sup>) if a>b<sup>d</sup>  

5. <b>Sliding window approach for minumum array problems</b><br/>
    We start with two pointers, left and right initially pointing to the first element of the array.\
    We use the right pointer to expand the window until we get a desirable window that satisfies all conditions.\
    Once we have a window with all the characters, we can move the left pointer ahead one by one. If the window is still a desirable one we keep on updating the minimum window size.\
    If the window is not desirable any more, we repeat step 2 onwards.

6. <b>Python constructions for advanced data structures</b><br/>
    ~~~ python
    #union-find (disjoint set)
    class DisjointSet:

        def __init__(self, n):
            self.parent = [i for i in range(n)]
            self.rank = [0 for i in range(n)]
        
        # Find with Path Compression
        def find(self, i):
            if self.parent[i] != i:
                self.parent[i] = self.find(self.parent[i])
            return self.parent[i]
        
        # Union by Rank
        def Union(self, i, j):
            i_idx = self.find(i)
            j_idx = self.find(j)      
            if j_idx == i_idx:
                return
            if self.rank[i_idx] > self.rank[j_idx]:
                self.parent[j_idx] = i_idx
            else:
                if self.rank[i_idx] == self.rank[j_idx]:
                    self.rank[j_idx] += 1
                self.parent[i_idx] = j_idx
    
    #trie (prefix tree)
    class TrieNode:
        def __init__(self):
            self.children = collections.defaultdict(TrieNode)
            self.is_word = False

    class Trie:

        def __init__(self):
            self.root = TrieNode()

        def insert(self, word):
            current = self.root
            for letter in word:
                current = current.children[letter]
            current.is_word = True

        def search(self, word):
            current = self.root
            for letter in word:
                current = current.children.get(letter)
                if current is None:
                    return False
            return current.is_word

        def startsWith(self, prefix):
            current = self.root
            for letter in prefix:
                current = current.children.get(letter)
                if current is None:
                    return False
            return True  
    ~~~




