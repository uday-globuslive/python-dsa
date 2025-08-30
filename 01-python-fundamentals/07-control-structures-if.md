# Control Structures: If/Elif/Else

## 🎯 Objective
Master Python's conditional statements and decision-making structures to create logical program flow and handle different scenarios in problem-solving.

## 📖 Overview

Control structures are fundamental to programming logic. They allow programs to make decisions, execute different code paths based on conditions, and respond dynamically to various inputs. Python's if/elif/else statements provide clean, readable syntax for implementing complex decision trees.

## 🔀 Basic If Statements

### Simple If Statement

```python
# Basic if statement
age = 18

if age >= 18:
    print("You are eligible to vote!")
    print("Welcome to adulthood!")

# if statement with multiple conditions
temperature = 75
is_sunny = True

if temperature > 70 and is_sunny:
    print("Perfect weather for a picnic!")

# Using variables in conditions
balance = 1000
withdrawal_amount = 500

if balance >= withdrawal_amount:
    balance -= withdrawal_amount
    print(f"Withdrawal successful. New balance: ${balance}")
```

### If-Else Statement

```python
# Basic if-else structure
score = 85

if score >= 90:
    print("Excellent! Grade: A")
else:
    print("Good effort! Keep improving.")

# Multiple conditions with logical operators
username = "admin"
password = "secret123"
is_authenticated = False

if username == "admin" and password == "secret123":
    is_authenticated = True
    print("Login successful!")
else:
    is_authenticated = False
    print("Invalid credentials!")

# Practical example: Even/Odd checker
number = 42

if number % 2 == 0:
    print(f"{number} is even")
else:
    print(f"{number} is odd")

# Boolean expression evaluation
is_weekend = True
has_plans = False

if is_weekend and not has_plans:
    print("Time to relax at home!")
else:
    print("Busy day ahead!")
```

## 🔀 Elif (Else-If) Chains

### Multiple Conditions

```python
# Grade calculator with multiple conditions
score = 87

if score >= 90:
    grade = "A"
    print("Outstanding performance!")
elif score >= 80:
    grade = "B"
    print("Great job!")
elif score >= 70:
    grade = "C"
    print("Good work!")
elif score >= 60:
    grade = "D"
    print("You passed, but consider studying more.")
else:
    grade = "F"
    print("Please retake the exam.")

print(f"Your grade is: {grade}")

# Weather recommendation system
temperature = 25  # Celsius
weather_condition = "sunny"

if temperature < 0:
    print("It's freezing! Stay inside and keep warm.")
elif temperature < 10:
    print("It's very cold. Wear heavy winter clothes.")
elif temperature < 20:
    print("It's cool. A jacket would be good.")
elif temperature < 30:
    if weather_condition == "sunny":
        print("Perfect weather! Great for outdoor activities.")
    elif weather_condition == "rainy":
        print("Pleasant temperature but bring an umbrella.")
    else:
        print("Nice temperature for a casual walk.")
else:
    print("It's hot! Stay hydrated and seek shade.")

# User input validation with multiple scenarios
def validate_age(age_input):
    """Validate age input with comprehensive checks."""
    
    # Check if input is a number
    try:
        age = int(age_input)
    except ValueError:
        return "Error: Age must be a number"
    
    # Validate age ranges
    if age < 0:
        return "Error: Age cannot be negative"
    elif age == 0:
        return "Welcome to the world, newborn!"
    elif age < 13:
        return f"You are {age} years old - enjoy your childhood!"
    elif age < 18:
        return f"You are {age} years old - teenage years!"
    elif age < 65:
        return f"You are {age} years old - adult"
    elif age < 100:
        return f"You are {age} years old - senior citizen"
    else:
        return f"Wow! {age} years old - that's amazing longevity!"

# Test age validation
test_ages = ["25", "abc", "-5", "0", "10", "16", "30", "70", "105"]
for age_str in test_ages:
    result = validate_age(age_str)
    print(f"Age '{age_str}': {result}")
```

### Complex Decision Trees

```python
# ATM transaction system
def process_atm_transaction(account_balance, transaction_type, amount, pin, correct_pin):
    """Process ATM transaction with multiple validation steps."""
    
    # Step 1: PIN validation
    if pin != correct_pin:
        return {
            'success': False,
            'message': 'Invalid PIN. Transaction denied.',
            'balance': account_balance
        }
    
    # Step 2: Transaction type validation
    if transaction_type not in ['withdraw', 'deposit', 'balance']:
        return {
            'success': False,
            'message': 'Invalid transaction type.',
            'balance': account_balance
        }
    
    # Step 3: Process based on transaction type
    if transaction_type == 'balance':
        return {
            'success': True,
            'message': f'Your current balance is ${account_balance:.2f}',
            'balance': account_balance
        }
    elif transaction_type == 'deposit':
        if amount <= 0:
            return {
                'success': False,
                'message': 'Deposit amount must be positive.',
                'balance': account_balance
            }
        elif amount > 10000:  # Daily deposit limit
            return {
                'success': False,
                'message': 'Daily deposit limit exceeded ($10,000).',
                'balance': account_balance
            }
        else:
            new_balance = account_balance + amount
            return {
                'success': True,
                'message': f'Deposited ${amount:.2f}. New balance: ${new_balance:.2f}',
                'balance': new_balance
            }
    elif transaction_type == 'withdraw':
        if amount <= 0:
            return {
                'success': False,
                'message': 'Withdrawal amount must be positive.',
                'balance': account_balance
            }
        elif amount > account_balance:
            return {
                'success': False,
                'message': 'Insufficient funds.',
                'balance': account_balance
            }
        elif amount > 500:  # Daily withdrawal limit
            return {
                'success': False,
                'message': 'Daily withdrawal limit exceeded ($500).',
                'balance': account_balance
            }
        else:
            new_balance = account_balance - amount
            return {
                'success': True,
                'message': f'Withdrew ${amount:.2f}. New balance: ${new_balance:.2f}',
                'balance': new_balance
            }

# Test ATM system
account_balance = 1000.00
correct_pin = "1234"

test_transactions = [
    ("1234", "balance", 0),
    ("1234", "deposit", 200),
    ("1234", "withdraw", 100),
    ("1234", "withdraw", 600),  # Exceeds limit
    ("wrong", "withdraw", 50),  # Wrong PIN
    ("1234", "withdraw", -10),  # Invalid amount
]

for pin, transaction_type, amount in test_transactions:
    result = process_atm_transaction(account_balance, transaction_type, amount, pin, correct_pin)
    print(f"Transaction: {transaction_type} ${amount}")
    print(f"Result: {result['message']}")
    if result['success']:
        account_balance = result['balance']
    print(f"Current balance: ${account_balance:.2f}\n")
```

## 🎯 Nested If Statements

### Multi-Level Decision Making

```python
# Student admission system with multiple criteria
def evaluate_admission(gpa, sat_score, extracurriculars, essay_score, has_recommendation):
    """Evaluate student admission with nested conditions."""
    
    admission_status = "Pending"
    scholarship_eligible = False
    
    # Primary GPA check
    if gpa >= 3.8:
        # High GPA students
        if sat_score >= 1400:
            # High GPA + High SAT
            admission_status = "Accepted"
            scholarship_eligible = True
            if extracurriculars >= 3 and essay_score >= 8:
                scholarship_eligible = "Full Scholarship"
            elif extracurriculars >= 2 or essay_score >= 7:
                scholarship_eligible = "Partial Scholarship"
        elif sat_score >= 1200:
            # High GPA + Medium SAT
            admission_status = "Accepted"
            if extracurriculars >= 2 and essay_score >= 7:
                scholarship_eligible = True
        else:
            # High GPA + Low SAT
            if extracurriculars >= 3 and essay_score >= 8 and has_recommendation:
                admission_status = "Accepted"
            else:
                admission_status = "Waitlisted"
    
    elif gpa >= 3.0:
        # Medium GPA students
        if sat_score >= 1300:
            # Medium GPA + High SAT
            admission_status = "Accepted"
            if extracurriculars >= 3 and essay_score >= 8:
                scholarship_eligible = True
        elif sat_score >= 1100:
            # Medium GPA + Medium SAT
            if extracurriculars >= 2 and essay_score >= 7 and has_recommendation:
                admission_status = "Accepted"
            else:
                admission_status = "Waitlisted"
        else:
            # Medium GPA + Low SAT
            admission_status = "Rejected"
    
    else:
        # Low GPA students
        if sat_score >= 1400 and extracurriculars >= 4 and essay_score >= 9:
            admission_status = "Waitlisted"
        else:
            admission_status = "Rejected"
    
    return {
        'status': admission_status,
        'scholarship': scholarship_eligible
    }

# Test admission system
students = [
    {"name": "Alice", "gpa": 3.9, "sat": 1450, "extra": 4, "essay": 9, "rec": True},
    {"name": "Bob", "gpa": 3.5, "sat": 1350, "extra": 2, "essay": 8, "rec": True},
    {"name": "Charlie", "gpa": 2.8, "sat": 1420, "extra": 5, "essay": 9, "rec": False},
    {"name": "Diana", "gpa": 3.2, "sat": 1050, "extra": 1, "essay": 6, "rec": False},
]

for student in students:
    result = evaluate_admission(
        student["gpa"], student["sat"], student["extra"], 
        student["essay"], student["rec"]
    )
    print(f"{student['name']}: {result['status']}")
    if result['scholarship']:
        print(f"  Scholarship: {result['scholarship']}")
    print()

# Game character stat system with nested conditions
def determine_character_class(strength, intelligence, agility, charisma):
    """Determine character class based on stats."""
    
    # Find primary and secondary stats
    stats = {
        'strength': strength,
        'intelligence': intelligence,
        'agility': agility,
        'charisma': charisma
    }
    
    sorted_stats = sorted(stats.items(), key=lambda x: x[1], reverse=True)
    primary_stat = sorted_stats[0]
    secondary_stat = sorted_stats[1]
    
    character_class = "Commoner"  # Default
    special_abilities = []
    
    # Determine class based on primary stat
    if primary_stat[0] == 'strength':
        if primary_stat[1] >= 15:
            if secondary_stat[0] == 'agility' and secondary_stat[1] >= 12:
                character_class = "Ranger"
                special_abilities = ["Dual Wield", "Nature Magic"]
            elif secondary_stat[0] == 'charisma' and secondary_stat[1] >= 12:
                character_class = "Paladin" 
                special_abilities = ["Divine Magic", "Leadership"]
            else:
                character_class = "Warrior"
                special_abilities = ["Heavy Armor", "Weapon Master"]
        else:
            character_class = "Fighter"
            special_abilities = ["Basic Combat"]
    
    elif primary_stat[0] == 'intelligence':
        if primary_stat[1] >= 15:
            if secondary_stat[0] == 'agility' and secondary_stat[1] >= 12:
                character_class = "Wizard"
                special_abilities = ["Elemental Magic", "Teleportation"]
            elif secondary_stat[0] == 'charisma' and secondary_stat[1] >= 12:
                character_class = "Sorcerer"
                special_abilities = ["Natural Magic", "Enchantment"]
            else:
                character_class = "Scholar"
                special_abilities = ["Research", "Alchemy"]
        else:
            character_class = "Apprentice"
            special_abilities = ["Basic Magic"]
    
    elif primary_stat[0] == 'agility':
        if primary_stat[1] >= 15:
            if secondary_stat[0] == 'intelligence' and secondary_stat[1] >= 12:
                character_class = "Assassin"
                special_abilities = ["Stealth", "Poison", "Critical Strike"]
            elif secondary_stat[0] == 'charisma' and secondary_stat[1] >= 12:
                character_class = "Bard"
                special_abilities = ["Music Magic", "Inspiration"]
            else:
                character_class = "Rogue"
                special_abilities = ["Lockpicking", "Stealth"]
        else:
            character_class = "Scout"
            special_abilities = ["Basic Stealth"]
    
    elif primary_stat[0] == 'charisma':
        if primary_stat[1] >= 15:
            if secondary_stat[0] == 'intelligence' and secondary_stat[1] >= 12:
                character_class = "Diplomat"
                special_abilities = ["Negotiation", "Leadership", "Politics"]
            elif secondary_stat[0] == 'strength' and secondary_stat[1] >= 12:
                character_class = "Knight"
                special_abilities = ["Honor Code", "Rally"]
            else:
                character_class = "Noble"
                special_abilities = ["Wealth", "Connections"]
        else:
            character_class = "Merchant"
            special_abilities = ["Trade"]
    
    return {
        'class': character_class,
        'abilities': special_abilities,
        'primary_stat': primary_stat,
        'secondary_stat': secondary_stat
    }

# Test character creation
characters = [
    {"name": "Conan", "str": 18, "int": 8, "agi": 12, "cha": 10},
    {"name": "Gandalf", "str": 10, "int": 18, "agi": 12, "cha": 16},
    {"name": "Legolas", "str": 14, "int": 12, "agi": 18, "cha": 14},
    {"name": "Aragorn", "str": 16, "int": 14, "agi": 15, "cha": 17},
]

for char in characters:
    result = determine_character_class(char["str"], char["int"], char["agi"], char["cha"])
    print(f"{char['name']}: {result['class']}")
    print(f"  Primary: {result['primary_stat'][0]} ({result['primary_stat'][1]})")
    print(f"  Abilities: {', '.join(result['abilities'])}")
    print()
```

## 🔀 Ternary Operator (Conditional Expression)

### Single-Line Conditionals

```python
# Basic ternary operator syntax: value_if_true if condition else value_if_false
age = 20
status = "adult" if age >= 18 else "minor"
print(f"Status: {status}")

# Multiple ternary operations
temperature = 85
weather_advice = ("Stay cool!" if temperature > 80 else 
                 "Perfect weather!" if temperature > 60 else 
                 "Bundle up!")
print(f"Weather advice: {weather_advice}")

# Ternary in function calls
def get_discount(is_member, purchase_amount):
    """Calculate discount using ternary operators."""
    base_discount = 0.1 if is_member else 0.05
    volume_bonus = 0.05 if purchase_amount > 100 else 0
    return base_discount + volume_bonus

# Ternary for default values
def greet_user(name=None):
    display_name = name if name else "Guest"
    return f"Hello, {display_name}!"

print(greet_user("Alice"))  # Hello, Alice!
print(greet_user())         # Hello, Guest!

# Complex ternary expressions
def analyze_number(num):
    """Analyze number properties using ternary operators."""
    sign = "positive" if num > 0 else "negative" if num < 0 else "zero"
    parity = "even" if num % 2 == 0 else "odd"
    magnitude = "large" if abs(num) > 100 else "small"
    
    return f"{num} is {sign}, {parity}, and {magnitude}"

numbers = [42, -17, 0, 150, -250]
for num in numbers:
    print(analyze_number(num))

# Ternary in list comprehensions
scores = [85, 92, 78, 96, 65, 88]
grades = ["Pass" if score >= 70 else "Fail" for score in scores]
print(f"Grades: {grades}")

# Nested ternary (use sparingly for readability)
def categorize_temperature(temp):
    """Categorize temperature with nested ternary."""
    return ("Hot" if temp > 85 else "Warm" if temp > 70 else 
            "Cool" if temp > 50 else "Cold")

temperatures = [95, 75, 60, 40]
for temp in temperatures:
    print(f"{temp}°F: {categorize_temperature(temp)}")
```

## 🎯 Practical Applications and Patterns

### Input Validation Patterns

```python
def validate_and_process_input():
    """Comprehensive input validation example."""
    
    while True:
        try:
            # Get user input
            user_input = input("Enter a positive number (or 'quit' to exit): ").strip()
            
            # Check for exit condition
            if user_input.lower() == 'quit':
                print("Goodbye!")
                break
            
            # Convert to number
            number = float(user_input)
            
            # Validate number
            if number < 0:
                print("Error: Number must be positive. Please try again.")
                continue
            elif number == 0:
                print("You entered zero. That's neither positive nor negative!")
                continue
            elif number > 1000000:
                print("Warning: That's a very large number!")
                # Continue processing despite warning
            
            # Process valid input
            if number.is_integer():
                number = int(number)
                if number % 2 == 0:
                    print(f"{number} is a positive even integer.")
                else:
                    print(f"{number} is a positive odd integer.")
            else:
                print(f"{number} is a positive decimal number.")
            
            # Additional analysis
            if number < 10:
                print("Single digit number!")
            elif number < 100:
                print("Double digit number!")
            else:
                print("Multi-digit number!")
            
            print()  # Empty line for readability
            
        except ValueError:
            print("Error: Please enter a valid number or 'quit'.")
        except KeyboardInterrupt:
            print("\nProgram interrupted. Goodbye!")
            break

# Menu-driven application pattern
def create_menu_system():
    """Example of menu-driven application with conditionals."""
    
    def show_menu():
        print("\n=== Calculator Menu ===")
        print("1. Addition")
        print("2. Subtraction") 
        print("3. Multiplication")
        print("4. Division")
        print("5. Power")
        print("6. Square Root")
        print("0. Exit")
        print("=" * 23)
    
    def get_numbers():
        """Get two numbers from user."""
        try:
            num1 = float(input("Enter first number: "))
            num2 = float(input("Enter second number: "))
            return num1, num2
        except ValueError:
            print("Error: Please enter valid numbers.")
            return None, None
    
    while True:
        show_menu()
        choice = input("Choose an option (0-6): ").strip()
        
        if choice == '0':
            print("Thank you for using the calculator!")
            break
        elif choice in ['1', '2', '3', '4', '5']:
            num1, num2 = get_numbers()
            if num1 is not None and num2 is not None:
                
                if choice == '1':
                    result = num1 + num2
                    operation = "addition"
                elif choice == '2':
                    result = num1 - num2
                    operation = "subtraction"
                elif choice == '3':
                    result = num1 * num2
                    operation = "multiplication"
                elif choice == '4':
                    if num2 != 0:
                        result = num1 / num2
                        operation = "division"
                    else:
                        print("Error: Cannot divide by zero!")
                        continue
                elif choice == '5':
                    result = num1 ** num2
                    operation = "exponentiation"
                
                print(f"Result of {operation}: {result}")
        
        elif choice == '6':
            try:
                num = float(input("Enter a number: "))
                if num >= 0:
                    result = num ** 0.5
                    print(f"Square root of {num}: {result}")
                else:
                    print("Error: Cannot take square root of negative number!")
            except ValueError:
                print("Error: Please enter a valid number.")
        
        else:
            print("Error: Invalid choice. Please try again.")

# Uncomment to run the menu system
# create_menu_system()
```

### State Machine Pattern

```python
class TrafficLight:
    """Traffic light state machine using conditionals."""
    
    def __init__(self):
        self.state = "RED"
        self.timer = 0
        self.red_duration = 30      # seconds
        self.yellow_duration = 5    # seconds  
        self.green_duration = 25    # seconds
    
    def update(self, seconds_elapsed):
        """Update traffic light state based on elapsed time."""
        self.timer += seconds_elapsed
        
        if self.state == "RED":
            if self.timer >= self.red_duration:
                self.state = "GREEN"
                self.timer = 0
                print("🟢 Traffic light changed to GREEN")
        
        elif self.state == "GREEN":
            if self.timer >= self.green_duration:
                self.state = "YELLOW"
                self.timer = 0
                print("🟡 Traffic light changed to YELLOW")
        
        elif self.state == "YELLOW":
            if self.timer >= self.yellow_duration:
                self.state = "RED"
                self.timer = 0
                print("🔴 Traffic light changed to RED")
    
    def get_status(self):
        """Get current status with time remaining."""
        if self.state == "RED":
            time_remaining = self.red_duration - self.timer
        elif self.state == "GREEN":
            time_remaining = self.green_duration - self.timer
        else:  # YELLOW
            time_remaining = self.yellow_duration - self.timer
        
        return f"Current: {self.state}, Time remaining: {time_remaining}s"
    
    def can_proceed(self, vehicle_type="car"):
        """Determine if vehicle can proceed based on current state."""
        if self.state == "GREEN":
            return True, "Proceed with caution"
        elif self.state == "YELLOW":
            if vehicle_type == "emergency":
                return True, "Emergency vehicle can proceed"
            elif self.timer < 2:  # Just turned yellow
                return False, "Stop if safe to do so"
            else:
                return False, "Stop - light about to turn red"
        else:  # RED
            if vehicle_type == "emergency":
                return True, "Emergency vehicle with sirens"
            else:
                return False, "Stop - red light"

# Simulate traffic light
traffic_light = TrafficLight()

# Simulate 2 minutes of operation
for second in range(0, 120, 5):  # Check every 5 seconds
    traffic_light.update(5)
    status = traffic_light.get_status()
    can_proceed, message = traffic_light.can_proceed()
    
    print(f"Time {second+5}s: {status}")
    print(f"  Can proceed: {can_proceed} - {message}")
    
    if second % 30 == 25:  # Check every 30 seconds
        print("-" * 50)
```

## ⚠️ Common Conditional Logic Pitfalls

### Pitfall 1: Assignment vs Comparison

```python
# Dangerous: Assignment instead of comparison
user_role = "admin"

# Wrong - this assigns, doesn't compare!
if user_role = "admin":  # SyntaxError: invalid syntax
    print("Admin access granted")

# Correct - comparison operator
if user_role == "admin":
    print("Admin access granted")

# Be careful with complex conditions
balance = 1000
withdrawal = 500

# Wrong logic - assignment in condition
if balance = balance - withdrawal:  # SyntaxError
    print("Withdrawal processed")

# Correct approach
if balance >= withdrawal:
    balance = balance - withdrawal
    print(f"Withdrawal processed. New balance: {balance}")
```

### Pitfall 2: Floating Point Comparison

```python
# Dangerous floating point comparison
price = 0.1 + 0.2  # 0.30000000000000004

if price == 0.3:  # False!
    print("Price is exactly 30 cents")
else:
    print("Price is not exactly 30 cents")

# Safe floating point comparison
import math

if math.isclose(price, 0.3):
    print("Price is approximately 30 cents")

# Or with tolerance
tolerance = 1e-10
if abs(price - 0.3) < tolerance:
    print("Price is close enough to 30 cents")
```

### Pitfall 3: Truthiness Confusion

```python
# Understanding Python's truthiness
values = [0, "", [], {}, None, False, "0", [0]]

print("Truthiness test:")
for value in values:
    if value:
        print(f"{repr(value)} is truthy")
    else:
        print(f"{repr(value)} is falsy")

# Common mistake: checking for empty collections
def process_data(data_list):
    # Wrong - this fails if data_list is [0] or [False]
    if data_list:
        print("Processing data...")
    
    # Better - explicitly check for None or length
    if data_list is not None and len(data_list) > 0:
        print("Processing data...")
    
    # Or check the specific condition you care about
    if data_list and any(item is not None for item in data_list):
        print("Processing non-None data...")

# Testing edge cases
test_lists = [[], [0], [False], [""], [None], None]
for test_list in test_lists:
    print(f"Testing {test_list}:")
    if test_list is not None:
        process_data(test_list)
    print()
```

## 🎯 Practice Exercises

### Exercise 1: Grade Calculator

```python
def calculate_final_grade(homework_avg, quiz_avg, midterm, final_exam, participation):
    """
    Calculate final grade based on weighted components:
    - Homework: 25%
    - Quizzes: 25% 
    - Midterm: 20%
    - Final Exam: 25%
    - Participation: 5%
    
    Implement grade boundaries and special cases.
    """
    # Your implementation here
    pass

# Test cases
students = [
    ("Alice", 95, 88, 92, 89, 95),
    ("Bob", 78, 82, 75, 80, 85),
    ("Charlie", 65, 70, 68, 72, 60),
]
```

### Exercise 2: Password Strength Validator

```python
def validate_password_strength(password):
    """
    Validate password strength with multiple criteria:
    - Length (8-128 characters)
    - Must contain uppercase, lowercase, digit, special character
    - Cannot contain common patterns
    - Return strength score and feedback
    """
    # Your implementation here
    pass

# Test passwords
passwords = [
    "password123",
    "MySecureP@ssw0rd!",
    "abc",
    "ALLUPPERCASE123!",
    "nouppercase123!",
]
```

### Exercise 3: Smart Thermostat Logic

```python
class SmartThermostat:
    """
    Smart thermostat with complex decision logic.
    Consider: current temp, target temp, time of day, occupancy, energy mode
    """
    
    def __init__(self, target_temp=72):
        self.target_temp = target_temp
        self.current_temp = 70
        self.mode = "auto"  # auto, heat, cool, off
        self.energy_saving = False
        
    def should_heat(self, current_time, is_occupied):
        """Determine if heating should turn on."""
        # Your implementation here
        pass
    
    def should_cool(self, current_time, is_occupied):
        """Determine if cooling should turn on."""
        # Your implementation here
        pass
```

## 📚 Summary and Best Practices

### Key Takeaways
1. **Use clear, readable conditions**: Avoid overly complex boolean expressions
2. **Handle edge cases**: Consider all possible input scenarios
3. **Avoid deep nesting**: Refactor complex nested conditions into functions
4. **Use early returns**: Reduce nesting with guard clauses
5. **Be explicit with comparisons**: Use `is` for None, `==` for values
6. **Test boundary conditions**: Always test edge cases and limits

### Best Practices Checklist
- [ ] Use parentheses to clarify complex boolean expressions
- [ ] Prefer `is` and `is not` for None comparisons
- [ ] Use `elif` instead of multiple `if` statements when appropriate
- [ ] Handle floating point comparisons with tolerance
- [ ] Consider using ternary operators for simple conditionals
- [ ] Validate input at the beginning of functions
- [ ] Use meaningful variable names for boolean expressions

### Decision-Making Patterns
1. **Guard Clauses**: Handle invalid cases first and return early
2. **Switch Alternatives**: Use dictionaries for complex mappings
3. **State Machines**: Use classes for complex state-dependent logic
4. **Chain of Responsibility**: Break complex decisions into smaller functions

### Next Steps
After mastering conditional statements:
1. Learn about [Loops (For/While)](./08-loops-for-while.md)
2. Practice implementing complex decision trees
3. Study state machine patterns
4. Explore functional programming alternatives to conditionals

---

**Remember**: Clean conditional logic is essential for maintainable code. Always prioritize readability and handle edge cases thoughtfully!
