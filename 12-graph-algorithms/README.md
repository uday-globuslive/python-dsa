# Graph Algorithms

## 📖 Module Overview

Graph algorithms are fundamental to computer science and appear frequently in coding interviews and real-world applications. This module covers graph representations, traversal algorithms, shortest path algorithms, and advanced graph techniques.

## 🎯 Learning Objectives

- Master graph representations and basic operations
- Understand depth-first search (DFS) and breadth-first search (BFS)
- Learn shortest path algorithms (Dijkstra, Bellman-Ford, Floyd-Warshall)
- Implement minimum spanning tree algorithms
- Solve topological sorting and cycle detection problems
- Apply graph algorithms to real-world problems

## 📚 Table of Contents

### 1. Graph Fundamentals
- **[1.1 Graph Theory Basics](./01-graph-theory-basics.md)**
- **[1.2 Graph Representations](./02-graph-representations.md)**
- **[1.3 Graph Types and Properties](./03-graph-types.md)**
- **[1.4 Graph Input/Output Handling](./04-graph-io.md)**

### 2. Graph Traversal Algorithms
- **[2.1 Depth-First Search (DFS)](./05-depth-first-search.md)**
- **[2.2 Breadth-First Search (BFS)](./06-breadth-first-search.md)**
- **[2.3 DFS vs BFS Applications](./07-dfs-vs-bfs.md)**
- **[2.4 Traversal Variations](./08-traversal-variations.md)**

### 3. Connectivity and Components
- **[3.1 Connected Components](./09-connected-components.md)**
- **[3.2 Strongly Connected Components](./10-strongly-connected-components.md)**
- **[3.3 Articulation Points and Bridges](./11-articulation-bridges.md)**
- **[3.4 Union-Find (Disjoint Set)](./12-union-find.md)**

### 4. Shortest Path Algorithms
- **[4.1 Single Source Shortest Path](./13-single-source-shortest-path.md)**
- **[4.2 Dijkstra's Algorithm](./14-dijkstra-algorithm.md)**
- **[4.3 Bellman-Ford Algorithm](./15-bellman-ford.md)**
- **[4.4 Floyd-Warshall Algorithm](./16-floyd-warshall.md)**

### 5. Minimum Spanning Trees
- **[5.1 MST Fundamentals](./17-mst-fundamentals.md)**
- **[5.2 Kruskal's Algorithm](./18-kruskal-algorithm.md)**
- **[5.3 Prim's Algorithm](./19-prim-algorithm.md)**
- **[5.4 MST Applications](./20-mst-applications.md)**

### 6. Topological Sorting and DAGs
- **[6.1 Directed Acyclic Graphs](./21-directed-acyclic-graphs.md)**
- **[6.2 Topological Sort (Kahn's Algorithm)](./22-topological-sort-kahn.md)**
- **[6.3 Topological Sort (DFS)](./23-topological-sort-dfs.md)**
- **[6.4 DAG Applications](./24-dag-applications.md)**

### 7. Cycle Detection
- **[7.1 Cycle Detection in Undirected Graphs](./25-cycle-detection-undirected.md)**
- **[7.2 Cycle Detection in Directed Graphs](./26-cycle-detection-directed.md)**
- **[7.3 Finding All Cycles](./27-finding-all-cycles.md)**
- **[7.4 Negative Cycle Detection](./28-negative-cycle-detection.md)**

### 8. Advanced Graph Algorithms
- **[8.1 Network Flow Algorithms](./29-network-flow.md)**
- **[8.2 Bipartite Graph Algorithms](./30-bipartite-graphs.md)**
- **[8.3 Graph Coloring](./31-graph-coloring.md)**
- **[8.4 Eulerian Paths and Circuits](./32-eulerian-paths.md)**

## 🏗️ Graph Representations

### Adjacency List Implementation
```python
class Graph:
    """Graph implementation using adjacency list."""
    
    def __init__(self, directed=False):
        self.graph = {}
        self.directed = directed
    
    def add_vertex(self, vertex):
        """Add a vertex to the graph."""
        if vertex not in self.graph:
            self.graph[vertex] = []
    
    def add_edge(self, u, v, weight=1):
        """Add an edge between vertices u and v."""
        self.add_vertex(u)
        self.add_vertex(v)
        
        self.graph[u].append((v, weight))
        if not self.directed:
            self.graph[v].append((u, weight))
    
    def get_vertices(self):
        """Get all vertices in the graph."""
        return list(self.graph.keys())
    
    def get_neighbors(self, vertex):
        """Get neighbors of a vertex."""
        return self.graph.get(vertex, [])
    
    def has_edge(self, u, v):
        """Check if edge exists between u and v."""
        return any(neighbor == v for neighbor, _ in self.get_neighbors(u))
    
    def remove_edge(self, u, v):
        """Remove edge between u and v."""
        if u in self.graph:
            self.graph[u] = [(neighbor, weight) for neighbor, weight in self.graph[u] 
                           if neighbor != v]
        if not self.directed and v in self.graph:
            self.graph[v] = [(neighbor, weight) for neighbor, weight in self.graph[v] 
                           if neighbor != u]
    
    def get_edge_weight(self, u, v):
        """Get weight of edge between u and v."""
        for neighbor, weight in self.get_neighbors(u):
            if neighbor == v:
                return weight
        return float('inf')
    
    def __str__(self):
        """String representation of the graph."""
        result = []
        for vertex in self.graph:
            neighbors = [f"{neighbor}({weight})" for neighbor, weight in self.graph[vertex]]
            result.append(f"{vertex}: {neighbors}")
        return "\n".join(result)
```

### Adjacency Matrix Implementation
```python
class GraphMatrix:
    """Graph implementation using adjacency matrix."""
    
    def __init__(self, num_vertices, directed=False):
        self.num_vertices = num_vertices
        self.directed = directed
        self.matrix = [[0] * num_vertices for _ in range(num_vertices)]
        self.vertex_map = {}  # Map vertex labels to indices
        self.reverse_map = {}  # Map indices to vertex labels
        self.next_index = 0
    
    def add_vertex(self, vertex):
        """Add a vertex to the graph."""
        if vertex not in self.vertex_map and self.next_index < self.num_vertices:
            self.vertex_map[vertex] = self.next_index
            self.reverse_map[self.next_index] = vertex
            self.next_index += 1
    
    def add_edge(self, u, v, weight=1):
        """Add an edge between vertices u and v."""
        self.add_vertex(u)
        self.add_vertex(v)
        
        u_idx = self.vertex_map[u]
        v_idx = self.vertex_map[v]
        
        self.matrix[u_idx][v_idx] = weight
        if not self.directed:
            self.matrix[v_idx][u_idx] = weight
    
    def has_edge(self, u, v):
        """Check if edge exists between u and v."""
        if u not in self.vertex_map or v not in self.vertex_map:
            return False
        u_idx = self.vertex_map[u]
        v_idx = self.vertex_map[v]
        return self.matrix[u_idx][v_idx] != 0
    
    def get_edge_weight(self, u, v):
        """Get weight of edge between u and v."""
        if not self.has_edge(u, v):
            return float('inf')
        u_idx = self.vertex_map[u]
        v_idx = self.vertex_map[v]
        return self.matrix[u_idx][v_idx]
    
    def get_neighbors(self, vertex):
        """Get neighbors of a vertex."""
        if vertex not in self.vertex_map:
            return []
        
        vertex_idx = self.vertex_map[vertex]
        neighbors = []
        
        for i in range(self.num_vertices):
            if self.matrix[vertex_idx][i] != 0:
                neighbor_vertex = self.reverse_map[i]
                weight = self.matrix[vertex_idx][i]
                neighbors.append((neighbor_vertex, weight))
        
        return neighbors
```

## 🔍 Core Graph Algorithms

### Depth-First Search (DFS)
```python
class DFS:
    """Depth-First Search implementation and applications."""
    
    def __init__(self, graph):
        self.graph = graph
        self.visited = set()
        self.discovery_time = {}
        self.finish_time = {}
        self.parent = {}
        self.time = 0
    
    def dfs(self, start_vertex, visit_function=None):
        """Standard DFS traversal."""
        self.visited.clear()
        self._dfs_recursive(start_vertex, visit_function)
    
    def _dfs_recursive(self, vertex, visit_function):
        """Recursive DFS helper."""
        self.visited.add(vertex)
        self.discovery_time[vertex] = self.time
        self.time += 1
        
        if visit_function:
            visit_function(vertex)
        
        for neighbor, _ in self.graph.get_neighbors(vertex):
            if neighbor not in self.visited:
                self.parent[neighbor] = vertex
                self._dfs_recursive(neighbor, visit_function)
        
        self.finish_time[vertex] = self.time
        self.time += 1
    
    def dfs_iterative(self, start_vertex, visit_function=None):
        """Iterative DFS using stack."""
        self.visited.clear()
        stack = [start_vertex]
        
        while stack:
            vertex = stack.pop()
            
            if vertex not in self.visited:
                self.visited.add(vertex)
                if visit_function:
                    visit_function(vertex)
                
                # Add neighbors to stack (reverse order for same traversal as recursive)
                neighbors = self.graph.get_neighbors(vertex)
                for neighbor, _ in reversed(neighbors):
                    if neighbor not in self.visited:
                        stack.append(neighbor)
    
    def find_path(self, start, end):
        """Find path between start and end vertices using DFS."""
        self.visited.clear()
        self.parent.clear()
        
        if self._dfs_path_helper(start, end):
            # Reconstruct path
            path = []
            current = end
            while current is not None:
                path.append(current)
                current = self.parent.get(current)
            return path[::-1]
        
        return None
    
    def _dfs_path_helper(self, current, target):
        """Helper function for path finding."""
        if current == target:
            return True
        
        self.visited.add(current)
        
        for neighbor, _ in self.graph.get_neighbors(current):
            if neighbor not in self.visited:
                self.parent[neighbor] = current
                if self._dfs_path_helper(neighbor, target):
                    return True
        
        return False
    
    def detect_cycle_undirected(self):
        """Detect cycle in undirected graph using DFS."""
        self.visited.clear()
        
        for vertex in self.graph.get_vertices():
            if vertex not in self.visited:
                if self._has_cycle_undirected(vertex, None):
                    return True
        return False
    
    def _has_cycle_undirected(self, vertex, parent):
        """Helper for cycle detection in undirected graph."""
        self.visited.add(vertex)
        
        for neighbor, _ in self.graph.get_neighbors(vertex):
            if neighbor not in self.visited:
                if self._has_cycle_undirected(neighbor, vertex):
                    return True
            elif neighbor != parent:
                return True
        
        return False
```

### Breadth-First Search (BFS)
```python
from collections import deque

class BFS:
    """Breadth-First Search implementation and applications."""
    
    def __init__(self, graph):
        self.graph = graph
        self.visited = set()
        self.distance = {}
        self.parent = {}
    
    def bfs(self, start_vertex, visit_function=None):
        """Standard BFS traversal."""
        self.visited.clear()
        self.distance.clear()
        
        queue = deque([start_vertex])
        self.visited.add(start_vertex)
        self.distance[start_vertex] = 0
        
        while queue:
            vertex = queue.popleft()
            
            if visit_function:
                visit_function(vertex)
            
            for neighbor, _ in self.graph.get_neighbors(vertex):
                if neighbor not in self.visited:
                    self.visited.add(neighbor)
                    self.distance[neighbor] = self.distance[vertex] + 1
                    self.parent[neighbor] = vertex
                    queue.append(neighbor)
    
    def shortest_path(self, start, end):
        """Find shortest path between start and end vertices."""
        self.visited.clear()
        self.parent.clear()
        
        queue = deque([start])
        self.visited.add(start)
        
        while queue:
            vertex = queue.popleft()
            
            if vertex == end:
                # Reconstruct path
                path = []
                current = end
                while current is not None:
                    path.append(current)
                    current = self.parent.get(current)
                return path[::-1]
            
            for neighbor, _ in self.graph.get_neighbors(vertex):
                if neighbor not in self.visited:
                    self.visited.add(neighbor)
                    self.parent[neighbor] = vertex
                    queue.append(neighbor)
        
        return None  # No path found
    
    def shortest_distances(self, start):
        """Find shortest distances from start to all reachable vertices."""
        self.bfs(start)
        return dict(self.distance)
    
    def is_bipartite(self):
        """Check if graph is bipartite using BFS coloring."""
        color = {}
        
        for start in self.graph.get_vertices():
            if start not in color:
                queue = deque([start])
                color[start] = 0
                
                while queue:
                    vertex = queue.popleft()
                    
                    for neighbor, _ in self.graph.get_neighbors(vertex):
                        if neighbor not in color:
                            color[neighbor] = 1 - color[vertex]
                            queue.append(neighbor)
                        elif color[neighbor] == color[vertex]:
                            return False
        
        return True
```

### Dijkstra's Algorithm
```python
import heapq

class Dijkstra:
    """Dijkstra's shortest path algorithm."""
    
    def __init__(self, graph):
        self.graph = graph
    
    def shortest_path(self, start, end=None):
        """
        Find shortest paths from start vertex.
        Returns distances and previous vertices for path reconstruction.
        """
        distances = {vertex: float('inf') for vertex in self.graph.get_vertices()}
        previous = {vertex: None for vertex in self.graph.get_vertices()}
        distances[start] = 0
        
        # Priority queue: (distance, vertex)
        pq = [(0, start)]
        visited = set()
        
        while pq:
            current_distance, current_vertex = heapq.heappop(pq)
            
            if current_vertex in visited:
                continue
            
            visited.add(current_vertex)
            
            # Early termination if we only need path to specific vertex
            if end and current_vertex == end:
                break
            
            for neighbor, weight in self.graph.get_neighbors(current_vertex):
                if neighbor not in visited:
                    new_distance = current_distance + weight
                    
                    if new_distance < distances[neighbor]:
                        distances[neighbor] = new_distance
                        previous[neighbor] = current_vertex
                        heapq.heappush(pq, (new_distance, neighbor))
        
        return distances, previous
    
    def get_path(self, start, end):
        """Get the actual shortest path from start to end."""
        distances, previous = self.shortest_path(start, end)
        
        if distances[end] == float('inf'):
            return None, float('inf')
        
        path = []
        current = end
        while current is not None:
            path.append(current)
            current = previous[current]
        
        return path[::-1], distances[end]
    
    def all_pairs_shortest_path(self):
        """Find shortest paths between all pairs of vertices."""
        all_distances = {}
        all_paths = {}
        
        for vertex in self.graph.get_vertices():
            distances, previous = self.shortest_path(vertex)
            all_distances[vertex] = distances
            all_paths[vertex] = previous
        
        return all_distances, all_paths
```

## 🎯 Common Graph Problem Patterns

### Pattern 1: Graph Traversal
**When to Use**: Visiting all nodes, finding connected components, path finding
**Common Problems**: Number of Islands, Clone Graph, Course Schedule

```python
# Example: Number of Islands (LeetCode 200)
def numIslands(grid):
    """
    Count number of islands in 2D grid using DFS.
    
    Time: O(m*n), Space: O(m*n) for recursion stack
    """
    if not grid or not grid[0]:
        return 0
    
    m, n = len(grid), len(grid[0])
    count = 0
    
    def dfs(i, j):
        if (i < 0 or i >= m or j < 0 or j >= n or 
            grid[i][j] == '0'):
            return
        
        grid[i][j] = '0'  # Mark as visited
        
        # Visit all 4 directions
        dfs(i+1, j)
        dfs(i-1, j)
        dfs(i, j+1)
        dfs(i, j-1)
    
    for i in range(m):
        for j in range(n):
            if grid[i][j] == '1':
                count += 1
                dfs(i, j)
    
    return count
```

### Pattern 2: Shortest Path
**When to Use**: Finding minimum distance, optimal path problems
**Common Problems**: Word Ladder, Network Delay Time, Cheapest Flights

```python
# Example: Word Ladder (LeetCode 127)
def ladderLength(beginWord, endWord, wordList):
    """
    Find shortest transformation sequence length using BFS.
    
    Time: O(M²*N) where M is word length, N is wordList size
    Space: O(M²*N)
    """
    if endWord not in wordList:
        return 0
    
    wordList = set(wordList)
    queue = deque([(beginWord, 1)])
    visited = {beginWord}
    
    while queue:
        word, length = queue.popleft()
        
        if word == endWord:
            return length
        
        # Try all possible one-character changes
        for i in range(len(word)):
            for c in 'abcdefghijklmnopqrstuvwxyz':
                next_word = word[:i] + c + word[i+1:]
                
                if (next_word in wordList and 
                    next_word not in visited):
                    visited.add(next_word)
                    queue.append((next_word, length + 1))
    
    return 0
```

### Pattern 3: Topological Sort
**When to Use**: Dependency resolution, scheduling problems
**Common Problems**: Course Schedule, Alien Dictionary, Task Scheduling

```python
# Example: Course Schedule (LeetCode 207)
def canFinish(numCourses, prerequisites):
    """
    Check if all courses can be finished using topological sort.
    
    Time: O(V + E), Space: O(V + E)
    """
    # Build adjacency list and in-degree count
    graph = [[] for _ in range(numCourses)]
    in_degree = [0] * numCourses
    
    for course, prereq in prerequisites:
        graph[prereq].append(course)
        in_degree[course] += 1
    
    # BFS with Kahn's algorithm
    queue = deque([i for i in range(numCourses) if in_degree[i] == 0])
    completed = 0
    
    while queue:
        course = queue.popleft()
        completed += 1
        
        for next_course in graph[course]:
            in_degree[next_course] -= 1
            if in_degree[next_course] == 0:
                queue.append(next_course)
    
    return completed == numCourses
```

### Pattern 4: Union-Find
**When to Use**: Dynamic connectivity, detecting cycles, grouping elements
**Common Problems**: Number of Connected Components, Redundant Connection

```python
class UnionFind:
    """Union-Find (Disjoint Set) data structure."""
    
    def __init__(self, n):
        self.parent = list(range(n))
        self.rank = [0] * n
        self.components = n
    
    def find(self, x):
        """Find root with path compression."""
        if self.parent[x] != x:
            self.parent[x] = self.find(self.parent[x])
        return self.parent[x]
    
    def union(self, x, y):
        """Union by rank."""
        root_x, root_y = self.find(x), self.find(y)
        
        if root_x != root_y:
            if self.rank[root_x] < self.rank[root_y]:
                self.parent[root_x] = root_y
            elif self.rank[root_x] > self.rank[root_y]:
                self.parent[root_y] = root_x
            else:
                self.parent[root_y] = root_x
                self.rank[root_x] += 1
            
            self.components -= 1
            return True
        return False
    
    def connected(self, x, y):
        """Check if two elements are connected."""
        return self.find(x) == self.find(y)

# Example: Number of Connected Components
def countComponents(n, edges):
    """Count connected components using Union-Find."""
    uf = UnionFind(n)
    
    for u, v in edges:
        uf.union(u, v)
    
    return uf.components
```

## 📊 Algorithm Complexity Summary

### Time Complexities
| Algorithm | Time Complexity | Space Complexity | Use Case |
|-----------|----------------|------------------|----------|
| DFS | O(V + E) | O(V) | Path finding, cycle detection |
| BFS | O(V + E) | O(V) | Shortest path (unweighted) |
| Dijkstra | O((V + E) log V) | O(V) | Shortest path (weighted) |
| Bellman-Ford | O(VE) | O(V) | Negative weights, cycle detection |
| Floyd-Warshall | O(V³) | O(V²) | All pairs shortest path |
| Kruskal's MST | O(E log E) | O(V) | Minimum spanning tree |
| Prim's MST | O(E log V) | O(V) | Minimum spanning tree |
| Topological Sort | O(V + E) | O(V) | Dependency resolution |

### Space Complexities
- **Adjacency List**: O(V + E)
- **Adjacency Matrix**: O(V²)
- **DFS Recursion**: O(V) for call stack
- **BFS Queue**: O(V) for queue storage

## 🧪 Practice Problem Categories

### Easy Level (Graph Fundamentals)
1. **Graph Representation**
   - Convert edge list to adjacency list
   - Graph from adjacency matrix
   - Detect graph properties (directed/undirected)

2. **Basic Traversal**
   - DFS and BFS implementation
   - Count connected components
   - Check if path exists

3. **Simple Applications**
   - Find all paths between nodes
   - Graph diameter calculation
   - Vertex degree calculations

### Medium Level (Algorithm Application)
1. **Shortest Path Problems**
   - Word Ladder
   - Network Delay Time
   - Cheapest Flights Within K Stops
   - Rotting Oranges

2. **Cycle Detection**
   - Course Schedule
   - Redundant Connection
   - Find Eventual Safe States

3. **Topological Sorting**
   - Course Schedule II
   - Alien Dictionary
   - Sequence Reconstruction

### Hard Level (Advanced Techniques)
1. **Advanced Shortest Path**
   - Floyd-Warshall variations
   - Dijkstra with modifications
   - K shortest paths

2. **Network Flow**
   - Maximum flow problems
   - Minimum cut problems
   - Bipartite matching

3. **Advanced Graph Properties**
   - Strongly connected components
   - Articulation points and bridges
   - Graph coloring problems

## 🏆 Mastery Checklist

### Core Concepts
- [ ] Understand graph terminology and properties
- [ ] Implement adjacency list and matrix representations
- [ ] Master DFS and BFS traversal algorithms
- [ ] Apply appropriate algorithms for different problem types
- [ ] Analyze time and space complexity correctly

### Algorithm Implementation
- [ ] Implement Dijkstra's algorithm correctly
- [ ] Code topological sort (both DFS and Kahn's)
- [ ] Implement Union-Find with optimizations
- [ ] Handle weighted and unweighted graphs
- [ ] Detect cycles in directed and undirected graphs

### Problem-Solving Skills
- [ ] Solve 15+ easy graph problems
- [ ] Solve 10+ medium graph problems
- [ ] Solve 5+ hard graph problems
- [ ] Recognize graph patterns in disguised problems
- [ ] Optimize solutions for time and space

## 🚀 Study Strategy

### Progressive Learning Path
1. **Week 1**: Graph basics and representations
2. **Week 2**: DFS and BFS mastery
3. **Week 3**: Shortest path algorithms
4. **Week 4**: Topological sort and cycle detection
5. **Week 5**: Union-Find and advanced techniques
6. **Week 6**: Complex problems and optimization

### Daily Practice
- **Theory** (20 minutes): Study one algorithm/concept
- **Implementation** (30 minutes): Code the algorithm from scratch
- **Problems** (40 minutes): Solve 1-2 related problems
- **Review** (10 minutes): Analyze solutions and optimizations

## 📚 Additional Resources

### Visualization Tools
- **GraphOnline**: Interactive graph algorithm visualization
- **VisuAlgo**: Comprehensive algorithm animations
- **Graphviz**: Graph layout and visualization
- **NetworkX**: Python graph library for analysis

### Books and References
- "Introduction to Algorithms" by CLRS
- "Algorithm Design" by Jon Kleinberg and Éva Tardos
- "Competitive Programming" by Steven Halim
- "Graph Theory" by Reinhard Diestel

### Online Platforms
- LeetCode graph problems
- GeeksforGeeks graph algorithms
- HackerRank graph theory domain
- Codeforces graph problems

---

**Remember**: Graph algorithms are powerful tools for solving complex problems. Start with understanding the basic traversal algorithms, then gradually work your way up to more sophisticated techniques. Practice implementing algorithms from scratch to build deep understanding, and focus on recognizing when to apply each algorithm based on problem characteristics!
