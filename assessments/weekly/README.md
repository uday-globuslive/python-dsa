# Weekly Assessments

## 📖 Overview

Weekly assessments are designed to evaluate your understanding of concepts, measure practical skills, and identify areas that need additional focus. Each assessment combines theoretical knowledge with hands-on problem solving.

## 🎯 Assessment Objectives

- Measure conceptual understanding of covered topics
- Evaluate practical implementation skills
- Test problem-solving approach and methodology
- Identify knowledge gaps for targeted improvement
- Track progress towards mastery goals

## 📅 Assessment Schedule

### Week 1: Python Fundamentals
**Topics Covered**: Basic syntax, data types, control structures, functions
**Assessment Format**: Mixed questions + coding challenges
**Duration**: 90 minutes
**Passing Score**: 80%

### Week 2: Problem Solving Fundamentals
**Topics Covered**: Algorithmic thinking, complexity analysis, debugging
**Assessment Format**: Problem analysis + implementation
**Duration**: 120 minutes
**Passing Score**: 75%

### Week 3-4: Arrays and Strings
**Topics Covered**: Array operations, string processing, two pointers, sliding window
**Assessment Format**: Coding problems + complexity analysis
**Duration**: 150 minutes
**Passing Score**: 75%

## 📋 Assessment Structure

### Part A: Conceptual Questions (30%)
**Format**: Multiple choice, short answers, true/false
**Topics**: Theory, terminology, complexity analysis
**Time Allocation**: 25-30% of total time

**Example Questions**:
```
1. What is the time complexity of accessing an element in an array by index?
   a) O(1)    b) O(log n)    c) O(n)    d) O(n²)

2. Which data structure is best for implementing undo functionality?
   a) Array   b) Stack      c) Queue    d) Hash Table

3. Explain the difference between memoization and tabulation in DP.
   [Short answer - 3-4 sentences]
```

### Part B: Code Analysis (25%)
**Format**: Debug code, predict output, analyze complexity
**Topics**: Reading and understanding existing code
**Time Allocation**: 20-25% of total time

**Example Questions**:
```python
# Question: What is the output of this code?
def mystery_function(arr):
    result = []
    for i in range(len(arr)):
        count = 0
        for j in range(len(arr)):
            if arr[j] < arr[i]:
                count += 1
        result.append(count)
    return result

print(mystery_function([3, 1, 4, 1, 5]))
# a) [2, 0, 4, 0, 4]  b) [1, 0, 3, 0, 4]  c) [2, 0, 3, 0, 4]  d) None of the above

# Question: What is the time complexity of the above function?
# Question: How would you optimize this function?
```

### Part C: Implementation Challenges (45%)
**Format**: Solve programming problems from scratch
**Topics**: Apply learned concepts to new problems
**Time Allocation**: 45-50% of total time

**Problem Categories**:
1. **Easy Implementation** (40% of Part C)
   - Direct application of concepts
   - Clear problem statements
   - Standard algorithms

2. **Medium Application** (40% of Part C)
   - Combine multiple concepts
   - Some optimization required
   - Pattern recognition needed

3. **Advanced Challenge** (20% of Part C)
   - Complex problem solving
   - Multiple approaches possible
   - Optimization and edge cases

## 🏆 Week-by-Week Assessment Details

### Week 1: Python Fundamentals Assessment

#### Conceptual Questions (30 points)
1. **Data Types and Operations** (10 points)
   - Variable declaration and naming conventions
   - Type conversion and casting
   - Operator precedence and associativity

2. **Control Structures** (10 points)
   - Conditional statements and logical operators
   - Loop types and their applications
   - Break, continue, and pass statements

3. **Functions and Scope** (10 points)
   - Function definition and calling
   - Parameter passing and return values
   - Local vs global scope

#### Code Analysis (25 points)
```python
# Problem 1: Predict the output (5 points)
x = 10
def func1():
    x = 20
    print(f"Inside func1: {x}")

def func2():
    global x
    x = 30
    print(f"Inside func2: {x}")

print(f"Initial: {x}")
func1()
print(f"After func1: {x}")
func2()
print(f"After func2: {x}")

# Problem 2: Debug this code (10 points)
def calculate_average(numbers):
    total = 0
    for num in numbers:
        total += num
    return total / len(numbers)

# Test cases
print(calculate_average([1, 2, 3, 4, 5]))  # Should work
print(calculate_average([]))               # What happens here?
print(calculate_average([1.5, 2.7, 3.2]))  # Should work

# Problem 3: Complexity analysis (10 points)
def find_pairs(arr, target):
    pairs = []
    for i in range(len(arr)):
        for j in range(i + 1, len(arr)):
            if arr[i] + arr[j] == target:
                pairs.append((arr[i], arr[j]))
    return pairs

# What is the time and space complexity?
```

#### Implementation Challenges (45 points)

**Problem 1: Basic Implementation (15 points)**
```python
def word_frequency(text):
    """
    Count frequency of each word in the given text.
    
    Args:
        text (str): Input text (case-insensitive)
    
    Returns:
        dict: Word frequencies
    
    Example:
        word_frequency("Hello world hello") → {"hello": 2, "world": 1}
    """
    # Your implementation here
    pass
```

**Problem 2: Medium Challenge (20 points)**
```python
def spiral_print(matrix):
    """
    Print matrix elements in spiral order (clockwise).
    
    Args:
        matrix (List[List[int]]): 2D matrix
    
    Returns:
        List[int]: Elements in spiral order
    
    Example:
        matrix = [[1,2,3],
                  [4,5,6],
                  [7,8,9]]
        Output: [1,2,3,6,9,8,7,4,5]
    """
    # Your implementation here
    pass
```

**Problem 3: Advanced Challenge (10 points)**
```python
def longest_common_prefix(strs):
    """
    Find the longest common prefix string amongst an array of strings.
    
    Args:
        strs (List[str]): Array of strings
    
    Returns:
        str: Longest common prefix
    
    Example:
        longest_common_prefix(["flower","flow","flight"]) → "fl"
        longest_common_prefix(["dog","racecar","car"]) → ""
    """
    # Your implementation here
    pass
```

### Week 3-4: Arrays and Strings Assessment

#### Conceptual Questions (30 points)
1. **Array Operations** (10 points)
   - Time complexity of array operations
   - Memory layout and cache efficiency
   - Dynamic vs static arrays

2. **String Processing** (10 points)
   - String immutability in Python
   - String methods and their complexity
   - Unicode and encoding considerations

3. **Algorithm Patterns** (10 points)
   - Two pointers technique applications
   - Sliding window pattern identification
   - When to use each approach

#### Code Analysis (25 points)
```python
# Problem 1: Algorithm identification (10 points)
def mystery_algorithm(arr, target):
    left, right = 0, len(arr) - 1
    
    while left < right:
        current_sum = arr[left] + arr[right]
        if current_sum == target:
            return [left, right]
        elif current_sum < target:
            left += 1
        else:
            right -= 1
    
    return [-1, -1]

# a) What algorithm pattern is this?
# b) What are the preconditions for this algorithm to work?
# c) What is the time and space complexity?

# Problem 2: Sliding window analysis (15 points)
def sliding_window_max(arr, k):
    if not arr or k == 0:
        return []
    
    result = []
    for i in range(len(arr) - k + 1):
        window_max = max(arr[i:i+k])
        result.append(window_max)
    
    return result

# a) What is the time complexity of this solution?
# b) How can you optimize this algorithm?
# c) Implement the optimized version.
```

#### Implementation Challenges (45 points)

**Problem 1: Two Pointers (15 points)**
```python
def three_sum(nums):
    """
    Find all unique triplets that sum to zero.
    
    Args:
        nums (List[int]): Array of integers
    
    Returns:
        List[List[int]]: All unique triplets that sum to zero
    
    Example:
        three_sum([-1,0,1,2,-1,-4]) → [[-1,-1,2],[-1,0,1]]
    """
    # Your implementation here
    pass
```

**Problem 2: Sliding Window (20 points)**
```python
def longest_substring_without_repeating(s):
    """
    Find length of longest substring without repeating characters.
    
    Args:
        s (str): Input string
    
    Returns:
        int: Length of longest substring
    
    Example:
        longest_substring_without_repeating("abcabcbb") → 3 ("abc")
        longest_substring_without_repeating("bbbbb") → 1 ("b")
    """
    # Your implementation here
    pass
```

**Problem 3: Advanced Array Manipulation (10 points)**
```python
def rotate_matrix(matrix):
    """
    Rotate n×n matrix 90 degrees clockwise in-place.
    
    Args:
        matrix (List[List[int]]): n×n matrix
    
    Returns:
        None: Modifies matrix in-place
    
    Example:
        matrix = [[1,2,3],
                  [4,5,6],
                  [7,8,9]]
        After rotation: [[7,4,1],
                        [8,5,2],
                        [9,6,3]]
    """
    # Your implementation here
    pass
```

## 📊 Grading Rubric

### Code Quality Assessment (Applied to Implementation Challenges)

#### Correctness (60%)
- **Excellent (90-100%)**: Solution works for all test cases including edge cases
- **Good (80-89%)**: Solution works for most test cases, minor edge case issues
- **Satisfactory (70-79%)**: Solution works for basic test cases, some logical errors
- **Needs Improvement (60-69%)**: Solution has significant logical errors
- **Unsatisfactory (<60%)**: Solution doesn't work or is incomplete

#### Code Quality (25%)
- **Excellent (90-100%)**: Clean, readable code with good naming and structure
- **Good (80-89%)**: Generally clean code with minor style issues
- **Satisfactory (70-79%)**: Code works but has readability issues
- **Needs Improvement (60-69%)**: Poor code organization and naming
- **Unsatisfactory (<60%)**: Code is hard to read and understand

#### Efficiency (15%)
- **Excellent (90-100%)**: Optimal time and space complexity
- **Good (80-89%)**: Good efficiency with minor suboptimal choices
- **Satisfactory (70-79%)**: Acceptable efficiency for the problem size
- **Needs Improvement (60-69%)**: Inefficient approach but works
- **Unsatisfactory (<60%)**: Very inefficient or incorrect complexity analysis

### Overall Grade Calculation
```
Final Score = (Conceptual Questions × 0.30) + 
              (Code Analysis × 0.25) + 
              (Implementation Challenges × 0.45)

Grade Scale:
A: 90-100%
B: 80-89%
C: 70-79%
D: 60-69%
F: <60%
```

## 🎯 Assessment Preparation Guide

### Study Strategies

#### Week Before Assessment
1. **Review Theory** (30% of time)
   - Read module summaries
   - Review key concepts and terminology
   - Practice complexity analysis

2. **Practice Implementation** (50% of time)
   - Solve similar problems
   - Time yourself on coding challenges
   - Practice writing code without IDE assistance

3. **Mock Assessment** (20% of time)
   - Take practice tests under time constraints
   - Review and analyze mistakes
   - Identify weak areas for final review

#### Day of Assessment
1. **Preparation**
   - Get adequate sleep and nutrition
   - Arrive early and set up workspace
   - Review key formulas and patterns

2. **Time Management**
   - Read all questions first
   - Allocate time based on point values
   - Leave time for review and testing

3. **Problem-Solving Strategy**
   - Understand the problem completely
   - Plan your approach before coding
   - Test with simple examples
   - Handle edge cases

### Common Mistakes to Avoid

#### Conceptual Questions
- Not reading questions carefully
- Confusing similar concepts
- Forgetting to consider edge cases in analysis

#### Code Analysis
- Not tracing through code step by step
- Ignoring variable scope and lifetime
- Miscalculating time/space complexity

#### Implementation Challenges
- Starting to code without planning
- Not testing with provided examples
- Ignoring edge cases (empty input, single element, etc.)
- Poor time management

## 📈 Post-Assessment Review

### Self-Assessment Checklist
```
After each assessment, review:

Strengths:
□ Which concepts did I understand well?
□ Which problem types did I solve efficiently?
□ What strategies worked well for me?

Areas for Improvement:
□ Which concepts need more study?
□ What types of errors did I make?
□ How can I improve my time management?

Action Plan:
□ What specific topics will I review?
□ Which problems will I practice?
□ How will I adjust my study strategy?
```

### Retake Policy
- Assessments with scores below 70% should be retaken
- Additional study time required before retake
- Focus on specific areas where improvement is needed
- Seek help from additional resources or mentoring

## 📚 Additional Resources

### Practice Platforms
- **LeetCode**: Timed problem-solving practice
- **HackerRank**: Structured assessment-style problems
- **CodeSignal**: Interactive coding assessments
- **Pramp**: Peer-to-peer mock interviews

### Study Materials
- Module README files for theory review
- Practice problem solutions for implementation patterns
- Complexity analysis guides and cheat sheets
- Code quality and style guides

---

**Remember**: Assessments are learning tools designed to help you identify areas for improvement. Focus on understanding concepts deeply rather than memorizing solutions. Use assessment feedback to guide your continued learning and practice!
