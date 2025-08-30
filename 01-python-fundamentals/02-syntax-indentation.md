# Python Syntax and Indentation

## 🎯 Objective
Master Python's unique syntax rules and indentation-based structure that forms the foundation of all Python programming.

## 📖 Overview

Python's syntax is designed for readability and simplicity. Unlike many programming languages that use braces `{}` or keywords to define code blocks, Python uses **indentation** to structure code. This makes Python code clean and forces good formatting practices.

## 🔍 Key Concepts

### 1. The Zen of Python
Before diving into syntax, let's understand Python's philosophy:

```python
import this
# Run this in Python to see the Zen of Python
```

**Core Principles:**
- Beautiful is better than ugly
- Explicit is better than implicit
- Simple is better than complex
- Readability counts
- There should be one obvious way to do it

### 2. Python's Case Sensitivity

Python is **case-sensitive**, meaning `Variable`, `variable`, and `VARIABLE` are three different identifiers.

```python
# These are all different variables
name = "Alice"
Name = "Bob"
NAME = "Charlie"

print(name)    # Output: Alice
print(Name)    # Output: Bob  
print(NAME)    # Output: Charlie
```

### 3. Statements and Expressions

**Statement**: A complete instruction that Python can execute
**Expression**: A combination of values, variables, and operators that evaluates to a value

```python
# Statements
x = 5                    # Assignment statement
print("Hello")           # Function call statement
if x > 0:               # Conditional statement
    print("Positive")

# Expressions  
5 + 3                   # Arithmetic expression
x * 2                   # Variable expression
len("hello")            # Function call expression
```

## 🏗️ Indentation Rules

### Why Indentation Matters

Python uses indentation to define code blocks. This eliminates the need for braces and makes code more readable.

```python
# Correct indentation
if x > 0:
    print("x is positive")
    print("This is inside the if block")
print("This is outside the if block")

# Incorrect indentation (will cause IndentationError)
if x > 0:
print("This will cause an error")  # Missing indentation
```

### Indentation Standards

**PEP 8 Guidelines:**
- Use **4 spaces** per indentation level
- Never mix tabs and spaces
- Be consistent throughout your code

```python
# Good: 4 spaces per level
def calculate_area(length, width):
    if length > 0 and width > 0:
        area = length * width
        return area
    else:
        return 0

# Bad: Inconsistent indentation
def calculate_area(length, width):
  if length > 0 and width > 0:    # 2 spaces
      area = length * width       # 6 spaces
    return area                   # 4 spaces - inconsistent!
```

### Nested Indentation

```python
# Multiple levels of indentation
def process_numbers(numbers):
    for num in numbers:                    # Level 1: 4 spaces
        if num > 0:                        # Level 2: 8 spaces
            if num % 2 == 0:              # Level 3: 12 spaces
                print(f"{num} is positive and even")
            else:                         # Level 3: 12 spaces
                print(f"{num} is positive and odd")
        elif num < 0:                     # Level 2: 8 spaces
            print(f"{num} is negative")
        else:                             # Level 2: 8 spaces
            print("Zero is neither positive nor negative")

numbers = [1, 2, -3, 0, 4]
process_numbers(numbers)
```

## 📝 Line Structure

### Physical and Logical Lines

**Physical Line**: What you see in the editor (ends with newline character)
**Logical Line**: A complete Python statement (may span multiple physical lines)

```python
# Single physical line = Single logical line
x = 5

# Multiple physical lines = Single logical line (using line continuation)
total = 1 + 2 + 3 + \
        4 + 5 + 6

# Using parentheses for line continuation (preferred)
total = (1 + 2 + 3 +
         4 + 5 + 6)

# Multiple statements on one physical line (not recommended)
x = 5; y = 10; print(x + y)
```

### Line Continuation

**Explicit Continuation** (using backslash):
```python
# Long string
message = "This is a very long string that " \
          "spans multiple lines for better " \
          "readability"

# Long calculation
result = (first_value + second_value + third_value + \
          fourth_value + fifth_value)
```

**Implicit Continuation** (inside parentheses, brackets, or braces):
```python
# Function calls
result = some_function(parameter1, parameter2,
                      parameter3, parameter4)

# Lists
my_list = [1, 2, 3,
           4, 5, 6,
           7, 8, 9]

# Dictionaries
person = {
    'name': 'Alice',
    'age': 30,
    'city': 'New York'
}

# Complex expressions
if (condition1 and condition2 and
    condition3 and condition4):
    print("All conditions met")
```

## 🔤 Identifiers and Keywords

### Identifiers

Identifiers are names used to identify variables, functions, classes, modules, etc.

**Rules for Identifiers:**
1. Must start with a letter (a-z, A-Z) or underscore (_)
2. Can contain letters, digits (0-9), and underscores
3. Case-sensitive
4. Cannot be a reserved keyword

```python
# Valid identifiers
variable_name = 10
_private_var = 20
MyClass = "class name"
function2 = "function"
__special__ = "special variable"

# Invalid identifiers
# 2variable = 10        # Cannot start with digit
# my-variable = 10      # Cannot contain hyphen
# class = 10            # Cannot use reserved keyword
```

### Reserved Keywords

Python has reserved keywords that cannot be used as identifiers:

```python
# View all keywords
import keyword
print(keyword.kwlist)

# Common keywords:
# False, None, True, and, as, assert, break, class, continue,
# def, del, elif, else, except, finally, for, from, global,
# if, import, in, is, lambda, nonlocal, not, or, pass,
# raise, return, try, while, with, yield
```

### Naming Conventions (PEP 8)

```python
# Variables and functions: lowercase with underscores
user_name = "Alice"
total_count = 100

def calculate_average(numbers):
    return sum(numbers) / len(numbers)

# Constants: uppercase with underscores
MAX_SIZE = 1000
DEFAULT_COLOR = "blue"

# Classes: CapWords (PascalCase)
class StudentRecord:
    pass

# Private variables: leading underscore
_internal_variable = "not for external use"

# Special methods: double underscores
def __init__(self):
    pass
```

## 💬 Comments and Docstrings

### Single-Line Comments

```python
# This is a single-line comment
x = 5  # Comments can be at the end of a line

# Use comments to explain WHY, not WHAT
user_count = get_user_count()  # Cache for performance optimization
```

### Multi-Line Comments

```python
# This is a multi-line comment
# that spans several lines
# to explain complex logic

"""
This is actually a multi-line string,
but it's often used as a multi-line comment
when not assigned to a variable.
"""
```

### Docstrings

```python
def calculate_bmi(weight, height):
    """
    Calculate Body Mass Index (BMI).
    
    Args:
        weight (float): Weight in kilograms
        height (float): Height in meters
    
    Returns:
        float: BMI value
    
    Example:
        >>> calculate_bmi(70, 1.75)
        22.857142857142858
    """
    return weight / (height ** 2)

class Person:
    """
    A class to represent a person.
    
    Attributes:
        name (str): The person's name
        age (int): The person's age
    """
    
    def __init__(self, name, age):
        """
        Initialize a Person object.
        
        Args:
            name (str): The person's name
            age (int): The person's age
        """
        self.name = name
        self.age = age
```

## 🔍 Python Execution Model

### Interactive Mode vs Script Mode

**Interactive Mode** (Python REPL):
```python
# Start Python interpreter
$ python
>>> print("Hello, World!")
Hello, World!
>>> x = 5
>>> x + 3
8
>>> exit()
```

**Script Mode** (save as .py file):
```python
# hello.py
print("Hello, World!")
x = 5
print(x + 3)

# Run from command line
$ python hello.py
```

### The `if __name__ == "__main__":` Pattern

```python
# my_module.py
def greet(name):
    """Greet a person by name."""
    return f"Hello, {name}!"

def main():
    """Main function to run when script is executed directly."""
    name = input("Enter your name: ")
    message = greet(name)
    print(message)

# This block runs only when script is executed directly,
# not when imported as a module
if __name__ == "__main__":
    main()
```

## 🛠️ Practical Examples

### Example 1: Basic Syntax Structure

```python
# fibonacci.py - Calculate Fibonacci sequence
def fibonacci(n):
    """
    Calculate the nth Fibonacci number.
    
    Args:
        n (int): Position in Fibonacci sequence
    
    Returns:
        int: The nth Fibonacci number
    """
    if n <= 1:
        return n
    else:
        return fibonacci(n - 1) + fibonacci(n - 2)

def main():
    """Main function to demonstrate Fibonacci calculation."""
    # Get input from user
    try:
        num = int(input("Enter a number: "))
        
        if num < 0:
            print("Please enter a non-negative number.")
        else:
            result = fibonacci(num)
            print(f"Fibonacci({num}) = {result}")
            
    except ValueError:
        print("Please enter a valid integer.")

if __name__ == "__main__":
    main()
```

### Example 2: Proper Indentation and Structure

```python
# grade_calculator.py
def calculate_grade(scores):
    """
    Calculate letter grade based on average score.
    
    Args:
        scores (list): List of numerical scores
    
    Returns:
        tuple: (average_score, letter_grade)
    """
    if not scores:  # Check for empty list
        return 0, 'F'
    
    average = sum(scores) / len(scores)
    
    # Determine letter grade
    if average >= 90:
        grade = 'A'
    elif average >= 80:
        grade = 'B'
    elif average >= 70:
        grade = 'C'
    elif average >= 60:
        grade = 'D'
    else:
        grade = 'F'
    
    return average, grade

def display_results(student_name, scores, average, grade):
    """Display formatted results."""
    print(f"\nStudent: {student_name}")
    print(f"Scores: {scores}")
    print(f"Average: {average:.2f}")
    print(f"Grade: {grade}")

def main():
    """Main program execution."""
    student_name = input("Enter student name: ")
    scores = []
    
    # Collect scores
    print("Enter scores (press Enter with empty input to finish):")
    while True:
        score_input = input("Score: ")
        
        if not score_input:  # Empty input to finish
            break
            
        try:
            score = float(score_input)
            if 0 <= score <= 100:
                scores.append(score)
            else:
                print("Score must be between 0 and 100.")
        except ValueError:
            print("Please enter a valid number.")
    
    if scores:
        average, grade = calculate_grade(scores)
        display_results(student_name, scores, average, grade)
    else:
        print("No valid scores entered.")

if __name__ == "__main__":
    main()
```

## ⚠️ Common Syntax Errors

### IndentationError
```python
# Wrong: Missing indentation
if x > 0:
print("Positive")  # IndentationError

# Correct:
if x > 0:
    print("Positive")
```

### SyntaxError
```python
# Wrong: Missing colon
if x > 0
    print("Positive")  # SyntaxError

# Correct:
if x > 0:
    print("Positive")
```

### NameError
```python
# Wrong: Using undefined variable
print(undefined_variable)  # NameError

# Correct: Define before use
undefined_variable = "Now it's defined"
print(undefined_variable)
```

## 🧪 Practice Exercises

### Exercise 1: Indentation Practice
Write a function that prints a multiplication table with proper indentation:

```python
def multiplication_table(n):
    """Print multiplication table for number n."""
    # Your code here - focus on proper indentation
    pass

# Expected output for multiplication_table(3):
# 3 x 1 = 3
# 3 x 2 = 6
# 3 x 3 = 9
# ... up to 3 x 10 = 30
```

### Exercise 2: Line Continuation Practice
Rewrite this long line using proper line continuation:

```python
# Rewrite this using line continuation
result = calculate_complex_value(parameter1, parameter2, parameter3, parameter4, parameter5, parameter6)
```

### Exercise 3: Comment and Docstring Practice
Add appropriate comments and docstrings to this code:

```python
def process_data(data):
    result = []
    for item in data:
        if item > 0:
            result.append(item * 2)
        else:
            result.append(0)
    return result
```

## 📊 Code Quality Checklist

Before proceeding to the next topic, ensure your code meets these standards:

- [ ] **Indentation**: Consistent 4-space indentation
- [ ] **Line Length**: Lines under 79 characters (PEP 8)
- [ ] **Comments**: Meaningful comments explaining WHY
- [ ] **Docstrings**: All functions have proper docstrings
- [ ] **Naming**: Follows PEP 8 naming conventions
- [ ] **Structure**: Logical organization with proper spacing

## 📚 Advanced Topics Preview

Understanding syntax and indentation prepares you for:
- **Complex nested structures** in data structures
- **Class definitions** in object-oriented programming
- **Function decorators** and advanced Python features
- **Code readability** in algorithmic implementations

## 🚀 Next Steps

Now that you understand Python's syntax and indentation:

1. **Practice Writing**: Create small programs focusing on structure
2. **Code Review**: Review existing Python code for syntax patterns
3. **Tool Setup**: Configure your editor for proper Python formatting
4. **Next Topic**: Proceed to [Variables and Naming Conventions](./03-variables-naming.md)

## 🎯 Key Takeaways

✅ **Indentation defines code structure** - use 4 spaces consistently
✅ **Python is case-sensitive** - pay attention to capitalization
✅ **Comments explain WHY, not WHAT** - write meaningful documentation
✅ **Follow PEP 8** - Python's official style guide
✅ **Proper structure** - makes code readable and maintainable

**Remember**: Good syntax habits formed now will make you a better programmer throughout your journey. Clean, well-structured code is easier to debug, maintain, and understand when solving complex algorithmic problems!
