# Loops: For and While

## 🎯 Objective
Master Python's iteration constructs to efficiently process collections, implement algorithms, and handle repetitive tasks in problem-solving scenarios.

## 📖 Overview

Loops are fundamental to programming, enabling you to perform repetitive tasks efficiently. Python provides two main types of loops: `for` loops (for iterating over sequences) and `while` loops (for condition-based iteration). Understanding both types and their applications is crucial for algorithm implementation and data processing.

## 🔁 For Loops

### Basic For Loop Syntax

```python
# Iterating over a list
fruits = ["apple", "banana", "cherry", "date"]

for fruit in fruits:
    print(f"I like {fruit}s")

# Iterating over a string
word = "Python"
for letter in word:
    print(f"Letter: {letter}")

# Iterating over a range
print("Counting from 1 to 5:")
for i in range(1, 6):
    print(f"Count: {i}")

# Range with step
print("Even numbers from 0 to 10:")
for num in range(0, 11, 2):
    print(num)

# Reverse iteration
print("Countdown:")
for i in range(10, 0, -1):
    print(i)
print("Blast off! 🚀")
```

### Advanced For Loop Patterns

```python
# Enumerate - getting index and value
students = ["Alice", "Bob", "Charlie", "Diana"]

print("Class roster:")
for index, student in enumerate(students):
    print(f"{index + 1}. {student}")

# Starting enumerate from different number
for rank, student in enumerate(students, start=1):
    print(f"Rank {rank}: {student}")

# Zip - iterating over multiple sequences
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30, 35]
cities = ["New York", "London", "Tokyo"]

print("Student information:")
for name, age, city in zip(names, ages, cities):
    print(f"{name} is {age} years old and lives in {city}")

# Iterating over dictionaries
student_grades = {
    "Alice": 95,
    "Bob": 87,
    "Charlie": 92,
    "Diana": 98
}

# Iterate over keys
print("Students:")
for student in student_grades:
    print(student)

# Iterate over values
print("Grades:")
for grade in student_grades.values():
    print(grade)

# Iterate over key-value pairs
print("Student grades:")
for student, grade in student_grades.items():
    letter_grade = "A" if grade >= 90 else "B" if grade >= 80 else "C"
    print(f"{student}: {grade} ({letter_grade})")

# Nested loops for 2D data
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

print("Matrix:")
for row_index, row in enumerate(matrix):
    for col_index, value in enumerate(row):
        print(f"matrix[{row_index}][{col_index}] = {value}")
```

### For Loops in Algorithms

```python
# Finding maximum element
def find_maximum(numbers):
    """Find maximum element using for loop."""
    if not numbers:
        return None
    
    max_value = numbers[0]
    for num in numbers[1:]:
        if num > max_value:
            max_value = num
    return max_value

# Linear search algorithm
def linear_search(array, target):
    """Search for target in array, return index or -1."""
    for index, value in enumerate(array):
        if value == target:
            return index
    return -1

# Bubble sort algorithm
def bubble_sort(arr):
    """Sort array using bubble sort."""
    n = len(arr)
    arr = arr.copy()  # Don't modify original
    
    for i in range(n):
        # Flag to optimize - if no swaps, array is sorted
        swapped = False
        
        # Last i elements are already in place
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True
        
        # If no swapping occurred, array is sorted
        if not swapped:
            break
    
    return arr

# Prime number generation using Sieve of Eratosthenes
def sieve_of_eratosthenes(limit):
    """Generate all prime numbers up to limit."""
    if limit < 2:
        return []
    
    # Initialize boolean array
    is_prime = [True] * (limit + 1)
    is_prime[0] = is_prime[1] = False
    
    # Sieve process
    for i in range(2, int(limit**0.5) + 1):
        if is_prime[i]:
            # Mark multiples of i as not prime
            for j in range(i*i, limit + 1, i):
                is_prime[j] = False
    
    # Collect prime numbers
    primes = []
    for i in range(2, limit + 1):
        if is_prime[i]:
            primes.append(i)
    
    return primes

# Test algorithms
test_numbers = [64, 34, 25, 12, 22, 11, 90]
print(f"Numbers: {test_numbers}")
print(f"Maximum: {find_maximum(test_numbers)}")
print(f"Index of 22: {linear_search(test_numbers, 22)}")
print(f"Sorted: {bubble_sort(test_numbers)}")
print(f"Primes up to 30: {sieve_of_eratosthenes(30)}")

# Pattern generation
def print_triangle(height):
    """Print a triangle pattern."""
    for i in range(1, height + 1):
        # Print spaces
        for j in range(height - i):
            print(" ", end="")
        
        # Print stars
        for k in range(2 * i - 1):
            print("*", end="")
        
        print()  # New line

def print_multiplication_table(num, up_to=10):
    """Print multiplication table."""
    print(f"Multiplication table for {num}:")
    for i in range(1, up_to + 1):
        result = num * i
        print(f"{num} × {i} = {result}")

print_triangle(5)
print()
print_multiplication_table(7)
```

## 🔄 While Loops

### Basic While Loop Syntax

```python
# Simple counting with while loop
count = 1
while count <= 5:
    print(f"Count: {count}")
    count += 1

# User input validation
def get_positive_integer():
    """Get positive integer from user with validation."""
    while True:
        try:
            value = int(input("Enter a positive integer: "))
            if value > 0:
                return value
            else:
                print("Error: Please enter a positive integer.")
        except ValueError:
            print("Error: Please enter a valid integer.")

# Processing until condition met
def find_first_divisible(start, divisor):
    """Find first number >= start that's divisible by divisor."""
    current = start
    while current % divisor != 0:
        current += 1
    return current

# Accumulating results
def calculate_factorial(n):
    """Calculate factorial using while loop."""
    if n < 0:
        return None
    
    result = 1
    current = 1
    
    while current <= n:
        result *= current
        current += 1
    
    return result

# String processing
def remove_duplicates(text):
    """Remove consecutive duplicate characters."""
    if not text:
        return ""
    
    result = text[0]
    i = 1
    
    while i < len(text):
        if text[i] != text[i-1]:
            result += text[i]
        i += 1
    
    return result

print(f"First number >= 10 divisible by 7: {find_first_divisible(10, 7)}")
print(f"5! = {calculate_factorial(5)}")
print(f"Remove duplicates from 'hello': {remove_duplicates('hello')}")
```

### Advanced While Loop Applications

```python
# Game loop pattern
def guess_the_number():
    """Number guessing game with while loop."""
    import random
    
    secret = random.randint(1, 100)
    attempts = 0
    max_attempts = 7
    
    print("I'm thinking of a number between 1 and 100!")
    print(f"You have {max_attempts} attempts to guess it.")
    
    while attempts < max_attempts:
        try:
            guess = int(input(f"Attempt {attempts + 1}: Enter your guess: "))
            attempts += 1
            
            if guess == secret:
                print(f"🎉 Congratulations! You guessed it in {attempts} attempts!")
                return True
            elif guess < secret:
                print("Too low! Try a higher number.")
            else:
                print("Too high! Try a lower number.")
                
            remaining = max_attempts - attempts
            if remaining > 0:
                print(f"You have {remaining} attempts left.")
        
        except ValueError:
            print("Please enter a valid number!")
            attempts -= 1  # Don't count invalid input as attempt
    
    print(f"😔 Game over! The number was {secret}")
    return False

# Iterative algorithms
def gcd_iterative(a, b):
    """Calculate Greatest Common Divisor using Euclidean algorithm."""
    while b:
        a, b = b, a % b
    return a

def fibonacci_iterative(n):
    """Generate first n Fibonacci numbers."""
    if n <= 0:
        return []
    elif n == 1:
        return [0]
    
    fib_sequence = [0, 1]
    
    while len(fib_sequence) < n:
        next_fib = fib_sequence[-1] + fib_sequence[-2]
        fib_sequence.append(next_fib)
    
    return fib_sequence

def collatz_sequence(n):
    """Generate Collatz sequence until reaching 1."""
    sequence = [n]
    
    while n != 1:
        if n % 2 == 0:
            n = n // 2
        else:
            n = 3 * n + 1
        sequence.append(n)
    
    return sequence

# Binary search implementation
def binary_search_iterative(sorted_array, target):
    """Binary search using while loop."""
    left, right = 0, len(sorted_array) - 1
    
    while left <= right:
        mid = (left + right) // 2
        mid_value = sorted_array[mid]
        
        if mid_value == target:
            return mid
        elif mid_value < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return -1

# Test iterative algorithms
print(f"GCD(48, 18) = {gcd_iterative(48, 18)}")
print(f"First 10 Fibonacci numbers: {fibonacci_iterative(10)}")
print(f"Collatz sequence for 13: {collatz_sequence(13)}")

sorted_nums = [1, 3, 5, 7, 9, 11, 13, 15, 17, 19]
target = 11
index = binary_search_iterative(sorted_nums, target)
print(f"Binary search for {target} in {sorted_nums}: index {index}")

# Uncomment to play the guessing game
# guess_the_number()
```

### While Loops for Data Processing

```python
# Processing streaming data
def process_sensor_data():
    """Simulate processing sensor data until threshold met."""
    import random
    
    readings = []
    reading_count = 0
    sum_readings = 0
    
    print("Processing sensor data...")
    
    while True:
        # Simulate sensor reading
        reading = random.uniform(18.0, 25.0)  # Temperature in Celsius
        readings.append(reading)
        reading_count += 1
        sum_readings += reading
        
        avg_temp = sum_readings / reading_count
        
        print(f"Reading {reading_count}: {reading:.2f}°C (Average: {avg_temp:.2f}°C)")
        
        # Stop conditions
        if reading > 24.0:
            print(f"🚨 High temperature alert! {reading:.2f}°C")
            break
        
        if reading_count >= 20:
            print("Maximum readings reached.")
            break
        
        # Simulate delay (in real app, this would be actual sensor timing)
        if reading_count % 5 == 0:
            print("--- Status check ---")
    
    return readings, avg_temp

# File processing line by line
def process_log_file(filename):
    """Process log file line by line (simulated)."""
    # Simulated log data
    log_lines = [
        "2024-01-15 10:30:15 INFO User login successful",
        "2024-01-15 10:31:20 WARNING High memory usage",
        "2024-01-15 10:32:01 ERROR Database connection failed",
        "2024-01-15 10:32:05 INFO Retrying database connection",
        "2024-01-15 10:32:10 INFO Database connection restored",
        "2024-01-15 10:35:00 INFO User logout"
    ]
    
    line_number = 0
    error_count = 0
    warning_count = 0
    
    while line_number < len(log_lines):
        line = log_lines[line_number]
        line_number += 1
        
        # Parse log level
        if "ERROR" in line:
            error_count += 1
            print(f"❌ Line {line_number}: {line}")
        elif "WARNING" in line:
            warning_count += 1
            print(f"⚠️  Line {line_number}: {line}")
        else:
            print(f"ℹ️  Line {line_number}: {line}")
        
        # Stop processing if too many errors
        if error_count >= 3:
            print("🛑 Too many errors, stopping log processing")
            break
    
    print(f"\nSummary: {error_count} errors, {warning_count} warnings processed")
    return error_count, warning_count

# Menu-driven application
def calculator_menu():
    """Calculator with while loop menu."""
    
    def show_menu():
        print("\n" + "="*30)
        print("         CALCULATOR")
        print("="*30)
        print("1. Addition")
        print("2. Subtraction")
        print("3. Multiplication")
        print("4. Division")
        print("5. Power")
        print("6. Show History")
        print("7. Clear History")
        print("0. Exit")
        print("="*30)
    
    history = []
    
    while True:
        show_menu()
        
        try:
            choice = input("Enter your choice (0-7): ").strip()
            
            if choice == '0':
                print("Thank you for using the calculator! Goodbye! 👋")
                break
            
            elif choice in ['1', '2', '3', '4', '5']:
                num1 = float(input("Enter first number: "))
                num2 = float(input("Enter second number: "))
                
                if choice == '1':
                    result = num1 + num2
                    operation = f"{num1} + {num2} = {result}"
                elif choice == '2':
                    result = num1 - num2
                    operation = f"{num1} - {num2} = {result}"
                elif choice == '3':
                    result = num1 * num2
                    operation = f"{num1} × {num2} = {result}"
                elif choice == '4':
                    if num2 == 0:
                        print("❌ Error: Division by zero!")
                        continue
                    result = num1 / num2
                    operation = f"{num1} ÷ {num2} = {result}"
                elif choice == '5':
                    result = num1 ** num2
                    operation = f"{num1} ^ {num2} = {result}"
                
                print(f"Result: {result}")
                history.append(operation)
            
            elif choice == '6':
                if history:
                    print("\n📊 Calculation History:")
                    for i, calc in enumerate(history, 1):
                        print(f"{i}. {calc}")
                else:
                    print("📭 No calculations in history")
            
            elif choice == '7':
                history.clear()
                print("🗑️  History cleared!")
            
            else:
                print("❌ Invalid choice! Please try again.")
        
        except ValueError:
            print("❌ Invalid input! Please enter valid numbers.")
        except KeyboardInterrupt:
            print("\n\n👋 Goodbye!")
            break

# Test data processing functions
print("=== Sensor Data Processing ===")
readings, avg = process_sensor_data()
print(f"\nFinal average temperature: {avg:.2f}°C")

print("\n=== Log File Processing ===")
errors, warnings = process_log_file("sample.log")

# Uncomment to run interactive calculator
# calculator_menu()
```

## 🛑 Loop Control Statements

### Break and Continue

```python
# Break statement - exit loop completely
def find_first_prime_greater_than(n):
    """Find first prime number greater than n."""
    candidate = n + 1
    
    while True:  # Infinite loop with break
        is_prime = True
        
        # Check if candidate is prime
        for i in range(2, int(candidate**0.5) + 1):
            if candidate % i == 0:
                is_prime = False
                break  # Break out of inner loop
        
        if is_prime:
            return candidate
        
        candidate += 1

# Continue statement - skip current iteration
def filter_positive_even_numbers(numbers):
    """Filter and process only positive even numbers."""
    result = []
    
    for num in numbers:
        # Skip negative numbers
        if num < 0:
            continue
        
        # Skip odd numbers
        if num % 2 != 0:
            continue
        
        # Process positive even numbers
        result.append(num * 2)  # Double them
    
    return result

# Using break and continue together
def interactive_number_processor():
    """Process numbers until user wants to quit."""
    processed_count = 0
    sum_total = 0
    
    print("Enter numbers to process (type 'quit' to exit):")
    
    while True:
        user_input = input("Enter a number: ").strip().lower()
        
        # Break condition
        if user_input == 'quit':
            print("Exiting...")
            break
        
        try:
            number = float(user_input)
        except ValueError:
            print("Invalid input! Please enter a number or 'quit'.")
            continue  # Skip rest of loop iteration
        
        # Skip zero (but count it as processed)
        if number == 0:
            print("Zero skipped, but counted as processed.")
            processed_count += 1
            continue
        
        # Process valid non-zero number
        processed_count += 1
        sum_total += number
        average = sum_total / processed_count
        
        print(f"Processed: {number}")
        print(f"Running total: {sum_total}")
        print(f"Average: {average:.2f}")
        print(f"Numbers processed: {processed_count}")
        print("-" * 30)
    
    return processed_count, sum_total

# Advanced break/continue patterns
def validate_and_process_data(data_list):
    """Validate and process data with complex skip logic."""
    valid_data = []
    errors = []
    
    for index, item in enumerate(data_list):
        # Skip None values
        if item is None:
            errors.append(f"Index {index}: None value skipped")
            continue
        
        # Skip empty strings
        if isinstance(item, str) and not item.strip():
            errors.append(f"Index {index}: Empty string skipped")
            continue
        
        # Convert to number if possible
        try:
            if isinstance(item, str):
                # Try int first, then float
                if '.' in item:
                    number = float(item)
                else:
                    number = int(item)
            else:
                number = item
        except ValueError:
            errors.append(f"Index {index}: Cannot convert '{item}' to number")
            continue
        
        # Skip negative numbers
        if number < 0:
            errors.append(f"Index {index}: Negative number {number} skipped")
            continue
        
        # Skip numbers that are too large
        if number > 1000000:
            errors.append(f"Index {index}: Number {number} too large, skipped")
            continue
        
        # Valid data - process it
        valid_data.append(number)
    
    return valid_data, errors

# Test loop control statements
print(f"First prime > 20: {find_first_prime_greater_than(20)}")

test_numbers = [-5, 2, -3, 4, 7, 8, -1, 10, 15, 16]
filtered = filter_positive_even_numbers(test_numbers)
print(f"Original: {test_numbers}")
print(f"Positive even doubled: {filtered}")

# Test data validation
messy_data = [10, "20", None, "", "30.5", -5, "invalid", 50, 2000000, 0]
valid, errors = validate_and_process_data(messy_data)
print(f"\nOriginal data: {messy_data}")
print(f"Valid data: {valid}")
print("Errors:")
for error in errors:
    print(f"  {error}")

# Uncomment to run interactive processor
# interactive_number_processor()
```

### Else Clause with Loops

```python
# For-else: else executes if loop completes without break
def search_with_else(data, target):
    """Demonstrate for-else pattern in search."""
    for index, value in enumerate(data):
        if value == target:
            print(f"Found {target} at index {index}")
            break
    else:
        print(f"{target} not found in the data")
        return -1
    
    return index

# While-else: else executes if condition becomes false naturally
def find_first_factor(n):
    """Find first factor > 1, demonstrating while-else."""
    if n <= 1:
        return None
    
    factor = 2
    while factor < n:
        if n % factor == 0:
            print(f"First factor of {n} is {factor}")
            return factor
        factor += 1
    else:
        print(f"{n} is prime (no factors found)")
        return None

# Practical example: User authentication with attempts
def authenticate_user(correct_password, max_attempts=3):
    """Authenticate user with limited attempts."""
    attempts = 0
    
    while attempts < max_attempts:
        password = input(f"Enter password (attempt {attempts + 1}/{max_attempts}): ")
        
        if password == correct_password:
            print("✅ Authentication successful!")
            return True
        
        attempts += 1
        remaining = max_attempts - attempts
        
        if remaining > 0:
            print(f"❌ Incorrect password. {remaining} attempts remaining.")
    else:
        print("🚫 Authentication failed. Account locked.")
        return False

# Validation with for-else
def validate_all_positive(numbers):
    """Check if all numbers are positive using for-else."""
    for num in numbers:
        if num <= 0:
            print(f"Found non-positive number: {num}")
            return False
    else:
        print("All numbers are positive!")
        return True

# Search for multiple targets
def find_all_targets(data, targets):
    """Find all targets in data, using loop-else patterns."""
    results = {}
    
    for target in targets:
        for index, value in enumerate(data):
            if value == target:
                results[target] = index
                break
        else:
            results[target] = -1  # Not found
    
    return results

# Test loop-else patterns
test_array = [1, 3, 5, 7, 9, 11, 13]
search_with_else(test_array, 7)   # Found
search_with_else(test_array, 8)   # Not found

find_first_factor(15)  # Has factor
find_first_factor(17)  # Prime

validate_all_positive([1, 2, 3, 4, 5])     # All positive
validate_all_positive([1, 2, -3, 4, 5])    # Has negative

targets = [3, 8, 11, 15]
results = find_all_targets(test_array, targets)
print(f"Search results: {results}")

# Uncomment to test authentication (will prompt for input)
# authenticate_user("secret123")
```

## 🧮 Nested Loops and Complex Patterns

### 2D Array Processing

```python
# Matrix operations with nested loops
def create_multiplication_table(size):
    """Create a multiplication table using nested loops."""
    table = []
    
    for i in range(1, size + 1):
        row = []
        for j in range(1, size + 1):
            row.append(i * j)
        table.append(row)
    
    return table

def print_matrix(matrix, title="Matrix"):
    """Pretty print a matrix."""
    print(f"\n{title}:")
    
    # Find maximum width for alignment
    max_width = max(len(str(item)) for row in matrix for item in row)
    
    for row in matrix:
        for item in row:
            print(f"{item:>{max_width}}", end="  ")
        print()

def transpose_matrix(matrix):
    """Transpose matrix using nested loops."""
    rows = len(matrix)
    cols = len(matrix[0]) if rows > 0 else 0
    
    transposed = []
    for j in range(cols):
        new_row = []
        for i in range(rows):
            new_row.append(matrix[i][j])
        transposed.append(new_row)
    
    return transposed

def matrix_multiply(A, B):
    """Multiply two matrices using nested loops."""
    rows_A, cols_A = len(A), len(A[0])
    rows_B, cols_B = len(B), len(B[0])
    
    if cols_A != rows_B:
        raise ValueError("Incompatible matrix dimensions for multiplication")
    
    # Initialize result matrix with zeros
    result = []
    for i in range(rows_A):
        row = []
        for j in range(cols_B):
            row.append(0)
        result.append(row)
    
    # Perform multiplication
    for i in range(rows_A):
        for j in range(cols_B):
            for k in range(cols_A):
                result[i][j] += A[i][k] * B[k][j]
    
    return result

# Test matrix operations
mult_table = create_multiplication_table(5)
print_matrix(mult_table, "5x5 Multiplication Table")

sample_matrix = [
    [1, 2, 3],
    [4, 5, 6]
]
print_matrix(sample_matrix, "Original Matrix")
print_matrix(transpose_matrix(sample_matrix), "Transposed Matrix")

# Matrix multiplication example
A = [[1, 2], [3, 4]]
B = [[5, 6], [7, 8]]
product = matrix_multiply(A, B)
print_matrix(A, "Matrix A")
print_matrix(B, "Matrix B")
print_matrix(product, "A × B")
```

### Pattern Generation

```python
# Various patterns using nested loops
def print_number_pyramid(height):
    """Print number pyramid pattern."""
    print(f"\nNumber Pyramid (height {height}):")
    
    for i in range(1, height + 1):
        # Print leading spaces
        for j in range(height - i):
            print(" ", end="")
        
        # Print ascending numbers
        for k in range(1, i + 1):
            print(k, end="")
        
        # Print descending numbers
        for l in range(i - 1, 0, -1):
            print(l, end="")
        
        print()  # New line

def print_diamond_pattern(size):
    """Print diamond pattern with stars."""
    print(f"\nDiamond Pattern (size {size}):")
    
    # Upper half (including middle)
    for i in range(size):
        # Print spaces
        for j in range(size - i - 1):
            print(" ", end="")
        
        # Print stars
        for k in range(2 * i + 1):
            print("*", end="")
        
        print()
    
    # Lower half
    for i in range(size - 2, -1, -1):
        # Print spaces
        for j in range(size - i - 1):
            print(" ", end="")
        
        # Print stars
        for k in range(2 * i + 1):
            print("*", end="")
        
        print()

def print_spiral_matrix(n):
    """Create and print spiral matrix."""
    # Initialize matrix
    matrix = [[0] * n for _ in range(n)]
    
    # Direction vectors: right, down, left, up
    directions = [(0, 1), (1, 0), (0, -1), (-1, 0)]
    current_direction = 0
    
    row, col = 0, 0
    
    for num in range(1, n * n + 1):
        matrix[row][col] = num
        
        # Calculate next position
        next_row = row + directions[current_direction][0]
        next_col = col + directions[current_direction][1]
        
        # Check if we need to turn (hit boundary or filled cell)
        if (next_row < 0 or next_row >= n or 
            next_col < 0 or next_col >= n or 
            matrix[next_row][next_col] != 0):
            
            # Turn clockwise
            current_direction = (current_direction + 1) % 4
            next_row = row + directions[current_direction][0]
            next_col = col + directions[current_direction][1]
        
        row, col = next_row, next_col
    
    print_matrix(matrix, f"Spiral Matrix ({n}x{n})")

# Pascal's triangle
def print_pascals_triangle(rows):
    """Print Pascal's triangle."""
    print(f"\nPascal's Triangle ({rows} rows):")
    
    triangle = []
    
    for i in range(rows):
        row = []
        for j in range(i + 1):
            if j == 0 or j == i:
                row.append(1)
            else:
                row.append(triangle[i-1][j-1] + triangle[i-1][j])
        triangle.append(row)
    
    # Print with proper spacing
    max_width = len(str(max(triangle[-1])))
    total_width = (max_width + 1) * rows
    
    for i, row in enumerate(triangle):
        # Center the row
        row_width = len(row) * (max_width + 1)
        leading_spaces = (total_width - row_width) // 2
        print(" " * leading_spaces, end="")
        
        for num in row:
            print(f"{num:>{max_width}}", end=" ")
        print()

# Test pattern generation
print_number_pyramid(5)
print_diamond_pattern(4)
print_spiral_matrix(4)
print_pascals_triangle(6)
```

## 🎯 Algorithm Implementations

### Sorting Algorithms

```python
def selection_sort(arr):
    """Selection sort using nested loops."""
    arr = arr.copy()
    n = len(arr)
    
    for i in range(n):
        min_index = i
        
        # Find minimum element in remaining unsorted array
        for j in range(i + 1, n):
            if arr[j] < arr[min_index]:
                min_index = j
        
        # Swap minimum element with first element
        arr[i], arr[min_index] = arr[min_index], arr[i]
    
    return arr

def insertion_sort(arr):
    """Insertion sort using while loop."""
    arr = arr.copy()
    
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1
        
        # Move elements greater than key one position ahead
        while j >= 0 and arr[j] > key:
            arr[j + 1] = arr[j]
            j -= 1
        
        arr[j + 1] = key
    
    return arr

def merge_sort(arr):
    """Merge sort using recursion and loops."""
    if len(arr) <= 1:
        return arr
    
    # Divide
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])
    
    # Merge
    merged = []
    i = j = 0
    
    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            merged.append(left[i])
            i += 1
        else:
            merged.append(right[j])
            j += 1
    
    # Add remaining elements
    while i < len(left):
        merged.append(left[i])
        i += 1
    
    while j < len(right):
        merged.append(right[j])
        j += 1
    
    return merged
```

### Graph Algorithms

```python
def bfs_traversal(graph, start):
    """Breadth-First Search traversal."""
    visited = set()
    queue = [start]
    result = []
    
    while queue:
        vertex = queue.pop(0)  # Remove from front
        
        if vertex not in visited:
            visited.add(vertex)
            result.append(vertex)
            
            # Add unvisited neighbors to queue
            for neighbor in graph.get(vertex, []):
                if neighbor not in visited:
                    queue.append(neighbor)
    
    return result

def dfs_traversal_iterative(graph, start):
    """Depth-First Search using iterative approach with stack."""
    visited = set()
    stack = [start]
    result = []
    
    while stack:
        vertex = stack.pop()  # Remove from top
        
        if vertex not in visited:
            visited.add(vertex)
            result.append(vertex)
            
            # Add unvisited neighbors to stack (reverse order for consistent ordering)
            for neighbor in reversed(graph.get(vertex, [])):
                if neighbor not in visited:
                    stack.append(neighbor)
    
    return result

def shortest_path_bfs(graph, start, end):
    """Find shortest path using BFS."""
    if start == end:
        return [start]
    
    visited = set()
    queue = [(start, [start])]  # (vertex, path)
    
    while queue:
        vertex, path = queue.pop(0)
        
        if vertex not in visited:
            visited.add(vertex)
            
            for neighbor in graph.get(vertex, []):
                if neighbor == end:
                    return path + [neighbor]
                
                if neighbor not in visited:
                    queue.append((neighbor, path + [neighbor]))
    
    return None  # No path found

# Test algorithms
test_array = [64, 34, 25, 12, 22, 11, 90]
print(f"Original array: {test_array}")
print(f"Selection sort: {selection_sort(test_array)}")
print(f"Insertion sort: {insertion_sort(test_array)}")
print(f"Merge sort: {merge_sort(test_array)}")

# Graph representation
sample_graph = {
    'A': ['B', 'C'],
    'B': ['A', 'D', 'E'],
    'C': ['A', 'F'],
    'D': ['B'],
    'E': ['B', 'F'],
    'F': ['C', 'E']
}

print(f"\nGraph: {sample_graph}")
print(f"BFS from A: {bfs_traversal(sample_graph, 'A')}")
print(f"DFS from A: {dfs_traversal_iterative(sample_graph, 'A')}")
print(f"Shortest path A to F: {shortest_path_bfs(sample_graph, 'A', 'F')}")
```

## ⚠️ Common Loop Pitfalls

### Infinite Loops

```python
# Dangerous: Infinite loop examples (commented to prevent execution)
def infinite_loop_examples():
    """Examples of common infinite loop mistakes."""
    
    # Mistake 1: Forgetting to update loop variable
    # i = 0
    # while i < 10:
    #     print(i)
    #     # Forgot: i += 1
    
    # Mistake 2: Wrong condition
    # i = 10
    # while i > 0:
    #     print(i)
    #     i += 1  # Should be i -= 1
    
    # Mistake 3: Floating point precision issues
    # x = 0.1
    # while x != 1.0:
    #     print(x)
    #     x += 0.1  # May never equal exactly 1.0
    
    print("Infinite loop examples shown in comments")

# Safe versions
def safe_loop_examples():
    """Safe versions of potentially infinite loops."""
    
    # Safe version 1: Always update loop variable
    i = 0
    while i < 5:
        print(f"Safe loop 1: {i}")
        i += 1
    
    # Safe version 2: Correct condition
    i = 5
    while i > 0:
        print(f"Safe loop 2: {i}")
        i -= 1
    
    # Safe version 3: Use integer counter or tolerance for floats
    x = 0.1
    count = 0
    while count < 9:  # Instead of x != 1.0
        print(f"Safe loop 3: {x:.1f}")
        x += 0.1
        count += 1

safe_loop_examples()
```

### Performance Issues

```python
import time

# Inefficient: List operations in loops
def inefficient_string_concatenation(words):
    """Inefficient string building."""
    result = ""
    for word in words:
        result += word + " "  # Creates new string each time
    return result.strip()

# Efficient: Using join
def efficient_string_concatenation(words):
    """Efficient string building."""
    return " ".join(words)

# Inefficient: Repeated calculations
def inefficient_calculation():
    """Inefficient repeated calculations."""
    numbers = list(range(1000))
    result = []
    
    for i in range(len(numbers)):
        for j in range(len(numbers)):  # len() called repeatedly
            if numbers[i] < numbers[j]:
                result.append((numbers[i], numbers[j]))
    
    return len(result)

# Efficient: Cache calculations
def efficient_calculation():
    """Efficient with cached calculations."""
    numbers = list(range(1000))
    result = []
    n = len(numbers)  # Cache length
    
    for i in range(n):
        for j in range(n):
            if numbers[i] < numbers[j]:
                result.append((numbers[i], numbers[j]))
    
    return len(result)

# Performance comparison
test_words = ["hello", "world", "python", "programming"] * 100

start_time = time.time()
result1 = inefficient_string_concatenation(test_words)
time1 = time.time() - start_time

start_time = time.time()
result2 = efficient_string_concatenation(test_words)
time2 = time.time() - start_time

print(f"Inefficient string concatenation: {time1:.4f} seconds")
print(f"Efficient string concatenation: {time2:.4f} seconds")
print(f"Speedup: {time1/time2:.1f}x faster")

# Test calculation efficiency
start_time = time.time()
count1 = inefficient_calculation()
time1 = time.time() - start_time

start_time = time.time()
count2 = efficient_calculation()
time2 = time.time() - start_time

print(f"Inefficient calculation: {time1:.4f} seconds")
print(f"Efficient calculation: {time2:.4f} seconds")
print(f"Speedup: {time1/time2:.1f}x faster")
```

## 🎯 Practice Exercises

### Exercise 1: Advanced Pattern Generator

```python
def generate_fractal_pattern(size, char='*'):
    """
    Generate a Sierpinski triangle-like pattern.
    Implement using nested loops.
    """
    # Your implementation here
    pass

# Test: generate_fractal_pattern(8)
```

### Exercise 2: Data Analysis with Loops

```python
def analyze_sales_data(sales_data):
    """
    Analyze sales data structure:
    [
        {"month": "Jan", "sales": [100, 200, 150, ...]},
        {"month": "Feb", "sales": [120, 180, 200, ...]},
        ...
    ]
    
    Return: monthly averages, highest day, trends, etc.
    """
    # Your implementation here
    pass
```

### Exercise 3: Game of Life Simulation

```python
def game_of_life_step(grid):
    """
    Implement one step of Conway's Game of Life.
    Rules:
    1. Live cell with 2-3 neighbors survives
    2. Dead cell with exactly 3 neighbors becomes alive
    3. All other live cells die, dead cells stay dead
    """
    # Your implementation here
    pass

def simulate_game_of_life(initial_grid, steps):
    """Run the simulation for given number of steps."""
    # Your implementation here
    pass
```

## 📚 Summary and Best Practices

### Key Takeaways
1. **Choose the right loop type**: `for` for sequences, `while` for conditions
2. **Use built-in functions**: `enumerate()`, `zip()`, `range()` for cleaner code
3. **Understand loop control**: `break`, `continue`, and `else` clauses
4. **Avoid infinite loops**: Always ensure loop variables are updated correctly
5. **Optimize performance**: Cache calculations, use appropriate data structures
6. **Handle edge cases**: Empty sequences, single elements, invalid inputs

### Loop Patterns Checklist
- [ ] Use `for` loops for iterating over known sequences
- [ ] Use `while` loops for condition-based iteration
- [ ] Use `enumerate()` when you need both index and value
- [ ] Use `zip()` for parallel iteration
- [ ] Use `range()` for numeric sequences
- [ ] Use `break` to exit loops early
- [ ] Use `continue` to skip iterations
- [ ] Consider loop-else patterns for search operations
- [ ] Avoid modifying sequences while iterating over them
- [ ] Cache expensive calculations outside loops

### Performance Guidelines
1. **Minimize work inside loops**: Move invariant calculations outside
2. **Use list comprehensions**: Often faster than explicit loops
3. **Choose efficient data structures**: Sets for membership testing, etc.
4. **Break early when possible**: Use early termination conditions
5. **Use built-in functions**: They're usually optimized

### Next Steps
After mastering loops:
1. Learn about [Lists and List Operations](./09-lists-operations.md)
2. Practice implementing classic algorithms
3. Study loop optimization techniques
4. Explore generator expressions and itertools

---

**Remember**: Loops are fundamental to algorithm implementation. Master them to write efficient, readable code for data processing and problem-solving!
