# Lists and List Operations

## 🎯 Objective
Master Python lists - one of the most versatile and commonly used data structures - including creation, manipulation, and advanced operations essential for problem-solving.

## 📖 Overview

Lists are ordered, mutable collections that can store items of different types. They are fundamental to Python programming and form the backbone of many algorithms and data processing tasks. Understanding lists thoroughly is crucial for effective problem-solving in competitive programming and real-world applications.

## 📝 List Creation and Initialization

### Basic List Creation

```python
# Empty list creation
empty_list = []
also_empty = list()

# List with initial values
numbers = [1, 2, 3, 4, 5]
mixed_types = [1, "hello", 3.14, True, [1, 2]]
fruits = ["apple", "banana", "cherry"]

# List from other iterables
string_to_list = list("hello")  # ['h', 'e', 'l', 'l', 'o']
range_to_list = list(range(5))  # [0, 1, 2, 3, 4]
tuple_to_list = list((1, 2, 3))  # [1, 2, 3]

print(f"Numbers: {numbers}")
print(f"Mixed types: {mixed_types}")
print(f"From string: {string_to_list}")
print(f"From range: {range_to_list}")

# List multiplication (repetition)
zeros = [0] * 5  # [0, 0, 0, 0, 0]
pattern = [1, 2] * 3  # [1, 2, 1, 2, 1, 2]

print(f"Zeros: {zeros}")
print(f"Pattern: {pattern}")

# Nested list creation
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
identity_matrix = [[1 if i == j else 0 for j in range(3)] for i in range(3)]

print(f"Matrix: {matrix}")
print(f"Identity matrix: {identity_matrix}")
```

### Advanced List Initialization

```python
# List comprehensions for initialization
squares = [x**2 for x in range(10)]
even_squares = [x**2 for x in range(10) if x % 2 == 0]
words = ["apple", "banana", "cherry"]
lengths = [len(word) for word in words]

print(f"Squares: {squares}")
print(f"Even squares: {even_squares}")
print(f"Word lengths: {lengths}")

# Nested list comprehensions
multiplication_table = [[i * j for j in range(1, 6)] for i in range(1, 6)]
print("Multiplication table:")
for row in multiplication_table:
    print(row)

# Creating lists with default values (careful with mutable objects!)
# WRONG way - all sublists are the same object
wrong_matrix = [[0] * 3] * 3
wrong_matrix[0][0] = 1
print(f"Wrong matrix (all rows affected): {wrong_matrix}")

# CORRECT way - each sublist is a separate object
correct_matrix = [[0] * 3 for _ in range(3)]
correct_matrix[0][0] = 1
print(f"Correct matrix (only first row affected): {correct_matrix}")

# Dynamic list creation based on conditions
def create_fibonacci_list(n):
    """Create list of first n Fibonacci numbers."""
    if n <= 0:
        return []
    elif n == 1:
        return [0]
    elif n == 2:
        return [0, 1]
    
    fib_list = [0, 1]
    for i in range(2, n):
        fib_list.append(fib_list[i-1] + fib_list[i-2])
    
    return fib_list

def create_prime_list(limit):
    """Create list of prime numbers up to limit."""
    if limit < 2:
        return []
    
    primes = []
    for num in range(2, limit + 1):
        is_prime = True
        for i in range(2, int(num**0.5) + 1):
            if num % i == 0:
                is_prime = False
                break
        if is_prime:
            primes.append(num)
    
    return primes

print(f"First 10 Fibonacci numbers: {create_fibonacci_list(10)}")
print(f"Primes up to 30: {create_prime_list(30)}")
```

## 🔍 List Indexing and Slicing

### Basic Indexing

```python
# Sample list for demonstrations
data = [10, 20, 30, 40, 50, 60, 70, 80, 90]

# Positive indexing (0-based)
first = data[0]      # 10
second = data[1]     # 20
last = data[8]       # 90

# Negative indexing (from end)
last_negative = data[-1]    # 90
second_last = data[-2]      # 80
first_negative = data[-9]   # 10

print(f"First element: {first}")
print(f"Last element: {last_negative}")
print(f"Second to last: {second_last}")

# Index validation
def safe_get(lst, index, default=None):
    """Safely get element at index, return default if out of bounds."""
    try:
        return lst[index]
    except IndexError:
        return default

print(f"Safe get index 5: {safe_get(data, 5)}")    # 60
print(f"Safe get index 20: {safe_get(data, 20)}")  # None
```

### Advanced Slicing

```python
# Basic slicing: list[start:end:step]
numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

# Basic slices
first_five = numbers[:5]        # [0, 1, 2, 3, 4]
last_five = numbers[-5:]        # [5, 6, 7, 8, 9]
middle = numbers[3:7]           # [3, 4, 5, 6]
copy_all = numbers[:]           # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

print(f"First five: {first_five}")
print(f"Last five: {last_five}")
print(f"Middle: {middle}")

# Step slicing
every_second = numbers[::2]     # [0, 2, 4, 6, 8]
every_third = numbers[1::3]     # [1, 4, 7]
reverse = numbers[::-1]         # [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
reverse_partial = numbers[7:2:-1]  # [7, 6, 5, 4, 3]

print(f"Every second: {every_second}")
print(f"Every third from index 1: {every_third}")
print(f"Reversed: {reverse}")
print(f"Reverse partial: {reverse_partial}")

# Practical slicing applications
def get_first_n_elements(lst, n):
    """Get first n elements safely."""
    return lst[:n]

def get_last_n_elements(lst, n):
    """Get last n elements safely."""
    return lst[-n:] if n <= len(lst) else lst[:]

def split_list_in_half(lst):
    """Split list into two halves."""
    mid = len(lst) // 2
    return lst[:mid], lst[mid:]

def get_every_nth_element(lst, n, start=0):
    """Get every nth element starting from start index."""
    return lst[start::n]

# Test slicing functions
test_list = list(range(20))
print(f"Test list: {test_list}")
print(f"First 7 elements: {get_first_n_elements(test_list, 7)}")
print(f"Last 5 elements: {get_last_n_elements(test_list, 5)}")

left, right = split_list_in_half(test_list)
print(f"Split in half: {left} | {right}")

print(f"Every 3rd element: {get_every_nth_element(test_list, 3)}")
print(f"Every 4th starting from index 1: {get_every_nth_element(test_list, 4, 1)}")
```

## ➕ Adding Elements to Lists

### Append and Insert Methods

```python
# Starting with empty list
shopping_cart = []

# Append - add to end
shopping_cart.append("apples")
shopping_cart.append("bread")
shopping_cart.append("milk")
print(f"After appends: {shopping_cart}")

# Insert - add at specific index
shopping_cart.insert(0, "bananas")      # Insert at beginning
shopping_cart.insert(2, "cheese")       # Insert at index 2
print(f"After inserts: {shopping_cart}")

# Extend - add multiple elements from iterable
more_items = ["eggs", "butter", "yogurt"]
shopping_cart.extend(more_items)
print(f"After extend: {shopping_cart}")

# Alternative to extend using +=
even_more = ["pasta", "sauce"]
shopping_cart += even_more
print(f"After += operator: {shopping_cart}")

# Difference between append and extend
list1 = [1, 2, 3]
list2 = [1, 2, 3]

list1.append([4, 5])    # Adds entire list as single element
list2.extend([4, 5])    # Adds each element individually

print(f"After append [4, 5]: {list1}")     # [1, 2, 3, [4, 5]]
print(f"After extend [4, 5]: {list2}")     # [1, 2, 3, 4, 5]
```

### Building Lists Dynamically

```python
# Building lists based on user input (simulated)
def build_number_list():
    """Build list of numbers with validation."""
    numbers = []
    
    # Simulated user inputs
    inputs = ["10", "20", "abc", "30", "40", "quit"]
    
    for user_input in inputs:
        if user_input.lower() == "quit":
            break
        
        try:
            number = float(user_input)
            numbers.append(number)
            print(f"Added {number}. Current list: {numbers}")
        except ValueError:
            print(f"'{user_input}' is not a valid number. Skipping.")
    
    return numbers

# Building filtered lists
def build_filtered_list(source_list, condition_func):
    """Build new list with elements meeting condition."""
    result = []
    for item in source_list:
        if condition_func(item):
            result.append(item)
    return result

# Building lists with transformations
def build_transformed_list(source_list, transform_func):
    """Build new list with transformed elements."""
    result = []
    for item in source_list:
        result.append(transform_func(item))
    return result

# Example usage
print("Building number list:")
final_numbers = build_number_list()
print(f"Final numbers: {final_numbers}")

# Filter examples
test_numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
evens = build_filtered_list(test_numbers, lambda x: x % 2 == 0)
large_numbers = build_filtered_list(test_numbers, lambda x: x > 5)

print(f"Original: {test_numbers}")
print(f"Even numbers: {evens}")
print(f"Numbers > 5: {large_numbers}")

# Transform examples
squares = build_transformed_list(test_numbers, lambda x: x**2)
words = ["hello", "world", "python"]
uppercased = build_transformed_list(words, lambda x: x.upper())

print(f"Squares: {squares}")
print(f"Uppercased: {uppercased}")

# Complex list building: Processing data
def process_student_data():
    """Process student data into organized lists."""
    # Simulated raw data
    raw_data = [
        "Alice,85,90,78",
        "Bob,92,88,85",
        "Charlie,78,82,90",
        "Diana,95,97,93"
    ]
    
    students = []
    all_scores = []
    
    for line in raw_data:
        parts = line.split(",")
        name = parts[0]
        scores = [int(parts[i]) for i in range(1, len(parts))]
        
        student_info = {
            "name": name,
            "scores": scores,
            "average": sum(scores) / len(scores)
        }
        
        students.append(student_info)
        all_scores.extend(scores)  # Add all scores to master list
    
    return students, all_scores

students, all_scores = process_student_data()
print("\nStudent data:")
for student in students:
    print(f"{student['name']}: {student['scores']} (avg: {student['average']:.1f})")

print(f"All scores: {all_scores}")
print(f"Overall average: {sum(all_scores) / len(all_scores):.1f}")
```

## ➖ Removing Elements from Lists

### Remove, Pop, and Clear Methods

```python
# Sample list for removal operations
fruits = ["apple", "banana", "cherry", "apple", "date", "elderberry"]
print(f"Original fruits: {fruits}")

# remove() - removes first occurrence of value
fruits.remove("apple")  # Removes first "apple"
print(f"After removing 'apple': {fruits}")

# pop() - removes and returns element at index (default: last)
last_fruit = fruits.pop()           # Removes and returns last element
second_fruit = fruits.pop(1)        # Removes and returns element at index 1

print(f"Popped last fruit: {last_fruit}")
print(f"Popped second fruit: {second_fruit}")
print(f"After pops: {fruits}")

# clear() - removes all elements
backup_fruits = fruits.copy()
fruits.clear()
print(f"After clear: {fruits}")
print(f"Backup: {backup_fruits}")

# del statement for removal
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9]
print(f"Original numbers: {numbers}")

del numbers[0]          # Delete first element
print(f"After del numbers[0]: {numbers}")

del numbers[2:5]        # Delete slice
print(f"After del numbers[2:5]: {numbers}")

del numbers[-1]         # Delete last element
print(f"After del numbers[-1]: {numbers}")
```

### Safe Removal Operations

```python
def safe_remove(lst, value):
    """Safely remove value from list, return True if removed."""
    try:
        lst.remove(value)
        return True
    except ValueError:
        return False

def safe_pop(lst, index=-1, default=None):
    """Safely pop element at index, return default if index invalid."""
    try:
        return lst.pop(index)
    except (IndexError, ValueError):
        return default

def remove_all_occurrences(lst, value):
    """Remove all occurrences of value from list."""
    while value in lst:
        lst.remove(value)

def remove_multiple_values(lst, values_to_remove):
    """Remove multiple values from list."""
    for value in values_to_remove:
        while value in lst:
            lst.remove(value)

# Test safe removal functions
test_list = [1, 2, 3, 2, 4, 2, 5]
print(f"Original: {test_list}")

# Safe remove
result = safe_remove(test_list, 2)
print(f"Removed 2: {result}, List: {test_list}")

result = safe_remove(test_list, 10)  # Not in list
print(f"Removed 10: {result}, List: {test_list}")

# Safe pop
popped = safe_pop(test_list)
print(f"Popped: {popped}, List: {test_list}")

popped = safe_pop(test_list, 10)  # Invalid index
print(f"Popped invalid index: {popped}, List: {test_list}")

# Remove all occurrences
test_list2 = [1, 2, 2, 3, 2, 4, 2, 5]
print(f"Before removing all 2s: {test_list2}")
remove_all_occurrences(test_list2, 2)
print(f"After removing all 2s: {test_list2}")

# Remove multiple values
test_list3 = [1, 2, 3, 4, 5, 2, 3, 6, 7]
print(f"Before removing [2, 3]: {test_list3}")
remove_multiple_values(test_list3, [2, 3])
print(f"After removing [2, 3]: {test_list3}")
```

### Filtering and Conditional Removal

```python
# Filter using list comprehensions (creates new list)
def filter_list(lst, condition_func):
    """Create new list with elements meeting condition."""
    return [item for item in lst if condition_func(item)]

# In-place filtering (modifies original list)
def filter_list_inplace(lst, condition_func):
    """Remove elements that don't meet condition (in-place)."""
    i = 0
    while i < len(lst):
        if not condition_func(lst[i]):
            lst.pop(i)
        else:
            i += 1

# Advanced filtering patterns
def remove_by_indices(lst, indices_to_remove):
    """Remove elements at specified indices."""
    # Sort indices in reverse order to avoid index shifting
    for index in sorted(indices_to_remove, reverse=True):
        if 0 <= index < len(lst):
            lst.pop(index)

def partition_list(lst, condition_func):
    """Partition list into two lists based on condition."""
    true_list = []
    false_list = []
    
    for item in lst:
        if condition_func(item):
            true_list.append(item)
        else:
            false_list.append(item)
    
    return true_list, false_list

# Test filtering functions
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Filter positive even numbers
evens = filter_list(numbers, lambda x: x % 2 == 0)
print(f"Original: {numbers}")
print(f"Even numbers: {evens}")

# Filter in-place (keep only numbers > 5)
numbers_copy = numbers.copy()
filter_list_inplace(numbers_copy, lambda x: x > 5)
print(f"After in-place filter (>5): {numbers_copy}")

# Remove by indices
test_list = ['a', 'b', 'c', 'd', 'e', 'f']
print(f"Before removing indices [0, 2, 4]: {test_list}")
remove_by_indices(test_list, [0, 2, 4])
print(f"After removing indices: {test_list}")

# Partition list
mixed_numbers = [-3, -1, 0, 2, 5, -7, 8, -2, 9]
positive, non_positive = partition_list(mixed_numbers, lambda x: x > 0)
print(f"Original: {mixed_numbers}")
print(f"Positive: {positive}")
print(f"Non-positive: {non_positive}")
```

## 🔄 List Modification and Transformation

### Sorting and Reversing

```python
# Sample data for sorting examples
numbers = [64, 34, 25, 12, 22, 11, 90]
words = ["banana", "Apple", "cherry", "Date"]
students = [
    {"name": "Alice", "grade": 85},
    {"name": "Bob", "grade": 92},
    {"name": "Charlie", "grade": 78}
]

print(f"Original numbers: {numbers}")
print(f"Original words: {words}")

# sort() - modifies list in place
numbers_copy = numbers.copy()
numbers_copy.sort()
print(f"Sorted numbers (ascending): {numbers_copy}")

numbers_copy = numbers.copy()
numbers_copy.sort(reverse=True)
print(f"Sorted numbers (descending): {numbers_copy}")

# sorted() - returns new sorted list
sorted_numbers = sorted(numbers)
print(f"Original unchanged: {numbers}")
print(f"New sorted list: {sorted_numbers}")

# Sorting with key function
words_copy = words.copy()
words_copy.sort(key=str.lower)  # Case-insensitive sort
print(f"Case-insensitive sorted words: {words_copy}")

# Sort by length
words_by_length = sorted(words, key=len)
print(f"Words sorted by length: {words_by_length}")

# Sort complex objects
students_by_grade = sorted(students, key=lambda x: x["grade"])
students_by_name = sorted(students, key=lambda x: x["name"])

print("Students sorted by grade:")
for student in students_by_grade:
    print(f"  {student['name']}: {student['grade']}")

print("Students sorted by name:")
for student in students_by_name:
    print(f"  {student['name']}: {student['grade']}")

# reverse() - reverses list in place
numbers_copy = numbers.copy()
numbers_copy.reverse()
print(f"Reversed numbers: {numbers_copy}")

# Reverse using slicing (creates new list)
reversed_numbers = numbers[::-1]
print(f"Reversed using slicing: {reversed_numbers}")
```

### List Modification Patterns

```python
# Map pattern - transform each element
def map_list(lst, transform_func):
    """Apply transformation to each element."""
    for i in range(len(lst)):
        lst[i] = transform_func(lst[i])

# Conditional modification
def modify_if(lst, condition_func, transform_func):
    """Modify elements that meet condition."""
    for i in range(len(lst)):
        if condition_func(lst[i]):
            lst[i] = transform_func(lst[i])

# Swap elements
def swap_elements(lst, i, j):
    """Swap elements at indices i and j."""
    if 0 <= i < len(lst) and 0 <= j < len(lst):
        lst[i], lst[j] = lst[j], lst[i]
        return True
    return False

# Rotate list elements
def rotate_left(lst, positions=1):
    """Rotate list left by specified positions."""
    if not lst:
        return
    
    positions = positions % len(lst)  # Handle positions > length
    lst[:] = lst[positions:] + lst[:positions]

def rotate_right(lst, positions=1):
    """Rotate list right by specified positions."""
    if not lst:
        return
    
    positions = positions % len(lst)
    lst[:] = lst[-positions:] + lst[:-positions]

# Test modification functions
test_numbers = [1, 2, 3, 4, 5]
print(f"Original: {test_numbers}")

# Map - square all numbers
test_copy = test_numbers.copy()
map_list(test_copy, lambda x: x**2)
print(f"After squaring: {test_copy}")

# Conditional modification - double even numbers
test_copy = test_numbers.copy()
modify_if(test_copy, lambda x: x % 2 == 0, lambda x: x * 2)
print(f"After doubling evens: {test_copy}")

# Swap elements
test_copy = test_numbers.copy()
swap_elements(test_copy, 0, 4)  # Swap first and last
print(f"After swapping first and last: {test_copy}")

# Rotate operations
test_copy = test_numbers.copy()
rotate_left(test_copy, 2)
print(f"After rotating left by 2: {test_copy}")

test_copy = test_numbers.copy()
rotate_right(test_copy, 1)
print(f"After rotating right by 1: {test_copy}")

# Advanced modification: Normalize data
def normalize_scores(scores, target_max=100):
    """Normalize scores to target maximum."""
    if not scores:
        return
    
    current_max = max(scores)
    if current_max == 0:
        return
    
    scale_factor = target_max / current_max
    for i in range(len(scores)):
        scores[i] = round(scores[i] * scale_factor, 2)

# Test normalization
raw_scores = [85, 92, 78, 96, 88, 90]
print(f"Raw scores: {raw_scores}")
normalize_scores(raw_scores)
print(f"Normalized scores: {raw_scores}")
```

## 🔍 Searching and Finding in Lists

### Basic Search Operations

```python
# Linear search implementation
def linear_search(lst, target):
    """Find index of target in list, return -1 if not found."""
    for i, value in enumerate(lst):
        if value == target:
            return i
    return -1

def linear_search_all(lst, target):
    """Find all indices where target appears."""
    indices = []
    for i, value in enumerate(lst):
        if value == target:
            indices.append(i)
    return indices

# Binary search (for sorted lists)
def binary_search(sorted_list, target):
    """Binary search in sorted list."""
    left, right = 0, len(sorted_list) - 1
    
    while left <= right:
        mid = (left + right) // 2
        mid_value = sorted_list[mid]
        
        if mid_value == target:
            return mid
        elif mid_value < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return -1

# Find minimum and maximum
def find_min_max(lst):
    """Find minimum and maximum values with their indices."""
    if not lst:
        return None
    
    min_val = max_val = lst[0]
    min_idx = max_idx = 0
    
    for i, value in enumerate(lst[1:], 1):
        if value < min_val:
            min_val = value
            min_idx = i
        if value > max_val:
            max_val = value
            max_idx = i
    
    return {
        'min': {'value': min_val, 'index': min_idx},
        'max': {'value': max_val, 'index': max_idx}
    }

# Test search functions
test_list = [3, 1, 4, 1, 5, 9, 2, 6, 5, 3]
print(f"Test list: {test_list}")

# Linear search
target = 5
index = linear_search(test_list, target)
print(f"Linear search for {target}: index {index}")

all_indices = linear_search_all(test_list, target)
print(f"All occurrences of {target}: {all_indices}")

# Binary search (need sorted list)
sorted_list = sorted(test_list)
print(f"Sorted list: {sorted_list}")
index = binary_search(sorted_list, target)
print(f"Binary search for {target}: index {index}")

# Min/max finding
min_max = find_min_max(test_list)
print(f"Min/Max: {min_max}")
```

### Advanced Search Patterns

```python
# Find elements meeting condition
def find_first(lst, condition_func):
    """Find first element meeting condition."""
    for item in lst:
        if condition_func(item):
            return item
    return None

def find_all(lst, condition_func):
    """Find all elements meeting condition."""
    return [item for item in lst if condition_func(item)]

def find_indices(lst, condition_func):
    """Find indices of elements meeting condition."""
    return [i for i, item in enumerate(lst) if condition_func(item)]

# Search in list of dictionaries
def search_students(students, **criteria):
    """Search students by multiple criteria."""
    results = []
    
    for student in students:
        match = True
        for key, value in criteria.items():
            if key not in student or student[key] != value:
                match = False
                break
        if match:
            results.append(student)
    
    return results

# Fuzzy search (partial string matching)
def fuzzy_search(strings, query, case_sensitive=False):
    """Find strings containing query."""
    if not case_sensitive:
        query = query.lower()
        return [s for s in strings if query in s.lower()]
    else:
        return [s for s in strings if query in s]

# Find closest value
def find_closest(lst, target):
    """Find value closest to target."""
    if not lst:
        return None
    
    closest = lst[0]
    min_diff = abs(lst[0] - target)
    
    for value in lst[1:]:
        diff = abs(value - target)
        if diff < min_diff:
            min_diff = diff
            closest = value
    
    return closest

# Test advanced search functions
numbers = [1, 3, 5, 7, 9, 12, 15, 18, 21]

# Find first even number
first_even = find_first(numbers, lambda x: x % 2 == 0)
print(f"First even number: {first_even}")

# Find all numbers > 10
large_numbers = find_all(numbers, lambda x: x > 10)
print(f"Numbers > 10: {large_numbers}")

# Find indices of numbers divisible by 3
div_by_3_indices = find_indices(numbers, lambda x: x % 3 == 0)
print(f"Indices of numbers divisible by 3: {div_by_3_indices}")

# Student search example
students = [
    {"name": "Alice", "grade": 85, "age": 20},
    {"name": "Bob", "grade": 92, "age": 19},
    {"name": "Charlie", "grade": 78, "age": 20},
    {"name": "Diana", "grade": 95, "age": 21}
]

# Search by grade
high_achievers = search_students(students, grade=95)
print(f"Students with grade 95: {high_achievers}")

# Search by age
twenty_year_olds = search_students(students, age=20)
print(f"20-year-old students: {twenty_year_olds}")

# Fuzzy search example
names = ["Alice", "Bob", "Charlie", "David", "Eve"]
search_results = fuzzy_search(names, "a", case_sensitive=False)
print(f"Names containing 'a': {search_results}")

# Find closest value
target_value = 14
closest = find_closest(numbers, target_value)
print(f"Value closest to {target_value}: {closest}")
```

## 🔗 List Combining and Splitting

### Combining Lists

```python
# Basic concatenation
list1 = [1, 2, 3]
list2 = [4, 5, 6]
list3 = [7, 8, 9]

# Using + operator
combined = list1 + list2 + list3
print(f"Combined with +: {combined}")

# Using extend
result = list1.copy()
result.extend(list2)
result.extend(list3)
print(f"Combined with extend: {result}")

# Using list comprehension
combined_comp = [item for sublist in [list1, list2, list3] for item in sublist]
print(f"Combined with comprehension: {combined_comp}")

# Zip - combine corresponding elements
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30, 35]
cities = ["NYC", "LA", "Chicago"]

combined_zip = list(zip(names, ages, cities))
print(f"Zipped data: {combined_zip}")

# Interleave lists
def interleave_lists(*lists):
    """Interleave elements from multiple lists."""
    result = []
    max_len = max(len(lst) for lst in lists) if lists else 0
    
    for i in range(max_len):
        for lst in lists:
            if i < len(lst):
                result.append(lst[i])
    
    return result

# Merge sorted lists
def merge_sorted_lists(list1, list2):
    """Merge two sorted lists maintaining order."""
    result = []
    i = j = 0
    
    while i < len(list1) and j < len(list2):
        if list1[i] <= list2[j]:
            result.append(list1[i])
            i += 1
        else:
            result.append(list2[j])
            j += 1
    
    # Add remaining elements
    result.extend(list1[i:])
    result.extend(list2[j:])
    
    return result

# Test combining functions
list_a = [1, 3, 5]
list_b = [2, 4, 6]
list_c = [7, 8]

interleaved = interleave_lists(list_a, list_b, list_c)
print(f"Interleaved: {interleaved}")

sorted1 = [1, 3, 5, 7, 9]
sorted2 = [2, 4, 6, 8, 10]
merged = merge_sorted_lists(sorted1, sorted2)
print(f"Merged sorted lists: {merged}")
```

### Splitting Lists

```python
# Split by size
def split_into_chunks(lst, chunk_size):
    """Split list into chunks of specified size."""
    chunks = []
    for i in range(0, len(lst), chunk_size):
        chunks.append(lst[i:i + chunk_size])
    return chunks

# Split by number of parts
def split_into_parts(lst, num_parts):
    """Split list into specified number of parts."""
    if num_parts <= 0:
        return []
    
    part_size = len(lst) // num_parts
    remainder = len(lst) % num_parts
    
    parts = []
    start = 0
    
    for i in range(num_parts):
        # Add one extra element to first 'remainder' parts
        current_size = part_size + (1 if i < remainder else 0)
        end = start + current_size
        parts.append(lst[start:end])
        start = end
    
    return parts

# Split by condition
def split_by_condition(lst, condition_func):
    """Split list into sublists based on condition."""
    if not lst:
        return []
    
    parts = []
    current_part = []
    
    for item in lst:
        if condition_func(item) and current_part:
            parts.append(current_part)
            current_part = [item]
        else:
            current_part.append(item)
    
    if current_part:
        parts.append(current_part)
    
    return parts

# Split by delimiter
def split_by_delimiter(lst, delimiter):
    """Split list by delimiter value."""
    parts = []
    current_part = []
    
    for item in lst:
        if item == delimiter:
            if current_part:
                parts.append(current_part)
                current_part = []
        else:
            current_part.append(item)
    
    if current_part:
        parts.append(current_part)
    
    return parts

# Test splitting functions
test_data = list(range(1, 21))  # [1, 2, 3, ..., 20]
print(f"Original data: {test_data}")

# Split into chunks
chunks = split_into_chunks(test_data, 5)
print(f"Chunks of 5: {chunks}")

# Split into parts
parts = split_into_parts(test_data, 3)
print(f"Split into 3 parts: {parts}")

# Split by condition (split when number is divisible by 5)
condition_parts = split_by_condition(test_data, lambda x: x % 5 == 0)
print(f"Split by multiples of 5: {condition_parts}")

# Split by delimiter
mixed_data = [1, 2, 0, 3, 4, 0, 5, 6, 7, 0, 8]
delimiter_parts = split_by_delimiter(mixed_data, 0)
print(f"Split by delimiter 0: {delimiter_parts}")

# Practical example: Process CSV-like data
def process_grouped_data(data):
    """Process data grouped by empty strings."""
    csv_like_data = [
        "Name", "Age", "City",
        "",  # Empty string as separator
        "Alice", "25", "NYC",
        "Bob", "30", "LA",
        "",
        "Charlie", "35", "Chicago",
        "Diana", "28", "Seattle"
    ]
    
    groups = split_by_delimiter(csv_like_data, "")
    
    if groups:
        headers = groups[0]
        print(f"Headers: {headers}")
        
        for i, group in enumerate(groups[1:], 1):
            print(f"Group {i}:")
            # Process in chunks of header length
            records = split_into_chunks(group, len(headers))
            for record in records:
                if len(record) == len(headers):
                    row_dict = dict(zip(headers, record))
                    print(f"  {row_dict}")

process_grouped_data([])
```

## 🎯 List Algorithms and Applications

### Common List Algorithms

```python
# Two pointer technique
def two_sum(nums, target):
    """Find two numbers that add up to target (assuming sorted list)."""
    left, right = 0, len(nums) - 1
    
    while left < right:
        current_sum = nums[left] + nums[right]
        if current_sum == target:
            return [left, right]
        elif current_sum < target:
            left += 1
        else:
            right -= 1
    
    return []

def remove_duplicates_sorted(nums):
    """Remove duplicates from sorted list in-place."""
    if not nums:
        return 0
    
    write_index = 1
    
    for read_index in range(1, len(nums)):
        if nums[read_index] != nums[read_index - 1]:
            nums[write_index] = nums[read_index]
            write_index += 1
    
    # Truncate list to new length
    nums[:] = nums[:write_index]
    return write_index

# Sliding window technique
def max_sum_subarray(nums, k):
    """Find maximum sum of subarray of length k."""
    if len(nums) < k:
        return None
    
    # Calculate sum of first window
    window_sum = sum(nums[:k])
    max_sum = window_sum
    
    # Slide the window
    for i in range(k, len(nums)):
        window_sum = window_sum - nums[i - k] + nums[i]
        max_sum = max(max_sum, window_sum)
    
    return max_sum

def contains_nearby_duplicate(nums, k):
    """Check if array contains duplicate within k distance."""
    seen = {}
    
    for i, num in enumerate(nums):
        if num in seen and i - seen[num] <= k:
            return True
        seen[num] = i
    
    return False

# Array rotation and manipulation
def rotate_array(nums, k):
    """Rotate array to the right by k steps."""
    k = k % len(nums)  # Handle k > length
    nums[:] = nums[-k:] + nums[:-k]

def reverse_words_in_place(chars):
    """Reverse words in character list in-place."""
    def reverse_section(start, end):
        while start < end:
            chars[start], chars[end] = chars[end], chars[start]
            start += 1
            end -= 1
    
    # First reverse the entire array
    reverse_section(0, len(chars) - 1)
    
    # Then reverse each word
    start = 0
    for i in range(len(chars) + 1):
        if i == len(chars) or chars[i] == ' ':
            reverse_section(start, i - 1)
            start = i + 1

# Test algorithms
print("=== Two Sum ===")
sorted_nums = [1, 2, 3, 4, 5, 6]
target = 9
result = two_sum(sorted_nums, target)
print(f"Two sum in {sorted_nums} for target {target}: {result}")

print("\n=== Remove Duplicates ===")
nums_with_dups = [1, 1, 2, 2, 2, 3, 4, 4, 5]
print(f"Before: {nums_with_dups}")
new_length = remove_duplicates_sorted(nums_with_dups)
print(f"After: {nums_with_dups} (new length: {new_length})")

print("\n=== Sliding Window ===")
test_nums = [1, 4, 2, 10, 23, 3, 1, 0, 20]
k = 4
max_sum = max_sum_subarray(test_nums, k)
print(f"Max sum of subarray of length {k} in {test_nums}: {max_sum}")

print("\n=== Nearby Duplicate ===")
test_array = [1, 2, 3, 1]
k = 3
has_nearby = contains_nearby_duplicate(test_array, k)
print(f"Array {test_array} has nearby duplicate within {k}: {has_nearby}")

print("\n=== Array Rotation ===")
rotation_test = [1, 2, 3, 4, 5, 6, 7]
print(f"Before rotation: {rotation_test}")
rotate_array(rotation_test, 3)
print(f"After rotating right by 3: {rotation_test}")

print("\n=== Reverse Words ===")
word_chars = list("the sky is blue")
print(f"Before: {''.join(word_chars)}")
reverse_words_in_place(word_chars)
print(f"After: {''.join(word_chars)}")
```

### Advanced List Processing

```python
# Matrix operations using lists
def transpose_matrix(matrix):
    """Transpose a matrix represented as list of lists."""
    if not matrix or not matrix[0]:
        return []
    
    rows, cols = len(matrix), len(matrix[0])
    return [[matrix[i][j] for i in range(rows)] for j in range(cols)]

def matrix_multiply(A, B):
    """Multiply two matrices."""
    rows_A, cols_A = len(A), len(A[0])
    rows_B, cols_B = len(B), len(B[0])
    
    if cols_A != rows_B:
        raise ValueError("Matrix dimensions incompatible for multiplication")
    
    result = [[0] * cols_B for _ in range(rows_A)]
    
    for i in range(rows_A):
        for j in range(cols_B):
            for k in range(cols_A):
                result[i][j] += A[i][k] * B[k][j]
    
    return result

def spiral_traverse(matrix):
    """Traverse matrix in spiral order."""
    if not matrix or not matrix[0]:
        return []
    
    result = []
    top, bottom = 0, len(matrix) - 1
    left, right = 0, len(matrix[0]) - 1
    
    while top <= bottom and left <= right:
        # Traverse right
        for col in range(left, right + 1):
            result.append(matrix[top][col])
        top += 1
        
        # Traverse down
        for row in range(top, bottom + 1):
            result.append(matrix[row][right])
        right -= 1
        
        # Traverse left (if we still have rows)
        if top <= bottom:
            for col in range(right, left - 1, -1):
                result.append(matrix[bottom][col])
            bottom -= 1
        
        # Traverse up (if we still have columns)
        if left <= right:
            for row in range(bottom, top - 1, -1):
                result.append(matrix[row][left])
            left += 1
    
    return result

# Data analysis with lists
def calculate_statistics(numbers):
    """Calculate various statistics for a list of numbers."""
    if not numbers:
        return {}
    
    n = len(numbers)
    sorted_nums = sorted(numbers)
    
    # Basic statistics
    mean = sum(numbers) / n
    median = sorted_nums[n // 2] if n % 2 == 1 else (sorted_nums[n // 2 - 1] + sorted_nums[n // 2]) / 2
    mode_count = {}
    for num in numbers:
        mode_count[num] = mode_count.get(num, 0) + 1
    mode = max(mode_count, key=mode_count.get)
    
    # Variance and standard deviation
    variance = sum((x - mean) ** 2 for x in numbers) / n
    std_dev = variance ** 0.5
    
    # Quartiles
    q1 = sorted_nums[n // 4]
    q3 = sorted_nums[3 * n // 4]
    iqr = q3 - q1
    
    return {
        'count': n,
        'mean': round(mean, 2),
        'median': median,
        'mode': mode,
        'min': min(numbers),
        'max': max(numbers),
        'range': max(numbers) - min(numbers),
        'variance': round(variance, 2),
        'std_dev': round(std_dev, 2),
        'q1': q1,
        'q3': q3,
        'iqr': iqr
    }

# Test advanced processing
print("=== Matrix Operations ===")
matrix_a = [
    [1, 2, 3],
    [4, 5, 6]
]

matrix_b = [
    [7, 8],
    [9, 10],
    [11, 12]
]

print(f"Matrix A:\n{matrix_a}")
print(f"Matrix B:\n{matrix_b}")

transposed_a = transpose_matrix(matrix_a)
print(f"A transposed:\n{transposed_a}")

product = matrix_multiply(matrix_a, matrix_b)
print(f"A × B:\n{product}")

# Spiral traversal
spiral_matrix = [
    [1,  2,  3,  4],
    [5,  6,  7,  8],
    [9,  10, 11, 12],
    [13, 14, 15, 16]
]

spiral_result = spiral_traverse(spiral_matrix)
print(f"Spiral traversal: {spiral_result}")

print("\n=== Statistical Analysis ===")
sample_data = [12, 15, 18, 13, 19, 12, 14, 16, 15, 17, 12, 18, 16, 14, 13]
stats = calculate_statistics(sample_data)
print(f"Data: {sample_data}")
print("Statistics:")
for key, value in stats.items():
    print(f"  {key}: {value}")
```

## ⚠️ Common List Pitfalls and Best Practices

### Avoiding Common Mistakes

```python
# Pitfall 1: Modifying list while iterating
def remove_evens_wrong(numbers):
    """WRONG: Modifying list while iterating."""
    for num in numbers:
        if num % 2 == 0:
            numbers.remove(num)  # This can skip elements!
    return numbers

def remove_evens_correct(numbers):
    """CORRECT: Create new list or iterate backwards."""
    return [num for num in numbers if num % 2 != 0]

def remove_evens_inplace(numbers):
    """CORRECT: Remove in reverse order."""
    for i in range(len(numbers) - 1, -1, -1):
        if numbers[i] % 2 == 0:
            numbers.pop(i)

# Pitfall 2: Shallow vs deep copy
def demonstrate_copy_issues():
    """Show shallow vs deep copy problems."""
    # Shallow copy problem with nested lists
    original = [[1, 2], [3, 4]]
    shallow_copy = original.copy()  # or original[:]
    
    # Modifying nested list affects both
    shallow_copy[0][0] = 999
    print(f"Original after shallow copy modification: {original}")
    print(f"Shallow copy: {shallow_copy}")
    
    # Deep copy solution
    import copy
    original = [[1, 2], [3, 4]]
    deep_copy = copy.deepcopy(original)
    
    deep_copy[0][0] = 999
    print(f"Original after deep copy modification: {original}")
    print(f"Deep copy: {deep_copy}")

# Pitfall 3: Default mutable arguments
def append_to_list_wrong(item, target_list=[]):
    """WRONG: Mutable default argument."""
    target_list.append(item)
    return target_list

def append_to_list_correct(item, target_list=None):
    """CORRECT: Use None and create new list."""
    if target_list is None:
        target_list = []
    target_list.append(item)
    return target_list

# Pitfall 4: List multiplication with mutable objects
def create_matrix_wrong(rows, cols):
    """WRONG: All rows reference same list."""
    return [[0] * cols] * rows

def create_matrix_correct(rows, cols):
    """CORRECT: Each row is separate list."""
    return [[0] * cols for _ in range(rows)]

# Test pitfalls
print("=== Testing Pitfalls ===")

# Test wrong removal
test_list = [1, 2, 3, 4, 5, 6]
print(f"Original: {test_list}")
result = remove_evens_wrong(test_list.copy())
print(f"After wrong removal: {result}")  # May not remove all evens!

result = remove_evens_correct(test_list)
print(f"After correct removal: {result}")

# Test copy issues
print("\n=== Copy Issues ===")
demonstrate_copy_issues()

# Test mutable defaults
print("\n=== Mutable Defaults ===")
list1 = append_to_list_wrong("first")
list2 = append_to_list_wrong("second")  # This will have both items!
print(f"Wrong implementation - list1: {list1}, list2: {list2}")

list3 = append_to_list_correct("first")
list4 = append_to_list_correct("second")
print(f"Correct implementation - list3: {list3}, list4: {list4}")

# Test matrix creation
print("\n=== Matrix Creation ===")
wrong_matrix = create_matrix_wrong(3, 3)
wrong_matrix[0][0] = 1  # This affects all rows!
print(f"Wrong matrix: {wrong_matrix}")

correct_matrix = create_matrix_correct(3, 3)
correct_matrix[0][0] = 1  # This affects only first row
print(f"Correct matrix: {correct_matrix}")
```

## 🎯 Practice Exercises

### Exercise 1: Advanced List Manipulation

```python
def implement_list_operations():
    """
    Implement the following operations:
    1. Find the longest increasing subsequence
    2. Merge k sorted lists
    3. Find all triplets that sum to zero
    4. Implement a circular buffer using lists
    """
    # Your implementations here
    pass
```

### Exercise 2: Data Processing Pipeline

```python
def create_data_pipeline(raw_data):
    """
    Create a data processing pipeline that:
    1. Filters invalid entries
    2. Normalizes data format
    3. Groups by categories
    4. Calculates aggregations
    5. Sorts by priority
    
    Raw data format: [{"id": 1, "value": 100, "category": "A", "valid": True}, ...]
    """
    # Your implementation here
    pass
```

### Exercise 3: Algorithm Implementation

```python
def implement_algorithms():
    """
    Implement these algorithms using lists:
    1. Quick sort with in-place partitioning
    2. Merge intervals
    3. Find peak element in array
    4. Implement LRU cache using lists
    """
    # Your implementations here
    pass
```

## 📚 Summary and Best Practices

### Key Takeaways
1. **Lists are versatile**: Ordered, mutable, and support mixed types
2. **Master slicing**: Powerful for data extraction and manipulation
3. **Choose appropriate methods**: append vs extend, remove vs pop vs del
4. **Understand references**: Shallow vs deep copying implications
5. **Use appropriate algorithms**: Linear vs binary search, in-place vs new list
6. **Optimize for performance**: List comprehensions, built-in functions

### Performance Guidelines
- **Use list comprehensions** for filtering and transforming
- **Pre-allocate space** when possible for large lists
- **Use collections.deque** for frequent front operations
- **Consider numpy arrays** for numerical computations
- **Profile before optimizing** - measure actual performance

### Best Practices Checklist
- [ ] Use appropriate list methods for the task
- [ ] Be careful when modifying lists during iteration
- [ ] Understand shallow vs deep copying
- [ ] Avoid mutable default arguments
- [ ] Use list comprehensions for readability and performance
- [ ] Handle edge cases (empty lists, single elements)
- [ ] Choose appropriate algorithms for your data size
- [ ] Consider memory usage for large datasets

### Next Steps
After mastering lists:
1. Learn about [Tuples and Sets](./10-tuples-sets.md)
2. Practice implementing classic algorithms with lists
3. Study advanced data structures (stacks, queues, deques)
4. Explore numpy for numerical list operations

---

**Remember**: Lists are fundamental to Python programming. Master them to write efficient, readable code for data processing and algorithm implementation!
