# Variables and Naming Conventions

## 🎯 Objective
Master Python variable declaration, naming conventions, and best practices that form the foundation of readable and maintainable code.

## 📖 Overview

Variables in Python are names that refer to objects in memory. Unlike some programming languages, Python variables don't have a fixed type - they can reference different types of objects during their lifetime. Understanding proper variable usage and naming conventions is crucial for writing professional Python code.

## 🔍 Variable Fundamentals

### What are Variables?

In Python, variables are **references** to objects in memory, not containers that hold values. When you assign a value to a variable, Python creates an object in memory and makes the variable name point to that object.

```python
# Variable assignment
x = 42  # x refers to an integer object with value 42
name = "Alice"  # name refers to a string object with value "Alice"
is_valid = True  # is_valid refers to a boolean object with value True

# Variables can be reassigned to different types
x = "Now I'm a string"  # x now refers to a string object
x = [1, 2, 3]  # x now refers to a list object
```

### Variable Assignment Patterns

```python
# Simple assignment
age = 25
pi = 3.14159

# Multiple assignment
x, y, z = 1, 2, 3
a = b = c = 0  # All variables refer to the same object

# Unpacking assignment
coordinates = (10, 20)
x, y = coordinates

# Swapping variables (Pythonic way)
a, b = 5, 10
a, b = b, a  # Now a=10, b=5

# Augmented assignment
count = 0
count += 1  # Equivalent to: count = count + 1
count *= 2  # Equivalent to: count = count * 2
```

### Variable Identity and Equality

```python
# Understanding object identity
a = [1, 2, 3]
b = [1, 2, 3]
c = a

print(a == b)  # True (same value)
print(a is b)  # False (different objects)
print(a is c)  # True (same object)

# Check object identity
print(id(a))  # Memory address of object a refers to
print(id(b))  # Different memory address
print(id(c))  # Same as id(a)

# Small integer caching (Python optimization)
x = 5
y = 5
print(x is y)  # True (Python caches small integers)

x = 1000
y = 1000
print(x is y)  # May be False (larger integers not always cached)
```

## 📝 Naming Conventions (PEP 8)

### Basic Naming Rules

**Legal Character Set:**
- Letters (a-z, A-Z)
- Digits (0-9) - but not as first character
- Underscore (_)

```python
# Valid variable names
user_name = "John"
age2 = 25
_private_var = "internal use"
MAX_SIZE = 100

# Invalid variable names (will cause SyntaxError)
# 2user = "John"     # Cannot start with digit
# user-name = "John"  # Hyphen not allowed
# class = "MyClass"   # Reserved keyword
# user name = "John"  # Space not allowed
```

### PEP 8 Style Guidelines

#### Variables and Functions: snake_case
```python
# Good: Descriptive, lowercase with underscores
user_name = "Alice"
total_count = 42
is_authenticated = True
max_retry_attempts = 3

def calculate_total_price(items):
    return sum(item.price for item in items)

def is_valid_email(email_address):
    return "@" in email_address
```

#### Constants: UPPER_SNAKE_CASE
```python
# Good: All uppercase with underscores
MAX_CONNECTIONS = 100
DEFAULT_TIMEOUT = 30
API_BASE_URL = "https://api.example.com"
PI = 3.14159265359

# Configuration constants
DATABASE_HOST = "localhost"
DATABASE_PORT = 5432
LOG_LEVEL = "INFO"
```

#### Classes: PascalCase (CapWords)
```python
# Good: Each word capitalized, no underscores
class UserAccount:
    pass

class PaymentProcessor:
    pass

class HTTPResponseHandler:
    pass
```

#### Private Variables: Leading Underscore
```python
class BankAccount:
    def __init__(self, balance):
        self.balance = balance
        self._account_number = self._generate_account_number()
        self.__secret_key = self._generate_secret()  # Name mangling
    
    def _generate_account_number(self):
        """Private method - internal use only."""
        return "ACC" + str(hash(self.balance))[:8]
    
    def __generate_secret(self):
        """Private method with name mangling."""
        return "SECRET"
```

#### Special Methods: Double Underscores
```python
class Person:
    def __init__(self, name, age):
        """Constructor method."""
        self.name = name
        self.age = age
    
    def __str__(self):
        """String representation."""
        return f"Person(name='{self.name}', age={self.age})"
    
    def __eq__(self, other):
        """Equality comparison."""
        return self.name == other.name and self.age == other.age
```

### Descriptive Naming Examples

#### Poor vs Good Variable Names
```python
# Poor: Unclear, abbreviated, not descriptive
n = "John Doe"
a = 25
x = True
lst = [1, 2, 3, 4, 5]
d = {"key": "value"}

# Good: Clear, descriptive, meaningful
full_name = "John Doe"
user_age = 25
is_authenticated = True
fibonacci_numbers = [1, 2, 3, 4, 5]
configuration_settings = {"key": "value"}
```

#### Context-Specific Naming
```python
# Mathematical context
def calculate_quadratic_formula(a, b, c):
    """In mathematical context, single letters are acceptable."""
    discriminant = b**2 - 4*a*c
    if discriminant < 0:
        return None
    
    x1 = (-b + discriminant**0.5) / (2*a)
    x2 = (-b - discriminant**0.5) / (2*a)
    return x1, x2

# Business logic context
def process_customer_order(customer_info, order_items, payment_method):
    """Business context requires descriptive names."""
    total_amount = calculate_order_total(order_items)
    tax_amount = calculate_tax(total_amount, customer_info.tax_rate)
    final_amount = total_amount + tax_amount
    
    if validate_payment(payment_method, final_amount):
        return create_order_confirmation(customer_info, order_items, final_amount)
    else:
        raise PaymentValidationError("Invalid payment information")
```

## 🔧 Variable Types and Scope

### Variable Types by Usage

#### Local Variables
```python
def calculate_area(length, width):
    """Local variables exist only within function scope."""
    area = length * width  # Local variable
    perimeter = 2 * (length + width)  # Local variable
    return area, perimeter

# area and perimeter are not accessible here
# print(area)  # NameError: name 'area' is not defined
```

#### Global Variables
```python
# Global variable (module level)
COMPANY_NAME = "TechCorp"
employee_count = 0

def hire_employee(name):
    """Function that modifies global variable."""
    global employee_count  # Declare intent to modify global
    employee_count += 1
    print(f"Hired {name}. Total employees: {employee_count}")

def get_company_info():
    """Function that reads global variable."""
    return f"{COMPANY_NAME} has {employee_count} employees"

hire_employee("Alice")
hire_employee("Bob")
print(get_company_info())
```

#### Class Variables vs Instance Variables
```python
class Employee:
    # Class variable (shared by all instances)
    company_name = "TechCorp"
    employee_count = 0
    
    def __init__(self, name, department):
        # Instance variables (unique to each instance)
        self.name = name
        self.department = department
        self.employee_id = self._generate_id()
        
        # Modify class variable
        Employee.employee_count += 1
    
    def _generate_id(self):
        """Generate unique employee ID."""
        return f"EMP{Employee.employee_count + 1:04d}"
    
    def get_info(self):
        """Access both instance and class variables."""
        return f"{self.name} (ID: {self.employee_id}) works in {self.department} at {self.company_name}"

# Creating instances
emp1 = Employee("Alice", "Engineering")
emp2 = Employee("Bob", "Marketing")

print(emp1.get_info())
print(emp2.get_info())
print(f"Total employees: {Employee.employee_count}")
```

### Variable Lifetime and Memory Management

```python
def demonstrate_variable_lifetime():
    """Show how variables are created and destroyed."""
    
    # Variable created when assigned
    temp_data = [1, 2, 3, 4, 5]
    print(f"temp_data created: {id(temp_data)}")
    
    # Variable reassigned - old object may be garbage collected
    temp_data = "New value"
    print(f"temp_data reassigned: {id(temp_data)}")
    
    # Local variables destroyed when function ends
    return temp_data

result = demonstrate_variable_lifetime()
print(f"Result: {result}")
# temp_data no longer exists here
```

## 🎯 Best Practices and Common Patterns

### Meaningful Variable Names

```python
# Good: Variable names explain their purpose
def process_user_registration(email_address, password, confirm_password):
    """Process new user registration with validation."""
    
    # Clear validation flags
    is_email_valid = validate_email_format(email_address)
    is_password_strong = check_password_strength(password)
    passwords_match = password == confirm_password
    
    # Clear conditional logic
    if not is_email_valid:
        raise ValueError("Invalid email format")
    
    if not is_password_strong:
        raise ValueError("Password does not meet strength requirements")
    
    if not passwords_match:
        raise ValueError("Passwords do not match")
    
    # Create user account
    new_user_account = create_user_account(email_address, password)
    return new_user_account
```

### Boolean Variable Naming

```python
# Good: Boolean variables use descriptive predicates
is_authenticated = check_user_credentials(username, password)
has_permission = check_user_permission(user, resource)
can_edit = has_permission and is_authenticated
should_log_action = can_edit and is_audit_enabled
will_send_notification = should_log_action and user.wants_notifications

# Use in conditional statements
if is_authenticated and has_permission:
    perform_action()

if not can_edit:
    raise PermissionError("User cannot edit this resource")
```

### Collection and Iterator Naming

```python
# Good: Use plural nouns for collections
user_accounts = get_all_users()
error_messages = validate_form_data(form)
configuration_options = load_configuration()

# Good: Use singular nouns for individual items
for user_account in user_accounts:
    print(user_account.email)

for error_message in error_messages:
    log_error(error_message)

# Good: Descriptive iterator variables
for index, item in enumerate(shopping_cart_items):
    print(f"{index + 1}. {item.name}: ${item.price}")

for filename, file_content in file_data.items():
    process_file(filename, file_content)
```

### Avoiding Name Conflicts

```python
# Avoid shadowing built-in names
# Bad: shadows built-in functions
list = [1, 2, 3]  # Don't do this!
dict = {"key": "value"}  # Don't do this!
str = "hello"  # Don't do this!

# Good: Use descriptive names
number_list = [1, 2, 3]
config_dict = {"key": "value"}
greeting_str = "hello"

# Avoid using single letters except in specific contexts
# Bad: unclear single letters
for i in users:  # What is i?
    for j in i.orders:  # What is j?
        print(j.total)

# Good: descriptive names
for user in users:
    for order in user.orders:
        print(order.total)

# Exception: Mathematical operations where single letters are conventional
def distance(x1, y1, x2, y2):
    """Calculate distance between two points."""
    return ((x2 - x1)**2 + (y2 - y1)**2)**0.5
```

## 🧪 Practical Examples

### Example 1: User Management System
```python
class UserManager:
    """Demonstrates proper variable naming in a real-world context."""
    
    def __init__(self):
        self.registered_users = {}
        self.active_sessions = {}
        self.failed_login_attempts = {}
        self.max_login_attempts = 3
        self.session_timeout_minutes = 30
    
    def register_new_user(self, email_address, password, full_name):
        """Register a new user with proper validation."""
        
        # Input validation variables
        is_email_available = email_address not in self.registered_users
        is_email_format_valid = self._validate_email_format(email_address)
        is_password_secure = self._validate_password_strength(password)
        
        # Validation logic
        if not is_email_available:
            raise ValueError("Email address already registered")
        
        if not is_email_format_valid:
            raise ValueError("Invalid email format")
        
        if not is_password_secure:
            raise ValueError("Password does not meet security requirements")
        
        # Create user account
        user_account = {
            'email': email_address,
            'password_hash': self._hash_password(password),
            'full_name': full_name,
            'registration_date': datetime.now(),
            'is_active': True,
            'last_login': None
        }
        
        self.registered_users[email_address] = user_account
        return user_account
    
    def authenticate_user(self, email_address, password):
        """Authenticate user with rate limiting."""
        
        # Check if user exists
        user_exists = email_address in self.registered_users
        if not user_exists:
            return False
        
        # Check failed attempts
        current_failed_attempts = self.failed_login_attempts.get(email_address, 0)
        is_account_locked = current_failed_attempts >= self.max_login_attempts
        
        if is_account_locked:
            raise SecurityError("Account temporarily locked due to failed login attempts")
        
        # Validate password
        user_account = self.registered_users[email_address]
        password_hash = self._hash_password(password)
        is_password_correct = password_hash == user_account['password_hash']
        
        if is_password_correct:
            # Reset failed attempts and create session
            self.failed_login_attempts[email_address] = 0
            session_id = self._create_session(email_address)
            user_account['last_login'] = datetime.now()
            return session_id
        else:
            # Increment failed attempts
            self.failed_login_attempts[email_address] = current_failed_attempts + 1
            return False
```

### Example 2: E-commerce Order Processing
```python
def process_customer_order(customer_data, order_items, payment_information):
    """Process customer order with comprehensive validation."""
    
    # Customer validation
    customer_id = customer_data.get('customer_id')
    customer_email = customer_data.get('email')
    shipping_address = customer_data.get('shipping_address')
    
    is_customer_valid = validate_customer(customer_id)
    is_email_valid = validate_email_format(customer_email)
    is_shipping_address_complete = validate_shipping_address(shipping_address)
    
    # Order validation
    order_has_items = len(order_items) > 0
    are_items_available = check_inventory_availability(order_items)
    
    # Price calculations
    subtotal_amount = calculate_subtotal(order_items)
    tax_rate = get_tax_rate(shipping_address.get('state'))
    tax_amount = subtotal_amount * tax_rate
    shipping_cost = calculate_shipping_cost(order_items, shipping_address)
    total_amount = subtotal_amount + tax_amount + shipping_cost
    
    # Payment validation
    payment_method = payment_information.get('method')
    is_payment_method_valid = validate_payment_method(payment_method)
    has_sufficient_funds = verify_payment_amount(payment_information, total_amount)
    
    # Process order if all validations pass
    if all([is_customer_valid, is_email_valid, is_shipping_address_complete,
            order_has_items, are_items_available, is_payment_method_valid, 
            has_sufficient_funds]):
        
        # Create order record
        order_confirmation = {
            'order_id': generate_order_id(),
            'customer_id': customer_id,
            'order_items': order_items,
            'subtotal': subtotal_amount,
            'tax': tax_amount,
            'shipping': shipping_cost,
            'total': total_amount,
            'order_date': datetime.now(),
            'estimated_delivery': calculate_delivery_date(shipping_address)
        }
        
        # Process payment and update inventory
        payment_confirmation = process_payment(payment_information, total_amount)
        inventory_update_result = update_inventory(order_items)
        
        # Send confirmation
        send_order_confirmation_email(customer_email, order_confirmation)
        
        return order_confirmation
    
    else:
        # Return detailed validation errors
        validation_errors = []
        if not is_customer_valid:
            validation_errors.append("Invalid customer information")
        if not is_email_valid:
            validation_errors.append("Invalid email address")
        # ... additional error checks
        
        raise OrderValidationError(validation_errors)
```

## ⚠️ Common Mistakes and How to Avoid Them

### Mistake 1: Using Ambiguous Names
```python
# Bad: Ambiguous variable names
data = get_user_info()
result = process_data(data)
flag = check_status(result)

# Good: Descriptive variable names
user_profile_data = get_user_info()
validation_result = process_data(user_profile_data)
is_profile_valid = check_status(validation_result)
```

### Mistake 2: Inconsistent Naming
```python
# Bad: Inconsistent naming styles
userName = "John"
user_email = "john@example.com"
UserAge = 25
user_IsActive = True

# Good: Consistent snake_case
user_name = "John"
user_email = "john@example.com"
user_age = 25
user_is_active = True
```

### Mistake 3: Not Using Constants for Magic Numbers
```python
# Bad: Magic numbers scattered throughout code
if user_age < 18:
    return "Too young"
elif user_age > 65:
    return "Senior discount available"

timeout = 30  # What is 30?
max_attempts = 5  # Why 5?

# Good: Named constants
MIN_ADULT_AGE = 18
SENIOR_DISCOUNT_AGE = 65
DEFAULT_TIMEOUT_SECONDS = 30
MAX_LOGIN_ATTEMPTS = 5

if user_age < MIN_ADULT_AGE:
    return "Too young"
elif user_age >= SENIOR_DISCOUNT_AGE:
    return "Senior discount available"

timeout = DEFAULT_TIMEOUT_SECONDS
max_attempts = MAX_LOGIN_ATTEMPTS
```

### Mistake 4: Modifying Variables Unexpectedly
```python
# Bad: Modifying variables can cause confusion
def process_items(item_list):
    """Function that unexpectedly modifies input."""
    item_list.sort()  # This modifies the original list!
    return item_list

original_items = [3, 1, 4, 1, 5]
processed_items = process_items(original_items)
print(original_items)  # [1, 1, 3, 4, 5] - Original was modified!

# Good: Don't modify inputs unless explicitly intended
def process_items(item_list):
    """Function that doesn't modify input."""
    sorted_items = sorted(item_list)  # Creates new list
    return sorted_items

original_items = [3, 1, 4, 1, 5]
processed_items = process_items(original_items)
print(original_items)  # [3, 1, 4, 1, 5] - Original unchanged
```

## 🎯 Exercises and Practice

### Exercise 1: Variable Naming Improvement
Improve the variable names in this code:
```python
# Original code with poor naming
def f(x, y):
    a = x + y
    b = x - y
    c = x * y
    d = x / y if y != 0 else 0
    return [a, b, c, d]

# Your improved version here
def calculate_basic_operations(first_number, second_number):
    # Implement with better variable names
    pass
```

### Exercise 2: Implement User Profile Manager
```python
class UserProfileManager:
    """Implement this class with proper variable naming."""
    
    def __init__(self):
        # Initialize instance variables with proper names
        pass
    
    def create_profile(self, email, password, first_name, last_name):
        # Implement with proper variable naming and validation
        pass
    
    def update_profile(self, user_id, update_data):
        # Implement profile update with proper validation
        pass
    
    def validate_profile_data(self, profile_data):
        # Implement validation with descriptive boolean variables
        pass
```

### Exercise 3: Debug Variable Scope Issues
```python
# Fix the scope issues in this code
total = 0
count = 0

def add_numbers(numbers):
    for number in numbers:
        total += number  # Error: UnboundLocalError
        count += 1       # Error: UnboundLocalError
    return total / count

# Fix this function to work correctly
```

## 📚 Summary and Best Practices

### Key Takeaways
1. **Variables are references** to objects in memory, not containers
2. **Use descriptive names** that clearly indicate purpose and content
3. **Follow PEP 8 conventions** consistently throughout your code
4. **Choose appropriate scope** for variables based on their usage
5. **Avoid name conflicts** with built-in functions and keywords

### Quick Reference Checklist
- [ ] Variable names are descriptive and meaningful
- [ ] Naming follows PEP 8 conventions (snake_case for variables/functions)
- [ ] Constants are in UPPER_SNAKE_CASE
- [ ] Boolean variables use is_, has_, can_, should_ prefixes
- [ ] Collection variables use plural nouns
- [ ] No conflicts with built-in names or keywords
- [ ] Scope is appropriate for variable usage
- [ ] Names are consistent within the codebase

### Next Steps
After mastering variable naming conventions:
1. Learn about [Comments and Documentation](./04-comments-documentation.md)
2. Practice with more complex variable scenarios
3. Study existing codebases to see naming patterns
4. Review and refactor your old code for better naming

---

**Remember**: Good variable names are investments in your future self and your teammates. They make code self-documenting and significantly easier to understand, debug, and maintain. Take the time to choose names that clearly communicate intent and purpose!
