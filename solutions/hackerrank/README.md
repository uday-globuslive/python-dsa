# HackerRank Solutions

## 📖 Overview

This directory contains comprehensive solutions to HackerRank problems, organized by domain and difficulty. Each solution includes detailed explanations, multiple approaches, complexity analysis, and test cases.

## 🗂️ Organization Structure

```
hackerrank/
├── algorithms/
│   ├── warmup/
│   ├── implementation/
│   ├── strings/
│   ├── sorting/
│   ├── search/
│   ├── graph-theory/
│   ├── greedy/
│   ├── dynamic-programming/
│   └── constructive-algorithms/
├── data-structures/
│   ├── arrays/
│   ├── linked-lists/
│   ├── stacks/
│   ├── queues/
│   ├── trees/
│   ├── balanced-trees/
│   ├── heap/
│   └── trie/
├── mathematics/
│   ├── fundamentals/
│   ├── number-theory/
│   ├── combinatorics/
│   └── geometry/
└── python/
    ├── introduction/
    ├── basic-data-types/
    ├── strings/
    ├── sets/
    ├── collections/
    └── date-and-time/
```

## 🎯 Solution Format

Each solution follows a standardized format for consistency and clarity:

### Template Structure
```python
"""
Problem: [Problem Title]
URL: [HackerRank Problem URL]
Difficulty: [Easy/Medium/Hard]
Domain: [Algorithms/Data Structures/Mathematics/Python]

Problem Description:
[Brief description of the problem]

Constraints:
[List of constraints from the problem]

Sample Input/Output:
[Examples provided in the problem]
"""

def solution_approach_1(params):
    """
    Approach 1: [Name of approach, e.g., Brute Force]
    
    Time Complexity: O(?)
    Space Complexity: O(?)
    
    Algorithm:
    1. [Step 1 description]
    2. [Step 2 description]
    3. [Step 3 description]
    """
    # Implementation
    pass

def solution_approach_2(params):
    """
    Approach 2: [Name of approach, e.g., Optimized]
    
    Time Complexity: O(?)
    Space Complexity: O(?)
    
    Algorithm:
    1. [Step 1 description]
    2. [Step 2 description]
    3. [Step 3 description]
    """
    # Implementation
    pass

def main():
    """Main function for HackerRank submission."""
    # Input reading
    # Function call
    # Output formatting
    pass

if __name__ == "__main__":
    main()

# Test Cases
def test_solution():
    """Test cases for the solution."""
    # Test case 1
    assert solution_approach_1(test_input) == expected_output
    
    # Test case 2
    assert solution_approach_2(test_input) == expected_output
    
    print("All test cases passed!")

# Complexity Analysis
"""
Time Complexity Analysis:
- Approach 1: [Detailed analysis]
- Approach 2: [Detailed analysis]

Space Complexity Analysis:
- Approach 1: [Detailed analysis]
- Approach 2: [Detailed analysis]

Which approach to choose:
[Explanation of when to use each approach]
"""
```

## 🏆 Problem Categories

### Algorithms Domain

#### Warmup Problems
**Purpose**: Build confidence and practice basic programming concepts
**Examples**:
- Simple Array Sum
- Compare the Triplets
- A Very Big Sum
- Diagonal Difference
- Plus Minus

```python
# Example: Simple Array Sum
def simpleArraySum(ar):
    """
    Calculate sum of array elements.
    
    Time Complexity: O(n)
    Space Complexity: O(1)
    """
    return sum(ar)
```

#### Implementation Problems
**Purpose**: Practice logical thinking and careful implementation
**Examples**:
- Grading Students
- Apple and Orange
- Breaking the Records
- Birthday Chocolate
- Divisible Sum Pairs

```python
# Example: Grading Students
def gradingStudents(grades):
    """
    Round grades according to university policy.
    
    Time Complexity: O(n)
    Space Complexity: O(1)
    """
    result = []
    for grade in grades:
        if grade >= 38:
            next_multiple = ((grade // 5) + 1) * 5
            if next_multiple - grade < 3:
                result.append(next_multiple)
            else:
                result.append(grade)
        else:
            result.append(grade)
    return result
```

#### String Problems
**Purpose**: Master string manipulation and pattern matching
**Examples**:
- HackerRank in a String!
- Pangrams
- Weighted Uniform Strings
- Separate the Numbers
- String Construction

#### Sorting Problems
**Purpose**: Understand sorting algorithms and their applications
**Examples**:
- Big Sorting
- Insertion Sort
- Quicksort
- Counting Sort
- Fraudulent Activity Notifications

#### Search Problems
**Purpose**: Learn various searching techniques
**Examples**:
- Ice Cream Parlor
- Missing Numbers
- Pairs
- Triple Sum
- Hash Tables: Ransom Note

### Data Structures Domain

#### Array Problems
**Purpose**: Master array operations and manipulations
**Examples**:
- Arrays: Left Rotation
- Dynamic Array
- Sparse Arrays
- Array Manipulation
- Minimum Swaps 2

#### Linked List Problems
**Purpose**: Understand pointer manipulation and linked structures
**Examples**:
- Print the Elements of a Linked List
- Insert a Node at the Tail
- Delete a Node
- Compare two linked lists
- Merge two sorted linked lists

#### Stack Problems
**Purpose**: Learn LIFO operations and applications
**Examples**:
- Maximum Element
- Balanced Brackets
- Equal Stacks
- Game of Two Stacks
- Largest Rectangle

#### Tree Problems
**Purpose**: Understand hierarchical data structures
**Examples**:
- Tree: Preorder Traversal
- Tree: Height of a Binary Tree
- Tree: Level Order Traversal
- Binary Search Tree: Insertion
- Tree: Huffman Decoding

## 📊 Difficulty Progression

### Easy Problems (Beginner Level)
**Characteristics**:
- Single concept application
- Straightforward implementation
- Small constraints
- Clear problem statements

**Learning Focus**:
- Basic programming constructs
- Simple algorithms
- Input/output handling
- Basic data structure operations

**Examples with Solutions**:

```python
# Plus Minus - Easy
def plusMinus(arr):
    """
    Calculate ratios of positive, negative, and zero elements.
    
    Time Complexity: O(n)
    Space Complexity: O(1)
    """
    n = len(arr)
    positive = negative = zero = 0
    
    for num in arr:
        if num > 0:
            positive += 1
        elif num < 0:
            negative += 1
        else:
            zero += 1
    
    print(f"{positive/n:.6f}")
    print(f"{negative/n:.6f}")
    print(f"{zero/n:.6f}")

# Staircase - Easy
def staircase(n):
    """
    Print a staircase pattern of size n.
    
    Time Complexity: O(n²)
    Space Complexity: O(1)
    """
    for i in range(1, n + 1):
        print(' ' * (n - i) + '#' * i)
```

### Medium Problems (Intermediate Level)
**Characteristics**:
- Multiple concept integration
- Moderate complexity
- Algorithmic thinking required
- Some optimization needed

**Learning Focus**:
- Algorithm design
- Complexity analysis
- Data structure selection
- Problem-solving patterns

**Examples with Solutions**:

```python
# Climbing the Leaderboard - Medium
def climbingLeaderboard(ranked, player):
    """
    Determine player's rank after each game.
    
    Time Complexity: O(n + m)
    Space Complexity: O(n)
    """
    # Remove duplicates and sort in descending order
    unique_scores = sorted(list(set(ranked)), reverse=True)
    result = []
    
    for score in player:
        # Binary search for position
        left, right = 0, len(unique_scores)
        while left < right:
            mid = (left + right) // 2
            if unique_scores[mid] <= score:
                right = mid
            else:
                left = mid + 1
        result.append(left + 1)
    
    return result

# Organizing Containers of Balls - Medium
def organizingContainers(container):
    """
    Determine if balls can be organized by type.
    
    Time Complexity: O(n²)
    Space Complexity: O(n)
    """
    n = len(container)
    
    # Calculate container capacities
    container_sizes = [sum(row) for row in container]
    
    # Calculate ball type counts
    ball_counts = [sum(container[i][j] for i in range(n)) for j in range(n)]
    
    # Sort both lists and compare
    return sorted(container_sizes) == sorted(ball_counts)
```

### Hard Problems (Advanced Level)
**Characteristics**:
- Complex algorithms required
- Advanced data structures
- Multiple optimization levels
- Deep algorithmic insight needed

**Learning Focus**:
- Advanced algorithms
- Complex data structures
- Optimization techniques
- Mathematical insights

## 🛠️ Development Workflow

### Solution Development Process

1. **Problem Analysis** (20% of time)
   ```python
   # Analysis template
   """
   PROBLEM ANALYSIS:
   
   1. Understanding:
      - What exactly are we asked to find/compute?
      - What are the inputs and their constraints?
      - What should the output format be?
   
   2. Examples:
      - Work through given examples manually
      - Create additional test cases
      - Identify edge cases
   
   3. Constraints:
      - Time limit implications
      - Memory limit considerations
      - Input size impact on algorithm choice
   """
   ```

2. **Approach Design** (30% of time)
   ```python
   # Approach comparison template
   """
   APPROACH COMPARISON:
   
   Approach 1: [Name]
   - Algorithm: [Description]
   - Time: O(?)
   - Space: O(?)
   - Pros: [Advantages]
   - Cons: [Disadvantages]
   
   Approach 2: [Name]
   - Algorithm: [Description]
   - Time: O(?)
   - Space: O(?)
   - Pros: [Advantages]
   - Cons: [Disadvantages]
   
   Chosen Approach: [Selection with reasoning]
   """
   ```

3. **Implementation** (40% of time)
   ```python
   # Implementation with debugging
   def solve_problem(inputs):
       """
       Main solution function.
       
       Args:
           inputs: Problem input parameters
       
       Returns:
           Problem solution
       """
       # Step 1: Input validation
       if not validate_input(inputs):
           raise ValueError("Invalid input")
       
       # Step 2: Core algorithm
       result = core_algorithm(inputs)
       
       # Step 3: Output formatting
       return format_output(result)
   
   def validate_input(inputs):
       """Validate input constraints."""
       # Implementation
       pass
   
   def core_algorithm(inputs):
       """Core problem-solving logic."""
       # Implementation
       pass
   
   def format_output(result):
       """Format output according to requirements."""
       # Implementation
       pass
   ```

4. **Testing and Optimization** (10% of time)
   ```python
   # Comprehensive testing
   def test_comprehensive():
       """Test with various cases."""
       
       # Test given examples
       test_given_examples()
       
       # Test edge cases
       test_edge_cases()
       
       # Test performance
       test_performance()
       
       # Test memory usage
       test_memory_usage()
   
   def test_given_examples():
       """Test with provided examples."""
       # Implementation
       pass
   
   def test_edge_cases():
       """Test boundary conditions."""
       test_cases = [
           # Minimum input size
           # Maximum input size
           # All same elements
           # All different elements
           # Empty input (if applicable)
       ]
       # Implementation
       pass
   ```

### Code Quality Standards

```python
# Code quality checklist
"""
CODE QUALITY CHECKLIST:

✅ Readability:
   - Clear variable names
   - Appropriate comments
   - Logical code structure
   - Consistent formatting

✅ Efficiency:
   - Optimal time complexity
   - Reasonable space usage
   - No redundant operations
   - Efficient data structures

✅ Robustness:
   - Input validation
   - Edge case handling
   - Error handling
   - Boundary checking

✅ Maintainability:
   - Modular design
   - Reusable functions
   - Clear documentation
   - Easy to modify
"""
```

## 📈 Progress Tracking

### Performance Metrics
```python
class HackerRankProgress:
    def __init__(self):
        self.problems_solved = {}
        self.domains = {
            'algorithms': 0,
            'data_structures': 0,
            'mathematics': 0,
            'python': 0
        }
        self.difficulty_stats = {
            'easy': 0,
            'medium': 0,
            'hard': 0
        }
    
    def add_solution(self, problem_name, domain, difficulty, points):
        """Track a solved problem."""
        self.problems_solved[problem_name] = {
            'domain': domain,
            'difficulty': difficulty,
            'points': points,
            'date_solved': datetime.now()
        }
        self.domains[domain] += points
        self.difficulty_stats[difficulty] += 1
    
    def get_stats(self):
        """Get comprehensive statistics."""
        total_problems = len(self.problems_solved)
        total_points = sum(self.domains.values())
        
        return {
            'total_problems': total_problems,
            'total_points': total_points,
            'domain_breakdown': self.domains,
            'difficulty_breakdown': self.difficulty_stats,
            'average_points': total_points / total_problems if total_problems > 0 else 0
        }
```

### Weekly Goals
- **Week 1-2**: Complete Python domain (20+ problems)
- **Week 3-4**: Algorithms warmup and implementation (25+ problems)
- **Week 5-6**: Data structures basics (20+ problems)
- **Week 7-8**: Sorting and searching (15+ problems)
- **Week 9-10**: String algorithms (15+ problems)
- **Week 11-12**: Dynamic programming basics (10+ problems)

## 🎯 Tips for Success

### HackerRank-Specific Strategies

1. **Read Carefully**: HackerRank problems often have specific output formats
2. **Check Constraints**: Pay attention to time and memory limits
3. **Use Fast I/O**: For large inputs, optimize input/output operations
4. **Test Thoroughly**: Use provided test cases and create additional ones
5. **Submit Early**: Get partial credit even with suboptimal solutions

### Common Pitfalls to Avoid

1. **Output Format**: Exactly match the required output format
2. **Integer Overflow**: Use appropriate data types for large numbers
3. **Edge Cases**: Handle minimum and maximum constraint values
4. **Time Limits**: Optimize for the given time constraints
5. **Memory Limits**: Be mindful of space complexity

### Platform Features to Leverage

1. **Editorial Solutions**: Study official explanations after solving
2. **Discussion Forum**: Learn from community solutions
3. **Test Cases**: Use provided test cases for debugging
4. **Submissions**: Analyze why submissions fail
5. **Leaderboard**: Compare approaches with top solutions

## 📚 Additional Resources

### Documentation and Tutorials
- HackerRank official documentation
- Algorithm visualization tools
- Complexity analysis guides
- Python optimization techniques

### Community Resources
- HackerRank discussion forums
- GitHub solution repositories
- YouTube tutorial channels
- Algorithm study groups

---

**Remember**: HackerRank is excellent for building systematic problem-solving skills. Focus on understanding the problem thoroughly before jumping to implementation. The platform's structured approach helps build strong foundations for more advanced competitive programming and technical interviews!
