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
    #hash map
    d={} #equivalently, d=dict()
    d[key] = value
    d.get(key[, default]) #None if default is not given
    d.keys(), d.values(), d.items() #view of keys, values, (key, value) pairs
    del d[key] #similarly, pop(key[, default]), which also returns value
    #queue/stack
    from collections import deque #O(1) for all operations
    q=deque(iterable[, maxlen]) #maxlen limits the longest length
    q.append(x), q.pop() #stack
    q.appendleft(x), q.leftpop() #queue
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
