# LeetCode Solutions

## 📖 Overview

This directory contains comprehensive solutions to LeetCode problems, organized by patterns and difficulty levels. Each solution emphasizes pattern recognition, multiple approaches, and interview-focused explanations.

## 🗂️ Organization Structure

```
leetcode/
├── patterns/
│   ├── two-pointers/
│   ├── sliding-window/
│   ├── merge-intervals/
│   ├── cyclic-sort/
│   ├── in-place-reversal/
│   ├── tree-bfs/
│   ├── tree-dfs/
│   ├── two-heaps/
│   ├── subsets/
│   ├── modified-binary-search/
│   ├── top-k-elements/
│   ├── k-way-merge/
│   ├── knapsack/
│   └── topological-sort/
├── difficulty/
│   ├── easy/
│   ├── medium/
│   └── hard/
├── company-specific/
│   ├── google/
│   ├── amazon/
│   ├── microsoft/
│   ├── facebook/
│   └── apple/
└── contest/
    ├── weekly/
    ├── biweekly/
    └── monthly/
```

## 🎯 Solution Format

Each solution follows an interview-focused format:

### Template Structure
```python
"""
Problem: [Problem Number]. [Problem Title]
URL: [LeetCode Problem URL]
Difficulty: [Easy/Medium/Hard]
Pattern: [Algorithm Pattern]
Companies: [List of companies that asked this problem]

Problem Description:
[Brief description of the problem]

Constraints:
[List of constraints from the problem]

Example:
Input: [Sample input]
Output: [Sample output]
Explanation: [Why this output]
"""

class Solution:
    def approach_1(self, params) -> return_type:
        """
        Approach 1: [Name of approach]
        
        Time Complexity: O(?)
        Space Complexity: O(?)
        
        Intuition:
        [Explain the key insight that leads to this solution]
        
        Algorithm:
        1. [Step 1]
        2. [Step 2]
        3. [Step 3]
        """
        # Implementation
        pass
    
    def approach_2(self, params) -> return_type:
        """
        Approach 2: [Optimized approach]
        
        Time Complexity: O(?)
        Space Complexity: O(?)
        
        Intuition:
        [Key optimization insight]
        
        Algorithm:
        1. [Step 1]
        2. [Step 2]
        3. [Step 3]
        """
        # Implementation
        pass

# Test Cases
def test_solution():
    """Comprehensive test cases."""
    sol = Solution()
    
    # Test case 1
    assert sol.approach_1(input1) == expected1
    assert sol.approach_2(input1) == expected1
    
    # Test case 2
    assert sol.approach_1(input2) == expected2
    assert sol.approach_2(input2) == expected2
    
    # Edge cases
    assert sol.approach_1(edge_case) == edge_expected
    
    print("All test cases passed!")

# Interview Discussion Points
"""
INTERVIEW DISCUSSION:

1. Clarifying Questions:
   - [Questions to ask the interviewer]

2. Edge Cases:
   - [Important edge cases to consider]

3. Follow-up Questions:
   - [How would you modify if constraints changed?]
   - [How to handle if input size was much larger?]

4. Related Problems:
   - [List of similar problems]

5. Alternative Approaches:
   - [Other ways to solve this problem]
"""
```

## 🧩 Problem Patterns

### Pattern 1: Two Pointers
**When to Use**: Problems involving pairs, triplets, or comparing elements from both ends
**Common Problems**: Two Sum II, 3Sum, Remove Duplicates, Container With Most Water

```python
# Example: Two Sum II - Input array is sorted
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        """
        Two pointers approach for sorted array.
        
        Time: O(n), Space: O(1)
        """
        left, right = 0, len(numbers) - 1
        
        while left < right:
            current_sum = numbers[left] + numbers[right]
            if current_sum == target:
                return [left + 1, right + 1]  # 1-indexed
            elif current_sum < target:
                left += 1
            else:
                right -= 1
        
        return []  # No solution found
```

### Pattern 2: Sliding Window
**When to Use**: Problems involving subarrays or substrings with specific conditions
**Common Problems**: Maximum Sum Subarray, Longest Substring Without Repeating Characters

```python
# Example: Longest Substring Without Repeating Characters
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        """
        Sliding window with hash set.
        
        Time: O(n), Space: O(min(m,n)) where m is charset size
        """
        char_set = set()
        left = 0
        max_length = 0
        
        for right in range(len(s)):
            while s[right] in char_set:
                char_set.remove(s[left])
                left += 1
            
            char_set.add(s[right])
            max_length = max(max_length, right - left + 1)
        
        return max_length
```

### Pattern 3: Fast and Slow Pointers
**When to Use**: Cycle detection, finding middle elements
**Common Problems**: Linked List Cycle, Happy Number, Middle of Linked List

```python
# Example: Linked List Cycle
class Solution:
    def hasCycle(self, head: ListNode) -> bool:
        """
        Floyd's Cycle Detection Algorithm.
        
        Time: O(n), Space: O(1)
        """
        if not head or not head.next:
            return False
        
        slow = fast = head
        
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            
            if slow == fast:
                return True
        
        return False
```

### Pattern 4: Merge Intervals
**When to Use**: Overlapping intervals, scheduling problems
**Common Problems**: Merge Intervals, Insert Interval, Meeting Rooms

```python
# Example: Merge Intervals
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        """
        Sort and merge overlapping intervals.
        
        Time: O(n log n), Space: O(1)
        """
        if not intervals:
            return []
        
        intervals.sort(key=lambda x: x[0])
        merged = [intervals[0]]
        
        for current in intervals[1:]:
            last = merged[-1]
            
            if current[0] <= last[1]:  # Overlapping
                last[1] = max(last[1], current[1])
            else:  # Non-overlapping
                merged.append(current)
        
        return merged
```

### Pattern 5: Tree DFS
**When to Use**: Tree traversal, path problems, recursive solutions
**Common Problems**: Maximum Depth, Path Sum, Validate BST

```python
# Example: Maximum Depth of Binary Tree
class Solution:
    def maxDepth(self, root: TreeNode) -> int:
        """
        Recursive DFS approach.
        
        Time: O(n), Space: O(h) where h is height
        """
        if not root:
            return 0
        
        return 1 + max(self.maxDepth(root.left), self.maxDepth(root.right))
    
    def maxDepthIterative(self, root: TreeNode) -> int:
        """
        Iterative DFS using stack.
        
        Time: O(n), Space: O(h)
        """
        if not root:
            return 0
        
        stack = [(root, 1)]
        max_depth = 0
        
        while stack:
            node, depth = stack.pop()
            max_depth = max(max_depth, depth)
            
            if node.left:
                stack.append((node.left, depth + 1))
            if node.right:
                stack.append((node.right, depth + 1))
        
        return max_depth
```

### Pattern 6: Dynamic Programming
**When to Use**: Optimization problems, overlapping subproblems
**Common Problems**: Climbing Stairs, House Robber, Coin Change

```python
# Example: Climbing Stairs
class Solution:
    def climbStairs(self, n: int) -> int:
        """
        Bottom-up DP approach.
        
        Time: O(n), Space: O(1)
        """
        if n <= 2:
            return n
        
        # dp[i] represents ways to reach step i
        prev2, prev1 = 1, 2
        
        for i in range(3, n + 1):
            current = prev1 + prev2
            prev2, prev1 = prev1, current
        
        return prev1
    
    def climbStairsMemo(self, n: int) -> int:
        """
        Top-down DP with memoization.
        
        Time: O(n), Space: O(n)
        """
        memo = {}
        
        def dp(i):
            if i <= 2:
                return i
            if i in memo:
                return memo[i]
            
            memo[i] = dp(i-1) + dp(i-2)
            return memo[i]
        
        return dp(n)
```

## 📊 Difficulty Progression

### Easy Problems (Fundamentals)
**Focus**: Basic concepts, simple implementations
**Examples**: Two Sum, Reverse Integer, Palindrome Number, Remove Duplicates

**Learning Objectives**:
- Master basic patterns
- Understand problem-solving approach
- Practice clean implementation
- Build confidence

```python
# Example: Valid Parentheses
class Solution:
    def isValid(self, s: str) -> bool:
        """
        Stack-based approach for balanced parentheses.
        
        Time: O(n), Space: O(n)
        """
        stack = []
        mapping = {')': '(', '}': '{', ']': '['}
        
        for char in s:
            if char in mapping:  # Closing bracket
                if not stack or stack.pop() != mapping[char]:
                    return False
            else:  # Opening bracket
                stack.append(char)
        
        return len(stack) == 0
```

### Medium Problems (Pattern Application)
**Focus**: Pattern recognition, optimization, multiple approaches
**Examples**: 3Sum, Group Anagrams, Product of Array Except Self

**Learning Objectives**:
- Apply multiple patterns
- Optimize time/space complexity
- Handle complex constraints
- Practice interview communication

```python
# Example: 3Sum
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        """
        Two pointers after fixing first element.
        
        Time: O(n²), Space: O(1)
        """
        nums.sort()
        result = []
        
        for i in range(len(nums) - 2):
            # Skip duplicates for first number
            if i > 0 and nums[i] == nums[i-1]:
                continue
            
            left, right = i + 1, len(nums) - 1
            
            while left < right:
                current_sum = nums[i] + nums[left] + nums[right]
                
                if current_sum == 0:
                    result.append([nums[i], nums[left], nums[right]])
                    
                    # Skip duplicates
                    while left < right and nums[left] == nums[left + 1]:
                        left += 1
                    while left < right and nums[right] == nums[right - 1]:
                        right -= 1
                    
                    left += 1
                    right -= 1
                elif current_sum < 0:
                    left += 1
                else:
                    right -= 1
        
        return result
```

### Hard Problems (Advanced Techniques)
**Focus**: Complex algorithms, advanced patterns, optimization
**Examples**: Median of Two Sorted Arrays, Trapping Rain Water, Edit Distance

**Learning Objectives**:
- Master advanced patterns
- Handle complex edge cases
- Optimize for extreme constraints
- Practice system design aspects

```python
# Example: Trapping Rain Water
class Solution:
    def trap(self, height: List[int]) -> int:
        """
        Two pointers approach.
        
        Time: O(n), Space: O(1)
        """
        if not height:
            return 0
        
        left, right = 0, len(height) - 1
        left_max = right_max = 0
        water = 0
        
        while left < right:
            if height[left] < height[right]:
                if height[left] >= left_max:
                    left_max = height[left]
                else:
                    water += left_max - height[left]
                left += 1
            else:
                if height[right] >= right_max:
                    right_max = height[right]
                else:
                    water += right_max - height[right]
                right -= 1
        
        return water
```

## 🏢 Company-Specific Focus

### Google
**Common Patterns**: Tree/Graph algorithms, System design, Array manipulation
**Focus Areas**: Clean code, scalability, edge cases
**Example Problems**: Word Ladder, Course Schedule, Design Search Autocomplete

### Amazon
**Common Patterns**: Tree/Graph, Dynamic Programming, String algorithms
**Focus Areas**: Optimal solutions, practical applications
**Example Problems**: Two Sum, Merge k Sorted Lists, Word Break

### Microsoft
**Common Patterns**: Array/String, Tree, Dynamic Programming
**Focus Areas**: Problem-solving approach, code quality
**Example Problems**: Reverse Linked List, Valid Parentheses, Longest Palindrome

### Facebook (Meta)
**Common Patterns**: Graph algorithms, Tree traversal, Hash tables
**Focus Areas**: Scalability, optimization, real-world applications
**Example Problems**: Clone Graph, Binary Tree Right Side View, Valid Palindrome

## 🎯 Interview Strategies

### Problem-Solving Framework

1. **Clarify Requirements** (2-3 minutes)
   ```
   Questions to Ask:
   - What are the input constraints?
   - What should I return for edge cases?
   - Are there any assumptions I can make?
   - What's the expected time/space complexity?
   ```

2. **Analyze Examples** (3-5 minutes)
   ```
   Process:
   - Work through given examples manually
   - Identify patterns in the examples
   - Create additional test cases
   - Understand the problem thoroughly
   ```

3. **Design Approach** (5-10 minutes)
   ```
   Steps:
   - Start with brute force approach
   - Identify optimization opportunities
   - Choose appropriate data structures
   - Discuss trade-offs with interviewer
   ```

4. **Implement Solution** (15-20 minutes)
   ```
   Best Practices:
   - Write clean, readable code
   - Add comments for complex logic
   - Handle edge cases
   - Test with examples as you go
   ```

5. **Test and Optimize** (5-10 minutes)
   ```
   Verification:
   - Test with given examples
   - Check edge cases
   - Analyze time/space complexity
   - Discuss potential improvements
   ```

### Communication Tips

```python
# Example of good interview communication
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        """
        Find indices of two numbers that add up to target.
        
        I'll use a hash map to store numbers we've seen and their indices.
        For each number, I'll check if its complement exists in the map.
        
        Time: O(n) - single pass through array
        Space: O(n) - hash map storage
        """
        # Dictionary to store {number: index}
        seen = {}
        
        for i, num in enumerate(nums):
            complement = target - num
            
            # Check if complement exists
            if complement in seen:
                return [seen[complement], i]
            
            # Store current number and index
            seen[num] = i
        
        # Problem guarantees exactly one solution
        return []
```

## 📈 Progress Tracking

### LeetCode Study Plan
```python
class LeetCodeProgress:
    def __init__(self):
        self.problems_solved = {}
        self.patterns_mastered = set()
        self.difficulty_stats = {'easy': 0, 'medium': 0, 'hard': 0}
        self.company_focus = {}
    
    def add_solution(self, problem_id, title, difficulty, pattern, companies):
        """Track a solved problem."""
        self.problems_solved[problem_id] = {
            'title': title,
            'difficulty': difficulty,
            'pattern': pattern,
            'companies': companies,
            'date_solved': datetime.now(),
            'review_count': 0
        }
        
        self.difficulty_stats[difficulty] += 1
        self.patterns_mastered.add(pattern)
        
        for company in companies:
            self.company_focus[company] = self.company_focus.get(company, 0) + 1
    
    def get_review_list(self, days_since=7):
        """Get problems to review based on time elapsed."""
        cutoff_date = datetime.now() - timedelta(days=days_since)
        
        review_list = []
        for problem_id, info in self.problems_solved.items():
            if info['date_solved'] < cutoff_date:
                review_list.append((problem_id, info['title']))
        
        return review_list
    
    def get_weak_patterns(self):
        """Identify patterns that need more practice."""
        pattern_counts = {}
        for info in self.problems_solved.values():
            pattern = info['pattern']
            pattern_counts[pattern] = pattern_counts.get(pattern, 0) + 1
        
        # Return patterns with fewer than 5 problems solved
        return [pattern for pattern, count in pattern_counts.items() if count < 5]
```

### Monthly Goals
- **Month 1**: 50 Easy problems (fundamentals)
- **Month 2**: 30 Medium problems (pattern recognition)
- **Month 3**: 15 Hard problems (advanced techniques)
- **Month 4**: Company-specific practice and mock interviews

## 🎯 Tips for Success

### LeetCode-Specific Strategies

1. **Pattern Recognition**: Focus on learning patterns rather than memorizing solutions
2. **Spaced Repetition**: Review solved problems after 1 day, 1 week, 1 month
3. **Company Focus**: Prioritize problems asked by target companies
4. **Contest Participation**: Join weekly contests for timed practice
5. **Discussion Reading**: Learn from community solutions and optimizations

### Time Management
- **Daily Target**: 1-2 problems per day consistently
- **Weekly Review**: Review and optimize previous week's solutions
- **Pattern Practice**: Dedicate specific days to specific patterns
- **Mock Interviews**: Weekly practice with time constraints

### Code Quality Standards
```python
# Code quality checklist for interviews
"""
INTERVIEW CODE QUALITY:

✅ Clarity:
   - Meaningful variable names
   - Clear logic flow
   - Appropriate comments
   - Proper formatting

✅ Correctness:
   - Handles all test cases
   - Proper edge case handling
   - No off-by-one errors
   - Correct return types

✅ Efficiency:
   - Optimal time complexity
   - Reasonable space usage
   - No redundant operations
   - Smart data structure choices

✅ Communication:
   - Explain approach clearly
   - Discuss trade-offs
   - Handle questions well
   - Show testing mindset
"""
```

## 📚 Study Resources

### Essential Resources
- LeetCode official platform and discussions
- "Cracking the Coding Interview" by Gayle McDowell
- "Elements of Programming Interviews" by Aziz, Lee, and Prakash
- Algorithm visualization tools (VisuAlgo, LeetCode Playground)

### Community Resources
- LeetCode discussion forums
- YouTube tutorial channels
- GitHub solution repositories
- Discord/Slack study groups

### Mock Interview Platforms
- Pramp
- InterviewBit
- Interviewing.io
- LeetCode Mock Interview

---

**Remember**: LeetCode is designed to prepare you for technical interviews. Focus on understanding patterns, communicating your thought process clearly, and building the ability to solve problems under time pressure. Consistency and pattern recognition are key to success!
