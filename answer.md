# Code 

## Q1. Divide and Conquer: Missing Number
- Time Complexity: O(logN)

```python

def search_missing(arr, size): 
    i = 0
    j = size - 1
    mid = 0
    while j > i + 1: 
        mid = (i + j) // 2
        if (arr[i] - i) != (arr[mid] - mid): 
            j = mid 
        else:
            i = mid
    return arr[mid] + 1

```

- New

```python

def find_missing(a:list, m:int, n:int)->int:
    if a[-1] == n:
        return a[-1] + 1
    if a[0] != 0:
        return 0
    mid = 0
    while n > m + 1: 
        mid = (m + n) // 2
        if a[mid] != mid:
            n = mid 
        else:
            m = mid
    return a[m] + 1
    
```

## Q2. Graph: Topological Sort
- Time Complexity: O(M+N)

```python

class GraphVertex:
    def __init__(self, label):
        self.label = label
        self.d = 0  # Distance to start vertex
        self.discovered = False
        self.processed = False
        self.parent = None  # The vertex discovers me 
        self.edges = []  # Edges in Adjacency List

def DFS(v:GraphVertex): 
    v.discovered = True 
    process_vertex_early(v.label)
    for t in v.edges:
        if not t.discovered:
            t.parent = v
            t.d = v.d + 1 
            process_edge(v.label, t.label)
            DFS(t)
        elif v.parent != t:
            process_edge(v.label, t.label)
    process_vertex_late(v.label)
    v.processed = True

order = []
def process_vertex_late(label:int):
    order.insert(0, label)
    
def process_edge(i:GraphVertex, j:GraphVertex):
    if edge_classification(i, j) == EdgeType.BACK:
        raise Exception("Cycle from %d to %d" % (i.label, j.label))

```

## Q3. Backtracking: Derangement

```python

def construct_candidate(a:list, inputs:list, c:list):
    curr_index = len(a) + 1
    for i in inputs:
        if (i not in a) and (i != curr_index):
            c.append(i)

```

- New

```python

def is_a_solution(a:list, inputs:list)->bool:
    return True if len(a) == len(inputs) else False

def construct_candidate(a:list, inputs:list, c:list):
    for i in inputs:
        if (i not in a) and (i != len(a)):
            c.append(i)
            
```

## Q4. Dynamic Programming: Cutting String

```python

def cutting_string(arr, size):
    arr = arr.copy()
    arr.insert(0, 0)
    arr.append(size)
    n = len(arr)
    res = [x[:] for x in [[0]*n]*n]
    for i in range(2, n):
        for x in range(0, n-i):
            res[x][x+i] = arr[x+i] - arr[x] + min([res[x][y] + res[y][x+i] for y in range(x+1, x+i)])
    # for each in res:
    #     print(each)
    return res[0][n-1]

```

- New

```python

def cut_str(cuts:list, m:int, n:int)->int:
    c = [x[:] for x in [[0]*len(cuts)]*len(cuts)]
    n = len(cuts)
    for i in range(2, n):
        for x in range(0, n-i):
            c[x][x+i] = cuts[x+i] - cuts[x] + min([c[x][y] + c[y][x+i] for y in range(x+1, x+i)])
    return c[0][n-1]

```
