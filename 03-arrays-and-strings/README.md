# Arrays and Strings

## 📖 Module Overview

Arrays and strings are the most fundamental data structures in programming and form the foundation for most algorithmic problems. This module provides comprehensive coverage of array and string manipulations, essential techniques, and common problem-solving patterns.

## 🎯 Learning Objectives

- Master array operations and manipulations
- Understand string processing and pattern matching
- Learn two-pointer and sliding window techniques
- Develop pattern recognition for array/string problems
- Optimize solutions for time and space complexity
- Handle edge cases and input validation

## 📚 Table of Contents

### 1. Array Fundamentals
- **[1.1 Array Basics and Memory Layout](./01-array-basics.md)**
- **[1.2 Array Operations and Time Complexity](./02-array-operations.md)**
- **[1.3 Multi-dimensional Arrays](./03-multidimensional-arrays.md)**
- **[1.4 Dynamic Arrays vs Static Arrays](./04-dynamic-vs-static.md)**

### 2. String Fundamentals
- **[2.1 String Representation and Memory](./05-string-basics.md)**
- **[2.2 String Operations and Methods](./06-string-operations.md)**
- **[2.3 String Mutability and Performance](./07-string-mutability.md)**
- **[2.4 Character Encoding and Unicode](./08-character-encoding.md)**

### 3. Essential Array Techniques
- **[3.1 Linear Search and Binary Search](./09-searching-techniques.md)**
- **[3.2 Array Sorting Fundamentals](./10-sorting-fundamentals.md)**
- **[3.3 Prefix Sums and Range Queries](./11-prefix-sums.md)**
- **[3.4 Array Rotation and Reversal](./12-rotation-reversal.md)**

### 4. Two-Pointer Technique
- **[4.1 Introduction to Two Pointers](./13-two-pointer-intro.md)**
- **[4.2 Opposite Direction Pointers](./14-opposite-pointers.md)**
- **[4.3 Same Direction Pointers](./15-same-direction-pointers.md)**
- **[4.4 Fast and Slow Pointers](./16-fast-slow-pointers.md)**

### 5. Sliding Window Technique
- **[5.1 Fixed Size Sliding Window](./17-fixed-sliding-window.md)**
- **[5.2 Variable Size Sliding Window](./18-variable-sliding-window.md)**
- **[5.3 Sliding Window Maximum/Minimum](./19-sliding-window-extremes.md)**
- **[5.4 Advanced Sliding Window Patterns](./20-advanced-sliding-window.md)**

### 6. String Pattern Matching
- **[6.1 Naive Pattern Matching](./21-naive-pattern-matching.md)**
- **[6.2 KMP Algorithm](./22-kmp-algorithm.md)**
- **[6.3 Rabin-Karp Algorithm](./23-rabin-karp.md)**
- **[6.4 Z-Algorithm](./24-z-algorithm.md)**

### 7. Advanced Array Problems
- **[7.1 Subarray Problems](./25-subarray-problems.md)**
- **[7.2 Matrix Manipulation](./26-matrix-manipulation.md)**
- **[7.3 Array Partitioning](./27-array-partitioning.md)**
- **[7.4 Merge Operations](./28-merge-operations.md)**

### 8. Advanced String Problems
- **[8.1 Palindrome Problems](./29-palindrome-problems.md)**
- **[8.2 Anagram and Permutation Problems](./30-anagram-problems.md)**
- **[8.3 String Transformation](./31-string-transformation.md)**
- **[8.4 Longest Common Subsequence/Substring](./32-longest-common.md)**

## 🛠️ Common Problem Patterns

### Pattern 1: Two Pointers
**When to Use**: Problems involving pairs, triplets, or comparison of elements
**Common Problems**: Two Sum, Three Sum, Remove Duplicates, Palindrome Check

```python
def two_sum_sorted(arr, target):
    """Find two numbers that add up to target in sorted array."""
    left, right = 0, len(arr) - 1
    
    while left < right:
        current_sum = arr[left] + arr[right]
        if current_sum == target:
            return [left, right]
        elif current_sum < target:
            left += 1
        else:
            right -= 1
    
    return []
```

### Pattern 2: Sliding Window
**When to Use**: Problems involving subarrays or substrings with specific conditions
**Common Problems**: Maximum Sum Subarray, Longest Substring, Minimum Window

```python
def max_sum_subarray_k(arr, k):
    """Find maximum sum of subarray of size k."""
    if len(arr) < k:
        return 0
    
    # Calculate sum of first window
    window_sum = sum(arr[:k])
    max_sum = window_sum
    
    # Slide the window
    for i in range(k, len(arr)):
        window_sum = window_sum - arr[i - k] + arr[i]
        max_sum = max(max_sum, window_sum)
    
    return max_sum
```

### Pattern 3: Prefix Sum
**When to Use**: Range sum queries, subarray sum problems
**Common Problems**: Range Sum Query, Subarray Sum Equals K

```python
def range_sum_query(arr, queries):
    """Process multiple range sum queries efficiently."""
    # Build prefix sum array
    prefix_sum = [0] * (len(arr) + 1)
    for i in range(len(arr)):
        prefix_sum[i + 1] = prefix_sum[i] + arr[i]
    
    results = []
    for start, end in queries:
        # Sum from start to end (inclusive)
        range_sum = prefix_sum[end + 1] - prefix_sum[start]
        results.append(range_sum)
    
    return results
```

### Pattern 4: Hash Map for Frequency
**When to Use**: Character/element frequency problems, anagrams
**Common Problems**: Valid Anagram, Group Anagrams, Character Frequency

```python
def is_anagram(s1, s2):
    """Check if two strings are anagrams."""
    if len(s1) != len(s2):
        return False
    
    char_count = {}
    
    # Count characters in first string
    for char in s1:
        char_count[char] = char_count.get(char, 0) + 1
    
    # Subtract characters from second string
    for char in s2:
        if char not in char_count:
            return False
        char_count[char] -= 1
        if char_count[char] == 0:
            del char_count[char]
    
    return len(char_count) == 0
```

## 📊 Complexity Analysis Guide

### Array Operations
| Operation | Best Case | Average Case | Worst Case | Space |
|-----------|-----------|--------------|------------|--------|
| Access by index | O(1) | O(1) | O(1) | O(1) |
| Linear search | O(1) | O(n) | O(n) | O(1) |
| Binary search | O(1) | O(log n) | O(log n) | O(1) |
| Insertion at end | O(1) | O(1) | O(n) | O(1) |
| Insertion at middle | O(1) | O(n) | O(n) | O(1) |
| Deletion | O(1) | O(n) | O(n) | O(1) |

### String Operations
| Operation | Complexity | Notes |
|-----------|------------|--------|
| Character access | O(1) | Direct indexing |
| String concatenation | O(n + m) | Creates new string |
| Substring | O(k) | Where k is substring length |
| String comparison | O(min(n, m)) | Character by character |
| Pattern matching (naive) | O(nm) | n = text, m = pattern |
| Pattern matching (KMP) | O(n + m) | With preprocessing |

## 🎯 Problem Categories

### Easy Level Problems (Building Foundation)
1. **Array Manipulation**
   - Find maximum/minimum element
   - Reverse an array
   - Rotate array by k positions
   - Remove duplicates from sorted array

2. **String Processing**
   - Check if string is palindrome
   - Count characters in string
   - Convert case (upper/lower)
   - Remove spaces and special characters

3. **Basic Searching**
   - Linear search implementation
   - Binary search in sorted array
   - Find first/last occurrence
   - Search in rotated sorted array

### Medium Level Problems (Pattern Recognition)
1. **Two Pointer Problems**
   - Two Sum in sorted array
   - Three Sum problem
   - Container with most water
   - Trapping rainwater

2. **Sliding Window Problems**
   - Maximum sum subarray of size k
   - Longest substring without repeating characters
   - Minimum window substring
   - Sliding window median

3. **Subarray Problems**
   - Maximum subarray sum (Kadane's algorithm)
   - Subarray sum equals k
   - Product of array except self
   - Maximum product subarray

### Hard Level Problems (Advanced Techniques)
1. **Advanced String Algorithms**
   - Implement KMP algorithm
   - Regular expression matching
   - Edit distance
   - Longest palindromic substring

2. **Complex Array Problems**
   - Merge intervals
   - Insert interval
   - Spiral matrix traversal
   - Search in 2D matrix

3. **Optimization Problems**
   - Best time to buy/sell stock
   - Gas station problem
   - Jump game variations
   - Candy distribution

## 🛠️ Implementation Templates

### Two Pointer Template
```python
def two_pointer_template(arr):
    """General template for two pointer problems."""
    left, right = 0, len(arr) - 1
    
    while left < right:
        # Process current state
        if condition_met(arr[left], arr[right]):
            # Found solution or take action
            return result
        elif need_larger_sum():
            left += 1  # Move left pointer right
        else:
            right -= 1  # Move right pointer left
    
    return default_result
```

### Sliding Window Template
```python
def sliding_window_template(arr, k):
    """General template for sliding window problems."""
    window_start = 0
    window_sum = 0
    result = float('-inf')
    
    for window_end in range(len(arr)):
        # Add current element to window
        window_sum += arr[window_end]
        
        # Shrink window if needed
        while window_end - window_start + 1 > k:
            window_sum -= arr[window_start]
            window_start += 1
        
        # Update result if window size is k
        if window_end - window_start + 1 == k:
            result = max(result, window_sum)
    
    return result
```

### Binary Search Template
```python
def binary_search_template(arr, target):
    """General template for binary search problems."""
    left, right = 0, len(arr) - 1
    
    while left <= right:
        mid = left + (right - left) // 2
        
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return -1  # Not found
```

## 🧪 Hands-on Exercises

### Exercise Set 1: Array Fundamentals
```python
# Exercise 1: Implement dynamic array
class DynamicArray:
    def __init__(self):
        self.capacity = 1
        self.size = 0
        self.data = [None] * self.capacity
    
    def get(self, index):
        # Implement get operation
        pass
    
    def set(self, index, value):
        # Implement set operation
        pass
    
    def append(self, value):
        # Implement append operation
        pass
    
    def insert(self, index, value):
        # Implement insert operation
        pass
    
    def delete(self, index):
        # Implement delete operation
        pass

# Exercise 2: Matrix operations
def rotate_matrix_90_degrees(matrix):
    """Rotate n×n matrix 90 degrees clockwise in-place."""
    # Your implementation here
    pass

def spiral_traverse(matrix):
    """Return elements of matrix in spiral order."""
    # Your implementation here
    pass
```

### Exercise Set 2: String Algorithms
```python
# Exercise 1: Implement string matching algorithms
def naive_string_match(text, pattern):
    """Find all occurrences of pattern in text (naive approach)."""
    # Your implementation here
    pass

def kmp_string_match(text, pattern):
    """Find all occurrences using KMP algorithm."""
    # Your implementation here
    pass

# Exercise 2: String transformations
def longest_palindromic_substring(s):
    """Find the longest palindromic substring."""
    # Your implementation here
    pass

def minimum_edit_distance(s1, s2):
    """Calculate minimum operations to transform s1 to s2."""
    # Your implementation here
    pass
```

### Exercise Set 3: Advanced Problems
```python
# Exercise 1: Subarray problems
def maximum_subarray_sum(arr):
    """Find maximum sum of contiguous subarray (Kadane's algorithm)."""
    # Your implementation here
    pass

def subarray_sum_equals_k(arr, k):
    """Count number of subarrays with sum equal to k."""
    # Your implementation here
    pass

# Exercise 2: Two pointer problems
def three_sum(arr):
    """Find all unique triplets that sum to zero."""
    # Your implementation here
    pass

def container_with_most_water(heights):
    """Find container that can hold most water."""
    # Your implementation here
    pass
```

## 📈 Assessment and Progress Tracking

### Knowledge Assessment
- **Conceptual Understanding**: Data structure properties and operations
- **Algorithm Analysis**: Time and space complexity of different approaches
- **Pattern Recognition**: Identifying appropriate techniques for problems
- **Implementation Skills**: Writing clean, efficient code

### Practical Assessment
- **Coding Challenges**: Solve problems within time constraints
- **Code Review**: Analyze and improve existing solutions
- **Optimization Tasks**: Improve time/space complexity
- **Edge Case Handling**: Robust input validation and error handling

### Project-Based Assessment
- **Algorithm Visualization**: Create visual representations of algorithms
- **Performance Benchmarking**: Compare different implementation approaches
- **Problem Creation**: Design original problems and test cases
- **Documentation**: Write clear explanations and tutorials

## 🏆 Mastery Checklist

### Array Mastery
- [ ] Understand array memory layout and access patterns
- [ ] Implement efficient array operations
- [ ] Master two-pointer technique for array problems
- [ ] Use sliding window for subarray problems
- [ ] Apply prefix sum for range queries
- [ ] Handle 2D array manipulation

### String Mastery
- [ ] Understand string representation and immutability
- [ ] Implement efficient string operations
- [ ] Master pattern matching algorithms
- [ ] Apply sliding window to string problems
- [ ] Use hash maps for character frequency problems
- [ ] Handle Unicode and encoding issues

### Problem-Solving Mastery
- [ ] Recognize common problem patterns quickly
- [ ] Choose optimal data structures and algorithms
- [ ] Optimize solutions for time and space
- [ ] Handle edge cases and input validation
- [ ] Write comprehensive test cases
- [ ] Explain solutions clearly

## 🚀 Next Steps

After mastering this module:

1. **Consolidate Learning**: Review and practice key concepts
2. **Advanced Practice**: Solve harder problems on coding platforms
3. **Next Module**: Proceed to [Linked Lists](../04-linked-lists/README.md)
4. **Continuous Practice**: Maintain daily problem-solving routine

## 📚 Additional Resources

### Books
- "Programming Pearls" by Jon Bentley
- "Elements of Programming Interviews" by Aziz, Lee, and Prakash
- "Algorithms on Strings, Trees, and Sequences" by Dan Gusfield

### Online Resources
- LeetCode Array and String problems
- HackerRank Arrays and Strings domain
- GeeksforGeeks Array and String articles
- VisuAlgo for algorithm visualization

### Tools and Libraries
- Python's built-in `array` module
- NumPy for numerical arrays
- String processing with `re` module
- Performance profiling tools

---

**Remember**: Arrays and strings are the foundation of most algorithmic problems. Master these fundamentals thoroughly, as they'll be used extensively in more advanced data structures and algorithms. Focus on understanding the patterns and techniques rather than memorizing specific solutions!
