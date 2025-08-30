# Tuples and Sets

## 🎯 Objective
Master Python's immutable tuple data structure and unique-element set data structure, understanding when and how to use each for optimal performance and data integrity.

## 📖 Overview

Tuples and sets are essential Python data structures that complement lists and dictionaries. Tuples provide immutable sequences ideal for representing fixed collections of related data, while sets offer efficient operations for unique elements and mathematical set operations. Understanding these structures is crucial for writing efficient, Pythonic code.

## 📝 Tuples: Immutable Sequences

### Tuple Creation and Characteristics

```python
# Creating tuples
empty_tuple = ()
also_empty = tuple()

# Tuple with parentheses (recommended for clarity)
coordinates = (3, 4)
rgb_color = (255, 128, 0)
student_info = ("Alice", 20, "Computer Science", 3.8)

# Tuple without parentheses (valid but less clear)
point = 10, 20
dimensions = 1920, 1080, 32

# Single element tuples (comma is required!)
single_element = (42,)  # Note the comma
also_single = 42,

# Tuple from other iterables
list_to_tuple = tuple([1, 2, 3, 4])
string_to_tuple = tuple("hello")
range_to_tuple = tuple(range(5))

print(f"Coordinates: {coordinates}")
print(f"Student info: {student_info}")
print(f"Single element: {single_element}")
print(f"From list: {list_to_tuple}")
print(f"From string: {string_to_tuple}")

# Nested tuples
matrix = ((1, 2, 3), (4, 5, 6), (7, 8, 9))
nested_data = (("Alice", (85, 90, 78)), ("Bob", (92, 88, 85)))

print(f"Matrix: {matrix}")
print(f"Nested data: {nested_data}")

# Tuple characteristics demonstration
def demonstrate_immutability():
    """Show that tuples are immutable."""
    point = (3, 4)
    print(f"Original point: {point}")
    
    try:
        point[0] = 5  # This will raise an error
    except TypeError as e:
        print(f"Cannot modify tuple: {e}")
    
    # But you can reassign the variable
    point = (5, 6)
    print(f"Reassigned point: {point}")

demonstrate_immutability()

# Tuple with mutable elements
mixed_tuple = ([1, 2, 3], "hello", (4, 5))
print(f"Mixed tuple: {mixed_tuple}")

# The tuple itself is immutable, but mutable elements can be changed
mixed_tuple[0].append(4)  # This works!
print(f"After modifying list inside: {mixed_tuple}")

# However, you cannot reassign elements
try:
    mixed_tuple[1] = "world"  # This will fail
except TypeError as e:
    print(f"Cannot reassign tuple element: {e}")
```

### Tuple Operations and Methods

```python
# Tuple indexing and slicing (same as lists)
colors = ("red", "green", "blue", "yellow", "purple")

print(f"First color: {colors[0]}")
print(f"Last color: {colors[-1]}")
print(f"First three: {colors[:3]}")
print(f"Every other: {colors[::2]}")

# Tuple methods (limited compared to lists)
numbers = (1, 2, 3, 2, 4, 2, 5)

count_of_2 = numbers.count(2)
index_of_4 = numbers.index(4)

print(f"Numbers: {numbers}")
print(f"Count of 2: {count_of_2}")
print(f"Index of 4: {index_of_4}")

# Length and membership
print(f"Length: {len(numbers)}")
print(f"3 in numbers: {3 in numbers}")
print(f"6 in numbers: {6 in numbers}")

# Tuple concatenation and repetition
tuple1 = (1, 2, 3)
tuple2 = (4, 5, 6)

combined = tuple1 + tuple2
repeated = tuple1 * 3

print(f"Combined: {combined}")
print(f"Repeated: {repeated}")

# Tuple comparison
print(f"(1, 2) < (1, 3): {(1, 2) < (1, 3)}")  # Lexicographic comparison
print(f"(1, 2) == (1, 2): {(1, 2) == (1, 2)}")

# Converting between tuples and lists
original_list = [1, 2, 3, 4, 5]
as_tuple = tuple(original_list)
back_to_list = list(as_tuple)

print(f"List -> Tuple -> List: {original_list} -> {as_tuple} -> {back_to_list}")
```

### Tuple Unpacking and Multiple Assignment

```python
# Basic tuple unpacking
point = (3, 4)
x, y = point
print(f"Point ({point}) unpacked to x={x}, y={y}")

# Multiple assignment
a, b, c = 1, 2, 3  # Same as (1, 2, 3)
print(f"Multiple assignment: a={a}, b={b}, c={c}")

# Swapping variables (elegant Python idiom)
a, b = 10, 20
print(f"Before swap: a={a}, b={b}")
a, b = b, a
print(f"After swap: a={a}, b={b}")

# Unpacking with different lengths
def safe_unpack_demo():
    """Demonstrate safe unpacking techniques."""
    # This will cause ValueError if lengths don't match
    try:
        x, y = (1, 2, 3)  # Too many values
    except ValueError as e:
        print(f"Unpacking error: {e}")
    
    # Use starred expression for flexible unpacking
    first, *middle, last = (1, 2, 3, 4, 5)
    print(f"Starred unpacking: first={first}, middle={middle}, last={last}")
    
    # Ignore values with underscore
    x, _, z = (1, 2, 3)  # Ignore middle value
    print(f"Ignoring middle: x={x}, z={z}")

safe_unpack_demo()

# Advanced unpacking patterns
def advanced_unpacking():
    """Show advanced unpacking techniques."""
    # Nested tuple unpacking
    nested = ((1, 2), (3, 4))
    (a, b), (c, d) = nested
    print(f"Nested unpacking: a={a}, b={b}, c={c}, d={d}")
    
    # Function returning multiple values
    def get_name_age():
        return "Alice", 25
    
    name, age = get_name_age()
    print(f"Function unpacking: name={name}, age={age}")
    
    # Enumerate unpacking
    items = ["apple", "banana", "cherry"]
    for index, value in enumerate(items):
        print(f"Index {index}: {value}")
    
    # Dictionary unpacking
    person = {"name": "Bob", "age": 30}
    for key, value in person.items():
        print(f"Key {key}: {value}")

advanced_unpacking()

# Practical unpacking applications
def process_coordinates(points):
    """Process list of coordinate tuples."""
    total_x = total_y = 0
    
    for x, y in points:
        total_x += x
        total_y += y
    
    center_x = total_x / len(points)
    center_y = total_y / len(points)
    
    return center_x, center_y

def parse_student_data(data_string):
    """Parse student data from string."""
    # Format: "Name,Age,Grade1,Grade2,Grade3"
    parts = data_string.split(",")
    name = parts[0]
    age = int(parts[1])
    grades = tuple(int(grade) for grade in parts[2:])
    
    return name, age, grades

# Test unpacking applications
coordinate_list = [(1, 2), (3, 4), (5, 6), (7, 8)]
center = process_coordinates(coordinate_list)
print(f"Center of {coordinate_list}: {center}")

student_string = "Alice,20,85,90,78"
name, age, grades = parse_student_data(student_string)
print(f"Student: {name}, Age: {age}, Grades: {grades}")
```

### Named Tuples for Structure

```python
from collections import namedtuple

# Creating named tuple classes
Point = namedtuple('Point', ['x', 'y'])
Person = namedtuple('Person', ['name', 'age', 'city'])
Color = namedtuple('Color', 'red green blue')  # Space-separated also works

# Creating instances
origin = Point(0, 0)
person1 = Person('Alice', 25, 'New York')
red_color = Color(255, 0, 0)

print(f"Origin: {origin}")
print(f"Person: {person1}")
print(f"Red color: {red_color}")

# Accessing elements (multiple ways)
print(f"Origin x: {origin.x}")
print(f"Origin x (index): {origin[0]}")
print(f"Person name: {person1.name}")
print(f"Person name (index): {person1[0]}")

# Named tuples are still tuples
print(f"Origin is tuple: {isinstance(origin, tuple)}")
print(f"Origin length: {len(origin)}")

# Named tuple methods
print(f"Origin as dict: {origin._asdict()}")
print(f"Person fields: {person1._fields}")

# Creating new instances with modifications
moved_origin = origin._replace(x=5)
older_person = person1._replace(age=26)

print(f"Moved origin: {moved_origin}")
print(f"Older person: {older_person}")

# Named tuples in practice
def calculate_distance(point1, point2):
    """Calculate distance between two points."""
    dx = point2.x - point1.x
    dy = point2.y - point1.y
    return (dx**2 + dy**2)**0.5

def create_person_record(name, age, city):
    """Create a person record with validation."""
    if age < 0:
        raise ValueError("Age cannot be negative")
    if not name.strip():
        raise ValueError("Name cannot be empty")
    
    return Person(name.strip(), age, city.strip())

# Test named tuple functions
p1 = Point(0, 0)
p2 = Point(3, 4)
distance = calculate_distance(p1, p2)
print(f"Distance from {p1} to {p2}: {distance}")

try:
    invalid_person = create_person_record("", -5, "City")
except ValueError as e:
    print(f"Validation error: {e}")

valid_person = create_person_record("  Bob  ", 30, "  Boston  ")
print(f"Valid person: {valid_person}")

# Advanced named tuple usage
Student = namedtuple('Student', ['name', 'grades', 'major'])

def process_students(student_data):
    """Process student records."""
    students = []
    
    for name, grades_str, major in student_data:
        grades = tuple(int(g) for g in grades_str.split(','))
        student = Student(name, grades, major)
        students.append(student)
    
    return students

def calculate_gpa(student):
    """Calculate GPA for a student."""
    if not student.grades:
        return 0.0
    return sum(student.grades) / len(student.grades)

# Test student processing
raw_data = [
    ("Alice", "85,90,78", "Computer Science"),
    ("Bob", "92,88,85", "Mathematics"),
    ("Charlie", "78,82,90", "Physics")
]

students = process_students(raw_data)
for student in students:
    gpa = calculate_gpa(student)
    print(f"{student.name} ({student.major}): GPA {gpa:.2f}")
```

## 🔧 Sets: Unique Element Collections

### Set Creation and Basic Operations

```python
# Creating sets
empty_set = set()  # Note: {} creates empty dict, not set
numbers_set = {1, 2, 3, 4, 5}
mixed_set = {1, "hello", 3.14, True}

# Set from other iterables
list_to_set = set([1, 2, 3, 2, 1])  # Duplicates removed
string_to_set = set("hello")  # {'h', 'e', 'l', 'o'}
tuple_to_set = set((1, 2, 3, 2))

print(f"Numbers set: {numbers_set}")
print(f"Mixed set: {mixed_set}")
print(f"From list (duplicates removed): {list_to_set}")
print(f"From string: {string_to_set}")

# Set characteristics: unordered and unique
duplicates_list = [1, 2, 2, 3, 3, 3, 4, 4, 4, 4]
unique_set = set(duplicates_list)
print(f"Original list: {duplicates_list}")
print(f"Unique elements: {unique_set}")

# Set comprehensions
squares_set = {x**2 for x in range(10)}
even_squares = {x**2 for x in range(10) if x % 2 == 0}

print(f"Squares set: {squares_set}")
print(f"Even squares: {even_squares}")

# Basic set operations
fruits = {"apple", "banana", "cherry"}

# Adding elements
fruits.add("date")
fruits.update(["elderberry", "fig"])  # Add multiple elements
fruits.update("grape")  # Adds each character as separate element!

print(f"After additions: {fruits}")

# Note: update with string adds each character
test_set = {"a", "b"}
test_set.update("cd")  # Adds 'c' and 'd'
print(f"String update result: {test_set}")

# Correct way to add a string
test_set = {"a", "b"}
test_set.add("cd")  # Adds "cd" as single element
print(f"String add result: {test_set}")

# Removing elements
fruits_copy = fruits.copy()
fruits_copy.remove("g")  # Raises KeyError if not found
fruits_copy.discard("nonexistent")  # Does not raise error
popped = fruits_copy.pop()  # Removes arbitrary element

print(f"After removals: {fruits_copy}")
print(f"Popped element: {popped}")

# Clear all elements
test_set = {1, 2, 3}
test_set.clear()
print(f"After clear: {test_set}")
```

### Set Mathematical Operations

```python
# Set theory operations
set_a = {1, 2, 3, 4, 5}
set_b = {4, 5, 6, 7, 8}
set_c = {1, 2, 3}

print(f"Set A: {set_a}")
print(f"Set B: {set_b}")
print(f"Set C: {set_c}")

# Union (all elements from both sets)
union_1 = set_a | set_b  # Operator syntax
union_2 = set_a.union(set_b)  # Method syntax

print(f"A ∪ B (operator): {union_1}")
print(f"A ∪ B (method): {union_2}")

# Intersection (common elements)
intersection_1 = set_a & set_b
intersection_2 = set_a.intersection(set_b)

print(f"A ∩ B (operator): {intersection_1}")
print(f"A ∩ B (method): {intersection_2}")

# Difference (elements in first but not second)
difference_1 = set_a - set_b
difference_2 = set_a.difference(set_b)

print(f"A - B (operator): {difference_1}")
print(f"A - B (method): {difference_2}")
print(f"B - A: {set_b - set_a}")

# Symmetric difference (elements in either but not both)
sym_diff_1 = set_a ^ set_b
sym_diff_2 = set_a.symmetric_difference(set_b)

print(f"A △ B (operator): {sym_diff_1}")
print(f"A △ B (method): {sym_diff_2}")

# Set relationships
print(f"Is C subset of A? {set_c.issubset(set_a)}")
print(f"Is C subset of A? {set_c <= set_a}")
print(f"Is A superset of C? {set_a.issuperset(set_c)}")
print(f"Is A superset of C? {set_a >= set_c}")
print(f"Are A and B disjoint? {set_a.isdisjoint(set_b)}")

# In-place operations (modify original set)
set_x = {1, 2, 3}
set_y = {3, 4, 5}

print(f"Original X: {set_x}")

set_x |= set_y  # Union update
print(f"After |= (union update): {set_x}")

set_x = {1, 2, 3}
set_x &= set_y  # Intersection update
print(f"After &= (intersection update): {set_x}")

set_x = {1, 2, 3}
set_x -= set_y  # Difference update
print(f"After -= (difference update): {set_x}")

set_x = {1, 2, 3}
set_x ^= set_y  # Symmetric difference update
print(f"After ^= (symmetric difference update): {set_x}")
```

### Practical Set Applications

```python
# Removing duplicates while preserving some order
def remove_duplicates_preserve_order(sequence):
    """Remove duplicates while preserving first occurrence order."""
    seen = set()
    result = []
    
    for item in sequence:
        if item not in seen:
            seen.add(item)
            result.append(item)
    
    return result

# Finding common elements across multiple lists
def find_common_elements(*lists):
    """Find elements common to all lists."""
    if not lists:
        return set()
    
    common = set(lists[0])
    for lst in lists[1:]:
        common &= set(lst)
    
    return common

# Analyzing data with sets
def analyze_survey_data(responses):
    """Analyze survey responses using set operations."""
    # responses format: [{"name": "Alice", "interests": ["music", "sports"]}, ...]
    
    all_interests = set()
    person_interests = {}
    
    for response in responses:
        name = response["name"]
        interests = set(response["interests"])
        
        person_interests[name] = interests
        all_interests.update(interests)
    
    # Find people with common interests
    common_pairs = []
    names = list(person_interests.keys())
    
    for i in range(len(names)):
        for j in range(i + 1, len(names)):
            name1, name2 = names[i], names[j]
            common = person_interests[name1] & person_interests[name2]
            if common:
                common_pairs.append((name1, name2, common))
    
    return {
        'all_interests': all_interests,
        'person_interests': person_interests,
        'common_pairs': common_pairs
    }

# Validating data integrity
def validate_data_integrity(primary_keys, foreign_keys):
    """Check if all foreign keys reference existing primary keys."""
    pk_set = set(primary_keys)
    fk_set = set(foreign_keys)
    
    invalid_fks = fk_set - pk_set
    unused_pks = pk_set - fk_set
    
    return {
        'is_valid': len(invalid_fks) == 0,
        'invalid_foreign_keys': invalid_fks,
        'unused_primary_keys': unused_pks
    }

# Test practical applications
print("=== Removing Duplicates ===")
original_list = [1, 2, 3, 2, 4, 1, 5, 3]
unique_list = remove_duplicates_preserve_order(original_list)
print(f"Original: {original_list}")
print(f"Unique (order preserved): {unique_list}")

print("\n=== Finding Common Elements ===")
list1 = [1, 2, 3, 4, 5]
list2 = [3, 4, 5, 6, 7]
list3 = [4, 5, 6, 7, 8]
common = find_common_elements(list1, list2, list3)
print(f"Lists: {list1}, {list2}, {list3}")
print(f"Common elements: {common}")

print("\n=== Survey Analysis ===")
survey_responses = [
    {"name": "Alice", "interests": ["music", "sports", "reading"]},
    {"name": "Bob", "interests": ["sports", "gaming", "cooking"]},
    {"name": "Charlie", "interests": ["reading", "music", "art"]},
    {"name": "Diana", "interests": ["sports", "art", "travel"]}
]

analysis = analyze_survey_data(survey_responses)
print(f"All interests: {analysis['all_interests']}")
print("Common interest pairs:")
for name1, name2, common in analysis['common_pairs']:
    print(f"  {name1} & {name2}: {common}")

print("\n=== Data Integrity ===")
primary_keys = [1, 2, 3, 4, 5]
foreign_keys = [1, 2, 2, 3, 6, 7]  # 6 and 7 are invalid
integrity = validate_data_integrity(primary_keys, foreign_keys)
print(f"Data valid: {integrity['is_valid']}")
print(f"Invalid foreign keys: {integrity['invalid_foreign_keys']}")
print(f"Unused primary keys: {integrity['unused_primary_keys']}")

# Performance comparison: list vs set for membership testing
import time

def compare_membership_performance():
    """Compare performance of membership testing in lists vs sets."""
    # Create large collections
    large_list = list(range(10000))
    large_set = set(large_list)
    
    # Test membership for elements at the end
    test_values = [9990, 9995, 9999]
    
    # List performance
    start_time = time.time()
    for _ in range(1000):
        for value in test_values:
            value in large_list
    list_time = time.time() - start_time
    
    # Set performance
    start_time = time.time()
    for _ in range(1000):
        for value in test_values:
            value in large_set
    set_time = time.time() - start_time
    
    print(f"List membership time: {list_time:.6f} seconds")
    print(f"Set membership time: {set_time:.6f} seconds")
    print(f"Set is {list_time/set_time:.1f}x faster")

print("\n=== Performance Comparison ===")
compare_membership_performance()
```

### Frozen Sets: Immutable Sets

```python
# Creating frozen sets
regular_set = {1, 2, 3}
frozen_set1 = frozenset([1, 2, 3, 4])
frozen_set2 = frozenset("hello")

print(f"Regular set: {regular_set}")
print(f"Frozen set 1: {frozen_set1}")
print(f"Frozen set 2: {frozen_set2}")

# Frozen sets are immutable
try:
    frozen_set1.add(5)  # This will raise AttributeError
except AttributeError as e:
    print(f"Cannot modify frozen set: {e}")

# But all read operations work
print(f"3 in frozen set: {3 in frozen_set1}")
print(f"Length: {len(frozen_set1)}")

# Set operations work with frozen sets
result = frozen_set1 | {5, 6}  # Returns new frozen set
print(f"Union result: {result}")
print(f"Result type: {type(result)}")

# Frozen sets can be dictionary keys (sets cannot!)
set_map = {
    frozenset([1, 2]): "Group A",
    frozenset([3, 4]): "Group B"
}

print(f"Set map: {set_map}")

# Use frozen sets for hashable collections
def group_students_by_subjects(student_data):
    """Group students by their subject combinations."""
    # student_data: [("Alice", ["Math", "Physics"]), ...]
    
    groups = {}
    
    for name, subjects in student_data:
        subject_key = frozenset(subjects)
        
        if subject_key not in groups:
            groups[subject_key] = []
        
        groups[subject_key].append(name)
    
    return groups

# Test frozen set applications
students = [
    ("Alice", ["Math", "Physics"]),
    ("Bob", ["Math", "Chemistry"]),
    ("Charlie", ["Physics", "Math"]),  # Same as Alice
    ("Diana", ["Chemistry", "Biology"]),
    ("Eve", ["Math", "Chemistry"]),    # Same as Bob
]

grouped = group_students_by_subjects(students)
print("\n=== Student Grouping ===")
for subjects, names in grouped.items():
    print(f"Subjects {set(subjects)}: {names}")

# Creating lookup tables with frozen sets
def create_permission_system():
    """Create a permission system using frozen sets."""
    # Define permissions
    read_perm = frozenset(["read"])
    write_perm = frozenset(["write"])
    execute_perm = frozenset(["execute"])
    
    # Define roles as combinations of permissions
    roles = {
        "viewer": read_perm,
        "editor": read_perm | write_perm,
        "admin": read_perm | write_perm | execute_perm,
        "executor": read_perm | execute_perm
    }
    
    # User assignments
    users = {
        "alice": roles["admin"],
        "bob": roles["editor"],
        "charlie": roles["viewer"],
        "diana": roles["executor"]
    }
    
    return roles, users

def check_permission(users, user, permission):
    """Check if user has specific permission."""
    if user not in users:
        return False
    
    return permission in users[user]

# Test permission system
roles, users = create_permission_system()
print("\n=== Permission System ===")

for user, permissions in users.items():
    print(f"{user}: {set(permissions)}")

# Check specific permissions
test_cases = [
    ("alice", "write"),
    ("bob", "execute"),
    ("charlie", "read"),
    ("diana", "write")
]

for user, perm in test_cases:
    has_perm = check_permission(users, user, perm)
    print(f"{user} can {perm}: {has_perm}")
```

## 🔄 When to Use Tuples vs Sets vs Lists

### Decision Matrix

```python
def demonstrate_data_structure_choice():
    """Demonstrate when to choose each data structure."""
    
    # Use TUPLE when:
    # 1. Data is immutable/fixed
    # 2. Order matters
    # 3. May contain duplicates
    # 4. Need to use as dictionary key
    
    # Example: Coordinates, RGB values, database records
    coordinates = (3, 4)  # Fixed pair of values
    rgb_color = (255, 128, 0)  # Fixed triple
    student_record = ("Alice", 20, "CS", 3.8)  # Fixed structure
    
    # Use as dictionary keys
    location_names = {
        (0, 0): "Origin",
        (1, 1): "Northeast",
        (-1, -1): "Southwest"
    }
    
    print("=== Tuple Use Cases ===")
    print(f"Coordinates: {coordinates}")
    print(f"RGB Color: {rgb_color}")
    print(f"Student: {student_record}")
    print(f"Location map: {location_names}")
    
    # Use SET when:
    # 1. Need unique elements only
    # 2. Order doesn't matter
    # 3. Need fast membership testing
    # 4. Need set operations (union, intersection, etc.)
    
    # Example: Tags, unique IDs, filters
    user_interests = {"music", "sports", "reading"}
    visited_pages = {"/home", "/about", "/contact", "/home"}  # Duplicates removed
    
    # Fast membership testing
    if "music" in user_interests:
        print("User likes music")
    
    # Set operations for filtering
    tech_interests = {"programming", "ai", "robotics"}
    common_interests = user_interests & tech_interests
    
    print("\n=== Set Use Cases ===")
    print(f"User interests: {user_interests}")
    print(f"Visited pages: {visited_pages}")
    print(f"Common with tech: {common_interests}")
    
    # Use LIST when:
    # 1. Need ordered, mutable collection
    # 2. May contain duplicates
    # 3. Need indexing/slicing
    # 4. Need to modify elements
    
    # Example: Shopping cart, task queue, scores
    shopping_cart = ["apple", "banana", "apple", "milk"]  # Duplicates OK
    task_queue = ["task1", "task2", "task3"]  # Order matters
    scores = [85, 90, 78, 85]  # Duplicates and order matter
    
    # Modify as needed
    shopping_cart.append("bread")
    task_queue.pop(0)  # Remove first task
    scores[0] = 87  # Update first score
    
    print("\n=== List Use Cases ===")
    print(f"Shopping cart: {shopping_cart}")
    print(f"Task queue: {task_queue}")
    print(f"Scores: {scores}")

demonstrate_data_structure_choice()

# Performance comparison for different operations
def performance_comparison():
    """Compare performance characteristics."""
    import time
    
    # Create test data
    n = 100000
    test_data = list(range(n))
    
    # Create structures
    test_list = test_data.copy()
    test_tuple = tuple(test_data)
    test_set = set(test_data)
    
    # Membership testing
    search_value = n - 1  # Worst case for list
    
    start = time.time()
    result = search_value in test_list
    list_time = time.time() - start
    
    start = time.time()
    result = search_value in test_tuple
    tuple_time = time.time() - start
    
    start = time.time()
    result = search_value in test_set
    set_time = time.time() - start
    
    print("\n=== Performance Comparison ===")
    print(f"List membership test: {list_time:.6f}s")
    print(f"Tuple membership test: {tuple_time:.6f}s")
    print(f"Set membership test: {set_time:.6f}s")
    
    # Memory usage (approximate)
    import sys
    print(f"\nMemory usage (bytes):")
    print(f"List: {sys.getsizeof(test_list)}")
    print(f"Tuple: {sys.getsizeof(test_tuple)}")
    print(f"Set: {sys.getsizeof(test_set)}")

performance_comparison()
```

## 🎯 Advanced Applications and Patterns

### Data Processing Patterns

```python
# Pattern 1: Using tuples for multiple return values
def get_statistics(numbers):
    """Return multiple statistics as a tuple."""
    if not numbers:
        return 0, 0, 0, 0  # count, sum, min, max
    
    return len(numbers), sum(numbers), min(numbers), max(numbers)

def parse_line(line):
    """Parse a data line into structured components."""
    parts = line.strip().split(',')
    name = parts[0]
    age = int(parts[1])
    scores = tuple(int(score) for score in parts[2:])
    
    return name, age, scores

# Pattern 2: Using sets for filtering and validation
def validate_required_fields(data, required_fields):
    """Validate that all required fields are present."""
    data_fields = set(data.keys())
    missing_fields = set(required_fields) - data_fields
    extra_fields = data_fields - set(required_fields)
    
    return {
        'is_valid': len(missing_fields) == 0,
        'missing_fields': missing_fields,
        'extra_fields': extra_fields
    }

def filter_by_categories(items, allowed_categories):
    """Filter items by allowed categories."""
    allowed_set = set(allowed_categories)
    return [item for item in items if item.get('category') in allowed_set]

# Pattern 3: Combining structures for complex data
def create_student_gradebook():
    """Create a complex gradebook using tuples and sets."""
    # Student data: (name, student_id, major)
    students = [
        ("Alice", "S001", "CS"),
        ("Bob", "S002", "Math"),
        ("Charlie", "S003", "CS"),
        ("Diana", "S004", "Physics")
    ]
    
    # Grades: {student_id: [(assignment, score), ...]}
    grades = {
        "S001": [("HW1", 85), ("HW2", 90), ("Exam1", 78)],
        "S002": [("HW1", 92), ("HW2", 88), ("Exam1", 85)],
        "S003": [("HW1", 78), ("HW2", 82), ("Exam1", 90)],
        "S004": [("HW1", 95), ("HW2", 97), ("Exam1", 93)]
    }
    
    # Majors requiring specific assignments
    cs_requirements = {"HW1", "HW2", "Project1", "Exam1"}
    math_requirements = {"HW1", "HW2", "Quiz1", "Exam1"}
    physics_requirements = {"Lab1", "Lab2", "HW1", "Exam1"}
    
    major_requirements = {
        "CS": cs_requirements,
        "Math": math_requirements,
        "Physics": physics_requirements
    }
    
    return students, grades, major_requirements

def analyze_gradebook(students, grades, major_requirements):
    """Analyze student progress and requirements."""
    analysis = {}
    
    for name, student_id, major in students:
        completed_assignments = set(assignment for assignment, _ in grades.get(student_id, []))
        required_assignments = major_requirements.get(major, set())
        
        missing_assignments = required_assignments - completed_assignments
        extra_assignments = completed_assignments - required_assignments
        
        # Calculate average
        student_grades = grades.get(student_id, [])
        avg_score = sum(score for _, score in student_grades) / len(student_grades) if student_grades else 0
        
        analysis[name] = {
            'student_id': student_id,
            'major': major,
            'average_score': avg_score,
            'completed_assignments': completed_assignments,
            'missing_assignments': missing_assignments,
            'extra_assignments': extra_assignments,
            'requirements_met': len(missing_assignments) == 0
        }
    
    return analysis

# Test advanced patterns
print("=== Statistics Function ===")
test_numbers = [85, 90, 78, 92, 88]
count, total, minimum, maximum = get_statistics(test_numbers)
print(f"Numbers: {test_numbers}")
print(f"Count: {count}, Sum: {total}, Min: {minimum}, Max: {maximum}")

print("\n=== Line Parsing ===")
test_line = "Alice,20,85,90,78"
name, age, scores = parse_line(test_line)
print(f"Parsed: name={name}, age={age}, scores={scores}")

print("\n=== Field Validation ===")
test_data = {"name": "Alice", "age": 20, "email": "alice@example.com"}
required = ["name", "age", "phone"]
validation = validate_required_fields(test_data, required)
print(f"Validation: {validation}")

print("\n=== Category Filtering ===")
items = [
    {"name": "Apple", "category": "fruit", "price": 1.50},
    {"name": "Carrot", "category": "vegetable", "price": 0.80},
    {"name": "Banana", "category": "fruit", "price": 1.20},
    {"name": "Broccoli", "category": "vegetable", "price": 2.00}
]
allowed = ["fruit"]
filtered = filter_by_categories(items, allowed)
print(f"Filtered items: {[item['name'] for item in filtered]}")

print("\n=== Gradebook Analysis ===")
students, grades, requirements = create_student_gradebook()
analysis = analyze_gradebook(students, grades, requirements)

for name, info in analysis.items():
    print(f"\n{name} ({info['major']}):")
    print(f"  Average: {info['average_score']:.1f}")
    print(f"  Requirements met: {info['requirements_met']}")
    if info['missing_assignments']:
        print(f"  Missing: {info['missing_assignments']}")
    if info['extra_assignments']:
        print(f"  Extra: {info['extra_assignments']}")
```

## 🎯 Practice Exercises

### Exercise 1: Data Deduplication System

```python
def create_deduplication_system():
    """
    Create a system that:
    1. Removes duplicate records while preserving order
    2. Identifies records with partial matches
    3. Groups similar records together
    4. Uses appropriate data structures for efficiency
    
    Input: List of tuples representing records
    Output: Deduplicated data with analysis
    """
    # Your implementation here
    pass
```

### Exercise 2: Set-Based Analytics

```python
def implement_analytics_engine():
    """
    Implement an analytics engine that:
    1. Tracks user activities using sets
    2. Finds overlapping user interests
    3. Calculates similarity scores
    4. Recommends content based on set operations
    
    Use sets for efficient operations
    """
    # Your implementation here
    pass
```

### Exercise 3: Configuration Management

```python
def create_config_system():
    """
    Create a configuration management system using:
    1. Named tuples for configuration schemas
    2. Sets for validation
    3. Tuples for immutable settings
    4. Proper error handling and validation
    """
    # Your implementation here
    pass
```

## 📚 Summary and Best Practices

### Key Takeaways

**Tuples:**
- **Immutable sequences** - cannot be changed after creation
- **Ordered** - maintain insertion order
- **Allow duplicates** - can contain repeated values
- **Hashable** - can be used as dictionary keys
- **Fast access** - good performance for reading operations

**Sets:**
- **Unique elements only** - automatically remove duplicates
- **Unordered** - no guaranteed order (though insertion order is preserved in Python 3.7+)
- **Mutable** - can add/remove elements (frozenset for immutable version)
- **Fast membership testing** - O(1) average case
- **Mathematical operations** - union, intersection, difference

### When to Use Each

| Use Tuples When: | Use Sets When: | Use Lists When: |
|-----------------|----------------|-----------------|
| Data won't change | Need unique elements | Need ordered, mutable data |
| Order matters | Order doesn't matter | May contain duplicates |
| Need dictionary keys | Fast membership testing | Need indexing/slicing |
| Representing records | Set operations needed | Frequent modifications |
| Multiple return values | Filtering duplicates | Sequential processing |

### Performance Guidelines

- **Membership testing**: Sets O(1) vs Lists/Tuples O(n)
- **Memory usage**: Tuples < Lists < Sets (generally)
- **Creation time**: Lists fastest, Sets slowest
- **Access time**: Lists/Tuples by index O(1), Sets not applicable

### Best Practices Checklist

**For Tuples:**
- [ ] Use for immutable data that belongs together
- [ ] Leverage tuple unpacking for cleaner code
- [ ] Consider named tuples for better readability
- [ ] Use as dictionary keys when appropriate
- [ ] Remember the comma for single-element tuples

**For Sets:**
- [ ] Use for uniqueness requirements
- [ ] Leverage set operations for data analysis
- [ ] Use frozensets when immutability needed
- [ ] Consider sets for fast membership testing
- [ ] Remember that sets are unordered

**General:**
- [ ] Choose the right structure for your use case
- [ ] Consider performance implications
- [ ] Use type hints for better code documentation
- [ ] Handle edge cases (empty collections)
- [ ] Test with realistic data sizes

### Common Pitfalls to Avoid

1. **Single-element tuple**: `(42)` is not a tuple, `(42,)` is
2. **Set ordering**: Don't rely on set order for logic
3. **Mutable elements in sets**: Only hashable types allowed
4. **Empty set creation**: Use `set()`, not `{}`
5. **Modifying during iteration**: Create new structures instead

### Next Steps

After mastering tuples and sets:
1. Learn about [Dictionaries](./11-dictionaries.md)
2. Study advanced collection types in `collections` module
3. Explore performance optimization techniques
4. Practice with real-world data processing problems

---

**Remember**: Choose the right data structure for the job. Understanding the strengths and use cases of tuples and sets will make your Python code more efficient and Pythonic!
