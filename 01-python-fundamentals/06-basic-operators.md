# Basic Operators

## 🎯 Objective
Master Python's operator system including arithmetic, comparison, logical, bitwise, and assignment operators to build efficient problem-solving solutions.

## 📖 Overview

Operators are the building blocks of expressions and calculations in Python. Understanding operators deeply enables you to write concise, readable, and efficient code. Python provides a rich set of operators that work with different data types and can be customized for your own classes through operator overloading.

## 🔢 Arithmetic Operators

### Basic Arithmetic Operations

```python
# Basic arithmetic operators
a, b = 17, 5

addition = a + b        # 22
subtraction = a - b     # 12
multiplication = a * b  # 85
division = a / b        # 3.4 (always returns float)
floor_division = a // b # 3 (integer division)
modulo = a % b         # 2 (remainder)
exponentiation = a ** b # 1419857 (17^5)

print(f"{a} + {b} = {addition}")
print(f"{a} - {b} = {subtraction}")
print(f"{a} * {b} = {multiplication}")
print(f"{a} / {b} = {division}")
print(f"{a} // {b} = {floor_division}")
print(f"{a} % {b} = {modulo}")
print(f"{a} ** {b} = {exponentiation}")

# Operator precedence (PEMDAS)
result = 2 + 3 * 4 ** 2 // 3 - 1
# Step by step: 4**2=16, 3*16=48, 48//3=16, 2+16=18, 18-1=17
print(f"2 + 3 * 4 ** 2 // 3 - 1 = {result}")

# Using parentheses to control precedence
result_with_parens = ((2 + 3) * 4) ** 2 // (3 - 1)
print(f"((2 + 3) * 4) ** 2 // (3 - 1) = {result_with_parens}")
```

### Advanced Arithmetic Applications

```python
# Greatest Common Divisor using Euclidean algorithm
def gcd(a, b):
    """Calculate GCD using modulo operator."""
    while b:
        a, b = b, a % b
    return a

# Least Common Multiple
def lcm(a, b):
    """Calculate LCM using GCD."""
    return abs(a * b) // gcd(a, b)

print(f"GCD(48, 18) = {gcd(48, 18)}")  # 6
print(f"LCM(48, 18) = {lcm(48, 18)}")  # 144

# Check if number is power of 2 using bitwise operations
def is_power_of_two(n):
    """Check if n is power of 2 using bit manipulation."""
    return n > 0 and (n & (n - 1)) == 0

# Fast exponentiation using repeated squaring
def fast_power(base, exponent):
    """Calculate base^exponent efficiently."""
    if exponent == 0:
        return 1
    
    result = 1
    while exponent > 0:
        if exponent % 2 == 1:  # If exponent is odd
            result *= base
        base *= base
        exponent //= 2
    
    return result

print(f"Is 16 power of 2? {is_power_of_two(16)}")  # True
print(f"Is 15 power of 2? {is_power_of_two(15)}")  # False
print(f"Fast 2^10 = {fast_power(2, 10)}")          # 1024

# Working with different numeric types
from decimal import Decimal
from fractions import Fraction

# Precise decimal arithmetic
price = Decimal('19.99')
tax_rate = Decimal('0.08')
total = price * (1 + tax_rate)
print(f"Precise total: ${total}")

# Fraction arithmetic
frac1 = Fraction(1, 3)
frac2 = Fraction(1, 6)
frac_sum = frac1 + frac2
print(f"{frac1} + {frac2} = {frac_sum}")  # 1/2

# Complex number arithmetic
z1 = 3 + 4j
z2 = 1 - 2j
print(f"({z1}) * ({z2}) = {z1 * z2}")
print(f"|{z1}| = {abs(z1)}")  # Magnitude
```

## 🔍 Comparison Operators

### Basic Comparisons

```python
# Comparison operators return boolean values
x, y = 10, 20

equal = x == y          # False
not_equal = x != y      # True
less_than = x < y       # True
less_equal = x <= y     # True
greater_than = x > y    # False
greater_equal = x >= y  # False

print(f"{x} == {y}: {equal}")
print(f"{x} != {y}: {not_equal}")
print(f"{x} < {y}: {less_than}")
print(f"{x} <= {y}: {less_equal}")
print(f"{x} > {y}: {greater_than}")
print(f"{x} >= {y}: {greater_equal}")

# Chained comparisons (very Pythonic!)
age = 25
is_adult = 18 <= age <= 65
print(f"Is {age} adult age? {is_adult}")

# Multiple chained comparisons
a, b, c = 5, 10, 15
is_ascending = a < b < c
is_descending = a > b > c
print(f"Is {a}, {b}, {c} ascending? {is_ascending}")
print(f"Is {a}, {b}, {c} descending? {is_descending}")
```

### Identity and Membership Operators

```python
# Identity operators: is, is not
list1 = [1, 2, 3]
list2 = [1, 2, 3]
list3 = list1

print(f"list1 == list2: {list1 == list2}")  # True (same content)
print(f"list1 is list2: {list1 is list2}")  # False (different objects)
print(f"list1 is list3: {list1 is list3}")  # True (same object)

# Small integer caching
a = 5
b = 5
print(f"a is b (small integers): {a is b}")  # True (cached)

x = 1000
y = 1000
print(f"x is y (large integers): {x is y}")  # May be False

# Checking for None (always use 'is')
value = None
print(f"value is None: {value is None}")      # Correct way
print(f"value == None: {value == None}")      # Works but not recommended

# Membership operators: in, not in
fruits = ['apple', 'banana', 'cherry']
text = "hello world"
numbers = {1, 2, 3, 4, 5}

print(f"'apple' in fruits: {'apple' in fruits}")           # True
print(f"'grape' not in fruits: {'grape' not in fruits}")   # True
print(f"'world' in text: {'world' in text}")               # True
print(f"3 in numbers: {3 in numbers}")                     # True

# Membership with dictionaries (checks keys by default)
person = {'name': 'Alice', 'age': 30}
print(f"'name' in person: {'name' in person}")             # True
print(f"'Alice' in person: {'Alice' in person}")           # False (not a key)
print(f"'Alice' in person.values(): {'Alice' in person.values()}")  # True
```

### Advanced Comparison Techniques

```python
# Custom comparison for complex objects
class Student:
    def __init__(self, name, grade):
        self.name = name
        self.grade = grade
    
    def __eq__(self, other):
        return isinstance(other, Student) and self.grade == other.grade
    
    def __lt__(self, other):
        return isinstance(other, Student) and self.grade < other.grade
    
    def __repr__(self):
        return f"Student('{self.name}', {self.grade})"

students = [
    Student("Alice", 85),
    Student("Bob", 92),
    Student("Charlie", 78)
]

# Now we can sort and compare students
students.sort()  # Sorts by grade (using __lt__)
print(f"Students sorted by grade: {students}")

# Find students with same grade
alice = Student("Alice", 85)
alice2 = Student("Another Alice", 85)
print(f"Same grade? {alice == alice2}")  # True

# Comparing different types safely
def safe_compare(a, b):
    """Safely compare values of potentially different types."""
    try:
        return a < b
    except TypeError:
        # If types can't be compared, compare string representations
        return str(a) < str(b)

mixed_list = [1, "hello", 3.14, [1, 2]]
print("Safe comparison results:")
for i in range(len(mixed_list) - 1):
    result = safe_compare(mixed_list[i], mixed_list[i + 1])
    print(f"{mixed_list[i]} < {mixed_list[i + 1]}: {result}")
```

## 🧠 Logical Operators

### Boolean Logic Operations

```python
# Basic logical operators
p, q = True, False

and_result = p and q    # False
or_result = p or q      # True
not_p = not p          # False
not_q = not q          # True

print(f"{p} and {q} = {and_result}")
print(f"{p} or {q} = {or_result}")
print(f"not {p} = {not_p}")
print(f"not {q} = {not_q}")

# Truth tables
print("\nTruth Table for AND:")
for a in [True, False]:
    for b in [True, False]:
        print(f"{a} and {b} = {a and b}")

print("\nTruth Table for OR:")
for a in [True, False]:
    for b in [True, False]:
        print(f"{a} or {b} = {a or b}")

# Short-circuit evaluation
def expensive_function():
    print("Expensive function called!")
    return True

# AND short-circuit: if first is False, second isn't evaluated
result = False and expensive_function()  # expensive_function NOT called
print(f"AND result: {result}")

# OR short-circuit: if first is True, second isn't evaluated  
result = True or expensive_function()    # expensive_function NOT called
print(f"OR result: {result}")

# When second function IS called
result = True and expensive_function()   # expensive_function IS called
print(f"AND result (both evaluated): {result}")
```

### Practical Logical Operations

```python
# Input validation using logical operators
def validate_user_input(username, password, age):
    """Validate user registration data."""
    
    # Username validation
    username_valid = (isinstance(username, str) and 
                     3 <= len(username) <= 20 and 
                     username.isalnum())
    
    # Password validation
    has_upper = any(c.isupper() for c in password)
    has_lower = any(c.islower() for c in password)
    has_digit = any(c.isdigit() for c in password)
    has_special = any(not c.isalnum() for c in password)
    
    password_valid = (isinstance(password, str) and 
                     len(password) >= 8 and
                     has_upper and has_lower and has_digit and has_special)
    
    # Age validation
    age_valid = isinstance(age, int) and 13 <= age <= 120
    
    # Overall validation
    all_valid = username_valid and password_valid and age_valid
    
    return {
        'valid': all_valid,
        'username_valid': username_valid,
        'password_valid': password_valid,
        'age_valid': age_valid
    }

# Test validation
test_cases = [
    ("john123", "MyPass123!", 25),
    ("ab", "weak", 15),  # Username too short, weak password
    ("validuser", "StrongPass123!", 30),
]

for username, password, age in test_cases:
    result = validate_user_input(username, password, age)
    print(f"User: {username}, Valid: {result['valid']}")
    if not result['valid']:
        print(f"  Issues: {[k for k, v in result.items() if k != 'valid' and not v]}")

# Complex conditions with logical operators
def determine_discount(customer_type, order_amount, is_member, days_since_last_order):
    """Determine discount based on multiple criteria."""
    
    # Different discount rules
    new_customer_discount = (customer_type == "new" and order_amount >= 50)
    loyalty_discount = (is_member and days_since_last_order >= 30)
    bulk_discount = (order_amount >= 200)
    special_combo = (is_member and customer_type == "premium" and order_amount >= 100)
    
    # Apply highest applicable discount
    if special_combo:
        return 0.25  # 25% for premium members with large orders
    elif bulk_discount:
        return 0.15  # 15% for bulk orders
    elif loyalty_discount:
        return 0.10  # 10% for returning members
    elif new_customer_discount:
        return 0.05  # 5% for new customers
    else:
        return 0.0   # No discount

# Test discount logic
customers = [
    ("new", 75, False, 0),      # New customer, decent order
    ("existing", 150, True, 45), # Member returning after long time
    ("premium", 250, True, 10),  # Premium member, large order
    ("existing", 25, False, 5),  # Small order, not member
]

for customer_type, amount, is_member, days in customers:
    discount = determine_discount(customer_type, amount, is_member, days)
    print(f"Customer: {customer_type}, Amount: ${amount}, Discount: {discount:.1%}")
```

## 🔢 Bitwise Operators

### Basic Bitwise Operations

```python
# Bitwise operators work on individual bits
a, b = 12, 10  # 12 = 1100 (binary), 10 = 1010 (binary)

bitwise_and = a & b    # 8  = 1000 (binary)
bitwise_or = a | b     # 14 = 1110 (binary)
bitwise_xor = a ^ b    # 6  = 0110 (binary)
bitwise_not = ~a       # -13 (two's complement)
left_shift = a << 2    # 48 = 110000 (binary)
right_shift = a >> 2   # 3  = 11 (binary)

print(f"a = {a} = {bin(a)}")
print(f"b = {b} = {bin(b)}")
print(f"a & b = {bitwise_and} = {bin(bitwise_and)}")
print(f"a | b = {bitwise_or} = {bin(bitwise_or)}")
print(f"a ^ b = {bitwise_xor} = {bin(bitwise_xor)}")
print(f"~a = {bitwise_not} = {bin(bitwise_not & 0xFFFF)}")  # Show as 16-bit
print(f"a << 2 = {left_shift} = {bin(left_shift)}")
print(f"a >> 2 = {right_shift} = {bin(right_shift)}")

# Practical applications of bitwise operations
def set_bit(number, position):
    """Set bit at given position."""
    return number | (1 << position)

def clear_bit(number, position):
    """Clear bit at given position."""
    return number & ~(1 << position)

def toggle_bit(number, position):
    """Toggle bit at given position."""
    return number ^ (1 << position)

def check_bit(number, position):
    """Check if bit is set at given position."""
    return bool(number & (1 << position))

# Example: Using bits as flags
PERMISSIONS = {
    'READ': 0,      # Bit 0
    'WRITE': 1,     # Bit 1
    'EXECUTE': 2,   # Bit 2
    'DELETE': 3,    # Bit 3
}

# Start with no permissions
user_permissions = 0

# Grant read and write permissions
user_permissions = set_bit(user_permissions, PERMISSIONS['READ'])
user_permissions = set_bit(user_permissions, PERMISSIONS['WRITE'])

print(f"User permissions: {bin(user_permissions)}")
print(f"Has read permission: {check_bit(user_permissions, PERMISSIONS['READ'])}")
print(f"Has execute permission: {check_bit(user_permissions, PERMISSIONS['EXECUTE'])}")

# Toggle execute permission
user_permissions = toggle_bit(user_permissions, PERMISSIONS['EXECUTE'])
print(f"After toggling execute: {check_bit(user_permissions, PERMISSIONS['EXECUTE'])}")
```

### Advanced Bitwise Algorithms

```python
# Count number of set bits (population count)
def count_set_bits(n):
    """Count number of 1s in binary representation."""
    count = 0
    while n:
        count += n & 1
        n >>= 1
    return count

# More efficient version using Brian Kernighan's algorithm
def count_set_bits_fast(n):
    """Faster bit counting using Brian Kernighan's algorithm."""
    count = 0
    while n:
        n &= n - 1  # This removes the rightmost set bit
        count += 1
    return count

# Find the only non-repeating element in array where all others appear twice
def find_single_number(nums):
    """Find single number using XOR properties."""
    result = 0
    for num in nums:
        result ^= num  # XOR all numbers; duplicates cancel out
    return result

# Check if two integers have opposite signs
def opposite_signs(a, b):
    """Check if two numbers have opposite signs using XOR."""
    return (a ^ b) < 0

# Swap two numbers without temporary variable
def swap_without_temp(a, b):
    """Swap two numbers using XOR."""
    print(f"Before: a={a}, b={b}")
    a = a ^ b
    b = a ^ b  # b = (a^b)^b = a
    a = a ^ b  # a = (a^b)^a = b
    print(f"After: a={a}, b={b}")
    return a, b

# Test bitwise algorithms
print(f"Set bits in 15: {count_set_bits(15)}")  # 15 = 1111, so 4 bits
print(f"Set bits in 15 (fast): {count_set_bits_fast(15)}")

test_array = [2, 1, 4, 9, 1, 4, 2]  # 9 appears once, others twice
print(f"Single number: {find_single_number(test_array)}")

print(f"5 and -3 opposite signs: {opposite_signs(5, -3)}")   # True
print(f"5 and 3 opposite signs: {opposite_signs(5, 3)}")     # False

swap_without_temp(10, 20)

# Bit manipulation for subsets generation
def generate_all_subsets(arr):
    """Generate all subsets using bit manipulation."""
    n = len(arr)
    subsets = []
    
    # There are 2^n possible subsets
    for i in range(1 << n):  # From 0 to 2^n - 1
        subset = []
        for j in range(n):
            # Check if j-th bit is set in i
            if i & (1 << j):
                subset.append(arr[j])
        subsets.append(subset)
    
    return subsets

# Example: Generate all subsets of [1, 2, 3]
subsets = generate_all_subsets([1, 2, 3])
print(f"All subsets of [1, 2, 3]: {subsets}")
```

## ⚙️ Assignment Operators

### Basic Assignment Operations

```python
# Basic assignment
x = 10
print(f"x = {x}")

# Augmented assignment operators
x += 5   # Equivalent to: x = x + 5
print(f"After x += 5: {x}")

x -= 3   # Equivalent to: x = x - 3
print(f"After x -= 3: {x}")

x *= 2   # Equivalent to: x = x * 2
print(f"After x *= 2: {x}")

x /= 4   # Equivalent to: x = x / 4
print(f"After x /= 4: {x}")

x //= 2  # Equivalent to: x = x // 2
print(f"After x //= 2: {x}")

x %= 3   # Equivalent to: x = x % 3
print(f"After x %= 3: {x}")

x **= 3  # Equivalent to: x = x ** 3
print(f"After x **= 3: {x}")

# Bitwise assignment operators
y = 12  # 1100 in binary
print(f"y = {y} = {bin(y)}")

y &= 10  # y = y & 10
print(f"After y &= 10: {y} = {bin(y)}")

y |= 5   # y = y | 5  
print(f"After y |= 5: {y} = {bin(y)}")

y ^= 3   # y = y ^ 3
print(f"After y ^= 3: {y} = {bin(y)}")

y <<= 1  # y = y << 1
print(f"After y <<= 1: {y} = {bin(y)}")

y >>= 2  # y = y >> 2
print(f"After y >>= 2: {y} = {bin(y)}")
```

### Multiple Assignment and Unpacking

```python
# Multiple assignment
a = b = c = 0
print(f"a={a}, b={b}, c={c}")

# Tuple unpacking
coordinates = (10, 20)
x, y = coordinates
print(f"x={x}, y={y}")

# List unpacking
data = [1, 2, 3, 4, 5]
first, second, *rest = data
print(f"first={first}, second={second}, rest={rest}")

# Swapping variables (Pythonic way)
a, b = 5, 10
print(f"Before swap: a={a}, b={b}")
a, b = b, a
print(f"After swap: a={a}, b={b}")

# Advanced unpacking patterns
def analyze_scores(*scores):
    """Analyze test scores with unpacking."""
    if not scores:
        return "No scores provided"
    
    lowest, *middle, highest = sorted(scores)
    average = sum(scores) / len(scores)
    
    return {
        'lowest': lowest,
        'highest': highest,
        'average': average,
        'middle_scores': middle
    }

result = analyze_scores(85, 92, 78, 96, 88)
print(f"Score analysis: {result}")

# Dictionary unpacking (Python 3.5+)
person1 = {'name': 'Alice', 'age': 30}
person2 = {'city': 'New York', 'job': 'Engineer'}
combined = {**person1, **person2}
print(f"Combined person data: {combined}")

# Function argument unpacking
def calculate_area(length, width, height=1):
    """Calculate area or volume."""
    return length * width * height

dimensions = [10, 5]
area = calculate_area(*dimensions)  # Unpack list as arguments
print(f"Area: {area}")

box_specs = {'length': 10, 'width': 5, 'height': 3}
volume = calculate_area(**box_specs)  # Unpack dict as keyword arguments
print(f"Volume: {volume}")
```

## 🎯 Operator Overloading for Custom Classes

### Creating Custom Operators

```python
class Vector:
    """2D Vector class with operator overloading."""
    
    def __init__(self, x, y):
        self.x = x
        self.y = y
    
    def __str__(self):
        return f"Vector({self.x}, {self.y})"
    
    def __repr__(self):
        return f"Vector({self.x}, {self.y})"
    
    # Arithmetic operators
    def __add__(self, other):
        if isinstance(other, Vector):
            return Vector(self.x + other.x, self.y + other.y)
        return NotImplemented
    
    def __sub__(self, other):
        if isinstance(other, Vector):
            return Vector(self.x - other.x, self.y - other.y)
        return NotImplemented
    
    def __mul__(self, scalar):
        if isinstance(scalar, (int, float)):
            return Vector(self.x * scalar, self.y * scalar)
        return NotImplemented
    
    def __rmul__(self, scalar):
        return self.__mul__(scalar)
    
    def __truediv__(self, scalar):
        if isinstance(scalar, (int, float)) and scalar != 0:
            return Vector(self.x / scalar, self.y / scalar)
        return NotImplemented
    
    # Comparison operators
    def __eq__(self, other):
        if isinstance(other, Vector):
            return self.x == other.x and self.y == other.y
        return False
    
    def __lt__(self, other):
        if isinstance(other, Vector):
            return self.magnitude() < other.magnitude()
        return NotImplemented
    
    # Utility methods
    def magnitude(self):
        return (self.x ** 2 + self.y ** 2) ** 0.5
    
    def dot_product(self, other):
        return self.x * other.x + self.y * other.y
    
    # Unary operators
    def __neg__(self):
        return Vector(-self.x, -self.y)
    
    def __abs__(self):
        return self.magnitude()

# Test vector operations
v1 = Vector(3, 4)
v2 = Vector(1, 2)

print(f"v1 = {v1}")
print(f"v2 = {v2}")
print(f"v1 + v2 = {v1 + v2}")
print(f"v1 - v2 = {v1 - v2}")
print(f"v1 * 2 = {v1 * 2}")
print(f"3 * v1 = {3 * v1}")
print(f"v1 / 2 = {v1 / 2}")
print(f"v1 == v2: {v1 == v2}")
print(f"v1 < v2: {v1 < v2}")
print(f"|v1| = {abs(v1)}")
print(f"-v1 = {-v1}")
print(f"v1 · v2 = {v1.dot_product(v2)}")

# Complex number-like class
class ComplexNumber:
    """Custom complex number implementation."""
    
    def __init__(self, real, imag):
        self.real = real
        self.imag = imag
    
    def __str__(self):
        sign = '+' if self.imag >= 0 else '-'
        return f"{self.real} {sign} {abs(self.imag)}i"
    
    def __add__(self, other):
        if isinstance(other, ComplexNumber):
            return ComplexNumber(self.real + other.real, self.imag + other.imag)
        elif isinstance(other, (int, float)):
            return ComplexNumber(self.real + other, self.imag)
        return NotImplemented
    
    def __radd__(self, other):
        return self.__add__(other)
    
    def __mul__(self, other):
        if isinstance(other, ComplexNumber):
            # (a + bi)(c + di) = (ac - bd) + (ad + bc)i
            real_part = self.real * other.real - self.imag * other.imag
            imag_part = self.real * other.imag + self.imag * other.real
            return ComplexNumber(real_part, imag_part)
        elif isinstance(other, (int, float)):
            return ComplexNumber(self.real * other, self.imag * other)
        return NotImplemented
    
    def __rmul__(self, other):
        return self.__mul__(other)
    
    def conjugate(self):
        return ComplexNumber(self.real, -self.imag)
    
    def magnitude(self):
        return (self.real ** 2 + self.imag ** 2) ** 0.5

# Test complex number operations
c1 = ComplexNumber(3, 4)
c2 = ComplexNumber(1, -2)

print(f"c1 = {c1}")
print(f"c2 = {c2}")
print(f"c1 + c2 = {c1 + c2}")
print(f"c1 * c2 = {c1 * c2}")
print(f"c1 + 5 = {c1 + 5}")
print(f"2 * c1 = {2 * c1}")
print(f"conjugate(c1) = {c1.conjugate()}")
print(f"|c1| = {c1.magnitude():.2f}")
```

## ⚠️ Common Operator Pitfalls

### Pitfall 1: Floating Point Comparison

```python
# Dangerous floating point comparison
a = 0.1 + 0.2
b = 0.3

print(f"0.1 + 0.2 = {a}")
print(f"a == 0.3: {a == b}")  # False!

# Safe floating point comparison
import math

def almost_equal(a, b, tolerance=1e-9):
    return abs(a - b) < tolerance

print(f"Almost equal: {almost_equal(a, b)}")  # True
print(f"Using math.isclose: {math.isclose(a, b)}")  # True

# For financial calculations, use Decimal
from decimal import Decimal

price1 = Decimal('0.1')
price2 = Decimal('0.2')
total = price1 + price2
print(f"Decimal sum: {total}")
print(f"Decimal == 0.3: {total == Decimal('0.3')}")  # True
```

### Pitfall 2: Integer Division Changes in Python 3

```python
# Python 3 behavior (different from Python 2)
print(f"5 / 2 = {5 / 2}")      # 3.0 (float division)
print(f"5 // 2 = {5 // 2}")    # 2 (floor division)

# Be careful with negative numbers and floor division
print(f"-5 // 2 = {-5 // 2}")  # -3 (floors toward negative infinity)
print(f"-5 / 2 = {-5 / 2}")    # -2.5

# If you want truncation toward zero (like C/Java)
import math
def truncate_divide(a, b):
    return math.trunc(a / b)

print(f"Truncate -5/2: {truncate_divide(-5, 2)}")  # -2
```

### Pitfall 3: Mutable Object Operations

```python
# Dangerous operations with mutable objects
list1 = [1, 2, 3]
list2 = list1  # Same object!

list2 += [4, 5]  # Modifies the original list
print(f"list1: {list1}")  # [1, 2, 3, 4, 5] - modified!

# Safe operations
list3 = [1, 2, 3]
list4 = list3 + [4, 5]  # Creates new list
print(f"list3: {list3}")  # [1, 2, 3] - unchanged
print(f"list4: {list4}")  # [1, 2, 3, 4, 5]

# Or use copy
list5 = list3.copy()
list5 += [4, 5]
print(f"list3 after copy operation: {list3}")  # [1, 2, 3] - unchanged
```

## 🎯 Practice Exercises

### Exercise 1: Expression Evaluator

```python
def evaluate_expression(expr_str):
    """
    Safely evaluate mathematical expressions.
    Support +, -, *, /, //, %, ** operators with proper precedence.
    """
    # Implement safe expression evaluation
    pass

# Test cases
expressions = [
    "2 + 3 * 4",
    "10 - 6 / 2",
    "2 ** 3 + 1",
    "(5 + 3) * 2",
]
```

### Exercise 2: Bitwise Calculator

```python
class BitwiseCalculator:
    """Calculator for bitwise operations with binary display."""
    
    def __init__(self):
        self.result = 0
    
    def and_op(self, a, b):
        """Perform bitwise AND and display result."""
        pass
    
    def or_op(self, a, b):
        """Perform bitwise OR and display result."""
        pass
    
    def show_binary(self, num, width=8):
        """Show number in binary format."""
        pass

# Example usage:
# calc = BitwiseCalculator()
# calc.and_op(12, 10)  # Should show: 12 (1100) & 10 (1010) = 8 (1000)
```

### Exercise 3: Smart Comparison Function

```python
def smart_compare(a, b, comparison_type="auto"):
    """
    Compare two values intelligently based on their types.
    
    Args:
        a, b: Values to compare
        comparison_type: "numeric", "string", "auto"
    
    Returns:
        -1 if a < b, 0 if a == b, 1 if a > b
    """
    # Implement intelligent comparison
    pass

# Test with mixed types
test_pairs = [
    (5, "10"),      # Should compare as numbers if possible
    ("apple", "Banana"),  # String comparison
    ([1, 2], [1, 2, 3]),  # List comparison
]
```

## 📚 Summary and Best Practices

### Key Takeaways
1. **Understand operator precedence**: Use parentheses for clarity
2. **Choose appropriate operators**: Know when to use `/` vs `//`
3. **Handle floating point carefully**: Use proper comparison methods
4. **Leverage short-circuit evaluation**: For efficiency and safety
5. **Use bitwise operators for flags**: Efficient for permissions and states
6. **Implement operator overloading thoughtfully**: Make custom classes intuitive

### Operator Precedence (High to Low)
1. `()` - Parentheses
2. `**` - Exponentiation
3. `+x`, `-x`, `~x` - Unary operators
4. `*`, `/`, `//`, `%` - Multiplication, Division, Modulo
5. `+`, `-` - Addition, Subtraction
6. `<<`, `>>` - Bit shifts
7. `&` - Bitwise AND
8. `^` - Bitwise XOR
9. `|` - Bitwise OR
10. `==`, `!=`, `<`, `<=`, `>`, `>=`, `is`, `is not`, `in`, `not in` - Comparisons
11. `not` - Boolean NOT
12. `and` - Boolean AND
13. `or` - Boolean OR

### Best Practices Checklist
- [ ] Use parentheses to clarify complex expressions
- [ ] Prefer `is` and `is not` for None comparisons
- [ ] Use `math.isclose()` for floating point comparisons
- [ ] Understand the difference between `==` and `is`
- [ ] Leverage short-circuit evaluation for performance
- [ ] Be careful with mutable object operations
- [ ] Use appropriate numeric types for precision requirements

### Next Steps
After mastering operators:
1. Learn about [Control Structures (If/Elif/Else)](./07-control-structures-if.md)
2. Practice operator precedence with complex expressions
3. Explore advanced bitwise algorithms
4. Study operator overloading in popular Python libraries

---

**Remember**: Operators are the foundation of expressions and calculations. Master them to write efficient, readable, and bug-free code!
