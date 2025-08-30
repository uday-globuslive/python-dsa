# Functions and Scope

## 🎯 Objective
Master Python functions - the building blocks of modular, reusable code - including function definition, parameters, return values, scope rules, and advanced functional programming concepts essential for problem-solving and algorithm implementation.

## 📖 Overview

Functions are fundamental to writing clean, maintainable, and efficient Python code. They enable code reuse, improve readability, and facilitate testing and debugging. Understanding functions thoroughly - including parameter passing, scope rules, and advanced concepts like closures and decorators - is crucial for effective programming and algorithm implementation.

## 📝 Function Basics and Definition

### Basic Function Structure

```python
# Basic function definition
def greet(name):
    """
    A simple greeting function.
    
    Args:
        name (str): The name to greet
    
    Returns:
        str: A greeting message
    """
    return f"Hello, {name}!"

# Function with multiple parameters
def add_numbers(a, b):
    """Add two numbers and return the result."""
    return a + b

# Function with no parameters
def get_current_time():
    """Get current timestamp."""
    import time
    return time.time()

# Function with no return value (returns None implicitly)
def print_separator():
    """Print a line separator."""
    print("-" * 50)

# Function with multiple return values
def get_min_max(numbers):
    """
    Find minimum and maximum values in a list.
    
    Args:
        numbers (list): List of numbers
    
    Returns:
        tuple: (minimum, maximum) values
    """
    if not numbers:
        return None, None
    return min(numbers), max(numbers)

# Test basic functions
print("=== Basic Functions ===")
greeting = greet("Alice")
print(greeting)

sum_result = add_numbers(5, 3)
print(f"5 + 3 = {sum_result}")

timestamp = get_current_time()
print(f"Current time: {timestamp}")

print_separator()

numbers = [1, 5, 3, 9, 2, 7]
min_val, max_val = get_min_max(numbers)
print(f"Min: {min_val}, Max: {max_val}")

# Function with docstring best practices
def calculate_area(length, width):
    """
    Calculate the area of a rectangle.
    
    This function multiplies length by width to compute the area.
    Both parameters must be positive numbers.
    
    Args:
        length (float): The length of the rectangle
        width (float): The width of the rectangle
    
    Returns:
        float: The area of the rectangle
    
    Raises:
        ValueError: If length or width is negative
        TypeError: If length or width is not a number
    
    Examples:
        >>> calculate_area(5, 3)
        15
        >>> calculate_area(2.5, 4.0)
        10.0
    """
    # Input validation
    if not isinstance(length, (int, float)) or not isinstance(width, (int, float)):
        raise TypeError("Length and width must be numbers")
    
    if length < 0 or width < 0:
        raise ValueError("Length and width must be positive")
    
    return length * width

# Test with validation
try:
    area = calculate_area(5, 3)
    print(f"Area: {area}")
    
    # This will raise an error
    area = calculate_area(-5, 3)
except ValueError as e:
    print(f"Error: {e}")
```

### Parameter Types and Default Values

```python
# Default parameters
def greet_with_title(name, title="Mr./Ms."):
    """Greet someone with an optional title."""
    return f"Hello, {title} {name}!"

# Multiple default parameters
def create_user_profile(name, age=None, city="Unknown", active=True):
    """Create a user profile with optional information."""
    profile = {
        "name": name,
        "age": age,
        "city": city,
        "active": active
    }
    return profile

# Variable-length arguments (*args)
def sum_all(*numbers):
    """Sum any number of arguments."""
    return sum(numbers)

def print_items(*items):
    """Print all items with numbering."""
    for i, item in enumerate(items, 1):
        print(f"{i}. {item}")

# Keyword arguments (**kwargs)
def create_config(**settings):
    """Create configuration from keyword arguments."""
    config = {}
    for key, value in settings.items():
        config[key] = value
    return config

# Mixed parameter types
def process_data(data, *transformations, **options):
    """
    Process data with transformations and options.
    
    Args:
        data: The data to process
        *transformations: Functions to apply to data
        **options: Processing options
    """
    result = data
    
    # Apply transformations
    for transform in transformations:
        result = transform(result)
    
    # Apply options
    if options.get("reverse", False):
        if hasattr(result, "__reversed__"):
            result = list(reversed(result))
    
    if options.get("sort", False):
        if hasattr(result, "sort"):
            result = sorted(result)
    
    return result

# Test parameter types
print("\n=== Parameter Types ===")

# Default parameters
print(greet_with_title("Alice"))
print(greet_with_title("Bob", "Dr."))

# User profiles
profile1 = create_user_profile("Charlie")
profile2 = create_user_profile("Diana", age=25, city="NYC")
print(f"Profile 1: {profile1}")
print(f"Profile 2: {profile2}")

# Variable arguments
total = sum_all(1, 2, 3, 4, 5)
print(f"Sum: {total}")

print("Items:")
print_items("apple", "banana", "cherry")

# Keyword arguments
config = create_config(debug=True, max_connections=100, timeout=30)
print(f"Config: {config}")

# Mixed parameters
def double(x):
    return x * 2

def add_one(x):
    return x + 1

numbers = [1, 2, 3, 4, 5]
result = process_data(numbers, double, add_one, reverse=True, sort=False)
print(f"Processed data: {result}")

# Keyword-only arguments (Python 3+)
def analyze_text(text, *, case_sensitive=False, remove_punctuation=True):
    """
    Analyze text with keyword-only options.
    
    Args:
        text (str): Text to analyze
        case_sensitive (bool): Whether to consider case
        remove_punctuation (bool): Whether to remove punctuation
    """
    if not case_sensitive:
        text = text.lower()
    
    if remove_punctuation:
        import string
        text = text.translate(str.maketrans("", "", string.punctuation))
    
    words = text.split()
    return {
        "word_count": len(words),
        "unique_words": len(set(words)),
        "words": words
    }

# Test keyword-only arguments
sample_text = "Hello, World! This is a Test."
analysis = analyze_text(sample_text, case_sensitive=False, remove_punctuation=True)
print(f"Text analysis: {analysis}")

# Positional-only arguments (Python 3.8+)
def calculate_bmi(weight, height, /):
    """
    Calculate BMI using positional-only arguments.
    
    Args:
        weight: Weight in kg (positional-only)
        height: Height in meters (positional-only)
    """
    return weight / (height ** 2)

# This works
bmi = calculate_bmi(70, 1.75)
print(f"BMI: {bmi:.2f}")

# This would cause an error (trying to use as keyword arguments):
# bmi = calculate_bmi(weight=70, height=1.75)  # TypeError
```

## 🔍 Scope and Namespaces

### Local and Global Scope

```python
# Global variables
global_counter = 0
global_config = {"debug": False, "version": "1.0"}

def demonstrate_local_scope():
    """Demonstrate local variable scope."""
    # Local variables
    local_var = "I'm local"
    local_counter = 10
    
    print(f"Local variable: {local_var}")
    print(f"Local counter: {local_counter}")
    print(f"Global counter (read): {global_counter}")
    
    # This creates a NEW local variable, doesn't modify global
    global_counter = 5  # This is actually a local variable!
    print(f"Local 'global_counter': {global_counter}")

def modify_global_scope():
    """Demonstrate modifying global variables."""
    global global_counter  # Declare intent to modify global
    
    global_counter += 1
    print(f"Modified global counter: {global_counter}")
    
    # Modifying mutable global objects
    global_config["debug"] = True
    global_config["users"] = []

def demonstrate_variable_shadowing():
    """Show how local variables can shadow global ones."""
    global_config = "I'm shadowing the global!"  # Local variable
    print(f"Shadowed config: {global_config}")
    print(f"Global config (via globals()): {globals()['global_config']}")

# Test scope demonstrations
print("=== Scope Demonstrations ===")
print(f"Initial global counter: {global_counter}")

demonstrate_local_scope()
print(f"Global counter after local demo: {global_counter}")  # Still 0

modify_global_scope()
print(f"Global counter after modification: {global_counter}")  # Now 1

demonstrate_variable_shadowing()
print(f"Global config after shadowing: {global_config}")

# Nonlocal scope (nested functions)
def outer_function(x):
    """Demonstrate nonlocal scope with nested functions."""
    
    def inner_function():
        nonlocal x  # Refer to the enclosing scope's x
        x += 10
        print(f"Inner function - x: {x}")
    
    def another_inner():
        # This creates a new local x, doesn't modify outer x
        x = 100
        print(f"Another inner - local x: {x}")
    
    print(f"Outer function - initial x: {x}")
    inner_function()
    print(f"Outer function - after inner: {x}")
    another_inner()
    print(f"Outer function - after another inner: {x}")
    
    return x

# Test nonlocal scope
print("\n=== Nonlocal Scope ===")
result = outer_function(5)
print(f"Final result: {result}")

# Scope resolution order: LEGB Rule
# Local -> Enclosing -> Global -> Built-in

def demonstrate_legb():
    """Demonstrate LEGB scope resolution."""
    
    # Built-in: len, max, min, etc.
    
    # Global level
    global_var = "global"
    
    def enclosing_function():
        # Enclosing level
        enclosing_var = "enclosing"
        
        def local_function():
            # Local level
            local_var = "local"
            
            # Python looks for variables in LEGB order
            print(f"Local: {local_var}")
            print(f"Enclosing: {enclosing_var}")
            print(f"Global: {global_var}")
            print(f"Built-in len function: {len}")
            
            # You can explicitly access different scopes
            print(f"Locals: {locals()}")
            # print(f"Globals: {list(globals().keys())[:5]}...")  # Too long to print all
        
        local_function()
    
    enclosing_function()

print("\n=== LEGB Rule ===")
demonstrate_legb()

# Practical scope example: Configuration management
class ConfigManager:
    """Example of scope management in a class context."""
    
    default_config = {"timeout": 30, "retries": 3}  # Class variable (global to methods)
    
    def __init__(self, custom_config=None):
        """Initialize with custom configuration."""
        self.config = self.default_config.copy()  # Instance variable (local to instance)
        if custom_config:
            self.config.update(custom_config)
    
    def get_setting(self, key, default=None):
        """Get a setting with fallback to default."""
        # Local variable
        value = self.config.get(key)
        
        if value is None:
            # Fallback to class default
            value = self.default_config.get(key, default)
        
        return value
    
    def update_setting(self, key, value):
        """Update a setting."""
        self.config[key] = value
    
    def reset_to_defaults(self):
        """Reset to default configuration."""
        self.config = self.default_config.copy()

# Test configuration manager
print("\n=== Configuration Manager ===")
config_mgr = ConfigManager({"timeout": 60, "debug": True})
print(f"Custom timeout: {config_mgr.get_setting('timeout')}")
print(f"Default retries: {config_mgr.get_setting('retries')}")
print(f"Debug setting: {config_mgr.get_setting('debug')}")
```

### Variable Lifetime and Memory Management

```python
def demonstrate_variable_lifetime():
    """Show how variable lifetime works."""
    
    def create_large_data():
        # Local variables are created when function is called
        large_list = list(range(1000000))  # This takes memory
        print(f"Created large list with {len(large_list)} elements")
        return len(large_list)
        # large_list is automatically garbage collected when function ends
    
    def function_with_reference():
        data = [1, 2, 3, 4, 5]
        
        def inner_function():
            # This creates a closure - data lives on even after function_with_reference ends
            return data
        
        return inner_function
    
    # Test variable lifetime
    size = create_large_data()
    print(f"Returned size: {size}")
    # large_list is gone now, memory is freed
    
    # Test closure
    closure_func = function_with_reference()
    # data is still alive because inner_function references it
    print(f"Data from closure: {closure_func()}")

# Memory management example
import gc  # Garbage collector

def memory_management_example():
    """Demonstrate memory management concepts."""
    
    class Node:
        def __init__(self, value):
            self.value = value
            self.references = []
        
        def add_reference(self, node):
            self.references.append(node)
        
        def __del__(self):
            print(f"Node {self.value} is being deleted")
    
    # Create nodes
    node1 = Node(1)
    node2 = Node(2)
    node3 = Node(3)
    
    # Create references
    node1.add_reference(node2)
    node2.add_reference(node3)
    node3.add_reference(node1)  # Circular reference!
    
    # Remove our references
    del node1, node2, node3
    
    # Force garbage collection
    print("Before garbage collection:")
    collected = gc.collect()
    print(f"Garbage collected {collected} objects")

print("\n=== Variable Lifetime ===")
demonstrate_variable_lifetime()

print("\n=== Memory Management ===")
memory_management_example()
```

## 🔧 Advanced Function Concepts

### Higher-Order Functions

```python
# Functions that take other functions as arguments
def apply_operation(numbers, operation):
    """Apply an operation to all numbers in a list."""
    return [operation(num) for num in numbers]

def filter_numbers(numbers, condition):
    """Filter numbers based on a condition function."""
    return [num for num in numbers if condition(num)]

def reduce_numbers(numbers, reducer, initial=0):
    """Reduce numbers using a reducer function."""
    result = initial
    for num in numbers:
        result = reducer(result, num)
    return result

# Functions that return other functions
def create_multiplier(factor):
    """Create a function that multiplies by a factor."""
    def multiplier(x):
        return x * factor
    return multiplier

def create_validator(min_val, max_val):
    """Create a validation function for a range."""
    def validator(value):
        return min_val <= value <= max_val
    return validator

def create_counter():
    """Create a counter function with internal state."""
    count = 0
    
    def counter():
        nonlocal count
        count += 1
        return count
    
    # Add methods to the function object
    counter.reset = lambda: exec('nonlocal count; count = 0')
    counter.get_count = lambda: count
    
    return counter

# Test higher-order functions
print("=== Higher-Order Functions ===")

numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Apply operations
squared = apply_operation(numbers, lambda x: x**2)
doubled = apply_operation(numbers, lambda x: x * 2)
print(f"Squared: {squared}")
print(f"Doubled: {doubled}")

# Filter numbers
evens = filter_numbers(numbers, lambda x: x % 2 == 0)
large_numbers = filter_numbers(numbers, lambda x: x > 5)
print(f"Even numbers: {evens}")
print(f"Large numbers: {large_numbers}")

# Reduce numbers
total = reduce_numbers(numbers, lambda acc, x: acc + x, 0)
product = reduce_numbers(numbers, lambda acc, x: acc * x, 1)
print(f"Sum: {total}")
print(f"Product: {product}")

# Function factories
multiply_by_3 = create_multiplier(3)
multiply_by_10 = create_multiplier(10)

print(f"3 * 5 = {multiply_by_3(5)}")
print(f"10 * 5 = {multiply_by_10(5)}")

# Validators
age_validator = create_validator(0, 120)
grade_validator = create_validator(0, 100)

print(f"Age 25 valid: {age_validator(25)}")
print(f"Age 150 valid: {age_validator(150)}")
print(f"Grade 85 valid: {grade_validator(85)}")
print(f"Grade 105 valid: {grade_validator(105)}")

# Counter with state
counter1 = create_counter()
counter2 = create_counter()

print(f"Counter1: {counter1()}, {counter1()}, {counter1()}")
print(f"Counter2: {counter2()}, {counter2()}")
print(f"Counter1 current count: {counter1.get_count()}")

# Function composition
def compose(f, g):
    """Compose two functions: f(g(x))."""
    def composed(x):
        return f(g(x))
    return composed

def add_one(x):
    return x + 1

def square(x):
    return x * x

# Compose functions
add_then_square = compose(square, add_one)
square_then_add = compose(add_one, square)

print(f"(5 + 1)² = {add_then_square(5)}")
print(f"5² + 1 = {square_then_add(5)}")
```

### Decorators

```python
# Basic decorator concept
def simple_decorator(func):
    """A simple decorator that prints before and after function execution."""
    def wrapper(*args, **kwargs):
        print(f"Before calling {func.__name__}")
        result = func(*args, **kwargs)
        print(f"After calling {func.__name__}")
        return result
    return wrapper

# Decorator with arguments
def timing_decorator(unit="seconds"):
    """Decorator that measures execution time."""
    import time
    
    def decorator(func):
        def wrapper(*args, **kwargs):
            start_time = time.time()
            result = func(*args, **kwargs)
            end_time = time.time()
            
            execution_time = end_time - start_time
            if unit == "milliseconds":
                execution_time *= 1000
                print(f"{func.__name__} took {execution_time:.2f} ms")
            else:
                print(f"{func.__name__} took {execution_time:.4f} seconds")
            
            return result
        return wrapper
    return decorator

# Class-based decorator
class CountCalls:
    """Decorator that counts function calls."""
    
    def __init__(self, func):
        self.func = func
        self.count = 0
    
    def __call__(self, *args, **kwargs):
        self.count += 1
        print(f"{self.func.__name__} has been called {self.count} times")
        return self.func(*args, **kwargs)

# Multiple decorators
def validate_positive(func):
    """Decorator that validates all arguments are positive."""
    def wrapper(*args, **kwargs):
        for arg in args:
            if isinstance(arg, (int, float)) and arg < 0:
                raise ValueError(f"Argument {arg} must be positive")
        return func(*args, **kwargs)
    return wrapper

def memoize(func):
    """Decorator that caches function results."""
    cache = {}
    
    def wrapper(*args, **kwargs):
        # Create a key from arguments
        key = str(args) + str(sorted(kwargs.items()))
        
        if key not in cache:
            cache[key] = func(*args, **kwargs)
            print(f"Computed {func.__name__}{args}: {cache[key]}")
        else:
            print(f"Cache hit for {func.__name__}{args}: {cache[key]}")
        
        return cache[key]
    
    wrapper.cache = cache  # Expose cache for inspection
    wrapper.cache_clear = lambda: cache.clear()
    return wrapper

# Apply decorators
@simple_decorator
def greet(name):
    """A simple greeting function."""
    return f"Hello, {name}!"

@timing_decorator("milliseconds")
def slow_function():
    """A function that takes some time."""
    import time
    time.sleep(0.1)  # Sleep for 100ms
    return "Done!"

@CountCalls
def say_hello():
    """Function to demonstrate call counting."""
    return "Hello!"

@validate_positive
@memoize
def fibonacci(n):
    """Calculate fibonacci number with memoization and validation."""
    if n <= 1:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)

@timing_decorator()
@validate_positive
def factorial(n):
    """Calculate factorial with validation and timing."""
    if n <= 1:
        return 1
    return n * factorial(n - 1)

# Test decorators
print("\n=== Decorators ===")

# Simple decorator
message = greet("Alice")
print(f"Result: {message}")

# Timing decorator
result = slow_function()
print(f"Slow function result: {result}")

# Call counting
print(say_hello())
print(say_hello())
print(say_hello())

# Memoization
print(f"Fibonacci(10): {fibonacci(10)}")
print(f"Fibonacci(8): {fibonacci(8)}")  # Should use cache

# Multiple decorators
try:
    print(f"Factorial(5): {factorial(5)}")
    print(f"Factorial(-3): {factorial(-3)}")  # Should raise error
except ValueError as e:
    print(f"Error: {e}")

# Preserve function metadata
import functools

def better_decorator(func):
    """A decorator that preserves function metadata."""
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        print(f"Calling {func.__name__}")
        return func(*args, **kwargs)
    return wrapper

@better_decorator
def documented_function():
    """This function has documentation."""
    return "I have preserved metadata!"

print(f"\nFunction name: {documented_function.__name__}")
print(f"Function doc: {documented_function.__doc__}")

# Decorator factory for retry logic
def retry(max_attempts=3, delay=1):
    """Decorator that retries a function on failure."""
    import time
    
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            last_exception = None
            
            for attempt in range(max_attempts):
                try:
                    return func(*args, **kwargs)
                except Exception as e:
                    last_exception = e
                    print(f"Attempt {attempt + 1} failed: {e}")
                    if attempt < max_attempts - 1:
                        time.sleep(delay)
            
            raise last_exception
        return wrapper
    return decorator

@retry(max_attempts=3, delay=0.1)
def unreliable_function():
    """Function that fails randomly."""
    import random
    if random.random() < 0.7:  # 70% chance of failure
        raise Exception("Random failure!")
    return "Success!"

# Test retry decorator
try:
    result = unreliable_function()
    print(f"Unreliable function result: {result}")
except Exception as e:
    print(f"Final failure: {e}")
```

### Lambda Functions and Functional Programming

```python
# Basic lambda functions
add = lambda x, y: x + y
square = lambda x: x ** 2
is_even = lambda x: x % 2 == 0

print("=== Lambda Functions ===")
print(f"Add: {add(5, 3)}")
print(f"Square: {square(4)}")
print(f"Is even: {is_even(7)}")

# Lambda with built-in functions
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# map() - apply function to each element
squared_numbers = list(map(lambda x: x**2, numbers))
doubled_numbers = list(map(lambda x: x * 2, numbers))

print(f"Original: {numbers}")
print(f"Squared: {squared_numbers}")
print(f"Doubled: {doubled_numbers}")

# filter() - keep elements that match condition
even_numbers = list(filter(lambda x: x % 2 == 0, numbers))
large_numbers = list(filter(lambda x: x > 5, numbers))

print(f"Even numbers: {even_numbers}")
print(f"Large numbers: {large_numbers}")

# reduce() - combine elements into single value
from functools import reduce

sum_all = reduce(lambda acc, x: acc + x, numbers, 0)
product_all = reduce(lambda acc, x: acc * x, numbers, 1)
max_value = reduce(lambda acc, x: x if x > acc else acc, numbers)

print(f"Sum: {sum_all}")
print(f"Product: {product_all}")
print(f"Max: {max_value}")

# Complex data processing with lambdas
students = [
    {"name": "Alice", "grade": 85, "age": 20},
    {"name": "Bob", "grade": 92, "age": 19},
    {"name": "Charlie", "grade": 78, "age": 21},
    {"name": "Diana", "grade": 95, "age": 20}
]

# Sort by different criteria
by_grade = sorted(students, key=lambda s: s["grade"], reverse=True)
by_age = sorted(students, key=lambda s: s["age"])
by_name = sorted(students, key=lambda s: s["name"])

print(f"\nSorted by grade: {[s['name'] for s in by_grade]}")
print(f"Sorted by age: {[s['name'] for s in by_age]}")
print(f"Sorted by name: {[s['name'] for s in by_name]}")

# Filter students
high_achievers = list(filter(lambda s: s["grade"] >= 90, students))
young_students = list(filter(lambda s: s["age"] < 21, students))

print(f"High achievers: {[s['name'] for s in high_achievers]}")
print(f"Young students: {[s['name'] for s in young_students]}")

# Transform data
grade_summary = list(map(lambda s: f"{s['name']}: {s['grade']}", students))
initials = list(map(lambda s: s['name'][0], students))

print(f"Grade summary: {grade_summary}")
print(f"Initials: {initials}")

# Functional programming patterns
def curry(func):
    """Convert a function to curried form."""
    def curried(*args, **kwargs):
        if len(args) + len(kwargs) >= func.__code__.co_argcount:
            return func(*args, **kwargs)
        return lambda *more_args, **more_kwargs: curried(*(args + more_args), **{**kwargs, **more_kwargs})
    return curried

@curry
def add_three_numbers(a, b, c):
    """Add three numbers."""
    return a + b + c

# Test currying
print("\n=== Currying ===")
add_5_and_3 = add_three_numbers(5)(3)  # Partially applied
result = add_5_and_3(2)  # Complete application
print(f"Curried result: {result}")

# Or apply all at once
result2 = add_three_numbers(1, 2, 3)
print(f"Direct result: {result2}")

# Partial application using functools
from functools import partial

def multiply(x, y, z):
    """Multiply three numbers."""
    return x * y * z

# Create partially applied functions
double = partial(multiply, 2)  # Fix first argument to 2
triple_double = partial(double, 3)  # Fix second argument to 3

print(f"Double 5: {double(5, 1)}")  # 2 * 5 * 1 = 10
print(f"Triple double 4: {triple_double(4)}")  # 2 * 3 * 4 = 24

# Function composition with lambdas
def compose_funcs(*funcs):
    """Compose multiple functions."""
    return reduce(lambda f, g: lambda x: f(g(x)), funcs)

# Create a pipeline
pipeline = compose_funcs(
    lambda x: x * 2,    # Double
    lambda x: x + 1,    # Add one
    lambda x: x ** 2    # Square
)

result = pipeline(3)  # ((3^2) + 1) * 2 = (9 + 1) * 2 = 20
print(f"Pipeline result: {result}")

# Advanced lambda usage with data structures
data = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Flatten 2D list
flattened = reduce(lambda acc, row: acc + row, data, [])
print(f"Flattened: {flattened}")

# Transpose matrix
transposed = list(map(list, zip(*data)))
print(f"Transposed: {transposed}")

# Find matrix maximum
matrix_max = reduce(lambda acc, row: max(acc, max(row)), data, float('-inf'))
print(f"Matrix max: {matrix_max}")

# Complex lambda with conditional logic
process_number = lambda x: x**2 if x > 0 else abs(x) if x < 0 else 1

test_numbers = [-3, 0, 4, -1, 5]
processed = list(map(process_number, test_numbers))
print(f"Processed numbers: {processed}")

# Lambda for event handling simulation
events = [
    {"type": "click", "x": 10, "y": 20},
    {"type": "keypress", "key": "a"},
    {"type": "click", "x": 30, "y": 40},
    {"type": "scroll", "delta": 5}
]

# Process events with lambdas
click_events = list(filter(lambda e: e["type"] == "click", events))
click_positions = list(map(lambda e: (e["x"], e["y"]), click_events))

print(f"Click events: {len(click_events)}")
print(f"Click positions: {click_positions}")

# Group events by type
from itertools import groupby
sorted_events = sorted(events, key=lambda e: e["type"])
grouped_events = {k: list(v) for k, v in groupby(sorted_events, key=lambda e: e["type"])}

print(f"Grouped events: {grouped_events}")
```

## 🎯 Practical Function Applications

### Algorithm Implementation with Functions

```python
# Sorting algorithms implemented as functions
def bubble_sort(arr):
    """
    Bubble sort implementation.
    
    Time Complexity: O(n²)
    Space Complexity: O(1)
    """
    n = len(arr)
    arr = arr.copy()  # Don't modify original
    
    for i in range(n):
        swapped = False
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True
        
        if not swapped:  # Array is sorted
            break
    
    return arr

def quick_sort(arr):
    """
    Quick sort implementation.
    
    Time Complexity: O(n log n) average, O(n²) worst
    Space Complexity: O(log n)
    """
    if len(arr) <= 1:
        return arr
    
    pivot = arr[len(arr) // 2]
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]
    
    return quick_sort(left) + middle + quick_sort(right)

def merge_sort(arr):
    """
    Merge sort implementation.
    
    Time Complexity: O(n log n)
    Space Complexity: O(n)
    """
    if len(arr) <= 1:
        return arr
    
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])
    
    return merge(left, right)

def merge(left, right):
    """Helper function for merge sort."""
    result = []
    i = j = 0
    
    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1
    
    result.extend(left[i:])
    result.extend(right[j:])
    return result

# Test sorting algorithms
print("=== Sorting Algorithms ===")
test_array = [64, 34, 25, 12, 22, 11, 90]
print(f"Original: {test_array}")
print(f"Bubble sort: {bubble_sort(test_array)}")
print(f"Quick sort: {quick_sort(test_array)}")
print(f"Merge sort: {merge_sort(test_array)}")

# Search algorithms
def linear_search(arr, target):
    """
    Linear search implementation.
    
    Time Complexity: O(n)
    Space Complexity: O(1)
    """
    for i, value in enumerate(arr):
        if value == target:
            return i
    return -1

def binary_search(arr, target):
    """
    Binary search implementation (requires sorted array).
    
    Time Complexity: O(log n)
    Space Complexity: O(1)
    """
    left, right = 0, len(arr) - 1
    
    while left <= right:
        mid = (left + right) // 2
        
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return -1

def binary_search_recursive(arr, target, left=0, right=None):
    """
    Recursive binary search implementation.
    
    Time Complexity: O(log n)
    Space Complexity: O(log n)
    """
    if right is None:
        right = len(arr) - 1
    
    if left > right:
        return -1
    
    mid = (left + right) // 2
    
    if arr[mid] == target:
        return mid
    elif arr[mid] < target:
        return binary_search_recursive(arr, target, mid + 1, right)
    else:
        return binary_search_recursive(arr, target, left, mid - 1)

# Test search algorithms
print("\n=== Search Algorithms ===")
sorted_array = [1, 3, 5, 7, 9, 11, 13, 15, 17, 19]
target = 7

print(f"Array: {sorted_array}")
print(f"Linear search for {target}: {linear_search(sorted_array, target)}")
print(f"Binary search for {target}: {binary_search(sorted_array, target)}")
print(f"Recursive binary search for {target}: {binary_search_recursive(sorted_array, target)}")

# Dynamic programming with functions
def fibonacci_dp(n):
    """
    Fibonacci with dynamic programming (bottom-up).
    
    Time Complexity: O(n)
    Space Complexity: O(n)
    """
    if n <= 1:
        return n
    
    dp = [0] * (n + 1)
    dp[1] = 1
    
    for i in range(2, n + 1):
        dp[i] = dp[i - 1] + dp[i - 2]
    
    return dp[n]

def fibonacci_optimized(n):
    """
    Space-optimized Fibonacci.
    
    Time Complexity: O(n)
    Space Complexity: O(1)
    """
    if n <= 1:
        return n
    
    prev, curr = 0, 1
    
    for _ in range(2, n + 1):
        prev, curr = curr, prev + curr
    
    return curr

def longest_common_subsequence(str1, str2):
    """
    Find length of longest common subsequence.
    
    Time Complexity: O(m * n)
    Space Complexity: O(m * n)
    """
    m, n = len(str1), len(str2)
    dp = [[0] * (n + 1) for _ in range(m + 1)]
    
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if str1[i - 1] == str2[j - 1]:
                dp[i][j] = 1 + dp[i - 1][j - 1]
            else:
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1])
    
    return dp[m][n]

# Test dynamic programming
print("\n=== Dynamic Programming ===")
print(f"Fibonacci(10) DP: {fibonacci_dp(10)}")
print(f"Fibonacci(10) optimized: {fibonacci_optimized(10)}")

str1, str2 = "ABCDGH", "AEDFHR"
lcs_length = longest_common_subsequence(str1, str2)
print(f"LCS of '{str1}' and '{str2}': {lcs_length}")

# Graph algorithms with functions
def dfs_iterative(graph, start):
    """
    Depth-first search using iteration.
    
    Time Complexity: O(V + E)
    Space Complexity: O(V)
    """
    visited = set()
    stack = [start]
    result = []
    
    while stack:
        vertex = stack.pop()
        if vertex not in visited:
            visited.add(vertex)
            result.append(vertex)
            
            # Add neighbors to stack (reverse order to maintain left-to-right traversal)
            for neighbor in reversed(graph.get(vertex, [])):
                if neighbor not in visited:
                    stack.append(neighbor)
    
    return result

def bfs(graph, start):
    """
    Breadth-first search implementation.
    
    Time Complexity: O(V + E)
    Space Complexity: O(V)
    """
    visited = set()
    queue = [start]
    result = []
    
    while queue:
        vertex = queue.pop(0)
        if vertex not in visited:
            visited.add(vertex)
            result.append(vertex)
            
            for neighbor in graph.get(vertex, []):
                if neighbor not in visited:
                    queue.append(neighbor)
    
    return result

# Test graph algorithms
print("\n=== Graph Algorithms ===")
graph = {
    'A': ['B', 'C'],
    'B': ['A', 'D', 'E'],
    'C': ['A', 'F'],
    'D': ['B'],
    'E': ['B', 'F'],
    'F': ['C', 'E']
}

print(f"Graph: {graph}")
print(f"DFS from A: {dfs_iterative(graph, 'A')}")
print(f"BFS from A: {bfs(graph, 'A')}")
```

### Function Design Patterns

```python
# Factory pattern with functions
def create_shape(shape_type, **kwargs):
    """Factory function to create different shapes."""
    
    def create_circle(radius):
        return {
            "type": "circle",
            "radius": radius,
            "area": lambda: 3.14159 * radius ** 2,
            "perimeter": lambda: 2 * 3.14159 * radius
        }
    
    def create_rectangle(width, height):
        return {
            "type": "rectangle",
            "width": width,
            "height": height,
            "area": lambda: width * height,
            "perimeter": lambda: 2 * (width + height)
        }
    
    def create_triangle(base, height, side1, side2):
        return {
            "type": "triangle",
            "base": base,
            "height": height,
            "area": lambda: 0.5 * base * height,
            "perimeter": lambda: base + side1 + side2
        }
    
    shape_creators = {
        "circle": lambda: create_circle(kwargs["radius"]),
        "rectangle": lambda: create_rectangle(kwargs["width"], kwargs["height"]),
        "triangle": lambda: create_triangle(kwargs["base"], kwargs["height"], 
                                          kwargs["side1"], kwargs["side2"])
    }
    
    if shape_type not in shape_creators:
        raise ValueError(f"Unknown shape type: {shape_type}")
    
    return shape_creators[shape_type]()

# Strategy pattern with functions
def create_payment_processor(strategy):
    """Create payment processor with different strategies."""
    
    def credit_card_payment(amount, card_number, cvv):
        print(f"Processing ${amount} via credit card ending in {card_number[-4:]}")
        return {"status": "success", "transaction_id": f"CC_{hash(card_number) % 10000}"}
    
    def paypal_payment(amount, email):
        print(f"Processing ${amount} via PayPal for {email}")
        return {"status": "success", "transaction_id": f"PP_{hash(email) % 10000}"}
    
    def bank_transfer_payment(amount, account_number, routing_number):
        print(f"Processing ${amount} via bank transfer to account {account_number[-4:]}")
        return {"status": "success", "transaction_id": f"BT_{hash(account_number) % 10000}"}
    
    strategies = {
        "credit_card": credit_card_payment,
        "paypal": paypal_payment,
        "bank_transfer": bank_transfer_payment
    }
    
    if strategy not in strategies:
        raise ValueError(f"Unknown payment strategy: {strategy}")
    
    return strategies[strategy]

# Observer pattern with functions
def create_event_system():
    """Create an event system with observers."""
    observers = {}
    
    def subscribe(event_type, callback):
        """Subscribe to an event type."""
        if event_type not in observers:
            observers[event_type] = []
        observers[event_type].append(callback)
    
    def unsubscribe(event_type, callback):
        """Unsubscribe from an event type."""
        if event_type in observers:
            observers[event_type].remove(callback)
    
    def notify(event_type, data):
        """Notify all observers of an event."""
        if event_type in observers:
            for callback in observers[event_type]:
                callback(data)
    
    return {
        "subscribe": subscribe,
        "unsubscribe": unsubscribe,
        "notify": notify,
        "get_observers": lambda: dict(observers)
    }

# Test design patterns
print("=== Design Patterns ===")

# Factory pattern
circle = create_shape("circle", radius=5)
rectangle = create_shape("rectangle", width=4, height=6)

print(f"Circle area: {circle['area']():.2f}")
print(f"Rectangle perimeter: {rectangle['perimeter']()}")

# Strategy pattern
cc_processor = create_payment_processor("credit_card")
paypal_processor = create_payment_processor("paypal")

cc_result = cc_processor(100.0, "1234567890123456", "123")
paypal_result = paypal_processor(75.0, "user@example.com")

print(f"Credit card result: {cc_result}")
print(f"PayPal result: {paypal_result}")

# Observer pattern
event_system = create_event_system()

def user_logged_in_handler(data):
    print(f"User {data['username']} logged in at {data['timestamp']}")

def user_logged_in_logger(data):
    print(f"LOG: Authentication event for user {data['username']}")

# Subscribe observers
event_system["subscribe"]("user_login", user_logged_in_handler)
event_system["subscribe"]("user_login", user_logged_in_logger)

# Trigger event
import time
event_system["notify"]("user_login", {
    "username": "alice",
    "timestamp": time.time()
})

# Builder pattern with functions
def create_query_builder():
    """Create a SQL query builder using functions."""
    
    def builder():
        query_parts = {
            "select": [],
            "from": "",
            "where": [],
            "order_by": [],
            "limit": None
        }
        
        def select(*columns):
            query_parts["select"].extend(columns)
            return builder_instance
        
        def from_table(table):
            query_parts["from"] = table
            return builder_instance
        
        def where(condition):
            query_parts["where"].append(condition)
            return builder_instance
        
        def order_by(column, direction="ASC"):
            query_parts["order_by"].append(f"{column} {direction}")
            return builder_instance
        
        def limit(count):
            query_parts["limit"] = count
            return builder_instance
        
        def build():
            query = "SELECT " + ", ".join(query_parts["select"])
            query += f" FROM {query_parts['from']}"
            
            if query_parts["where"]:
                query += " WHERE " + " AND ".join(query_parts["where"])
            
            if query_parts["order_by"]:
                query += " ORDER BY " + ", ".join(query_parts["order_by"])
            
            if query_parts["limit"]:
                query += f" LIMIT {query_parts['limit']}"
            
            return query
        
        builder_instance = {
            "select": select,
            "from": from_table,
            "where": where,
            "order_by": order_by,
            "limit": limit,
            "build": build
        }
        
        return builder_instance
    
    return builder()

# Test builder pattern
print("\n=== Builder Pattern ===")
query_builder = create_query_builder()

query = (query_builder
         .select("name", "email", "age")
         .from_table("users")
         .where("age >= 18")
         .where("active = 1")
         .order_by("name")
         .limit(10)
         .build())

print(f"Built query: {query}")
```

## 🎯 Practice Exercises

### Exercise 1: Advanced Function Toolkit

```python
def create_function_toolkit():
    """
    Create a comprehensive function toolkit with:
    1. Function composition utilities
    2. Currying and partial application
    3. Function caching with different strategies
    4. Function timing and profiling
    5. Error handling and retry mechanisms
    """
    # Your implementation here
    pass
```

### Exercise 2: Functional Data Processing Pipeline

```python
def build_data_pipeline():
    """
    Build a functional data processing pipeline with:
    1. Data validation functions
    2. Data transformation functions
    3. Data aggregation functions
    4. Error handling and logging
    5. Pipeline composition and chaining
    """
    # Your implementation here
    pass
```

### Exercise 3: Algorithm Framework

```python
def create_algorithm_framework():
    """
    Create a framework for implementing algorithms with:
    1. Generic algorithm templates
    2. Performance measurement decorators
    3. Visualization hooks
    4. Testing utilities
    5. Comparison tools
    """
    # Your implementation here
    pass
```

## 📚 Summary and Best Practices

### Key Function Concepts

**Function Fundamentals:**
- **Parameters**: positional, keyword, default, *args, **kwargs
- **Return values**: single, multiple, None
- **Documentation**: docstrings, type hints
- **Error handling**: validation, exceptions

**Scope and Lifetime:**
- **LEGB rule**: Local → Enclosing → Global → Built-in
- **Variable lifetime**: creation, usage, garbage collection
- **Closures**: capturing enclosing scope variables

**Advanced Concepts:**
- **Higher-order functions**: functions as arguments/return values
- **Decorators**: function modification and enhancement
- **Lambda functions**: anonymous functions for simple operations
- **Functional programming**: composition, currying, partial application

### Performance Guidelines

| Concept | Best Practice | Avoid |
|---------|--------------|-------|
| Parameters | Use appropriate parameter types | Too many parameters |
| Scope | Minimize global variable usage | Global state mutation |
| Return values | Return consistent types | Side effects in pure functions |
| Documentation | Write clear docstrings | Undocumented complex functions |
| Error handling | Validate inputs early | Silent failures |

### When to Use Different Function Types

**Regular Functions:**
- Complex logic requiring multiple statements
- Need documentation and type hints
- Reusable code blocks
- Clear, named operations

**Lambda Functions:**
- Simple, one-line operations
- Used with map(), filter(), sort()
- Short-lived callback functions
- Functional programming patterns

**Decorators:**
- Cross-cutting concerns (logging, timing, caching)
- Modifying function behavior
- Aspect-oriented programming
- Framework and library development

### Best Practices Checklist

**Function Design:**
- [ ] Single responsibility principle
- [ ] Meaningful function names
- [ ] Appropriate parameter count (≤5 recommended)
- [ ] Consistent return types
- [ ] Clear documentation

**Parameter Handling:**
- [ ] Use default values appropriately
- [ ] Validate input parameters
- [ ] Use type hints for clarity
- [ ] Handle *args and **kwargs carefully
- [ ] Avoid mutable default arguments

**Scope Management:**
- [ ] Minimize global variable usage
- [ ] Use local variables when possible
- [ ] Understand closure implications
- [ ] Be careful with nonlocal modifications
- [ ] Avoid variable shadowing

**Error Handling:**
- [ ] Validate inputs early
- [ ] Use appropriate exception types
- [ ] Document expected exceptions
- [ ] Fail fast and clearly
- [ ] Provide meaningful error messages

**Performance:**
- [ ] Avoid unnecessary function calls in loops
- [ ] Use appropriate caching strategies
- [ ] Consider function call overhead
- [ ] Profile performance-critical functions
- [ ] Use built-in functions when possible

### Common Pitfalls to Avoid

1. **Mutable default arguments**: Use None and create new objects
2. **Modifying global state**: Use return values instead
3. **Too many parameters**: Use data structures or builder pattern
4. **Inconsistent return types**: Always return same type
5. **Side effects in pure functions**: Keep functions predictable
6. **Circular imports**: Organize code properly
7. **Not handling edge cases**: Validate inputs thoroughly

### Advanced Patterns

**Function Factories:**
```python
def create_validator(rule):
    def validator(value):
        return rule(value)
    return validator
```

**Decorator with State:**
```python
def rate_limit(calls_per_second):
    def decorator(func):
        # Implementation here
        pass
    return decorator
```

**Function Pipeline:**
```python
def pipeline(*functions):
    return reduce(lambda f, g: lambda x: g(f(x)), functions)
```

### Next Steps

After mastering functions:
1. Learn about [Classes and Objects](./13-classes-objects.md)
2. Study advanced decorators and metaclasses
3. Explore async functions and coroutines
4. Practice with functional programming libraries
5. Learn about generator functions and iterators

---

**Remember**: Functions are the building blocks of well-structured Python programs. Master them to write clean, maintainable, and efficient code for any programming challenge!
