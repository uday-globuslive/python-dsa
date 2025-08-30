# Data Types and Type Conversion

## 🎯 Objective
Master Python's built-in data types, understand type conversion mechanisms, and learn best practices for working with different data types in problem-solving scenarios.

## 📖 Overview

Python's type system is fundamental to effective programming and problem-solving. Understanding data types helps you choose the right tool for each task, optimize memory usage, and avoid common bugs. Python is dynamically typed but strongly typed, meaning variables can change types but operations between incompatible types require explicit conversion.

## 🔍 Python's Built-in Data Types

### Numeric Types

#### Integers (int)
```python
# Integer basics
age = 25
year = 2024
negative_number = -42

# Different integer representations
binary_num = 0b1010      # Binary: 10 in decimal
octal_num = 0o12         # Octal: 10 in decimal  
hex_num = 0xa            # Hexadecimal: 10 in decimal

print(f"Binary {binary_num}, Octal {octal_num}, Hex {hex_num}")

# Large integers (Python handles arbitrarily large integers)
large_number = 12345678901234567890123456789
factorial_100 = 1
for i in range(1, 101):
    factorial_100 *= i

print(f"100! = {factorial_100}")

# Integer operations
a, b = 17, 5
print(f"Division: {a / b}")         # 3.4 (float result)
print(f"Floor division: {a // b}")  # 3 (integer result)
print(f"Modulo: {a % b}")           # 2 (remainder)
print(f"Power: {a ** b}")           # 1419857 (17^5)
```

#### Floating Point Numbers (float)
```python
# Float basics
price = 19.99
temperature = -273.15
scientific = 1.5e-10  # 1.5 × 10^-10

# Float precision considerations
result = 0.1 + 0.2
print(f"0.1 + 0.2 = {result}")           # 0.30000000000000004
print(f"Is 0.1 + 0.2 == 0.3? {result == 0.3}")  # False!

# Proper float comparison
from math import isclose
print(f"Is close to 0.3? {isclose(result, 0.3)}")  # True

# Special float values
import math
positive_infinity = float('inf')
negative_infinity = float('-inf')
not_a_number = float('nan')

print(f"Infinity: {positive_infinity}")
print(f"Is infinite? {math.isinf(positive_infinity)}")
print(f"NaN: {not_a_number}")
print(f"Is NaN? {math.isnan(not_a_number)}")

# Float operations and precision
import decimal
# Using Decimal for precise financial calculations
price_decimal = decimal.Decimal('19.99')
tax_rate = decimal.Decimal('0.08')
total = price_decimal * (1 + tax_rate)
print(f"Precise total: {total}")  # Exact decimal arithmetic
```

#### Complex Numbers (complex)
```python
# Complex number basics
z1 = 3 + 4j
z2 = complex(2, -1)  # 2 - 1j
z3 = complex('5+2j')  # From string

print(f"z1 = {z1}")
print(f"Real part: {z1.real}, Imaginary part: {z1.imag}")

# Complex operations
z_sum = z1 + z2
z_product = z1 * z2
z_conjugate = z1.conjugate()

print(f"Sum: {z_sum}")
print(f"Product: {z_product}")
print(f"Conjugate of z1: {z_conjugate}")

# Magnitude and phase
import cmath
magnitude = abs(z1)
phase = cmath.phase(z1)
print(f"Magnitude: {magnitude}, Phase: {phase} radians")

# Practical use case: Signal processing
def dft_single_frequency(signal, frequency, sample_rate):
    """Calculate DFT for a single frequency."""
    N = len(signal)
    result = 0
    for n in range(N):
        angle = -2j * cmath.pi * frequency * n / sample_rate
        result += signal[n] * cmath.exp(angle)
    return result / N
```

### Text Type

#### Strings (str)
```python
# String creation methods
name = "Alice"
greeting = 'Hello, World!'
multiline = """This is a
multiline string
with several lines"""

raw_string = r"C:\Users\Alice\Documents"  # Raw string (no escape processing)
formatted = f"Hello, {name}!"             # f-string formatting

# String indexing and slicing
text = "Python Programming"
print(f"First character: {text[0]}")      # P
print(f"Last character: {text[-1]}")      # g
print(f"First 6 chars: {text[:6]}")       # Python
print(f"Last 11 chars: {text[7:]}")       # ogramming
print(f"Every 2nd char: {text[::2]}")     # Pto rgamn

# String methods for problem solving
email = "  user@example.com  "
password = "MySecretPassword123"

# Cleaning and validation
clean_email = email.strip().lower()
is_valid_email = "@" in clean_email and "." in clean_email.split("@")[1]

# Password strength checking
has_upper = any(c.isupper() for c in password)
has_lower = any(c.islower() for c in password)
has_digit = any(c.isdigit() for c in password)
has_special = any(not c.isalnum() for c in password)
is_long_enough = len(password) >= 8

print(f"Password strength: {sum([has_upper, has_lower, has_digit, has_special, is_long_enough])}/5")

# String manipulation for algorithms
def is_palindrome(s):
    """Check if string is palindrome (ignoring case and spaces)."""
    cleaned = ''.join(c.lower() for c in s if c.isalnum())
    return cleaned == cleaned[::-1]

def word_frequency(text):
    """Count word frequencies in text."""
    words = text.lower().split()
    frequency = {}
    for word in words:
        # Remove punctuation
        clean_word = ''.join(c for c in word if c.isalnum())
        if clean_word:
            frequency[clean_word] = frequency.get(clean_word, 0) + 1
    return frequency

# Advanced string operations
text = "The quick brown fox jumps over the lazy dog"
print(f"Palindrome check: {is_palindrome('A man a plan a canal Panama')}")
print(f"Word frequencies: {word_frequency(text)}")
```

### Boolean Type

#### Boolean (bool)
```python
# Boolean basics
is_active = True
is_complete = False
is_valid = bool(1)     # True
is_empty = bool(0)     # False

# Truthiness in Python
truthy_values = [True, 1, "hello", [1, 2], {"key": "value"}]
falsy_values = [False, 0, "", [], {}, None]

print("Truthy values:")
for value in truthy_values:
    print(f"{value} -> {bool(value)}")

print("\nFalsy values:")
for value in falsy_values:
    print(f"{value} -> {bool(value)}")

# Boolean operations
a, b = True, False
print(f"AND: {a and b}")      # False
print(f"OR: {a or b}")        # True  
print(f"NOT: {not a}")        # False
print(f"XOR: {a ^ b}")        # True (exclusive or)

# Short-circuit evaluation
def expensive_operation():
    print("Expensive operation called!")
    return True

# This won't call expensive_operation() because first condition is False
result = False and expensive_operation()
print(f"Result: {result}")

# This will call expensive_operation() because first condition is False
result = False or expensive_operation()
print(f"Result: {result}")

# Practical boolean usage in algorithms
def is_prime(n):
    """Check if number is prime."""
    if n < 2:
        return False
    
    # Check divisibility up to sqrt(n)
    for i in range(2, int(n ** 0.5) + 1):
        if n % i == 0:
            return False
    return True

def validate_input(data):
    """Validate user input with multiple conditions."""
    is_string = isinstance(data, str)
    is_not_empty = bool(data.strip()) if is_string else False
    is_reasonable_length = len(data) <= 100 if is_string else False
    
    return is_string and is_not_empty and is_reasonable_length

# Chained comparisons (returns boolean)
age = 25
is_adult = 18 <= age <= 65  # More readable than: age >= 18 and age <= 65
print(f"Is working age adult: {is_adult}")
```

## 🔄 Type Conversion and Casting

### Implicit Type Conversion (Coercion)

```python
# Python automatically converts types in mixed operations
integer_num = 10
float_num = 3.14

# int + float -> float
result = integer_num + float_num
print(f"10 + 3.14 = {result} (type: {type(result)})")

# Boolean arithmetic (True=1, False=0)
bool_sum = True + False + True  # 1 + 0 + 1 = 2
print(f"True + False + True = {bool_sum}")

# String repetition with integers
repeated = "Hello" * 3
print(f"'Hello' * 3 = {repeated}")

# Be aware of unexpected behaviors
unexpected = "5" + "3"  # String concatenation, not addition!
print(f"'5' + '3' = {unexpected}")  # "53", not 8
```

### Explicit Type Conversion (Casting)

```python
# String to numeric conversions
str_number = "42"
str_float = "3.14159"
str_invalid = "hello"

# Safe conversion with error handling
def safe_int(value, default=0):
    """Safely convert value to int with default fallback."""
    try:
        return int(value)
    except (ValueError, TypeError):
        return default

def safe_float(value, default=0.0):
    """Safely convert value to float with default fallback."""
    try:
        return float(value)
    except (ValueError, TypeError):
        return default

# Examples of conversions
print(f"String to int: {int(str_number)}")           # 42
print(f"String to float: {float(str_float)}")        # 3.14159
print(f"Float to int: {int(3.99)}")                  # 3 (truncation)
print(f"Safe conversion: {safe_int(str_invalid)}")   # 0 (default)

# Numeric to string conversions
number = 42
pi = 3.14159

string_number = str(number)
formatted_pi = f"{pi:.2f}"  # Format to 2 decimal places

print(f"Number as string: '{string_number}'")
print(f"Formatted pi: '{formatted_pi}'")

# Boolean conversions
print(f"int to bool: {bool(0)} and {bool(1)}")        # False and True
print(f"string to bool: {bool('')} and {bool('hi')}")  # False and True
print(f"list to bool: {bool([])} and {bool([1])}")     # False and True

# Advanced conversion patterns for problem solving
def parse_csv_line(line):
    """Parse CSV line with type conversion."""
    parts = line.strip().split(',')
    try:
        return {
            'name': parts[0].strip(),
            'age': int(parts[1].strip()),
            'salary': float(parts[2].strip()),
            'is_active': parts[3].strip().lower() == 'true'
        }
    except (ValueError, IndexError) as e:
        print(f"Error parsing line '{line}': {e}")
        return None

# Test CSV parsing
csv_data = "John Doe, 30, 50000.5, true"
parsed = parse_csv_line(csv_data)
print(f"Parsed data: {parsed}")
```

### Container Type Conversions

```python
# List, Tuple, Set conversions
numbers = [1, 2, 3, 2, 1]

# Convert between container types
list_to_tuple = tuple(numbers)          # (1, 2, 3, 2, 1)
list_to_set = set(numbers)              # {1, 2, 3} - removes duplicates
set_to_list = list(list_to_set)         # [1, 2, 3] - order may vary

print(f"Original list: {numbers}")
print(f"As tuple: {list_to_tuple}")
print(f"As set (unique): {list_to_set}")
print(f"Back to list: {set_to_list}")

# String to list conversions
text = "hello"
chars = list(text)                      # ['h', 'e', 'l', 'l', 'o']
words = "python is awesome".split()     # ['python', 'is', 'awesome']

# List to string conversions
char_string = ''.join(chars)            # "hello"
word_string = ' '.join(words)           # "python is awesome"

print(f"String to chars: {chars}")
print(f"Chars back to string: {char_string}")

# Dictionary conversions
pairs = [('a', 1), ('b', 2), ('c', 3)]
list_to_dict = dict(pairs)              # {'a': 1, 'b': 2, 'c': 3}
dict_to_list = list(list_to_dict.items())  # [('a', 1), ('b', 2), ('c', 3)]

print(f"Pairs to dict: {list_to_dict}")
print(f"Dict back to pairs: {dict_to_list}")

# Practical conversion example: Data cleaning
def clean_and_convert_data(raw_data):
    """Clean and convert mixed data types."""
    cleaned = []
    
    for item in raw_data:
        if isinstance(item, str):
            # Try to convert string to number
            item = item.strip()
            if item.isdigit():
                cleaned.append(int(item))
            elif item.replace('.', '').isdigit():
                cleaned.append(float(item))
            else:
                cleaned.append(item.lower())
        else:
            cleaned.append(item)
    
    return cleaned

# Test data cleaning
messy_data = ["  123  ", "45.67", "Hello", 89, "  WORLD  "]
clean_data = clean_and_convert_data(messy_data)
print(f"Original: {messy_data}")
print(f"Cleaned: {clean_data}")
```

## 🔍 Type Checking and Validation

### Runtime Type Checking

```python
# Using isinstance() for type checking
def process_input(data):
    """Process input based on its type."""
    if isinstance(data, int):
        return f"Integer: {data * 2}"
    elif isinstance(data, float):
        return f"Float: {data:.2f}"
    elif isinstance(data, str):
        return f"String: {data.upper()}"
    elif isinstance(data, list):
        return f"List with {len(data)} items"
    elif isinstance(data, dict):
        return f"Dict with keys: {list(data.keys())}"
    else:
        return f"Unknown type: {type(data)}"

# Test with different types
test_values = [42, 3.14, "hello", [1, 2, 3], {"key": "value"}, (1, 2)]
for value in test_values:
    print(process_input(value))

# Checking for multiple types
def handle_numeric(value):
    """Handle both int and float types."""
    if isinstance(value, (int, float)):
        return value ** 2
    else:
        raise TypeError(f"Expected numeric type, got {type(value)}")

# Type checking with inheritance
class Animal:
    pass

class Dog(Animal):
    def bark(self):
        return "Woof!"

class Cat(Animal):
    def meow(self):
        return "Meow!"

def pet_animal(animal):
    """Pet an animal if it's the right type."""
    if isinstance(animal, Animal):  # Works for subclasses too
        return f"Petting a {type(animal).__name__}"
    else:
        return "Not an animal!"

dog = Dog()
cat = Cat()
print(pet_animal(dog))  # Petting a Dog
print(pet_animal(cat))  # Petting a Cat
```

### Duck Typing and Protocol Checking

```python
# Duck typing: "If it walks like a duck and quacks like a duck, it's a duck"
def process_file_like(file_obj):
    """Process any object that behaves like a file."""
    if hasattr(file_obj, 'read') and hasattr(file_obj, 'write'):
        content = file_obj.read()
        file_obj.write("Processed: " + content)
        return True
    return False

# Custom class that acts like a file
class StringFile:
    def __init__(self, initial_content=""):
        self.content = initial_content
        self.position = 0
    
    def read(self):
        return self.content[self.position:]
    
    def write(self, data):
        self.content += data

# Works with our custom "file-like" object
fake_file = StringFile("Hello")
process_file_like(fake_file)
print(fake_file.content)  # "HelloProcessed: Hello"

# Checking for specific methods/attributes
def is_iterable(obj):
    """Check if object is iterable."""
    return hasattr(obj, '__iter__')

def is_callable(obj):
    """Check if object is callable."""
    return hasattr(obj, '__call__')

# Test iterability and callability
test_objects = [
    [1, 2, 3],          # List - iterable
    "hello",            # String - iterable  
    42,                 # Int - not iterable
    len,                # Function - callable
    lambda x: x * 2,    # Lambda - callable
]

for obj in test_objects:
    print(f"{obj}: iterable={is_iterable(obj)}, callable={is_callable(obj)}")
```

## 🧮 Practical Applications in Problem Solving

### Number System Conversions

```python
def convert_base(number, from_base, to_base):
    """Convert number from one base to another."""
    if from_base == 10:
        decimal = number
    else:
        # Convert from given base to decimal
        decimal = 0
        for i, digit in enumerate(str(number)[::-1]):
            decimal += int(digit) * (from_base ** i)
    
    if to_base == 10:
        return decimal
    
    # Convert decimal to target base
    if decimal == 0:
        return "0"
    
    digits = "0123456789ABCDEF"
    result = ""
    
    while decimal > 0:
        result = digits[decimal % to_base] + result
        decimal //= to_base
    
    return result

# Examples
print(f"Binary 1010 to decimal: {convert_base(1010, 2, 10)}")    # 10
print(f"Decimal 255 to hex: {convert_base(255, 10, 16)}")        # FF
print(f"Hex FF to binary: {convert_base(255, 10, 2)}")           # 11111111

# Built-in base conversion functions
number = 42
print(f"Decimal {number}:")
print(f"  Binary: {bin(number)}")    # 0b101010
print(f"  Octal: {oct(number)}")     # 0o52
print(f"  Hex: {hex(number)}")       # 0x2a
```

### Data Type Validation for Input Processing

```python
import re
from datetime import datetime

class InputValidator:
    """Comprehensive input validation with type conversion."""
    
    @staticmethod
    def validate_email(email):
        """Validate email format and return cleaned version."""
        if not isinstance(email, str):
            return None, "Email must be a string"
        
        email = email.strip().lower()
        pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
        
        if re.match(pattern, email):
            return email, None
        else:
            return None, "Invalid email format"
    
    @staticmethod
    def validate_phone(phone):
        """Validate and normalize phone number."""
        if not isinstance(phone, str):
            return None, "Phone must be a string"
        
        # Remove all non-digit characters
        digits = re.sub(r'\D', '', phone)
        
        if len(digits) == 10:
            # Format as (XXX) XXX-XXXX
            return f"({digits[:3]}) {digits[3:6]}-{digits[6:]}", None
        elif len(digits) == 11 and digits[0] == '1':
            # Handle country code
            return f"+1 ({digits[1:4]}) {digits[4:7]}-{digits[7:]}", None
        else:
            return None, "Invalid phone number format"
    
    @staticmethod
    def validate_date(date_str, format_str="%Y-%m-%d"):
        """Validate and parse date string."""
        if not isinstance(date_str, str):
            return None, "Date must be a string"
        
        try:
            parsed_date = datetime.strptime(date_str.strip(), format_str)
            return parsed_date, None
        except ValueError:
            return None, f"Invalid date format. Expected {format_str}"
    
    @staticmethod
    def validate_numeric_range(value, min_val=None, max_val=None, convert_type=float):
        """Validate numeric value within range."""
        try:
            converted = convert_type(value)
        except (ValueError, TypeError):
            return None, f"Cannot convert to {convert_type.__name__}"
        
        if min_val is not None and converted < min_val:
            return None, f"Value must be >= {min_val}"
        
        if max_val is not None and converted > max_val:
            return None, f"Value must be <= {max_val}"
        
        return converted, None

# Example usage
validator = InputValidator()

# Test email validation
test_emails = ["user@example.com", "  USER@EXAMPLE.COM  ", "invalid-email", 123]
for email in test_emails:
    result, error = validator.validate_email(email)
    print(f"Email '{email}': {result if result else error}")

# Test phone validation
test_phones = ["(555) 123-4567", "555-123-4567", "5551234567", "1-555-123-4567"]
for phone in test_phones:
    result, error = validator.validate_phone(phone)
    print(f"Phone '{phone}': {result if result else error}")

# Test numeric validation
test_numbers = ["25", "30.5", "abc", 40, -5]
for num in test_numbers:
    result, error = validator.validate_numeric_range(num, min_val=0, max_val=100)
    print(f"Number '{num}': {result if result else error}")
```

### Type-Based Algorithm Selection

```python
def smart_sort(data):
    """Sort data using appropriate algorithm based on type and characteristics."""
    
    if not isinstance(data, (list, tuple)):
        raise TypeError("Data must be a list or tuple")
    
    if len(data) <= 1:
        return list(data)
    
    # Determine data characteristics
    sample = data[0]
    is_numeric = isinstance(sample, (int, float))
    is_string = isinstance(sample, str)
    is_small_dataset = len(data) < 50
    
    # Type-based sorting strategy
    if is_numeric:
        if is_small_dataset:
            # Use insertion sort for small numeric datasets
            return insertion_sort(list(data))
        else:
            # Use built-in sort (Timsort) for larger datasets
            return sorted(data)
    
    elif is_string:
        if all(len(s) <= 10 for s in data):
            # Short strings - use built-in sort
            return sorted(data)
        else:
            # Long strings - custom comparison
            return sorted(data, key=lambda x: (len(x), x.lower()))
    
    else:
        # Mixed or custom types - use default comparison
        try:
            return sorted(data)
        except TypeError:
            # If items aren't comparable, sort by string representation
            return sorted(data, key=str)

def insertion_sort(arr):
    """Simple insertion sort for small datasets."""
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1
        while j >= 0 and arr[j] > key:
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = key
    return arr

# Test with different data types
test_datasets = [
    [3, 1, 4, 1, 5, 9, 2, 6],                    # Small numeric
    list(range(100, 0, -1)),                      # Large numeric
    ["banana", "apple", "cherry"],                # Short strings
    ["very long string here", "short", "medium length string"],  # Long strings
    [3, "hello", 1.5, "world"]                   # Mixed types
]

for i, dataset in enumerate(test_datasets):
    print(f"Dataset {i + 1}: {dataset[:5]}{'...' if len(dataset) > 5 else ''}")
    sorted_data = smart_sort(dataset)
    print(f"Sorted: {sorted_data[:5]}{'...' if len(sorted_data) > 5 else ''}\n")
```

## ⚠️ Common Type-Related Pitfalls

### Pitfall 1: Mutable Default Arguments

```python
# Bad: Mutable default argument
def add_item_bad(item, target_list=[]):  # DON'T DO THIS!
    target_list.append(item)
    return target_list

# This causes unexpected behavior
list1 = add_item_bad("first")
list2 = add_item_bad("second")  
print(f"List 1: {list1}")  # ['first', 'second'] - unexpected!
print(f"List 2: {list2}")  # ['first', 'second'] - same list!

# Good: Use None and create new list inside function
def add_item_good(item, target_list=None):
    if target_list is None:
        target_list = []
    target_list.append(item)
    return target_list

# This works correctly
list3 = add_item_good("third")
list4 = add_item_good("fourth")
print(f"List 3: {list3}")  # ['third']
print(f"List 4: {list4}")  # ['fourth']
```

### Pitfall 2: Integer Division vs Float Division

```python
# Python 3 behavior (different from Python 2)
print(f"5 / 2 = {5 / 2}")    # 2.5 (float division)
print(f"5 // 2 = {5 // 2}")  # 2 (floor division)

# Be careful with floor division and negative numbers
print(f"-5 // 2 = {-5 // 2}")  # -3 (not -2!)
print(f"-5 / 2 = {-5 / 2}")    # -2.5

# For true truncation towards zero, use int()
def truncate_division(a, b):
    return int(a / b)

print(f"Truncated -5/2 = {truncate_division(-5, 2)}")  # -2
```

### Pitfall 3: String Immutability

```python
# Strings are immutable - modifying creates new objects
text = "hello"
original_id = id(text)

# This creates a new string object
text = text.upper()
new_id = id(text)

print(f"Original ID: {original_id}")
print(f"New ID: {new_id}")
print(f"Same object? {original_id == new_id}")  # False

# Inefficient string concatenation
def build_string_inefficient(words):
    result = ""
    for word in words:
        result += word + " "  # Creates new string each time!
    return result.strip()

# Efficient string concatenation
def build_string_efficient(words):
    return " ".join(words)  # Much faster for many strings

# Performance comparison
import time
words = ["word"] * 1000

start = time.time()
result1 = build_string_inefficient(words)
time1 = time.time() - start

start = time.time()
result2 = build_string_efficient(words)
time2 = time.time() - start

print(f"Inefficient method: {time1:.4f} seconds")
print(f"Efficient method: {time2:.4f} seconds")
print(f"Speedup: {time1/time2:.1f}x faster")
```

## 🎯 Practice Exercises

### Exercise 1: Type Converter Utility

```python
def universal_converter(value, target_type):
    """
    Convert value to target_type with intelligent handling.
    
    Args:
        value: Value to convert
        target_type: Target type ('int', 'float', 'str', 'bool', 'list')
    
    Returns:
        Converted value or None if conversion impossible
    """
    # Implement this function
    pass

# Test cases
test_cases = [
    ("123", "int"),
    ("3.14", "float"),
    (42, "str"),
    ("true", "bool"),
    ("1,2,3", "list"),
    ([1, 2, 3], "str"),
]

# Your implementation here
```

### Exercise 2: Data Type Analyzer

```python
def analyze_data_types(data_list):
    """
    Analyze a list of mixed data types and provide statistics.
    
    Returns:
        Dictionary with type counts, conversion possibilities, etc.
    """
    # Implement comprehensive analysis
    pass

# Test with mixed data
mixed_data = [1, "2", 3.0, "hello", True, [1, 2], {"key": "value"}, None]
analysis = analyze_data_types(mixed_data)
print(analysis)
```

### Exercise 3: Smart Calculator

```python
class SmartCalculator:
    """Calculator that handles multiple data types intelligently."""
    
    def add(self, a, b):
        """Add two values, handling different types appropriately."""
        pass
    
    def multiply(self, a, b):
        """Multiply two values, handling different types."""
        pass
    
    def calculate(self, expression):
        """Parse and calculate string expressions."""
        pass

# Example usage:
# calc = SmartCalculator()
# calc.add(5, "3")        # Should return 8
# calc.multiply("hello", 3)  # Should return "hellohellohello"
# calc.calculate("5 + 3 * 2")  # Should return 11
```

## 📚 Summary and Best Practices

### Key Takeaways
1. **Understand Python's type system**: Dynamically typed but strongly typed
2. **Use appropriate types for tasks**: Choose the right tool for the job
3. **Handle type conversions safely**: Always validate before converting
4. **Leverage duck typing**: Focus on behavior, not just type
5. **Be aware of type-related pitfalls**: Mutable defaults, float precision, etc.

### Best Practices Checklist
- [ ] Use `isinstance()` instead of `type()` for type checking
- [ ] Handle type conversion errors with try/except
- [ ] Understand the difference between `==` and `is`
- [ ] Use appropriate numeric types for precision requirements
- [ ] Validate user input and convert to appropriate types
- [ ] Be aware of truthiness and falsiness in Python
- [ ] Use type hints to document expected types

### Next Steps
After mastering data types and conversion:
1. Learn about [Basic Operators](./06-basic-operators.md)
2. Practice type-safe programming patterns
3. Explore advanced typing features (typing module)
4. Study type-related performance implications

---

**Remember**: Understanding data types is fundamental to writing robust, efficient Python code. Proper type handling prevents bugs, improves performance, and makes your code more maintainable!
