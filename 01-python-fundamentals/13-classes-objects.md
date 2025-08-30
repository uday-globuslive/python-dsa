# Classes and Objects

## 🎯 Objective
Master Python's object-oriented programming paradigm, including class definition, object creation, inheritance, encapsulation, polymorphism, and advanced OOP concepts essential for building scalable and maintainable applications.

## 📖 Overview

Object-Oriented Programming (OOP) is a programming paradigm that organizes code into classes and objects, promoting code reusability, modularity, and maintainability. Python's OOP implementation provides powerful features for modeling real-world entities and creating robust software architectures essential for complex problem-solving.

## 📝 Class Basics and Object Creation

### Basic Class Definition

```python
# Simple class definition
class Person:
    """A simple Person class demonstrating basic OOP concepts."""
    
    # Class variables (shared by all instances)
    species = "Homo sapiens"
    population = 0
    
    def __init__(self, name, age):
        """
        Initialize a Person instance.
        
        Args:
            name (str): The person's name
            age (int): The person's age
        """
        # Instance variables (unique to each instance)
        self.name = name
        self.age = age
        self.is_alive = True
        
        # Update class variable
        Person.population += 1
    
    def introduce(self):
        """Return a self-introduction."""
        return f"Hi, I'm {self.name} and I'm {self.age} years old."
    
    def have_birthday(self):
        """Celebrate a birthday by increasing age."""
        self.age += 1
        print(f"Happy birthday {self.name}! You're now {self.age}.")
    
    def is_adult(self):
        """Check if person is an adult."""
        return self.age >= 18
    
    def __str__(self):
        """String representation of the object."""
        return f"Person(name='{self.name}', age={self.age})"
    
    def __repr__(self):
        """Developer-friendly representation of the object."""
        return f"Person('{self.name}', {self.age})"

# Creating and using objects
print("=== Basic Class Usage ===")

# Create instances
person1 = Person("Alice", 25)
person2 = Person("Bob", 17)

# Access instance attributes
print(f"Person 1: {person1.name}, Age: {person1.age}")
print(f"Person 2: {person2.name}, Age: {person2.age}")

# Call instance methods
print(person1.introduce())
print(person2.introduce())

# Check adult status
print(f"{person1.name} is adult: {person1.is_adult()}")
print(f"{person2.name} is adult: {person2.is_adult()}")

# Access class variables
print(f"Species: {person1.species}")
print(f"Population: {Person.population}")

# Have a birthday
person2.have_birthday()
print(f"{person2.name} is now adult: {person2.is_adult()}")

# String representations
print(f"str(person1): {str(person1)}")
print(f"repr(person1): {repr(person1)}")

# Class vs instance attributes
print(f"\nClass attribute via class: {Person.species}")
print(f"Class attribute via instance: {person1.species}")

# Modifying class attribute
Person.species = "Human"
print(f"Modified species: {person1.species}, {person2.species}")

# Instance-specific modification (creates instance attribute)
person1.species = "Superhuman"
print(f"person1 species: {person1.species}")
print(f"person2 species: {person2.species}")
print(f"Class species: {Person.species}")
```

### Instance and Class Methods

```python
class BankAccount:
    """A bank account class demonstrating different method types."""
    
    # Class variables
    bank_name = "Python Bank"
    interest_rate = 0.02
    total_accounts = 0
    
    def __init__(self, account_holder, initial_balance=0):
        """Initialize a bank account."""
        self.account_holder = account_holder
        self.balance = initial_balance
        self.account_number = f"ACC{BankAccount.total_accounts + 1:06d}"
        self.transaction_history = []
        
        # Update class variable
        BankAccount.total_accounts += 1
        
        # Log initial deposit
        if initial_balance > 0:
            self._log_transaction("Initial Deposit", initial_balance)
    
    # Instance methods
    def deposit(self, amount):
        """Deposit money into the account."""
        if amount <= 0:
            raise ValueError("Deposit amount must be positive")
        
        self.balance += amount
        self._log_transaction("Deposit", amount)
        return self.balance
    
    def withdraw(self, amount):
        """Withdraw money from the account."""
        if amount <= 0:
            raise ValueError("Withdrawal amount must be positive")
        
        if amount > self.balance:
            raise ValueError("Insufficient funds")
        
        self.balance -= amount
        self._log_transaction("Withdrawal", -amount)
        return self.balance
    
    def get_balance(self):
        """Get current balance."""
        return self.balance
    
    def _log_transaction(self, transaction_type, amount):
        """Private method to log transactions."""
        import datetime
        transaction = {
            "type": transaction_type,
            "amount": amount,
            "timestamp": datetime.datetime.now(),
            "balance_after": self.balance
        }
        self.transaction_history.append(transaction)
    
    def get_statement(self):
        """Get account statement."""
        statement = f"Account Statement for {self.account_holder}\n"
        statement += f"Account Number: {self.account_number}\n"
        statement += f"Current Balance: ${self.balance:.2f}\n\n"
        statement += "Transaction History:\n"
        
        for transaction in self.transaction_history:
            statement += f"{transaction['timestamp'].strftime('%Y-%m-%d %H:%M:%S')} - "
            statement += f"{transaction['type']}: ${transaction['amount']:.2f} "
            statement += f"(Balance: ${transaction['balance_after']:.2f})\n"
        
        return statement
    
    # Class methods
    @classmethod
    def get_bank_info(cls):
        """Get information about the bank."""
        return f"{cls.bank_name} - Total Accounts: {cls.total_accounts}"
    
    @classmethod
    def set_interest_rate(cls, new_rate):
        """Set the interest rate for all accounts."""
        if not 0 <= new_rate <= 1:
            raise ValueError("Interest rate must be between 0 and 1")
        cls.interest_rate = new_rate
    
    @classmethod
    def create_savings_account(cls, account_holder, initial_balance=100):
        """Factory method to create a savings account with minimum balance."""
        if initial_balance < 100:
            raise ValueError("Savings account requires minimum $100")
        return cls(account_holder, initial_balance)
    
    # Static methods
    @staticmethod
    def calculate_compound_interest(principal, rate, time, compounds_per_year=12):
        """Calculate compound interest."""
        return principal * (1 + rate / compounds_per_year) ** (compounds_per_year * time)
    
    @staticmethod
    def is_valid_account_number(account_number):
        """Validate account number format."""
        return (account_number.startswith("ACC") and 
                len(account_number) == 9 and 
                account_number[3:].isdigit())
    
    def apply_interest(self):
        """Apply interest to the account balance."""
        interest = self.balance * self.interest_rate
        self.balance += interest
        self._log_transaction("Interest", interest)
        return interest
    
    def __str__(self):
        """String representation."""
        return f"BankAccount({self.account_holder}, ${self.balance:.2f})"
    
    def __repr__(self):
        """Developer representation."""
        return f"BankAccount('{self.account_holder}', {self.balance})"

# Test bank account class
print("\n=== Bank Account Class ===")

# Create accounts
account1 = BankAccount("Alice Johnson", 1000)
account2 = BankAccount.create_savings_account("Bob Smith", 500)

print(f"Account 1: {account1}")
print(f"Account 2: {account2}")

# Use instance methods
account1.deposit(200)
account1.withdraw(50)
account2.deposit(100)

print(f"Alice's balance: ${account1.get_balance():.2f}")
print(f"Bob's balance: ${account2.get_balance():.2f}")

# Use class methods
print(f"Bank info: {BankAccount.get_bank_info()}")

# Change interest rate for all accounts
BankAccount.set_interest_rate(0.03)
print(f"New interest rate: {BankAccount.interest_rate}")

# Apply interest
alice_interest = account1.apply_interest()
bob_interest = account2.apply_interest()

print(f"Alice earned ${alice_interest:.2f} in interest")
print(f"Bob earned ${bob_interest:.2f} in interest")

# Use static methods
future_value = BankAccount.calculate_compound_interest(1000, 0.05, 2)
print(f"$1000 at 5% for 2 years: ${future_value:.2f}")

print(f"Valid account number 'ACC000001': {BankAccount.is_valid_account_number('ACC000001')}")
print(f"Valid account number 'INVALID': {BankAccount.is_valid_account_number('INVALID')}")

# Get statement
print(f"\n{account1.get_statement()}")
```

### Properties and Descriptors

```python
class Temperature:
    """Temperature class demonstrating properties and validation."""
    
    def __init__(self, celsius=0):
        """Initialize temperature in Celsius."""
        self._celsius = None
        self.celsius = celsius  # Use property setter for validation
    
    @property
    def celsius(self):
        """Get temperature in Celsius."""
        return self._celsius
    
    @celsius.setter
    def celsius(self, value):
        """Set temperature in Celsius with validation."""
        if not isinstance(value, (int, float)):
            raise TypeError("Temperature must be a number")
        
        if value < -273.15:
            raise ValueError("Temperature cannot be below absolute zero (-273.15°C)")
        
        self._celsius = value
    
    @property
    def fahrenheit(self):
        """Get temperature in Fahrenheit."""
        return (self._celsius * 9/5) + 32
    
    @fahrenheit.setter
    def fahrenheit(self, value):
        """Set temperature in Fahrenheit."""
        if not isinstance(value, (int, float)):
            raise TypeError("Temperature must be a number")
        
        celsius_equivalent = (value - 32) * 5/9
        self.celsius = celsius_equivalent  # Use celsius setter for validation
    
    @property
    def kelvin(self):
        """Get temperature in Kelvin."""
        return self._celsius + 273.15
    
    @kelvin.setter
    def kelvin(self, value):
        """Set temperature in Kelvin."""
        if not isinstance(value, (int, float)):
            raise TypeError("Temperature must be a number")
        
        celsius_equivalent = value - 273.15
        self.celsius = celsius_equivalent  # Use celsius setter for validation
    
    def __str__(self):
        """String representation."""
        return f"{self._celsius:.1f}°C"
    
    def __repr__(self):
        """Developer representation."""
        return f"Temperature({self._celsius})"

# Custom descriptor class
class ValidatedAttribute:
    """A descriptor that validates attribute values."""
    
    def __init__(self, validation_func, error_msg="Invalid value"):
        self.validation_func = validation_func
        self.error_msg = error_msg
        self.value = None
    
    def __get__(self, obj, objtype=None):
        """Get the attribute value."""
        if obj is None:
            return self
        return getattr(obj, self.private_name, None)
    
    def __set__(self, obj, value):
        """Set the attribute value with validation."""
        if not self.validation_func(value):
            raise ValueError(self.error_msg)
        setattr(obj, self.private_name, value)
    
    def __set_name__(self, owner, name):
        """Called when the descriptor is assigned to a class attribute."""
        self.private_name = f'_{name}'

class Person:
    """Person class using descriptors for validation."""
    
    # Using descriptors for validation
    name = ValidatedAttribute(
        lambda x: isinstance(x, str) and len(x.strip()) > 0,
        "Name must be a non-empty string"
    )
    
    age = ValidatedAttribute(
        lambda x: isinstance(x, int) and 0 <= x <= 150,
        "Age must be an integer between 0 and 150"
    )
    
    email = ValidatedAttribute(
        lambda x: isinstance(x, str) and '@' in x and '.' in x,
        "Email must contain @ and . characters"
    )
    
    def __init__(self, name, age, email):
        """Initialize person with validated attributes."""
        self.name = name
        self.age = age
        self.email = email
    
    def __str__(self):
        """String representation."""
        return f"Person(name='{self.name}', age={self.age}, email='{self.email}')"

# Test properties and descriptors
print("\n=== Properties and Descriptors ===")

# Temperature properties
temp = Temperature(25)
print(f"Temperature: {temp}")
print(f"Celsius: {temp.celsius}°C")
print(f"Fahrenheit: {temp.fahrenheit}°F")
print(f"Kelvin: {temp.kelvin}K")

# Set temperature in different units
temp.fahrenheit = 86
print(f"After setting to 86°F: {temp}")

temp.kelvin = 300
print(f"After setting to 300K: {temp}")

# Test validation
try:
    temp.celsius = -300  # Below absolute zero
except ValueError as e:
    print(f"Validation error: {e}")

# Test descriptors
try:
    person = Person("Alice", 25, "alice@example.com")
    print(f"Valid person: {person}")
    
    # Test validation
    person.age = 30  # Valid
    print(f"Updated age: {person}")
    
    person.age = -5  # Invalid
except ValueError as e:
    print(f"Descriptor validation error: {e}")

# Property with caching
class CachedProperty:
    """Property that caches expensive computations."""
    
    def __init__(self, func):
        self.func = func
        self.cached_value = None
        self.cached = False
    
    def __get__(self, obj, objtype=None):
        if obj is None:
            return self
        
        if not self.cached:
            self.cached_value = self.func(obj)
            self.cached = True
            print(f"Computing {self.func.__name__}...")
        else:
            print(f"Using cached {self.func.__name__}...")
        
        return self.cached_value
    
    def __set__(self, obj, value):
        """Reset cache when property is set."""
        self.cached_value = value
        self.cached = True

class DataProcessor:
    """Class demonstrating cached properties."""
    
    def __init__(self, data):
        self.data = data
        self._expensive_computation = CachedProperty(self._compute_expensive_result)
    
    def _compute_expensive_result(self):
        """Simulate expensive computation."""
        import time
        time.sleep(0.1)  # Simulate delay
        return sum(x**2 for x in self.data)
    
    @property
    def expensive_computation(self):
        """Access the cached property."""
        return self._expensive_computation.__get__(self, DataProcessor)

# Test cached property
print("\n=== Cached Properties ===")
processor = DataProcessor([1, 2, 3, 4, 5])

# First access - computes
result1 = processor.expensive_computation
print(f"Result: {result1}")

# Second access - uses cache
result2 = processor.expensive_computation
print(f"Result: {result2}")
```

## 🔍 Inheritance and Polymorphism

### Single Inheritance

```python
# Base class
class Animal:
    """Base class for all animals."""
    
    def __init__(self, name, species):
        """Initialize an animal."""
        self.name = name
        self.species = species
        self.is_alive = True
    
    def speak(self):
        """Make a sound (to be overridden by subclasses)."""
        return "Some generic animal sound"
    
    def eat(self, food):
        """Eat food."""
        return f"{self.name} is eating {food}"
    
    def sleep(self):
        """Sleep."""
        return f"{self.name} is sleeping"
    
    def __str__(self):
        """String representation."""
        return f"{self.species} named {self.name}"

# Derived classes
class Dog(Animal):
    """Dog class inheriting from Animal."""
    
    def __init__(self, name, breed):
        """Initialize a dog."""
        super().__init__(name, "Dog")  # Call parent constructor
        self.breed = breed
        self.tricks = []
    
    def speak(self):
        """Override the speak method."""
        return "Woof! Woof!"
    
    def fetch(self, item):
        """Dog-specific behavior."""
        return f"{self.name} fetches the {item}"
    
    def learn_trick(self, trick):
        """Learn a new trick."""
        if trick not in self.tricks:
            self.tricks.append(trick)
            return f"{self.name} learned to {trick}!"
        return f"{self.name} already knows how to {trick}"
    
    def perform_tricks(self):
        """Perform all known tricks."""
        if not self.tricks:
            return f"{self.name} doesn't know any tricks yet"
        
        return f"{self.name} performs: {', '.join(self.tricks)}"

class Cat(Animal):
    """Cat class inheriting from Animal."""
    
    def __init__(self, name, indoor=True):
        """Initialize a cat."""
        super().__init__(name, "Cat")
        self.indoor = indoor
        self.lives_remaining = 9
    
    def speak(self):
        """Override the speak method."""
        return "Meow!"
    
    def purr(self):
        """Cat-specific behavior."""
        return f"{self.name} is purring contentedly"
    
    def climb(self, location):
        """Climb to a location."""
        return f"{self.name} climbs up the {location}"
    
    def use_life(self):
        """Use one of the cat's nine lives."""
        if self.lives_remaining > 0:
            self.lives_remaining -= 1
            return f"{self.name} used a life! {self.lives_remaining} lives remaining"
        return f"{self.name} has no lives left!"

class Bird(Animal):
    """Bird class inheriting from Animal."""
    
    def __init__(self, name, species, can_fly=True):
        """Initialize a bird."""
        super().__init__(name, species)
        self.can_fly = can_fly
        self.altitude = 0
    
    def speak(self):
        """Override the speak method."""
        return "Tweet! Tweet!"
    
    def fly(self, height):
        """Fly to a certain height."""
        if not self.can_fly:
            return f"{self.name} cannot fly"
        
        self.altitude = height
        return f"{self.name} flies to {height} feet"
    
    def land(self):
        """Land on the ground."""
        self.altitude = 0
        return f"{self.name} lands on the ground"

# Test inheritance
print("=== Inheritance ===")

# Create instances
dog = Dog("Buddy", "Golden Retriever")
cat = Cat("Whiskers", indoor=True)
bird = Bird("Tweety", "Canary")

# Test inherited methods
animals = [dog, cat, bird]

print("All animals:")
for animal in animals:
    print(f"  {animal}")

print("\nEach animal speaks:")
for animal in animals:
    print(f"  {animal.name}: {animal.speak()}")

print("\nAll animals eating:")
for animal in animals:
    print(f"  {animal.eat('food')}")

# Test specific methods
print(f"\nDog specific: {dog.fetch('ball')}")
print(f"Cat specific: {cat.purr()}")
print(f"Bird specific: {bird.fly(100)}")

# Test method inheritance and overriding
print(f"\nDog tricks:")
print(f"  {dog.learn_trick('sit')}")
print(f"  {dog.learn_trick('stay')}")
print(f"  {dog.learn_trick('roll over')}")
print(f"  {dog.perform_tricks()}")

# Test isinstance and issubclass
print(f"\nType checking:")
print(f"  dog is Animal: {isinstance(dog, Animal)}")
print(f"  dog is Dog: {isinstance(dog, Dog)}")
print(f"  Dog is subclass of Animal: {issubclass(Dog, Animal)}")
print(f"  Animal is subclass of Dog: {issubclass(Animal, Dog)}")

# Method Resolution Order (MRO)
print(f"\nDog MRO: {Dog.__mro__}")
```

### Multiple Inheritance and Mixins

```python
# Mixin classes for shared functionality
class FlyingMixin:
    """Mixin for flying capabilities."""
    
    def __init__(self):
        self.altitude = 0
        self.max_altitude = 1000
    
    def take_off(self):
        """Take off into the air."""
        if self.altitude == 0:
            self.altitude = 10
            return f"{self.name} takes off!"
        return f"{self.name} is already flying"
    
    def fly_to(self, altitude):
        """Fly to a specific altitude."""
        if altitude > self.max_altitude:
            return f"{self.name} cannot fly that high (max: {self.max_altitude}ft)"
        
        self.altitude = altitude
        return f"{self.name} flies to {altitude}ft"
    
    def land(self):
        """Land on the ground."""
        if self.altitude > 0:
            self.altitude = 0
            return f"{self.name} lands safely"
        return f"{self.name} is already on the ground"

class SwimmingMixin:
    """Mixin for swimming capabilities."""
    
    def __init__(self):
        self.depth = 0
        self.max_depth = 100
    
    def dive(self, depth):
        """Dive to a specific depth."""
        if depth > self.max_depth:
            return f"{self.name} cannot dive that deep (max: {self.max_depth}ft)"
        
        self.depth = depth
        return f"{self.name} dives to {depth}ft depth"
    
    def surface(self):
        """Return to the surface."""
        if self.depth > 0:
            self.depth = 0
            return f"{self.name} surfaces"
        return f"{self.name} is already at the surface"
    
    def swim(self, direction):
        """Swim in a direction."""
        return f"{self.name} swims {direction}"

class TalkingMixin:
    """Mixin for talking capabilities."""
    
    def __init__(self):
        self.vocabulary = []
    
    def learn_word(self, word):
        """Learn a new word."""
        if word not in self.vocabulary:
            self.vocabulary.append(word)
            return f"{self.name} learned the word '{word}'"
        return f"{self.name} already knows '{word}'"
    
    def say(self, phrase):
        """Say a phrase."""
        return f"{self.name} says: '{phrase}'"
    
    def get_vocabulary_size(self):
        """Get the size of vocabulary."""
        return len(self.vocabulary)

# Base animal class
class AdvancedAnimal:
    """Advanced animal base class."""
    
    def __init__(self, name, species):
        self.name = name
        self.species = species
        # Call mixin constructors
        super().__init__()
    
    def __str__(self):
        return f"{self.species} named {self.name}"

# Multiple inheritance with mixins
class Duck(AdvancedAnimal, FlyingMixin, SwimmingMixin):
    """Duck that can fly and swim."""
    
    def __init__(self, name):
        super().__init__(name, "Duck")
        self.max_altitude = 500  # Override flying mixin
        self.max_depth = 20      # Override swimming mixin
    
    def quack(self):
        """Duck-specific sound."""
        return f"{self.name} says: Quack!"
    
    def migrate(self, destination):
        """Migrate to a destination."""
        return f"{self.name} migrates to {destination}"

class Parrot(AdvancedAnimal, FlyingMixin, TalkingMixin):
    """Parrot that can fly and talk."""
    
    def __init__(self, name, species="Parrot"):
        super().__init__(name, species)
        self.max_altitude = 800
    
    def mimic(self, sound):
        """Mimic a sound."""
        return f"{self.name} mimics: '{sound}'"

class Penguin(AdvancedAnimal, SwimmingMixin):
    """Penguin that can swim but not fly."""
    
    def __init__(self, name):
        super().__init__(name, "Penguin")
        self.max_depth = 200  # Penguins are excellent divers
    
    def slide(self):
        """Slide on ice."""
        return f"{self.name} slides on the ice"
    
    def huddle(self, group_size):
        """Huddle for warmth."""
        return f"{self.name} huddles with {group_size} other penguins"

class Dragon(AdvancedAnimal, FlyingMixin, TalkingMixin):
    """Mythical dragon that can fly and talk."""
    
    def __init__(self, name, color="red"):
        super().__init__(name, "Dragon")
        self.color = color
        self.max_altitude = 5000  # Dragons fly very high
        self.treasure = 0
    
    def breathe_fire(self):
        """Breathe fire."""
        return f"{self.name} breathes a stream of fire!"
    
    def hoard_treasure(self, amount):
        """Add treasure to hoard."""
        self.treasure += amount
        return f"{self.name} adds {amount} gold to the hoard (total: {self.treasure})"

# Test multiple inheritance
print("\n=== Multiple Inheritance ===")

# Create instances
duck = Duck("Donald")
parrot = Parrot("Polly")
penguin = Penguin("Pingu")
dragon = Dragon("Smaug", "gold")

# Test flying animals
flying_animals = [duck, parrot, dragon]
print("Flying animals:")
for animal in flying_animals:
    print(f"  {animal}")
    print(f"    {animal.take_off()}")
    print(f"    {animal.fly_to(100)}")

# Test swimming animals
swimming_animals = [duck, penguin]
print("\nSwimming animals:")
for animal in swimming_animals:
    print(f"  {animal}")
    print(f"    {animal.dive(50)}")
    print(f"    {animal.swim('north')}")

# Test talking animals
talking_animals = [parrot, dragon]
print("\nTalking animals:")
for animal in talking_animals:
    print(f"  {animal}")
    print(f"    {animal.learn_word('hello')}")
    print(f"    {animal.say('How are you?')}")

# Test specific behaviors
print(f"\nSpecific behaviors:")
print(f"  {duck.quack()}")
print(f"  {parrot.mimic('telephone ring')}")
print(f"  {penguin.slide()}")
print(f"  {dragon.breathe_fire()}")
print(f"  {dragon.hoard_treasure(1000)}")

# Check method resolution order
print(f"\nDuck MRO: {Duck.__mro__}")
print(f"Dragon MRO: {Dragon.__mro__}")

# Diamond problem example
class A:
    def method(self):
        return "A"

class B(A):
    def method(self):
        return "B -> " + super().method()

class C(A):
    def method(self):
        return "C -> " + super().method()

class D(B, C):
    def method(self):
        return "D -> " + super().method()

# Test diamond inheritance
print(f"\nDiamond inheritance:")
d = D()
print(f"  D().method(): {d.method()}")
print(f"  D MRO: {D.__mro__}")
```

### Polymorphism and Abstract Classes

```python
from abc import ABC, abstractmethod

# Abstract base class
class Shape(ABC):
    """Abstract base class for all shapes."""
    
    def __init__(self, name):
        self.name = name
    
    @abstractmethod
    def area(self):
        """Calculate the area of the shape."""
        pass
    
    @abstractmethod
    def perimeter(self):
        """Calculate the perimeter of the shape."""
        pass
    
    def describe(self):
        """Describe the shape."""
        return f"This is a {self.name} with area {self.area():.2f} and perimeter {self.perimeter():.2f}"
    
    def __str__(self):
        return f"{self.name}"

# Concrete implementations
class Rectangle(Shape):
    """Rectangle implementation."""
    
    def __init__(self, width, height):
        super().__init__("Rectangle")
        self.width = width
        self.height = height
    
    def area(self):
        """Calculate rectangle area."""
        return self.width * self.height
    
    def perimeter(self):
        """Calculate rectangle perimeter."""
        return 2 * (self.width + self.height)
    
    def __str__(self):
        return f"Rectangle({self.width}x{self.height})"

class Circle(Shape):
    """Circle implementation."""
    
    def __init__(self, radius):
        super().__init__("Circle")
        self.radius = radius
        self.pi = 3.14159
    
    def area(self):
        """Calculate circle area."""
        return self.pi * self.radius ** 2
    
    def perimeter(self):
        """Calculate circle circumference."""
        return 2 * self.pi * self.radius
    
    def __str__(self):
        return f"Circle(radius={self.radius})"

class Triangle(Shape):
    """Triangle implementation."""
    
    def __init__(self, side1, side2, side3):
        super().__init__("Triangle")
        self.side1 = side1
        self.side2 = side2
        self.side3 = side3
        
        # Validate triangle inequality
        if not (side1 + side2 > side3 and 
                side2 + side3 > side1 and 
                side1 + side3 > side2):
            raise ValueError("Invalid triangle: sides don't satisfy triangle inequality")
    
    def area(self):
        """Calculate triangle area using Heron's formula."""
        s = self.perimeter() / 2  # Semi-perimeter
        return (s * (s - self.side1) * (s - self.side2) * (s - self.side3)) ** 0.5
    
    def perimeter(self):
        """Calculate triangle perimeter."""
        return self.side1 + self.side2 + self.side3
    
    def __str__(self):
        return f"Triangle({self.side1}, {self.side2}, {self.side3})"

# Polymorphism demonstration
def calculate_total_area(shapes):
    """Calculate total area of a list of shapes."""
    total = 0
    for shape in shapes:
        total += shape.area()  # Polymorphic call
    return total

def print_shape_info(shapes):
    """Print information about shapes."""
    for shape in shapes:
        print(f"  {shape}: {shape.describe()}")

# Test polymorphism
print("=== Polymorphism and Abstract Classes ===")

# Create different shapes
rectangle = Rectangle(5, 3)
circle = Circle(4)
triangle = Triangle(3, 4, 5)

shapes = [rectangle, circle, triangle]

print("Shape information:")
print_shape_info(shapes)

total_area = calculate_total_area(shapes)
print(f"\nTotal area of all shapes: {total_area:.2f}")

# Try to create abstract shape (this will fail)
try:
    abstract_shape = Shape("Abstract")  # This will raise TypeError
except TypeError as e:
    print(f"\nCannot instantiate abstract class: {e}")

# Protocol-based polymorphism (Duck Typing)
class Duck:
    """Duck class for duck typing demonstration."""
    
    def quack(self):
        return "Quack!"
    
    def fly(self):
        return "Duck is flying"

class Robot:
    """Robot class that quacks and flies like a duck."""
    
    def quack(self):
        return "Beep! (robot quack)"
    
    def fly(self):
        return "Robot jetpack activated"

class Airplane:
    """Airplane that only flies."""
    
    def fly(self):
        return "Airplane soaring through the sky"

def make_it_quack_and_fly(duck_like_object):
    """Function that works with duck-like objects."""
    results = []
    
    # Try to make it quack
    if hasattr(duck_like_object, 'quack'):
        results.append(duck_like_object.quack())
    else:
        results.append(f"{type(duck_like_object).__name__} cannot quack")
    
    # Try to make it fly
    if hasattr(duck_like_object, 'fly'):
        results.append(duck_like_object.fly())
    else:
        results.append(f"{type(duck_like_object).__name__} cannot fly")
    
    return results

# Test duck typing
print("\n=== Duck Typing ===")

duck = Duck()
robot = Robot()
airplane = Airplane()

duck_like_objects = [duck, robot, airplane]

for obj in duck_like_objects:
    results = make_it_quack_and_fly(obj)
    print(f"{type(obj).__name__}:")
    for result in results:
        print(f"  {result}")

# Interface using protocols (Python 3.8+)
try:
    from typing import Protocol
    
    class Drawable(Protocol):
        """Protocol for drawable objects."""
        
        def draw(self) -> str:
            """Draw the object."""
            pass
        
        def get_bounds(self) -> tuple:
            """Get bounding rectangle."""
            pass
    
    class DrawableRectangle:
        """Rectangle that implements Drawable protocol."""
        
        def __init__(self, x, y, width, height):
            self.x = x
            self.y = y
            self.width = width
            self.height = height
        
        def draw(self) -> str:
            return f"Drawing rectangle at ({self.x}, {self.y})"
        
        def get_bounds(self) -> tuple:
            return (self.x, self.y, self.width, self.height)
    
    class DrawableCircle:
        """Circle that implements Drawable protocol."""
        
        def __init__(self, x, y, radius):
            self.x = x
            self.y = y
            self.radius = radius
        
        def draw(self) -> str:
            return f"Drawing circle at ({self.x}, {self.y})"
        
        def get_bounds(self) -> tuple:
            return (self.x - self.radius, self.y - self.radius, 
                   2 * self.radius, 2 * self.radius)
    
    def draw_objects(drawables: list[Drawable]):
        """Draw a list of drawable objects."""
        for drawable in drawables:
            print(f"  {drawable.draw()}")
            print(f"    Bounds: {drawable.get_bounds()}")
    
    # Test protocols
    print("\n=== Protocols ===")
    drawable_rect = DrawableRectangle(10, 20, 50, 30)
    drawable_circle = DrawableCircle(100, 100, 25)
    
    drawables = [drawable_rect, drawable_circle]
    draw_objects(drawables)

except ImportError:
    print("\n=== Protocols not available (Python < 3.8) ===")
```

## 🔧 Advanced OOP Concepts

### Special Methods (Magic Methods)

```python
class Vector:
    """2D Vector class demonstrating special methods."""
    
    def __init__(self, x, y):
        """Initialize vector with x and y components."""
        self.x = x
        self.y = y
    
    # String representation
    def __str__(self):
        """User-friendly string representation."""
        return f"Vector({self.x}, {self.y})"
    
    def __repr__(self):
        """Developer-friendly representation."""
        return f"Vector({self.x!r}, {self.y!r})"
    
    # Arithmetic operations
    def __add__(self, other):
        """Add two vectors."""
        if isinstance(other, Vector):
            return Vector(self.x + other.x, self.y + other.y)
        return NotImplemented
    
    def __sub__(self, other):
        """Subtract two vectors."""
        if isinstance(other, Vector):
            return Vector(self.x - other.x, self.y - other.y)
        return NotImplemented
    
    def __mul__(self, scalar):
        """Multiply vector by scalar."""
        if isinstance(scalar, (int, float)):
            return Vector(self.x * scalar, self.y * scalar)
        return NotImplemented
    
    def __rmul__(self, scalar):
        """Right multiplication (scalar * vector)."""
        return self.__mul__(scalar)
    
    def __truediv__(self, scalar):
        """Divide vector by scalar."""
        if isinstance(scalar, (int, float)) and scalar != 0:
            return Vector(self.x / scalar, self.y / scalar)
        return NotImplemented
    
    def __neg__(self):
        """Negate vector."""
        return Vector(-self.x, -self.y)
    
    def __abs__(self):
        """Get magnitude of vector."""
        return (self.x**2 + self.y**2)**0.5
    
    # Comparison operations
    def __eq__(self, other):
        """Check equality."""
        if isinstance(other, Vector):
            return self.x == other.x and self.y == other.y
        return False
    
    def __lt__(self, other):
        """Compare by magnitude."""
        if isinstance(other, Vector):
            return abs(self) < abs(other)
        return NotImplemented
    
    def __le__(self, other):
        """Less than or equal."""
        return self < other or self == other
    
    # Container-like behavior
    def __len__(self):
        """Return number of components."""
        return 2
    
    def __getitem__(self, index):
        """Get component by index."""
        if index == 0:
            return self.x
        elif index == 1:
            return self.y
        else:
            raise IndexError("Vector index out of range")
    
    def __setitem__(self, index, value):
        """Set component by index."""
        if index == 0:
            self.x = value
        elif index == 1:
            self.y = value
        else:
            raise IndexError("Vector index out of range")
    
    def __iter__(self):
        """Make vector iterable."""
        yield self.x
        yield self.y
    
    def __contains__(self, value):
        """Check if value is a component."""
        return value in (self.x, self.y)
    
    # Hash and boolean
    def __hash__(self):
        """Make vector hashable."""
        return hash((self.x, self.y))
    
    def __bool__(self):
        """Boolean conversion (False if zero vector)."""
        return self.x != 0 or self.y != 0
    
    # Method calls
    def __call__(self, scalar=1):
        """Make vector callable (normalize with optional scaling)."""
        magnitude = abs(self)
        if magnitude == 0:
            return Vector(0, 0)
        return Vector(self.x * scalar / magnitude, self.y * scalar / magnitude)
    
    # Context manager
    def __enter__(self):
        """Enter context manager."""
        print(f"Working with vector {self}")
        return self
    
    def __exit__(self, exc_type, exc_val, exc_tb):
        """Exit context manager."""
        print(f"Finished working with vector {self}")
    
    # Additional vector operations
    def dot(self, other):
        """Dot product with another vector."""
        if isinstance(other, Vector):
            return self.x * other.x + self.y * other.y
        raise TypeError("Dot product requires another Vector")
    
    def cross(self, other):
        """Cross product magnitude (2D vectors)."""
        if isinstance(other, Vector):
            return self.x * other.y - self.y * other.x
        raise TypeError("Cross product requires another Vector")

# Test special methods
print("=== Special Methods ===")

# Create vectors
v1 = Vector(3, 4)
v2 = Vector(1, 2)

# String representation
print(f"v1: {v1}")
print(f"repr(v1): {repr(v1)}")

# Arithmetic operations
print(f"v1 + v2: {v1 + v2}")
print(f"v1 - v2: {v1 - v2}")
print(f"v1 * 2: {v1 * 2}")
print(f"2 * v1: {2 * v1}")
print(f"v1 / 2: {v1 / 2}")
print(f"-v1: {-v1}")
print(f"|v1|: {abs(v1)}")

# Comparison operations
print(f"v1 == v2: {v1 == v2}")
print(f"v1 < v2: {v1 < v2}")
print(f"v1 <= v2: {v1 <= v2}")

# Container-like behavior
print(f"len(v1): {len(v1)}")
print(f"v1[0]: {v1[0]}")
print(f"v1[1]: {v1[1]}")

# Iteration
print(f"Iterate v1: {list(v1)}")
print(f"3 in v1: {3 in v1}")
print(f"5 in v1: {5 in v1}")

# Hash and boolean
print(f"hash(v1): {hash(v1)}")
print(f"bool(v1): {bool(v1)}")
print(f"bool(Vector(0, 0)): {bool(Vector(0, 0))}")

# Callable
normalized = v1()
print(f"v1 normalized: {normalized}")
print(f"v1 normalized * 2: {v1(2)}")

# Context manager
with v1 as vector:
    print(f"  Working with {vector}")

# Vector operations
print(f"v1 · v2: {v1.dot(v2)}")
print(f"v1 × v2: {v1.cross(v2)}")

# Matrix class with operator overloading
class Matrix:
    """Simple matrix class with operator overloading."""
    
    def __init__(self, data):
        """Initialize matrix with 2D list."""
        if not data or not data[0]:
            raise ValueError("Matrix cannot be empty")
        
        # Validate dimensions
        rows = len(data)
        cols = len(data[0])
        
        for row in data:
            if len(row) != cols:
                raise ValueError("All rows must have same length")
        
        self.data = [row[:] for row in data]  # Deep copy
        self.rows = rows
        self.cols = cols
    
    def __str__(self):
        """String representation."""
        lines = []
        for row in self.data:
            lines.append("  " + " ".join(f"{val:6.2f}" for val in row))
        return "[\n" + "\n".join(lines) + "\n]"
    
    def __repr__(self):
        """Developer representation."""
        return f"Matrix({self.data!r})"
    
    def __getitem__(self, key):
        """Get item by row, col or row only."""
        if isinstance(key, tuple):
            row, col = key
            return self.data[row][col]
        else:
            return self.data[key]
    
    def __setitem__(self, key, value):
        """Set item by row, col or row only."""
        if isinstance(key, tuple):
            row, col = key
            self.data[row][col] = value
        else:
            self.data[key] = value
    
    def __add__(self, other):
        """Add two matrices."""
        if not isinstance(other, Matrix):
            return NotImplemented
        
        if self.rows != other.rows or self.cols != other.cols:
            raise ValueError("Matrices must have same dimensions")
        
        result = []
        for i in range(self.rows):
            row = []
            for j in range(self.cols):
                row.append(self.data[i][j] + other.data[i][j])
            result.append(row)
        
        return Matrix(result)
    
    def __mul__(self, other):
        """Multiply matrix by scalar or another matrix."""
        if isinstance(other, (int, float)):
            # Scalar multiplication
            result = []
            for i in range(self.rows):
                row = []
                for j in range(self.cols):
                    row.append(self.data[i][j] * other)
                result.append(row)
            return Matrix(result)
        
        elif isinstance(other, Matrix):
            # Matrix multiplication
            if self.cols != other.rows:
                raise ValueError("Cannot multiply: incompatible dimensions")
            
            result = []
            for i in range(self.rows):
                row = []
                for j in range(other.cols):
                    cell = 0
                    for k in range(self.cols):
                        cell += self.data[i][k] * other.data[k][j]
                    row.append(cell)
                result.append(row)
            
            return Matrix(result)
        
        return NotImplemented
    
    def __eq__(self, other):
        """Check equality."""
        if not isinstance(other, Matrix):
            return False
        
        return (self.rows == other.rows and 
                self.cols == other.cols and 
                self.data == other.data)
    
    def transpose(self):
        """Return transposed matrix."""
        result = []
        for j in range(self.cols):
            row = []
            for i in range(self.rows):
                row.append(self.data[i][j])
            result.append(row)
        
        return Matrix(result)

# Test matrix operations
print("\n=== Matrix Operations ===")

# Create matrices
m1 = Matrix([[1, 2], [3, 4]])
m2 = Matrix([[5, 6], [7, 8]])

print(f"Matrix 1:\n{m1}")
print(f"Matrix 2:\n{m2}")

# Matrix arithmetic
print(f"m1 + m2:\n{m1 + m2}")
print(f"m1 * 2:\n{m1 * 2}")
print(f"m1 * m2:\n{m1 * m2}")

# Matrix access
print(f"m1[0][1]: {m1[0][1]}")
print(f"m1[0, 1]: {m1[0, 1]}")

# Transpose
print(f"m1 transposed:\n{m1.transpose()}")
```

### Metaclasses and Class Customization

```python
# Simple metaclass example
class SingletonMeta(type):
    """Metaclass that creates singleton classes."""
    
    _instances = {}
    
    def __call__(cls, *args, **kwargs):
        """Override instance creation."""
        if cls not in cls._instances:
            cls._instances[cls] = super().__call__(*args, **kwargs)
        return cls._instances[cls]

class DatabaseConnection(metaclass=SingletonMeta):
    """Database connection using singleton pattern."""
    
    def __init__(self, host="localhost", port=5432):
        """Initialize connection (only happens once)."""
        self.host = host
        self.port = port
        self.connected = False
        print(f"Creating database connection to {host}:{port}")
    
    def connect(self):
        """Connect to database."""
        if not self.connected:
            self.connected = True
            print(f"Connected to {self.host}:{self.port}")
        else:
            print("Already connected")
    
    def disconnect(self):
        """Disconnect from database."""
        if self.connected:
            self.connected = False
            print(f"Disconnected from {self.host}:{self.port}")

# Attribute validation metaclass
class ValidatedMeta(type):
    """Metaclass that adds validation to classes."""
    
    def __new__(mcs, name, bases, attrs):
        """Create class with validation."""
        # Find validation rules
        validations = {}
        for key, value in attrs.items():
            if key.startswith('_validate_'):
                field_name = key[10:]  # Remove '_validate_' prefix
                validations[field_name] = value
        
        # Store validations in class
        attrs['_validations'] = validations
        
        # Wrap __setattr__ to include validation
        original_setattr = attrs.get('__setattr__', object.__setattr__)
        
        def validated_setattr(self, name, value):
            if name in self._validations:
                if not self._validations[name](value):
                    raise ValueError(f"Invalid value for {name}: {value}")
            original_setattr(self, name, value)
        
        attrs['__setattr__'] = validated_setattr
        
        return super().__new__(mcs, name, bases, attrs)

class Person(metaclass=ValidatedMeta):
    """Person class with automatic validation."""
    
    def __init__(self, name, age, email):
        """Initialize person."""
        self.name = name
        self.age = age
        self.email = email
    
    # Validation rules
    @staticmethod
    def _validate_name(value):
        return isinstance(value, str) and len(value.strip()) > 0
    
    @staticmethod
    def _validate_age(value):
        return isinstance(value, int) and 0 <= value <= 150
    
    @staticmethod
    def _validate_email(value):
        return isinstance(value, str) and '@' in value and '.' in value
    
    def __str__(self):
        return f"Person(name='{self.name}', age={self.age}, email='{self.email}')"

# Class decorator for automatic property creation
def auto_properties(cls):
    """Class decorator that creates properties for private attributes."""
    
    for name in dir(cls):
        if name.startswith('_') and not name.startswith('__'):
            prop_name = name[1:]  # Remove leading underscore
            
            def make_property(attr_name):
                def getter(self):
                    return getattr(self, attr_name)
                
                def setter(self, value):
                    setattr(self, attr_name, value)
                
                return property(getter, setter)
            
            setattr(cls, prop_name, make_property(name))
    
    return cls

@auto_properties
class AutoPropertyClass:
    """Class with automatic properties."""
    
    def __init__(self, x, y):
        self._x = x
        self._y = y

# Test metaclasses and class customization
print("=== Metaclasses and Class Customization ===")

# Test singleton
print("Testing singleton:")
db1 = DatabaseConnection("server1", 5432)
db2 = DatabaseConnection("server2", 3306)  # Same instance!

print(f"db1 is db2: {db1 is db2}")
print(f"db1 host: {db1.host}")
print(f"db2 host: {db2.host}")

db1.connect()
db2.connect()  # Same instance, already connected

# Test validation metaclass
print("\nTesting validation metaclass:")
try:
    person = Person("Alice", 25, "alice@example.com")
    print(f"Valid person: {person}")
    
    person.age = 30  # Valid
    print(f"Updated person: {person}")
    
    person.age = -5  # Invalid
except ValueError as e:
    print(f"Validation error: {e}")

# Test auto properties
print("\nTesting auto properties:")
auto_obj = AutoPropertyClass(10, 20)
print(f"auto_obj.x: {auto_obj.x}")  # Uses auto-generated property
print(f"auto_obj.y: {auto_obj.y}")

auto_obj.x = 30  # Uses auto-generated setter
print(f"Updated auto_obj.x: {auto_obj.x}")

# __init_subclass__ hook (Python 3.6+)
class RegisteredClass:
    """Base class that registers all subclasses."""
    
    _registry = {}
    
    def __init_subclass__(cls, **kwargs):
        """Called when a class is subclassed."""
        super().__init_subclass__(**kwargs)
        RegisteredClass._registry[cls.__name__] = cls
        print(f"Registered class: {cls.__name__}")
    
    @classmethod
    def get_registered_classes(cls):
        """Get all registered classes."""
        return cls._registry.copy()

class ChildA(RegisteredClass):
    """First child class."""
    pass

class ChildB(RegisteredClass):
    """Second child class."""
    pass

# Test class registration
print("\nTesting class registration:")
registry = RegisteredClass.get_registered_classes()
print(f"Registered classes: {list(registry.keys())}")

# Dataclass-like behavior using __set_name__
class TypedAttribute:
    """Descriptor that enforces type checking."""
    
    def __init__(self, expected_type):
        self.expected_type = expected_type
        self.name = None
    
    def __set_name__(self, owner, name):
        """Called when descriptor is assigned to class attribute."""
        self.name = f'_{name}'
    
    def __get__(self, obj, objtype=None):
        """Get attribute value."""
        if obj is None:
            return self
        return getattr(obj, self.name, None)
    
    def __set__(self, obj, value):
        """Set attribute value with type checking."""
        if not isinstance(value, self.expected_type):
            raise TypeError(f"{self.name[1:]} must be {self.expected_type.__name__}")
        setattr(obj, self.name, value)

class TypedPerson:
    """Person class with typed attributes."""
    
    name = TypedAttribute(str)
    age = TypedAttribute(int)
    
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def __str__(self):
        return f"TypedPerson(name='{self.name}', age={self.age})"

# Test typed attributes
print("\nTesting typed attributes:")
try:
    typed_person = TypedPerson("Bob", 25)
    print(f"Valid typed person: {typed_person}")
    
    typed_person.name = "Charlie"  # Valid
    print(f"Updated: {typed_person}")
    
    typed_person.age = "thirty"  # Invalid type
except TypeError as e:
    print(f"Type error: {e}")
```

## 🎯 Practice Exercises

### Exercise 1: Advanced Library System

```python
def create_library_system():
    """
    Create a comprehensive library management system with:
    1. Abstract base classes for library items
    2. Multiple inheritance for different item types
    3. Special methods for searching and sorting
    4. Property-based access control
    5. Observer pattern for notifications
    """
    # Your implementation here
    pass
```

### Exercise 2: Game Entity Framework

```python
def build_game_framework():
    """
    Build a game entity framework with:
    1. Component-based architecture using mixins
    2. Event system with custom metaclass
    3. Automatic serialization using descriptors
    4. Performance monitoring with decorators
    5. Plugin system using class registration
    """
    # Your implementation here
    pass
```

### Exercise 3: Data Validation Framework

```python
def create_validation_framework():
    """
    Create a data validation framework with:
    1. Custom metaclass for automatic validation
    2. Descriptor-based field types
    3. Inheritance-based validation rules
    4. Special methods for data export/import
    5. Context managers for batch operations
    """
    # Your implementation here
    pass
```

## 📚 Summary and Best Practices

### Key OOP Concepts

**Core Principles:**
- **Encapsulation**: Bundle data and methods together
- **Inheritance**: Create new classes based on existing ones
- **Polymorphism**: Same interface, different implementations
- **Abstraction**: Hide implementation details

**Advanced Features:**
- **Special methods**: Customize object behavior
- **Descriptors**: Control attribute access
- **Metaclasses**: Customize class creation
- **Multiple inheritance**: Combine multiple parent classes

### Class Design Guidelines

| Principle | Good Practice | Avoid |
|-----------|--------------|-------|
| Single Responsibility | One clear purpose per class | God objects |
| Inheritance | "is-a" relationships | Deep hierarchies |
| Composition | "has-a" relationships | Tight coupling |
| Interface | Abstract base classes | Implicit contracts |
| Naming | Clear, descriptive names | Abbreviations |

### When to Use OOP Features

**Classes:**
- Model real-world entities
- Group related data and behavior
- Need multiple instances
- Complex state management

**Inheritance:**
- Clear "is-a" relationships
- Share common functionality
- Extend existing behavior
- Polymorphic interfaces

**Composition:**
- "has-a" relationships
- Mix different behaviors
- Avoid deep inheritance
- Flexible architectures

**Special Methods:**
- Natural object operations
- Custom container behavior
- Operator overloading
- Context management

### Best Practices Checklist

**Class Design:**
- [ ] Single responsibility principle
- [ ] Clear constructor arguments
- [ ] Appropriate access levels (public/private)
- [ ] Meaningful class and method names
- [ ] Comprehensive documentation

**Inheritance:**
- [ ] Use composition over inheritance when possible
- [ ] Keep inheritance hierarchies shallow
- [ ] Follow Liskov substitution principle
- [ ] Use abstract base classes for interfaces
- [ ] Call parent constructors properly

**Method Design:**
- [ ] Keep methods focused and small
- [ ] Use appropriate parameter types
- [ ] Handle edge cases gracefully
- [ ] Return consistent types
- [ ] Avoid side effects when possible

**Special Methods:**
- [ ] Implement `__str__` and `__repr__`
- [ ] Make objects hashable when appropriate
- [ ] Follow operator semantics
- [ ] Handle NotImplemented properly
- [ ] Use context managers for resource management

### Common Pitfalls to Avoid

1. **Mutable default arguments**: Use None and create new objects
2. **Circular imports**: Organize modules properly
3. **Deep inheritance hierarchies**: Prefer composition
4. **Tight coupling**: Use dependency injection
5. **Global state in classes**: Keep state local
6. **Ignoring special method contracts**: Follow conventions
7. **Premature optimization**: Design first, optimize later

### Design Patterns with Classes

**Creational Patterns:**
- Factory: Create objects without specifying exact class
- Singleton: Ensure only one instance exists
- Builder: Construct complex objects step by step

**Structural Patterns:**
- Adapter: Make incompatible interfaces work together
- Decorator: Add functionality to objects dynamically
- Facade: Provide simplified interface to complex system

**Behavioral Patterns:**
- Observer: Notify multiple objects about state changes
- Strategy: Encapsulate algorithms and make them interchangeable
- Command: Encapsulate requests as objects

### Performance Considerations

**Memory Usage:**
- Use `__slots__` for memory-critical classes
- Be aware of reference cycles
- Implement `__del__` carefully
- Consider weak references

**Speed Optimization:**
- Profile before optimizing
- Use built-in types when possible
- Cache expensive computations
- Minimize attribute lookups in loops

### Next Steps

After mastering classes and objects:
1. Learn about [File I/O and Exception Handling](./14-file-io-exceptions.md)
2. Study design patterns in depth
3. Explore advanced Python features (metaclasses, descriptors)
4. Practice with real-world OOP projects
5. Learn about concurrent programming with classes

---

**Remember**: Object-oriented programming is about modeling real-world relationships and creating maintainable, reusable code. Master these concepts to build robust and scalable applications!
