# Dictionaries and Dictionary Operations

## 🎯 Objective
Master Python dictionaries - the versatile key-value data structure essential for efficient data storage, retrieval, and manipulation in competitive programming and real-world applications.

## 📖 Overview

Dictionaries are Python's implementation of hash tables, providing O(1) average-case performance for key-based operations. They are fundamental for mapping relationships, caching, counting, grouping, and representing structured data. Understanding dictionaries thoroughly is crucial for efficient problem-solving and data processing.

## 📝 Dictionary Creation and Basic Operations

### Creating Dictionaries

```python
# Empty dictionary creation
empty_dict = {}
also_empty = dict()

# Dictionary with initial key-value pairs
student_grades = {"Alice": 85, "Bob": 92, "Charlie": 78}
mixed_types = {1: "one", "two": 2, 3.14: "pi", True: "boolean"}

# Dictionary from other structures
pairs = [("a", 1), ("b", 2), ("c", 3)]
from_pairs = dict(pairs)

keys = ["name", "age", "city"]
values = ["Alice", 25, "NYC"]
from_zip = dict(zip(keys, values))

# Using dict() constructor with keyword arguments
person = dict(name="Bob", age=30, city="LA")

# Dictionary comprehensions
squares = {x: x**2 for x in range(5)}
even_squares = {x: x**2 for x in range(10) if x % 2 == 0}

# Create dictionary from string
char_count = {char: char.upper() for char in "hello"}

print(f"Student grades: {student_grades}")
print(f"Mixed types: {mixed_types}")
print(f"From pairs: {from_pairs}")
print(f"From zip: {from_zip}")
print(f"Person: {person}")
print(f"Squares: {squares}")
print(f"Even squares: {even_squares}")
print(f"Character mapping: {char_count}")

# Nested dictionaries
company = {
    "employees": {
        "engineering": ["Alice", "Bob"],
        "marketing": ["Charlie", "Diana"]
    },
    "locations": {
        "headquarters": "NYC",
        "branch": "LA"
    },
    "founded": 2020
}

print(f"Company structure: {company}")

# Complex key types (must be hashable)
def demonstrate_key_types():
    """Show different types that can be used as dictionary keys."""
    complex_dict = {
        42: "integer key",
        "string": "string key",
        3.14: "float key",
        True: "boolean key",
        (1, 2): "tuple key",
        frozenset([1, 2]): "frozenset key"
    }
    
    print("Valid key types:")
    for key, value in complex_dict.items():
        print(f"  {type(key).__name__}: {key} -> {value}")
    
    # These would cause errors (unhashable types):
    # complex_dict[[1, 2]] = "list key"  # TypeError
    # complex_dict[{1, 2}] = "set key"   # TypeError
    # complex_dict[{}] = "dict key"      # TypeError

demonstrate_key_types()
```

### Accessing and Modifying Dictionary Elements

```python
# Sample dictionary for operations
inventory = {
    "apples": 50,
    "bananas": 30,
    "oranges": 25,
    "grapes": 40
}

print(f"Original inventory: {inventory}")

# Accessing values
apple_count = inventory["apples"]  # Direct access (raises KeyError if missing)
banana_count = inventory.get("bananas")  # Safe access (returns None if missing)
grape_count = inventory.get("grapes", 0)  # With default value

print(f"Apples: {apple_count}")
print(f"Bananas: {banana_count}")
print(f"Grapes: {grape_count}")

# Safe access for missing keys
missing = inventory.get("pears", 0)  # Returns 0 instead of error
print(f"Pears (missing): {missing}")

# Adding/updating values
inventory["pears"] = 20  # Add new key-value pair
inventory["apples"] += 10  # Update existing value
inventory.update({"kiwis": 15, "mangoes": 12})  # Add multiple items

print(f"After additions: {inventory}")

# Update with another dictionary
new_stock = {"apples": 70, "strawberries": 8}
inventory.update(new_stock)
print(f"After update: {inventory}")

# setdefault - add key only if it doesn't exist
default_value = inventory.setdefault("coconuts", 5)
existing_value = inventory.setdefault("apples", 100)  # Won't change existing

print(f"Coconuts (new): {default_value}")
print(f"Apples (existing): {existing_value}")
print(f"After setdefault: {inventory}")

# Removing items
removed_oranges = inventory.pop("oranges")  # Remove and return value
removed_missing = inventory.pop("lemons", 0)  # Safe removal with default

print(f"Removed oranges: {removed_oranges}")
print(f"Removed lemons (missing): {removed_missing}")

# Remove arbitrary item
item_key, item_value = inventory.popitem()  # Removes last inserted item (LIFO)
print(f"Popped item: {item_key} = {item_value}")

# Delete with del statement
del inventory["grapes"]
print(f"After deletions: {inventory}")

# Clear all items
backup = inventory.copy()
inventory.clear()
print(f"After clear: {inventory}")
print(f"Backup: {backup}")
```

### Dictionary Views and Iteration

```python
# Sample data for iteration examples
student_info = {
    "Alice": {"age": 20, "grade": 85, "major": "CS"},
    "Bob": {"age": 21, "grade": 92, "major": "Math"},
    "Charlie": {"age": 19, "grade": 78, "major": "Physics"},
    "Diana": {"age": 22, "grade": 95, "major": "CS"}
}

print("=== Dictionary Views ===")

# Dictionary views (live views of the dictionary)
keys_view = student_info.keys()
values_view = student_info.values()
items_view = student_info.items()

print(f"Keys view: {keys_view}")
print(f"Values view: {list(values_view)}")  # Convert to list for display
print(f"Items view: {list(items_view)}")

# Views are live - they reflect changes
student_info["Eve"] = {"age": 20, "grade": 88, "major": "Biology"}
print(f"Keys after addition: {keys_view}")

# Iteration patterns
print("\n=== Iteration Patterns ===")

# Iterate over keys (default)
print("Students (keys only):")
for student in student_info:
    print(f"  {student}")

# Iterate over values
print("\nStudent details (values only):")
for details in student_info.values():
    print(f"  Age: {details['age']}, Grade: {details['grade']}")

# Iterate over key-value pairs
print("\nKey-value pairs:")
for name, details in student_info.items():
    print(f"  {name}: {details}")

# Conditional iteration
print("\nCS majors only:")
for name, details in student_info.items():
    if details["major"] == "CS":
        print(f"  {name}: Grade {details['grade']}")

# Enumerate with dictionaries
print("\nEnumerated items:")
for i, (name, details) in enumerate(student_info.items()):
    print(f"  {i}: {name}")

# Sorted iteration
print("\nSorted by name:")
for name in sorted(student_info.keys()):
    print(f"  {name}: {student_info[name]['grade']}")

print("\nSorted by grade (descending):")
sorted_by_grade = sorted(student_info.items(), 
                        key=lambda item: item[1]['grade'], 
                        reverse=True)
for name, details in sorted_by_grade:
    print(f"  {name}: {details['grade']}")
```

## 🔍 Advanced Dictionary Operations

### Dictionary Comprehensions and Transformations

```python
# Sample data for transformations
raw_data = [
    ("Alice", 85, "CS"),
    ("Bob", 92, "Math"),
    ("Charlie", 78, "Physics"),
    ("Diana", 95, "CS"),
    ("Eve", 88, "Biology")
]

numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Basic dictionary comprehensions
name_to_grade = {name: grade for name, grade, major in raw_data}
grade_categories = {name: "High" if grade >= 90 else "Medium" if grade >= 80 else "Low" 
                   for name, grade, major in raw_data}

print(f"Name to grade: {name_to_grade}")
print(f"Grade categories: {grade_categories}")

# Filtering with comprehensions
cs_students = {name: grade for name, grade, major in raw_data if major == "CS"}
high_performers = {name: grade for name, grade, major in raw_data if grade >= 90}

print(f"CS students: {cs_students}")
print(f"High performers: {high_performers}")

# Mathematical transformations
number_properties = {
    num: {
        "square": num**2,
        "cube": num**3,
        "is_even": num % 2 == 0,
        "is_prime": all(num % i != 0 for i in range(2, int(num**0.5) + 1)) and num > 1
    }
    for num in numbers
}

print("\nNumber properties (first 5):")
for num in list(number_properties.keys())[:5]:
    print(f"  {num}: {number_properties[num]}")

# String transformations
words = ["hello", "world", "python", "programming", "dictionary"]
word_analysis = {
    word: {
        "length": len(word),
        "uppercase": word.upper(),
        "vowel_count": sum(1 for char in word.lower() if char in "aeiou"),
        "starts_with_vowel": word[0].lower() in "aeiou"
    }
    for word in words
}

print("\nWord analysis:")
for word, analysis in word_analysis.items():
    print(f"  {word}: {analysis}")

# Nested comprehensions
multiplication_table = {
    i: {j: i*j for j in range(1, 6)} 
    for i in range(1, 6)
}

print("\nMultiplication table (5x5):")
for i, row in multiplication_table.items():
    print(f"  {i}: {row}")

# Conditional nested structures
student_groups = {
    major: {
        name: grade for name, grade, student_major in raw_data 
        if student_major == major
    }
    for major in set(major for _, _, major in raw_data)
}

print("\nStudents grouped by major:")
for major, students in student_groups.items():
    print(f"  {major}: {students}")
```

### Dictionary Merging and Combining

```python
# Sample dictionaries for merging
dict1 = {"a": 1, "b": 2, "c": 3}
dict2 = {"b": 20, "d": 4, "e": 5}
dict3 = {"c": 30, "f": 6, "g": 7}

print(f"Dict1: {dict1}")
print(f"Dict2: {dict2}")
print(f"Dict3: {dict3}")

# Method 1: Using update() (modifies original)
merged_update = dict1.copy()
merged_update.update(dict2)
print(f"Merged with update: {merged_update}")

# Method 2: Using {**dict1, **dict2} (Python 3.5+)
merged_unpack = {**dict1, **dict2}
print(f"Merged with unpacking: {merged_unpack}")

# Method 3: Using | operator (Python 3.9+)
try:
    merged_union = dict1 | dict2
    print(f"Merged with union operator: {merged_union}")
except TypeError:
    print("Union operator not available (Python < 3.9)")

# Method 4: Custom merging with conflict resolution
def merge_dicts_with_strategy(strategy="last_wins", *dicts):
    """Merge dictionaries with different conflict resolution strategies."""
    result = {}
    
    for d in dicts:
        for key, value in d.items():
            if key not in result:
                result[key] = value
            else:
                if strategy == "last_wins":
                    result[key] = value
                elif strategy == "first_wins":
                    pass  # Keep existing value
                elif strategy == "sum":
                    if isinstance(result[key], (int, float)) and isinstance(value, (int, float)):
                        result[key] += value
                    else:
                        result[key] = value
                elif strategy == "list":
                    if not isinstance(result[key], list):
                        result[key] = [result[key]]
                    result[key].append(value)
    
    return result

# Test different merging strategies
print("\n=== Merging Strategies ===")
print(f"Last wins: {merge_dicts_with_strategy('last_wins', dict1, dict2, dict3)}")
print(f"First wins: {merge_dicts_with_strategy('first_wins', dict1, dict2, dict3)}")
print(f"Sum values: {merge_dicts_with_strategy('sum', dict1, dict2, dict3)}")
print(f"Collect in lists: {merge_dicts_with_strategy('list', dict1, dict2, dict3)}")

# Deep merging of nested dictionaries
def deep_merge(dict1, dict2):
    """Recursively merge nested dictionaries."""
    result = dict1.copy()
    
    for key, value in dict2.items():
        if key in result and isinstance(result[key], dict) and isinstance(value, dict):
            result[key] = deep_merge(result[key], value)
        else:
            result[key] = value
    
    return result

# Test deep merging
nested_dict1 = {
    "users": {"alice": {"age": 25, "city": "NYC"}},
    "settings": {"theme": "dark", "notifications": True}
}

nested_dict2 = {
    "users": {"alice": {"email": "alice@example.com"}, "bob": {"age": 30}},
    "settings": {"language": "en"},
    "features": {"beta": True}
}

deep_merged = deep_merge(nested_dict1, nested_dict2)
print(f"\nDeep merged: {deep_merged}")

# Combining dictionaries for analysis
sales_data = [
    {"product": "laptop", "region": "north", "sales": 100},
    {"product": "mouse", "region": "north", "sales": 50},
    {"product": "laptop", "region": "south", "sales": 80},
    {"product": "keyboard", "region": "north", "sales": 30},
    {"product": "laptop", "region": "east", "sales": 120},
]

def aggregate_sales(data, group_by):
    """Aggregate sales data by specified field."""
    result = {}
    
    for record in data:
        key = record[group_by]
        if key not in result:
            result[key] = {"total_sales": 0, "count": 0}
        
        result[key]["total_sales"] += record["sales"]
        result[key]["count"] += 1
        result[key]["average"] = result[key]["total_sales"] / result[key]["count"]
    
    return result

# Aggregate by different dimensions
by_product = aggregate_sales(sales_data, "product")
by_region = aggregate_sales(sales_data, "region")

print("\n=== Sales Analysis ===")
print("By product:")
for product, stats in by_product.items():
    print(f"  {product}: {stats}")

print("By region:")
for region, stats in by_region.items():
    print(f"  {region}: {stats}")
```

### Dictionary Sorting and Filtering

```python
# Sample data for sorting and filtering
employees = {
    "emp001": {"name": "Alice", "salary": 75000, "department": "Engineering", "years": 3},
    "emp002": {"name": "Bob", "salary": 65000, "department": "Marketing", "years": 2},
    "emp003": {"name": "Charlie", "salary": 85000, "department": "Engineering", "years": 5},
    "emp004": {"name": "Diana", "salary": 70000, "department": "Sales", "years": 4},
    "emp005": {"name": "Eve", "salary": 90000, "department": "Engineering", "years": 6},
}

print("Original employees:")
for emp_id, details in employees.items():
    print(f"  {emp_id}: {details['name']} - ${details['salary']}")

# Sorting by different criteria
print("\n=== Sorting Examples ===")

# Sort by salary (descending)
by_salary = dict(sorted(employees.items(), 
                       key=lambda item: item[1]['salary'], 
                       reverse=True))

print("Sorted by salary (highest first):")
for emp_id, details in by_salary.items():
    print(f"  {details['name']}: ${details['salary']}")

# Sort by name (alphabetical)
by_name = dict(sorted(employees.items(), 
                     key=lambda item: item[1]['name']))

print("\nSorted by name:")
for emp_id, details in by_name.items():
    print(f"  {details['name']}")

# Sort by multiple criteria (department, then salary)
by_dept_salary = dict(sorted(employees.items(), 
                            key=lambda item: (item[1]['department'], -item[1]['salary'])))

print("\nSorted by department, then salary (desc):")
for emp_id, details in by_dept_salary.items():
    print(f"  {details['department']} - {details['name']}: ${details['salary']}")

# Filtering operations
print("\n=== Filtering Examples ===")

# Filter by salary threshold
high_earners = {emp_id: details for emp_id, details in employees.items() 
                if details['salary'] >= 80000}

print("High earners (>=80k):")
for emp_id, details in high_earners.items():
    print(f"  {details['name']}: ${details['salary']}")

# Filter by department
engineers = {emp_id: details for emp_id, details in employees.items() 
             if details['department'] == 'Engineering'}

print("\nEngineering employees:")
for emp_id, details in engineers.items():
    print(f"  {details['name']}")

# Complex filtering with multiple conditions
senior_engineers = {
    emp_id: details for emp_id, details in employees.items() 
    if details['department'] == 'Engineering' and details['years'] >= 4
}

print("\nSenior engineers (4+ years):")
for emp_id, details in senior_engineers.items():
    print(f"  {details['name']}: {details['years']} years")

# Filtering with custom functions
def filter_employees(employees, condition_func):
    """Filter employees using a custom condition function."""
    return {emp_id: details for emp_id, details in employees.items() 
            if condition_func(details)}

# Define custom filters
def is_experienced(employee):
    return employee['years'] >= 5

def is_well_paid(employee):
    return employee['salary'] >= 75000

def is_in_tech(employee):
    return employee['department'] in ['Engineering', 'IT', 'Data Science']

# Apply custom filters
experienced = filter_employees(employees, is_experienced)
well_paid = filter_employees(employees, is_well_paid)
tech_workers = filter_employees(employees, is_in_tech)

print("\nExperienced employees (5+ years):")
for emp_id, details in experienced.items():
    print(f"  {details['name']}: {details['years']} years")

# Combine filters
experienced_and_well_paid = filter_employees(
    employees, 
    lambda emp: is_experienced(emp) and is_well_paid(emp)
)

print("\nExperienced AND well-paid:")
for emp_id, details in experienced_and_well_paid.items():
    print(f"  {details['name']}: {details['years']} years, ${details['salary']}")

# Statistical filtering
salaries = [details['salary'] for details in employees.values()]
avg_salary = sum(salaries) / len(salaries)
above_average = filter_employees(employees, lambda emp: emp['salary'] > avg_salary)

print(f"\nAverage salary: ${avg_salary:.2f}")
print("Above average earners:")
for emp_id, details in above_average.items():
    print(f"  {details['name']}: ${details['salary']}")
```

## 🔄 Common Dictionary Patterns and Algorithms

### Counting and Frequency Analysis

```python
# Text analysis using dictionaries
def analyze_text(text):
    """Comprehensive text analysis using dictionaries."""
    # Character frequency
    char_freq = {}
    for char in text.lower():
        if char.isalpha():  # Only count letters
            char_freq[char] = char_freq.get(char, 0) + 1
    
    # Word frequency
    words = text.lower().split()
    word_freq = {}
    for word in words:
        # Clean word (remove punctuation)
        clean_word = ''.join(char for char in word if char.isalnum())
        if clean_word:
            word_freq[clean_word] = word_freq.get(clean_word, 0) + 1
    
    # Word length distribution
    length_dist = {}
    for word in word_freq:
        length = len(word)
        length_dist[length] = length_dist.get(length, 0) + word_freq[word]
    
    return {
        'char_frequency': char_freq,
        'word_frequency': word_freq,
        'length_distribution': length_dist,
        'total_chars': len([c for c in text if c.isalpha()]),
        'total_words': len(words),
        'unique_words': len(word_freq)
    }

# Alternative counting using defaultdict
from collections import defaultdict, Counter

def analyze_text_advanced(text):
    """Text analysis using collections.defaultdict and Counter."""
    # Using defaultdict for automatic initialization
    char_freq = defaultdict(int)
    word_freq = defaultdict(int)
    
    for char in text.lower():
        if char.isalpha():
            char_freq[char] += 1
    
    words = text.lower().split()
    for word in words:
        clean_word = ''.join(char for char in word if char.isalnum())
        if clean_word:
            word_freq[clean_word] += 1
    
    # Using Counter for even simpler counting
    counter_chars = Counter(char.lower() for char in text if char.isalpha())
    counter_words = Counter(''.join(char for char in word if char.isalnum())
                           for word in text.lower().split()
                           if ''.join(char for char in word if char.isalnum()))
    
    return {
        'defaultdict_chars': dict(char_freq),
        'defaultdict_words': dict(word_freq),
        'counter_chars': dict(counter_chars),
        'counter_words': dict(counter_words),
        'most_common_chars': counter_chars.most_common(5),
        'most_common_words': counter_words.most_common(5)
    }

# Test text analysis
sample_text = """
Python is a powerful programming language. Python is easy to learn and Python is versatile.
Many developers choose Python for data science, web development, and automation.
Python's simplicity makes Python popular among beginners and experts alike.
"""

print("=== Text Analysis ===")
basic_analysis = analyze_text(sample_text)
print(f"Total characters: {basic_analysis['total_chars']}")
print(f"Total words: {basic_analysis['total_words']}")
print(f"Unique words: {basic_analysis['unique_words']}")

print("\nTop character frequencies:")
sorted_chars = sorted(basic_analysis['char_frequency'].items(), 
                     key=lambda x: x[1], reverse=True)
for char, count in sorted_chars[:5]:
    print(f"  '{char}': {count}")

print("\nTop word frequencies:")
sorted_words = sorted(basic_analysis['word_frequency'].items(), 
                     key=lambda x: x[1], reverse=True)
for word, count in sorted_words[:5]:
    print(f"  '{word}': {count}")

# Advanced analysis
advanced_analysis = analyze_text_advanced(sample_text)
print("\nMost common characters (Counter):")
for char, count in advanced_analysis['most_common_chars']:
    print(f"  '{char}': {count}")

print("\nMost common words (Counter):")
for word, count in advanced_analysis['most_common_words']:
    print(f"  '{word}': {count}")

# Practical counting applications
def count_elements_by_property(items, property_func):
    """Count items grouped by a property function."""
    counts = {}
    for item in items:
        prop = property_func(item)
        counts[prop] = counts.get(prop, 0) + 1
    return counts

# Example: Count students by grade ranges
students_data = [
    {"name": "Alice", "grade": 85},
    {"name": "Bob", "grade": 92},
    {"name": "Charlie", "grade": 78},
    {"name": "Diana", "grade": 95},
    {"name": "Eve", "grade": 88},
    {"name": "Frank", "grade": 73},
    {"name": "Grace", "grade": 97}
]

def grade_category(student):
    """Categorize student by grade."""
    grade = student['grade']
    if grade >= 90:
        return "A"
    elif grade >= 80:
        return "B"
    elif grade >= 70:
        return "C"
    else:
        return "F"

grade_distribution = count_elements_by_property(students_data, grade_category)
print(f"\nGrade distribution: {grade_distribution}")

# Count by multiple properties
def count_by_multiple_properties(items, property_funcs):
    """Count items by combinations of properties."""
    counts = {}
    
    for item in items:
        key = tuple(func(item) for func in property_funcs)
        counts[key] = counts.get(key, 0) + 1
    
    return counts

# Example with employees data
extended_employees = [
    {"name": "Alice", "dept": "Engineering", "level": "Senior", "salary": 85000},
    {"name": "Bob", "dept": "Marketing", "level": "Junior", "salary": 55000},
    {"name": "Charlie", "dept": "Engineering", "level": "Senior", "salary": 90000},
    {"name": "Diana", "dept": "Sales", "level": "Mid", "salary": 70000},
    {"name": "Eve", "dept": "Engineering", "level": "Mid", "salary": 75000},
]

dept_level_counts = count_by_multiple_properties(
    extended_employees,
    [lambda emp: emp['dept'], lambda emp: emp['level']]
)

print("\nEmployee count by department and level:")
for (dept, level), count in dept_level_counts.items():
    print(f"  {dept} {level}: {count}")
```

### Grouping and Aggregation

```python
# Advanced grouping patterns
def group_by(items, key_func):
    """Group items by a key function."""
    groups = {}
    for item in items:
        key = key_func(item)
        if key not in groups:
            groups[key] = []
        groups[key].append(item)
    return groups

def group_by_multiple(items, key_funcs):
    """Group items by multiple key functions."""
    groups = {}
    for item in items:
        key = tuple(func(item) for func in key_funcs)
        if key not in groups:
            groups[key] = []
        groups[key].append(item)
    return groups

# Sales data for grouping examples
sales_transactions = [
    {"id": 1, "product": "laptop", "category": "electronics", "amount": 1200, "region": "north", "month": "jan"},
    {"id": 2, "product": "mouse", "category": "electronics", "amount": 25, "region": "south", "month": "jan"},
    {"id": 3, "product": "desk", "category": "furniture", "amount": 300, "region": "north", "month": "feb"},
    {"id": 4, "product": "laptop", "category": "electronics", "amount": 1200, "region": "east", "month": "jan"},
    {"id": 5, "product": "chair", "category": "furniture", "amount": 150, "region": "south", "month": "feb"},
    {"id": 6, "product": "keyboard", "category": "electronics", "amount": 75, "region": "north", "month": "mar"},
    {"id": 7, "product": "laptop", "category": "electronics", "amount": 1200, "region": "west", "month": "mar"},
]

print("=== Grouping and Aggregation ===")

# Group by single property
by_category = group_by(sales_transactions, lambda x: x['category'])
print("Sales by category:")
for category, transactions in by_category.items():
    total = sum(t['amount'] for t in transactions)
    count = len(transactions)
    print(f"  {category}: {count} transactions, ${total} total")

# Group by multiple properties
by_region_month = group_by_multiple(
    sales_transactions, 
    [lambda x: x['region'], lambda x: x['month']]
)

print("\nSales by region and month:")
for (region, month), transactions in by_region_month.items():
    total = sum(t['amount'] for t in transactions)
    print(f"  {region.title()} {month.title()}: ${total}")

# Advanced aggregation functions
def aggregate_data(items, group_key, aggregations):
    """
    Aggregate data with multiple aggregation functions.
    
    aggregations: dict of {result_key: aggregation_function}
    """
    groups = group_by(items, group_key)
    result = {}
    
    for key, group_items in groups.items():
        result[key] = {}
        for agg_name, agg_func in aggregations.items():
            result[key][agg_name] = agg_func(group_items)
    
    return result

# Define aggregation functions
aggregations = {
    'total_sales': lambda items: sum(item['amount'] for item in items),
    'transaction_count': len,
    'average_sale': lambda items: sum(item['amount'] for item in items) / len(items),
    'max_sale': lambda items: max(item['amount'] for item in items),
    'min_sale': lambda items: min(item['amount'] for item in items),
    'products': lambda items: list(set(item['product'] for item in items))
}

# Aggregate by region
region_stats = aggregate_data(
    sales_transactions, 
    lambda x: x['region'], 
    aggregations
)

print("\nRegional sales statistics:")
for region, stats in region_stats.items():
    print(f"  {region.title()}:")
    for stat_name, value in stats.items():
        if stat_name == 'products':
            print(f"    {stat_name}: {value}")
        elif stat_name == 'average_sale':
            print(f"    {stat_name}: ${value:.2f}")
        elif isinstance(value, (int, float)):
            print(f"    {stat_name}: ${value}")
        else:
            print(f"    {stat_name}: {value}")

# Pivot table functionality
def create_pivot_table(data, row_key, col_key, value_key, agg_func=sum):
    """Create a pivot table from data."""
    pivot = {}
    
    # Group data
    for item in data:
        row = row_key(item)
        col = col_key(item)
        val = value_key(item)
        
        if row not in pivot:
            pivot[row] = {}
        if col not in pivot[row]:
            pivot[row][col] = []
        
        pivot[row][col].append(val)
    
    # Apply aggregation
    for row in pivot:
        for col in pivot[row]:
            pivot[row][col] = agg_func(pivot[row][col])
    
    return pivot

# Create pivot table: region vs month with total sales
pivot_table = create_pivot_table(
    sales_transactions,
    lambda x: x['region'],
    lambda x: x['month'],
    lambda x: x['amount'],
    sum
)

print("\nPivot table (Region vs Month - Total Sales):")
months = sorted(set(t['month'] for t in sales_transactions))
regions = sorted(pivot_table.keys())

# Print header
print(f"{'Region':<10}", end="")
for month in months:
    print(f"{month.title():<8}", end="")
print()

# Print data
for region in regions:
    print(f"{region.title():<10}", end="")
    for month in months:
        value = pivot_table.get(region, {}).get(month, 0)
        print(f"${value:<7}", end="")
    print()

# Cross-tabulation
def cross_tabulate(data, row_key, col_key):
    """Create a cross-tabulation table."""
    return create_pivot_table(data, row_key, col_key, lambda x: 1, sum)

# Cross-tab: category vs region (count of transactions)
cross_tab = cross_tabulate(
    sales_transactions,
    lambda x: x['category'],
    lambda x: x['region']
)

print("\nCross-tabulation (Category vs Region - Transaction Count):")
regions = sorted(set(t['region'] for t in sales_transactions))
categories = sorted(cross_tab.keys())

print(f"{'Category':<12}", end="")
for region in regions:
    print(f"{region.title():<8}", end="")
print()

for category in categories:
    print(f"{category.title():<12}", end="")
    for region in regions:
        count = cross_tab.get(category, {}).get(region, 0)
        print(f"{count:<8}", end="")
    print()
```

### Caching and Memoization

```python
# Simple memoization using dictionaries
def memoize(func):
    """Decorator to add memoization to a function."""
    cache = {}
    
    def wrapper(*args, **kwargs):
        # Create a key from arguments (only for hashable args)
        key = (args, tuple(sorted(kwargs.items())))
        
        if key not in cache:
            cache[key] = func(*args, **kwargs)
            print(f"Computing {func.__name__}{args}: {cache[key]}")
        else:
            print(f"Cache hit for {func.__name__}{args}: {cache[key]}")
        
        return cache[key]
    
    wrapper.cache = cache  # Expose cache for inspection
    wrapper.cache_clear = lambda: cache.clear()  # Method to clear cache
    return wrapper

# Example: Fibonacci with memoization
@memoize
def fibonacci(n):
    """Calculate nth Fibonacci number with memoization."""
    if n <= 1:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)

@memoize
def factorial(n):
    """Calculate factorial with memoization."""
    if n <= 1:
        return 1
    return n * factorial(n - 1)

# Test memoization
print("=== Memoization Examples ===")
print(f"Fibonacci(10): {fibonacci(10)}")
print(f"Fibonacci(8): {fibonacci(8)}")  # Should use cache
print(f"Factorial(5): {factorial(5)}")

# LRU Cache implementation using dictionaries
class LRUCache:
    """Least Recently Used cache implementation."""
    
    def __init__(self, capacity):
        self.capacity = capacity
        self.cache = {}
        self.access_order = []  # Track access order
    
    def get(self, key):
        """Get value by key, return None if not found."""
        if key in self.cache:
            # Move to end (most recently used)
            self.access_order.remove(key)
            self.access_order.append(key)
            return self.cache[key]
        return None
    
    def put(self, key, value):
        """Put key-value pair in cache."""
        if key in self.cache:
            # Update existing key
            self.cache[key] = value
            self.access_order.remove(key)
            self.access_order.append(key)
        else:
            # Add new key
            if len(self.cache) >= self.capacity:
                # Remove least recently used
                lru_key = self.access_order.pop(0)
                del self.cache[lru_key]
                print(f"Evicted {lru_key} from cache")
            
            self.cache[key] = value
            self.access_order.append(key)
    
    def display(self):
        """Display current cache state."""
        print(f"Cache: {self.cache}")
        print(f"Access order: {self.access_order}")

# Test LRU Cache
print("\n=== LRU Cache Example ===")
lru = LRUCache(3)

lru.put("a", 1)
lru.put("b", 2)
lru.put("c", 3)
lru.display()

print(f"Get 'a': {lru.get('a')}")  # 'a' becomes most recently used
lru.display()

lru.put("d", 4)  # Should evict 'b' (least recently used)
lru.display()

print(f"Get 'b': {lru.get('b')}")  # Should return None

# Frequency-based cache
class FrequencyCache:
    """Cache that evicts least frequently used items."""
    
    def __init__(self, capacity):
        self.capacity = capacity
        self.cache = {}
        self.frequencies = {}
    
    def get(self, key):
        """Get value and increment frequency."""
        if key in self.cache:
            self.frequencies[key] += 1
            return self.cache[key]
        return None
    
    def put(self, key, value):
        """Put value and manage capacity."""
        if key in self.cache:
            self.cache[key] = value
            self.frequencies[key] += 1
        else:
            if len(self.cache) >= self.capacity:
                # Find and remove least frequent item
                lfu_key = min(self.frequencies, key=self.frequencies.get)
                del self.cache[lfu_key]
                del self.frequencies[lfu_key]
                print(f"Evicted {lfu_key} (frequency: {self.frequencies.get(lfu_key, 0)})")
            
            self.cache[key] = value
            self.frequencies[key] = 1
    
    def display(self):
        """Display cache and frequencies."""
        print(f"Cache: {self.cache}")
        print(f"Frequencies: {self.frequencies}")

# Test frequency cache
print("\n=== Frequency Cache Example ===")
freq_cache = FrequencyCache(3)

freq_cache.put("x", 10)
freq_cache.put("y", 20)
freq_cache.put("z", 30)
freq_cache.display()

# Access some items multiple times
freq_cache.get("x")
freq_cache.get("x")
freq_cache.get("y")
freq_cache.display()

freq_cache.put("w", 40)  # Should evict 'z' (least frequent)
freq_cache.display()

# Cache with TTL (Time To Live)
import time

class TTLCache:
    """Cache with time-to-live expiration."""
    
    def __init__(self, default_ttl=60):
        self.cache = {}
        self.timestamps = {}
        self.ttls = {}
        self.default_ttl = default_ttl
    
    def put(self, key, value, ttl=None):
        """Put value with optional TTL."""
        current_time = time.time()
        self.cache[key] = value
        self.timestamps[key] = current_time
        self.ttls[key] = ttl or self.default_ttl
    
    def get(self, key):
        """Get value if not expired."""
        if key not in self.cache:
            return None
        
        current_time = time.time()
        if current_time - self.timestamps[key] > self.ttls[key]:
            # Expired
            del self.cache[key]
            del self.timestamps[key]
            del self.ttls[key]
            return None
        
        return self.cache[key]
    
    def cleanup_expired(self):
        """Remove all expired entries."""
        current_time = time.time()
        expired_keys = []
        
        for key in self.cache:
            if current_time - self.timestamps[key] > self.ttls[key]:
                expired_keys.append(key)
        
        for key in expired_keys:
            del self.cache[key]
            del self.timestamps[key]
            del self.ttls[key]
        
        return len(expired_keys)

# Test TTL cache
print("\n=== TTL Cache Example ===")
ttl_cache = TTLCache(default_ttl=2)  # 2 second TTL

ttl_cache.put("short", "expires soon", ttl=1)
ttl_cache.put("long", "expires later", ttl=5)

print(f"Short: {ttl_cache.get('short')}")
print(f"Long: {ttl_cache.get('long')}")

time.sleep(1.5)  # Wait 1.5 seconds

print(f"After 1.5s - Short: {ttl_cache.get('short')}")  # Should be None
print(f"After 1.5s - Long: {ttl_cache.get('long')}")   # Should still exist
```

## 🎯 Dictionary Applications in Algorithms

### Graph Representation and Algorithms

```python
# Graph representation using dictionaries
class Graph:
    """Graph implementation using adjacency list (dictionary)."""
    
    def __init__(self, directed=False):
        self.graph = {}
        self.directed = directed
    
    def add_vertex(self, vertex):
        """Add a vertex to the graph."""
        if vertex not in self.graph:
            self.graph[vertex] = []
    
    def add_edge(self, from_vertex, to_vertex, weight=1):
        """Add an edge between vertices."""
        # Ensure vertices exist
        self.add_vertex(from_vertex)
        self.add_vertex(to_vertex)
        
        # Add edge
        self.graph[from_vertex].append((to_vertex, weight))
        
        # Add reverse edge for undirected graph
        if not self.directed:
            self.graph[to_vertex].append((from_vertex, weight))
    
    def get_neighbors(self, vertex):
        """Get neighbors of a vertex."""
        return self.graph.get(vertex, [])
    
    def display(self):
        """Display the graph."""
        for vertex, edges in self.graph.items():
            print(f"{vertex}: {edges}")
    
    def bfs(self, start_vertex):
        """Breadth-first search."""
        if start_vertex not in self.graph:
            return []
        
        visited = set()
        queue = [start_vertex]
        result = []
        
        while queue:
            vertex = queue.pop(0)
            if vertex not in visited:
                visited.add(vertex)
                result.append(vertex)
                
                # Add unvisited neighbors to queue
                for neighbor, _ in self.get_neighbors(vertex):
                    if neighbor not in visited:
                        queue.append(neighbor)
        
        return result
    
    def dfs(self, start_vertex, visited=None):
        """Depth-first search."""
        if visited is None:
            visited = set()
        
        if start_vertex not in self.graph or start_vertex in visited:
            return []
        
        visited.add(start_vertex)
        result = [start_vertex]
        
        for neighbor, _ in self.get_neighbors(start_vertex):
            if neighbor not in visited:
                result.extend(self.dfs(neighbor, visited))
        
        return result
    
    def shortest_path(self, start, end):
        """Find shortest path using BFS (unweighted)."""
        if start not in self.graph or end not in self.graph:
            return None
        
        queue = [(start, [start])]
        visited = set()
        
        while queue:
            vertex, path = queue.pop(0)
            
            if vertex == end:
                return path
            
            if vertex not in visited:
                visited.add(vertex)
                
                for neighbor, _ in self.get_neighbors(vertex):
                    if neighbor not in visited:
                        queue.append((neighbor, path + [neighbor]))
        
        return None  # No path found

# Test graph implementation
print("=== Graph Algorithms ===")
g = Graph()

# Add edges to create a graph
edges = [
    ("A", "B"), ("A", "C"), ("B", "D"), ("C", "D"), 
    ("D", "E"), ("B", "E"), ("C", "F"), ("F", "E")
]

for from_v, to_v in edges:
    g.add_edge(from_v, to_v)

print("Graph structure:")
g.display()

print(f"\nBFS from A: {g.bfs('A')}")
print(f"DFS from A: {g.dfs('A')}")
print(f"Shortest path A to E: {g.shortest_path('A', 'E')}")

# Weighted graph for Dijkstra's algorithm
def dijkstra(graph, start):
    """Dijkstra's shortest path algorithm."""
    distances = {vertex: float('infinity') for vertex in graph}
    distances[start] = 0
    unvisited = set(graph.keys())
    previous = {}
    
    while unvisited:
        # Find unvisited vertex with minimum distance
        current = min(unvisited, key=lambda vertex: distances[vertex])
        unvisited.remove(current)
        
        # Update distances to neighbors
        for neighbor, weight in graph[current]:
            if neighbor in unvisited:
                new_distance = distances[current] + weight
                if new_distance < distances[neighbor]:
                    distances[neighbor] = new_distance
                    previous[neighbor] = current
    
    return distances, previous

def construct_path(previous, start, end):
    """Construct path from previous vertices dictionary."""
    path = []
    current = end
    
    while current is not None:
        path.append(current)
        current = previous.get(current)
    
    path.reverse()
    return path if path[0] == start else []

# Test Dijkstra's algorithm
weighted_graph = {
    'A': [('B', 4), ('C', 2)],
    'B': [('C', 1), ('D', 5)],
    'C': [('D', 8), ('E', 10)],
    'D': [('E', 2)],
    'E': []
}

print("\n=== Dijkstra's Algorithm ===")
distances, previous = dijkstra(weighted_graph, 'A')
print(f"Distances from A: {distances}")

path_to_e = construct_path(previous, 'A', 'E')
print(f"Shortest path A to E: {path_to_e}")
print(f"Distance: {distances['E']}")
```

### Dynamic Programming with Dictionaries

```python
# Dynamic programming problems using dictionaries for memoization

def knapsack_memo(weights, values, capacity):
    """0/1 Knapsack problem with memoization."""
    memo = {}
    n = len(weights)
    
    def dp(i, remaining_capacity):
        # Base case
        if i == n or remaining_capacity == 0:
            return 0
        
        # Check memo
        if (i, remaining_capacity) in memo:
            return memo[(i, remaining_capacity)]
        
        # Option 1: Don't take current item
        result = dp(i + 1, remaining_capacity)
        
        # Option 2: Take current item (if it fits)
        if weights[i] <= remaining_capacity:
            result = max(result, values[i] + dp(i + 1, remaining_capacity - weights[i]))
        
        memo[(i, remaining_capacity)] = result
        return result
    
    return dp(0, capacity), memo

def longest_common_subsequence(str1, str2):
    """Find longest common subsequence using memoization."""
    memo = {}
    
    def lcs(i, j):
        # Base case
        if i == len(str1) or j == len(str2):
            return 0
        
        # Check memo
        if (i, j) in memo:
            return memo[(i, j)]
        
        if str1[i] == str2[j]:
            result = 1 + lcs(i + 1, j + 1)
        else:
            result = max(lcs(i + 1, j), lcs(i, j + 1))
        
        memo[(i, j)] = result
        return result
    
    return lcs(0, 0), memo

def coin_change(coins, amount):
    """Minimum coins needed to make amount."""
    memo = {}
    
    def dp(remaining):
        if remaining == 0:
            return 0
        if remaining < 0:
            return float('inf')
        
        if remaining in memo:
            return memo[remaining]
        
        result = float('inf')
        for coin in coins:
            result = min(result, 1 + dp(remaining - coin))
        
        memo[remaining] = result
        return result
    
    result = dp(amount)
    return result if result != float('inf') else -1, memo

# Test DP problems
print("=== Dynamic Programming ===")

# Knapsack problem
weights = [1, 3, 4, 5]
values = [1, 4, 5, 7]
capacity = 7

max_value, knapsack_memo_dict = knapsack_memo(weights, values, capacity)
print(f"Knapsack max value: {max_value}")
print(f"Memo entries: {len(knapsack_memo_dict)}")

# LCS problem
str1 = "ABCDGH"
str2 = "AEDFHR"
lcs_length, lcs_memo_dict = longest_common_subsequence(str1, str2)
print(f"LCS of '{str1}' and '{str2}': {lcs_length}")
print(f"Memo entries: {len(lcs_memo_dict)}")

# Coin change problem
coins = [1, 3, 4]
amount = 6
min_coins, coin_memo = coin_change(coins, amount)
print(f"Min coins for amount {amount}: {min_coins}")
print(f"Memo entries: {len(coin_memo)}")

# Edit distance with path reconstruction
def edit_distance_with_path(str1, str2):
    """Calculate edit distance and reconstruct operations."""
    memo = {}
    operations = {}
    
    def dp(i, j):
        if i == 0:
            return j
        if j == 0:
            return i
        
        if (i, j) in memo:
            return memo[(i, j)]
        
        if str1[i-1] == str2[j-1]:
            result = dp(i-1, j-1)
            operations[(i, j)] = "match"
        else:
            replace_cost = 1 + dp(i-1, j-1)
            insert_cost = 1 + dp(i, j-1)
            delete_cost = 1 + dp(i-1, j)
            
            result = min(replace_cost, insert_cost, delete_cost)
            
            if result == replace_cost:
                operations[(i, j)] = "replace"
            elif result == insert_cost:
                operations[(i, j)] = "insert"
            else:
                operations[(i, j)] = "delete"
        
        memo[(i, j)] = result
        return result
    
    distance = dp(len(str1), len(str2))
    
    # Reconstruct path
    path = []
    i, j = len(str1), len(str2)
    while i > 0 or j > 0:
        op = operations.get((i, j), "")
        if op == "match":
            path.append(f"Match {str1[i-1]}")
            i, j = i-1, j-1
        elif op == "replace":
            path.append(f"Replace {str1[i-1]} with {str2[j-1]}")
            i, j = i-1, j-1
        elif op == "insert":
            path.append(f"Insert {str2[j-1]}")
            j = j-1
        elif op == "delete":
            path.append(f"Delete {str1[i-1]}")
            i = i-1
        else:
            break
    
    path.reverse()
    return distance, path

# Test edit distance
print("\n=== Edit Distance ===")
word1 = "kitten"
word2 = "sitting"
distance, ops = edit_distance_with_path(word1, word2)
print(f"Edit distance from '{word1}' to '{word2}': {distance}")
print("Operations:")
for op in ops:
    print(f"  {op}")
```

## 🎯 Practice Exercises

### Exercise 1: Multi-Level Cache System

```python
def implement_multi_level_cache():
    """
    Implement a multi-level cache system with:
    1. L1 cache (small, fast) - LRU eviction
    2. L2 cache (medium, slower) - LFU eviction  
    3. L3 cache (large, slowest) - TTL eviction
    4. Cache coherency between levels
    5. Statistics tracking
    """
    # Your implementation here
    pass
```

### Exercise 2: Social Network Analysis

```python
def create_social_network_analyzer():
    """
    Create a social network analysis system using dictionaries:
    1. User profiles and connections
    2. Friend recommendation algorithm
    3. Community detection
    4. Influence scoring
    5. Activity tracking and analytics
    """
    # Your implementation here
    pass
```

### Exercise 3: Configuration Management System

```python
def build_config_manager():
    """
    Build a configuration management system:
    1. Hierarchical configuration (default -> environment -> user)
    2. Configuration validation and type checking
    3. Dynamic configuration updates
    4. Configuration history and rollback
    5. Environment-specific overrides
    """
    # Your implementation here
    pass
```

## 📚 Summary and Best Practices

### Key Dictionary Concepts

**Core Properties:**
- **Key-value mapping** - Associate keys with values
- **Mutable** - Can be modified after creation
- **Unordered** (Python 3.7+ maintains insertion order)
- **Keys must be hashable** - Immutable types only
- **O(1) average access time** - Very fast lookups

**Common Operations:**
- Access: `dict[key]` or `dict.get(key, default)`
- Modify: `dict[key] = value`
- Remove: `del dict[key]` or `dict.pop(key)`
- Iterate: `dict.keys()`, `dict.values()`, `dict.items()`

### Performance Guidelines

| Operation | Time Complexity | Notes |
|-----------|----------------|-------|
| Access (get/set) | O(1) average | O(n) worst case (rare) |
| Deletion | O(1) average | O(n) worst case (rare) |
| Iteration | O(n) | Over all key-value pairs |
| Membership test | O(1) average | `key in dict` |
| Copy | O(n) | Creates shallow copy |

### When to Use Dictionaries

**Ideal Use Cases:**
- **Mapping relationships** - Associate keys with values
- **Fast lookups** - Need O(1) access time
- **Counting/frequency** - Track occurrences
- **Caching/memoization** - Store computed results
- **Configuration data** - Key-value settings
- **Grouping data** - Organize by categories
- **Graph adjacency lists** - Represent connections

**Avoid When:**
- Need ordered sequence (use list instead)
- Keys are not hashable (use list of tuples)
- Need to store multiple values per key (use list/set as values)
- Memory is extremely constrained (dicts have overhead)

### Best Practices Checklist

**Design:**
- [ ] Use meaningful key names
- [ ] Ensure keys are immutable and hashable
- [ ] Consider using default values with `get()`
- [ ] Use `setdefault()` for conditional initialization
- [ ] Leverage dictionary comprehensions for transformations

**Performance:**
- [ ] Use `in` operator for membership testing
- [ ] Pre-allocate dictionaries when size is known
- [ ] Use `collections.defaultdict` for automatic initialization
- [ ] Use `collections.Counter` for counting operations
- [ ] Consider `dict.fromkeys()` for initialization

**Safety:**
- [ ] Handle missing keys gracefully
- [ ] Validate key types when necessary
- [ ] Use `copy()` or `deepcopy()` when needed
- [ ] Be careful with mutable values
- [ ] Consider using `collections.ChainMap` for layered configs

**Code Quality:**
- [ ] Use descriptive variable names
- [ ] Add type hints for better documentation
- [ ] Handle edge cases (empty dicts, None values)
- [ ] Use appropriate iteration methods
- [ ] Keep dictionary operations simple and readable

### Common Pitfalls to Avoid

1. **Modifying dict during iteration**: Create new dict or collect keys first
2. **Using mutable keys**: Lists, sets, and dicts cannot be keys
3. **KeyError for missing keys**: Use `get()` or `in` operator
4. **Shallow copy issues**: Use `copy.deepcopy()` for nested structures
5. **Performance assumptions**: Dict operations are average O(1), not guaranteed

### Advanced Patterns

**Dictionary as dispatch table:**
```python
operations = {
    'add': lambda x, y: x + y,
    'multiply': lambda x, y: x * y,
    'subtract': lambda x, y: x - y
}
result = operations[operation](a, b)
```

**Dictionary for state machines:**
```python
states = {
    'idle': {'start': 'running', 'quit': 'stopped'},
    'running': {'pause': 'paused', 'stop': 'idle'},
    'paused': {'resume': 'running', 'stop': 'idle'}
}
```

**Dictionary for caching with decorators:**
```python
def memoize(func):
    cache = {}
    def wrapper(*args):
        if args not in cache:
            cache[args] = func(*args)
        return cache[args]
    return wrapper
```

### Next Steps

After mastering dictionaries:
1. Learn about [Functions and Scope](./12-functions-scope.md)
2. Explore `collections` module (OrderedDict, defaultdict, Counter)
3. Study advanced hashing and hash table implementations
4. Practice with algorithm problems involving maps and lookups
5. Learn about JSON and data serialization

---

**Remember**: Dictionaries are one of Python's most powerful and versatile data structures. Master them to write efficient, readable code for data processing, algorithm implementation, and system design!
