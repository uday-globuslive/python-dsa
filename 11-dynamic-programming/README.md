# Dynamic Programming

## 📖 Module Overview

Dynamic Programming (DP) is one of the most important algorithmic paradigms for solving optimization problems. This module provides comprehensive coverage from basic concepts to advanced techniques, focusing on pattern recognition and systematic problem-solving approaches.

## 🎯 Learning Objectives

- Understand the fundamental principles of dynamic programming
- Master memoization and tabulation techniques
- Recognize common DP patterns and when to apply them
- Solve classic DP problems with optimal solutions
- Develop intuition for state design and transitions
- Optimize time and space complexity in DP solutions

## 📚 Table of Contents

### 1. DP Fundamentals
- **[1.1 Introduction to Dynamic Programming](./01-dp-introduction.md)**
- **[1.2 Overlapping Subproblems](./02-overlapping-subproblems.md)**
- **[1.3 Optimal Substructure](./03-optimal-substructure.md)**
- **[1.4 Memoization vs Tabulation](./04-memoization-vs-tabulation.md)**

### 2. Basic DP Patterns
- **[2.1 Linear DP (1D)](./05-linear-dp.md)**
- **[2.2 Grid DP (2D)](./06-grid-dp.md)**
- **[2.3 String DP](./07-string-dp.md)**
- **[2.4 Decision Making DP](./08-decision-making-dp.md)**

### 3. Classical DP Problems
- **[3.1 Fibonacci and Variants](./09-fibonacci-variants.md)**
- **[3.2 Climbing Stairs Problems](./10-climbing-stairs.md)**
- **[3.3 House Robber Series](./11-house-robber.md)**
- **[3.4 Coin Change Problems](./12-coin-change.md)**

### 4. Sequence DP
- **[4.1 Longest Increasing Subsequence](./13-lis.md)**
- **[4.2 Longest Common Subsequence](./14-lcs.md)**
- **[4.3 Edit Distance](./15-edit-distance.md)**
- **[4.4 Palindrome Problems](./16-palindrome-dp.md)**

### 5. Grid and Path DP
- **[5.1 Unique Paths](./17-unique-paths.md)**
- **[5.2 Minimum Path Sum](./18-minimum-path-sum.md)**
- **[5.3 Dungeon Game](./19-dungeon-game.md)**
- **[5.4 Cherry Pickup](./20-cherry-pickup.md)**

### 6. Knapsack Problems
- **[6.1 0/1 Knapsack](./21-01-knapsack.md)**
- **[6.2 Unbounded Knapsack](./22-unbounded-knapsack.md)**
- **[6.3 Partition Problems](./23-partition-problems.md)**
- **[6.4 Target Sum](./24-target-sum.md)**

### 7. Advanced DP Patterns
- **[7.1 State Machine DP](./25-state-machine-dp.md)**
- **[7.2 Interval DP](./26-interval-dp.md)**
- **[7.3 Tree DP](./27-tree-dp.md)**
- **[7.4 Digit DP](./28-digit-dp.md)**

### 8. DP Optimization Techniques
- **[8.1 Space Optimization](./29-space-optimization.md)**
- **[8.2 Rolling Array Technique](./30-rolling-array.md)**
- **[8.3 Matrix Exponentiation](./31-matrix-exponentiation.md)**
- **[8.4 Convex Hull Optimization](./32-convex-hull-optimization.md)**

## 🧭 DP Problem-Solving Framework

### The DPSE Method

**D** - **Define** the state and what it represents
**P** - **Plan** the recurrence relation
**S** - **Solve** the base cases
**E** - **Execute** and optimize the solution

### Step-by-Step Process

1. **Identify DP Nature** (5-10 minutes)
   ```python
   # Check for DP characteristics
   def is_dp_problem(problem):
       """
       Checklist for DP problems:
       ✓ Optimization problem (min/max/count)
       ✓ Overlapping subproblems
       ✓ Optimal substructure
       ✓ Decision at each step affects future decisions
       """
       pass
   ```

2. **Define State** (10-15 minutes)
   ```python
   # State definition template
   """
   State Definition:
   dp[i] = [what does this represent?]
   
   Parameters:
   - i: [meaning of index/parameter]
   - Additional parameters if needed
   
   State Space:
   - Range: [minimum to maximum values]
   - Size: [total number of states]
   """
   ```

3. **Establish Recurrence** (10-15 minutes)
   ```python
   # Recurrence relation template
   def recurrence_relation():
       """
       Base Cases:
       dp[base_case] = base_value
       
       Recurrence:
       dp[i] = function(dp[previous_states])
       
       Transitions:
       For each state, consider all possible transitions
       """
       pass
   ```

4. **Implement Solution** (15-20 minutes)
   ```python
   # Implementation approaches
   def solve_recursive_memo(params):
       """Top-down approach with memoization."""
       pass
   
   def solve_tabulation(params):
       """Bottom-up approach with tabulation."""
       pass
   
   def solve_space_optimized(params):
       """Space-optimized version if possible."""
       pass
   ```

## 📊 DP Pattern Categories

### Pattern 1: Linear DP
**Characteristics**: State depends on previous few states in sequence
**Common Problems**: Climbing Stairs, House Robber, Maximum Subarray

```python
# Template: Linear DP
def linear_dp_template(arr):
    """
    General template for linear DP problems.
    
    Time: O(n), Space: O(n) or O(1) with optimization
    """
    n = len(arr)
    if n == 0:
        return 0
    
    # dp[i] represents optimal solution for first i elements
    dp = [0] * n
    
    # Base cases
    dp[0] = base_case_value
    if n > 1:
        dp[1] = base_case_value_2
    
    # Fill the DP table
    for i in range(2, n):
        dp[i] = transition_function(dp[i-1], dp[i-2], arr[i])
    
    return dp[n-1]

# Example: Climbing Stairs
def climbStairs(n):
    """Number of ways to climb n stairs (1 or 2 steps at a time)."""
    if n <= 2:
        return n
    
    # Space-optimized version
    prev2, prev1 = 1, 2
    for i in range(3, n + 1):
        current = prev1 + prev2
        prev2, prev1 = prev1, current
    
    return prev1
```

### Pattern 2: 2D Grid DP
**Characteristics**: State depends on position in 2D grid
**Common Problems**: Unique Paths, Minimum Path Sum, Longest Common Subsequence

```python
# Template: 2D Grid DP
def grid_dp_template(grid):
    """
    General template for 2D grid DP problems.
    
    Time: O(m*n), Space: O(m*n) or O(n) with optimization
    """
    if not grid or not grid[0]:
        return 0
    
    m, n = len(grid), len(grid[0])
    
    # dp[i][j] represents optimal solution at position (i,j)
    dp = [[0] * n for _ in range(m)]
    
    # Base cases
    dp[0][0] = initial_value
    
    # Fill first row
    for j in range(1, n):
        dp[0][j] = transition_from_left(dp[0][j-1], grid[0][j])
    
    # Fill first column
    for i in range(1, m):
        dp[i][0] = transition_from_top(dp[i-1][0], grid[i][0])
    
    # Fill the rest of the table
    for i in range(1, m):
        for j in range(1, n):
            dp[i][j] = transition_function(dp[i-1][j], dp[i][j-1], grid[i][j])
    
    return dp[m-1][n-1]

# Example: Unique Paths
def uniquePaths(m, n):
    """Number of unique paths in m×n grid."""
    # Space-optimized version using 1D array
    dp = [1] * n
    
    for i in range(1, m):
        for j in range(1, n):
            dp[j] += dp[j-1]
    
    return dp[n-1]
```

### Pattern 3: Knapsack DP
**Characteristics**: Decision to include/exclude items with constraints
**Common Problems**: 0/1 Knapsack, Coin Change, Partition Equal Subset Sum

```python
# Template: 0/1 Knapsack
def knapsack_01(weights, values, capacity):
    """
    0/1 Knapsack problem template.
    
    Time: O(n*W), Space: O(n*W) or O(W) with optimization
    """
    n = len(weights)
    
    # dp[i][w] = maximum value using first i items with weight limit w
    dp = [[0] * (capacity + 1) for _ in range(n + 1)]
    
    for i in range(1, n + 1):
        for w in range(capacity + 1):
            # Don't take item i-1
            dp[i][w] = dp[i-1][w]
            
            # Take item i-1 if possible
            if weights[i-1] <= w:
                dp[i][w] = max(dp[i][w], 
                              dp[i-1][w - weights[i-1]] + values[i-1])
    
    return dp[n][capacity]

# Space-optimized version
def knapsack_01_optimized(weights, values, capacity):
    """Space-optimized 0/1 Knapsack."""
    dp = [0] * (capacity + 1)
    
    for i in range(len(weights)):
        # Traverse backwards to avoid using updated values
        for w in range(capacity, weights[i] - 1, -1):
            dp[w] = max(dp[w], dp[w - weights[i]] + values[i])
    
    return dp[capacity]
```

### Pattern 4: String DP
**Characteristics**: Problems involving string manipulation or comparison
**Common Problems**: Edit Distance, Longest Common Subsequence, Palindrome Partitioning

```python
# Template: String DP
def string_dp_template(s1, s2):
    """
    General template for string DP problems.
    
    Time: O(m*n), Space: O(m*n) or O(n) with optimization
    """
    m, n = len(s1), len(s2)
    
    # dp[i][j] represents optimal solution for s1[:i] and s2[:j]
    dp = [[0] * (n + 1) for _ in range(m + 1)]
    
    # Base cases
    for i in range(m + 1):
        dp[i][0] = base_case_for_empty_s2(i)
    for j in range(n + 1):
        dp[0][j] = base_case_for_empty_s1(j)
    
    # Fill the DP table
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if s1[i-1] == s2[j-1]:
                dp[i][j] = match_case(dp[i-1][j-1])
            else:
                dp[i][j] = mismatch_case(dp[i-1][j], dp[i][j-1], dp[i-1][j-1])
    
    return dp[m][n]

# Example: Edit Distance
def minDistance(word1, word2):
    """Minimum edit distance between two words."""
    m, n = len(word1), len(word2)
    dp = [[0] * (n + 1) for _ in range(m + 1)]
    
    # Base cases
    for i in range(m + 1):
        dp[i][0] = i  # Delete all characters
    for j in range(n + 1):
        dp[0][j] = j  # Insert all characters
    
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if word1[i-1] == word2[j-1]:
                dp[i][j] = dp[i-1][j-1]  # No operation needed
            else:
                dp[i][j] = 1 + min(
                    dp[i-1][j],    # Delete
                    dp[i][j-1],    # Insert
                    dp[i-1][j-1]   # Replace
                )
    
    return dp[m][n]
```

## 🎯 Common DP Problems by Category

### Easy Level (Foundation Building)
1. **Fibonacci Sequence** - Basic memoization
2. **Climbing Stairs** - Simple recurrence relation
3. **Min Cost Climbing Stairs** - Choice between options
4. **House Robber** - Non-adjacent selection
5. **Maximum Subarray** - Kadane's algorithm

### Medium Level (Pattern Recognition)
1. **Coin Change** - Unbounded knapsack
2. **Longest Increasing Subsequence** - Sequence DP
3. **Unique Paths** - Grid traversal
4. **Word Break** - String partitioning
5. **Partition Equal Subset Sum** - Subset sum problem

### Hard Level (Advanced Techniques)
1. **Edit Distance** - String transformation
2. **Regular Expression Matching** - Complex state transitions
3. **Burst Balloons** - Interval DP
4. **Cherry Pickup** - Multiple path optimization
5. **Russian Doll Envelopes** - Multi-dimensional LIS

## 🛠️ Implementation Strategies

### Memoization (Top-Down)
```python
def solve_with_memoization(n):
    """
    Top-down approach with memoization.
    
    Pros:
    - Intuitive recursive thinking
    - Only computes needed subproblems
    - Easy to implement from recursive solution
    
    Cons:
    - Function call overhead
    - Risk of stack overflow for large inputs
    """
    memo = {}
    
    def dp(state):
        if state in memo:
            return memo[state]
        
        if base_case(state):
            return base_value
        
        result = recurrence_relation(state)
        memo[state] = result
        return result
    
    return dp(n)

# Example: Fibonacci with memoization
def fibonacci_memo(n):
    memo = {}
    
    def fib(n):
        if n in memo:
            return memo[n]
        if n <= 1:
            return n
        
        memo[n] = fib(n-1) + fib(n-2)
        return memo[n]
    
    return fib(n)
```

### Tabulation (Bottom-Up)
```python
def solve_with_tabulation(n):
    """
    Bottom-up approach with tabulation.
    
    Pros:
    - No function call overhead
    - Iterative approach (no stack overflow)
    - Often easier to optimize space
    
    Cons:
    - May compute unnecessary subproblems
    - Requires careful ordering of computation
    """
    dp = [0] * (n + 1)
    
    # Base cases
    dp[0] = base_value_0
    if n > 0:
        dp[1] = base_value_1
    
    # Fill table in order
    for i in range(2, n + 1):
        dp[i] = recurrence_relation(dp, i)
    
    return dp[n]

# Example: Fibonacci with tabulation
def fibonacci_tab(n):
    if n <= 1:
        return n
    
    dp = [0] * (n + 1)
    dp[0], dp[1] = 0, 1
    
    for i in range(2, n + 1):
        dp[i] = dp[i-1] + dp[i-2]
    
    return dp[n]
```

### Space Optimization
```python
def solve_space_optimized(n):
    """
    Space-optimized DP when only recent states are needed.
    
    Common Optimizations:
    - Rolling array for 2D DP
    - Variables for linear DP
    - Sliding window for sequence problems
    """
    # For linear DP with O(1) space
    if n <= 1:
        return base_cases[n]
    
    prev2, prev1 = base_cases[0], base_cases[1]
    
    for i in range(2, n + 1):
        current = recurrence_relation(prev1, prev2)
        prev2, prev1 = prev1, current
    
    return prev1

# Example: Space-optimized Fibonacci
def fibonacci_optimized(n):
    if n <= 1:
        return n
    
    prev2, prev1 = 0, 1
    for i in range(2, n + 1):
        current = prev1 + prev2
        prev2, prev1 = prev1, current
    
    return prev1
```

## 📈 Complexity Analysis

### Time Complexity Patterns
```python
# Common DP time complexities
"""
Linear DP (1D):           O(n)
Grid DP (2D):            O(m × n)
Knapsack:                O(n × W)
String DP:               O(m × n)
Tree DP:                 O(n)
Interval DP:             O(n³)
State Machine DP:        O(n × states)
"""
```

### Space Complexity Optimization
```python
# Space optimization techniques
"""
Original Space:          O(state_space)
Rolling Array:           O(min_dimension)
Variables Only:          O(1)
Memoization:            O(unique_subproblems)
"""

def analyze_space_optimization():
    """
    Guidelines for space optimization:
    
    1. Linear DP: Usually O(n) → O(1)
    2. 2D DP: Usually O(m×n) → O(min(m,n))
    3. Check if current state only depends on recent states
    4. Use rolling array when full history not needed
    """
    pass
```

## 🧪 Practice Problem Sets

### Beginner DP Problems
```python
# Problem Set 1: Introduction to DP
problems_beginner = [
    "70. Climbing Stairs",
    "746. Min Cost Climbing Stairs", 
    "198. House Robber",
    "53. Maximum Subarray",
    "121. Best Time to Buy and Sell Stock"
]

# Problem Set 2: Basic Patterns
problems_basic_patterns = [
    "322. Coin Change",
    "518. Coin Change 2",
    "62. Unique Paths",
    "64. Minimum Path Sum",
    "91. Decode Ways"
]
```

### Intermediate DP Problems
```python
# Problem Set 3: String DP
problems_string_dp = [
    "1143. Longest Common Subsequence",
    "72. Edit Distance",
    "139. Word Break",
    "647. Palindromic Substrings",
    "5. Longest Palindromic Substring"
]

# Problem Set 4: Knapsack Variants
problems_knapsack = [
    "416. Partition Equal Subset Sum",
    "494. Target Sum",
    "474. Ones and Zeroes",
    "1049. Last Stone Weight II",
    "879. Profitable Schemes"
]
```

### Advanced DP Problems
```python
# Problem Set 5: Advanced Patterns
problems_advanced = [
    "300. Longest Increasing Subsequence",
    "354. Russian Doll Envelopes",
    "312. Burst Balloons",
    "741. Cherry Pickup",
    "10. Regular Expression Matching"
]

# Problem Set 6: Optimization Techniques
problems_optimization = [
    "188. Best Time to Buy and Sell Stock IV",
    "1235. Maximum Profit in Job Scheduling",
    "1547. Minimum Cost to Cut a Stick",
    "1000. Minimum Cost to Merge Stones",
    "546. Remove Boxes"
]
```

## 🎯 Mastery Checklist

### Core Concepts
- [ ] Understand optimal substructure property
- [ ] Identify overlapping subproblems
- [ ] Design appropriate state representations
- [ ] Write correct recurrence relations
- [ ] Implement both memoization and tabulation
- [ ] Optimize space complexity when possible

### Pattern Recognition
- [ ] Linear DP problems (1D arrays)
- [ ] Grid DP problems (2D arrays)
- [ ] String DP problems (LCS, Edit Distance)
- [ ] Knapsack and subset problems
- [ ] Interval and range DP
- [ ] Tree and graph DP

### Problem-Solving Skills
- [ ] Solve 20+ easy DP problems
- [ ] Solve 15+ medium DP problems
- [ ] Solve 5+ hard DP problems
- [ ] Explain solutions clearly
- [ ] Optimize time and space complexity
- [ ] Handle edge cases properly

## 🚀 Study Strategy

### Week-by-Week Plan

**Week 1-2: Fundamentals**
- Understand DP principles
- Master memoization and tabulation
- Solve linear DP problems
- Practice space optimization

**Week 3-4: Basic Patterns**
- Grid DP problems
- String DP introduction
- Basic knapsack problems
- Decision-making DP

**Week 5-6: Intermediate Patterns**
- Advanced string DP
- Sequence DP problems
- Knapsack variants
- Interval DP introduction

**Week 7-8: Advanced Techniques**
- Tree DP
- State machine DP
- Optimization techniques
- Complex problem solving

### Daily Practice Routine
1. **Theory Study** (20 minutes): Read concepts and patterns
2. **Problem Solving** (40 minutes): Solve 1-2 problems with different approaches
3. **Review** (15 minutes): Analyze solutions and optimization opportunities

## 📚 Additional Resources

### Books
- "Dynamic Programming for Coding Interviews" by Meenakshi and Kamal Rawat
- "Algorithm Design" by Jon Kleinberg and Éva Tardos
- "Introduction to Algorithms" by CLRS

### Online Resources
- LeetCode DP problems with solutions
- GeeksforGeeks DP articles
- YouTube channels: Back To Back SWE, Tushar Roy
- Codeforces DP problems and tutorials

### Visualization Tools
- DP visualizer tools
- Recursion tree visualizers
- State transition diagrams
- Complexity analysis tools

---

**Remember**: Dynamic Programming is all about recognizing patterns and building solutions systematically. Start with understanding the fundamentals, practice identifying when to use DP, and gradually work your way up to more complex problems. The key is to develop intuition for state design and recurrence relations!
