# File I/O and Exception Handling

## 🎯 Objective
Master Python's file input/output operations and exception handling mechanisms, essential for building robust applications that interact with external data sources and handle errors gracefully in competitive programming and real-world scenarios.

## 📖 Overview

File I/O and exception handling are fundamental aspects of Python programming that enable applications to interact with external data and handle unexpected situations gracefully. These concepts are crucial for data processing, log management, configuration handling, and building resilient applications that can recover from errors.

## 📁 File Input/Output Operations

### Basic File Operations

```python
import os
import tempfile
from pathlib import Path

# Basic file reading
def demonstrate_basic_file_operations():
    """Demonstrate fundamental file operations."""
    
    # Create a temporary file for demonstration
    with tempfile.NamedTemporaryFile(mode='w', delete=False, suffix='.txt') as temp_file:
        temp_file.write("Hello, World!\n")
        temp_file.write("Python File I/O\n")
        temp_file.write("Line 3\n")
        temp_filename = temp_file.name
    
    print("=== Basic File Reading ===")
    
    # Method 1: Read entire file
    with open(temp_filename, 'r') as file:
        content = file.read()
        print("Entire file content:")
        print(repr(content))
    
    # Method 2: Read line by line
    print("\nReading line by line:")
    with open(temp_filename, 'r') as file:
        for line_number, line in enumerate(file, 1):
            print(f"Line {line_number}: {repr(line)}")
    
    # Method 3: Read all lines into a list
    with open(temp_filename, 'r') as file:
        lines = file.readlines()
        print(f"\nAll lines as list: {lines}")
    
    # Method 4: Read specific number of characters
    with open(temp_filename, 'r') as file:
        first_10_chars = file.read(10)
        print(f"\nFirst 10 characters: {repr(first_10_chars)}")
    
    # Method 5: Read one line at a time
    with open(temp_filename, 'r') as file:
        first_line = file.readline()
        second_line = file.readline()
        print(f"\nFirst line: {repr(first_line)}")
        print(f"Second line: {repr(second_line)}")
    
    # Basic file writing
    print("\n=== Basic File Writing ===")
    
    # Write to file (overwrites existing content)
    with open(temp_filename, 'w') as file:
        file.write("New content\n")
        file.write("Overwrote previous content\n")
    
    # Append to file
    with open(temp_filename, 'a') as file:
        file.write("Appended line 1\n")
        file.write("Appended line 2\n")
    
    # Read the modified file
    with open(temp_filename, 'r') as file:
        print("File after writing and appending:")
        print(file.read())
    
    # Writing multiple lines
    lines_to_write = ["Line 1\n", "Line 2\n", "Line 3\n"]
    with open(temp_filename, 'w') as file:
        file.writelines(lines_to_write)
    
    # Cleanup
    os.unlink(temp_filename)

# Advanced file operations
def demonstrate_advanced_file_operations():
    """Demonstrate advanced file handling techniques."""
    
    # Create a test file with various data types
    test_file = "advanced_test.txt"
    
    # Writing structured data
    print("=== Writing Structured Data ===")
    
    data = {
        'numbers': [1, 2, 3, 4, 5],
        'text': "Hello World",
        'boolean': True,
        'nested': {'key': 'value'}
    }
    
    # Write data in different formats
    with open(test_file, 'w') as file:
        # Write header
        file.write("=== Data File ===\n")
        
        # Write numbers
        file.write("Numbers: ")
        file.write(','.join(map(str, data['numbers'])))
        file.write('\n')
        
        # Write text
        file.write(f"Text: {data['text']}\n")
        
        # Write boolean
        file.write(f"Boolean: {data['boolean']}\n")
        
        # Write nested data
        file.write(f"Nested: {data['nested']}\n")
    
    # Reading and parsing structured data
    print("\n=== Reading Structured Data ===")
    
    parsed_data = {}
    with open(test_file, 'r') as file:
        for line in file:
            line = line.strip()
            if line.startswith('Numbers:'):
                numbers_str = line.split(':', 1)[1].strip()
                parsed_data['numbers'] = [int(x) for x in numbers_str.split(',')]
            elif line.startswith('Text:'):
                parsed_data['text'] = line.split(':', 1)[1].strip()
            elif line.startswith('Boolean:'):
                bool_str = line.split(':', 1)[1].strip()
                parsed_data['boolean'] = bool_str.lower() == 'true'
    
    print(f"Parsed data: {parsed_data}")
    
    # File positioning
    print("\n=== File Positioning ===")
    
    with open(test_file, 'r') as file:
        # Read first 10 characters
        first_part = file.read(10)
        print(f"First 10 chars: {repr(first_part)}")
        
        # Get current position
        position = file.tell()
        print(f"Current position: {position}")
        
        # Seek to beginning
        file.seek(0)
        first_line = file.readline()
        print(f"After seeking to start: {repr(first_line)}")
        
        # Seek to end
        file.seek(0, 2)  # 2 means from end
        end_position = file.tell()
        print(f"File size: {end_position} bytes")
    
    # Binary file operations
    print("\n=== Binary File Operations ===")
    
    binary_file = "binary_test.bin"
    
    # Write binary data
    with open(binary_file, 'wb') as file:
        # Write integers as bytes
        for i in range(10):
            file.write(i.to_bytes(4, byteorder='big'))
        
        # Write string as bytes
        text = "Hello Binary World"
        file.write(text.encode('utf-8'))
    
    # Read binary data
    with open(binary_file, 'rb') as file:
        # Read integers
        integers = []
        for _ in range(10):
            int_bytes = file.read(4)
            if int_bytes:
                integers.append(int.from_bytes(int_bytes, byteorder='big'))
        
        print(f"Read integers: {integers}")
        
        # Read remaining as text
        remaining_bytes = file.read()
        text = remaining_bytes.decode('utf-8')
        print(f"Read text: {repr(text)}")
    
    # Cleanup
    os.unlink(test_file)
    os.unlink(binary_file)

# Working with CSV files
def demonstrate_csv_operations():
    """Demonstrate CSV file operations."""
    
    import csv
    
    print("=== CSV File Operations ===")
    
    csv_file = "test_data.csv"
    
    # Writing CSV data
    data = [
        ['Name', 'Age', 'City', 'Salary'],
        ['Alice', '25', 'New York', '50000'],
        ['Bob', '30', 'San Francisco', '75000'],
        ['Charlie', '35', 'Chicago', '60000'],
        ['Diana', '28', 'Boston', '55000']
    ]
    
    # Write CSV file
    with open(csv_file, 'w', newline='') as file:
        writer = csv.writer(file)
        writer.writerows(data)
    
    print(f"Created CSV file with {len(data)} rows")
    
    # Read CSV file
    print("\nReading CSV data:")
    with open(csv_file, 'r') as file:
        reader = csv.reader(file)
        for row_num, row in enumerate(reader):
            print(f"Row {row_num}: {row}")
    
    # Using DictReader and DictWriter
    print("\n=== CSV with Dictionaries ===")
    
    # Read as dictionaries
    with open(csv_file, 'r') as file:
        dict_reader = csv.DictReader(file)
        print("Reading as dictionaries:")
        for row in dict_reader:
            print(f"  {row}")
    
    # Write dictionaries to CSV
    dict_csv_file = "dict_data.csv"
    dict_data = [
        {'Product': 'Laptop', 'Price': 1000, 'Stock': 50},
        {'Product': 'Mouse', 'Price': 25, 'Stock': 200},
        {'Product': 'Keyboard', 'Price': 75, 'Stock': 100}
    ]
    
    with open(dict_csv_file, 'w', newline='') as file:
        fieldnames = ['Product', 'Price', 'Stock']
        dict_writer = csv.DictWriter(file, fieldnames=fieldnames)
        
        dict_writer.writeheader()
        dict_writer.writerows(dict_data)
    
    print(f"\nCreated dictionary CSV with {len(dict_data)} products")
    
    # Custom CSV format
    print("\n=== Custom CSV Format ===")
    
    custom_csv = "custom_format.csv"
    
    # Write with custom delimiter and quoting
    with open(custom_csv, 'w', newline='') as file:
        writer = csv.writer(file, delimiter=';', quotechar='"', 
                          quoting=csv.QUOTE_NONNUMERIC)
        writer.writerow(['Item', 'Description', 'Value'])
        writer.writerow(['Apple', 'Red fruit', 1.5])
        writer.writerow(['Book', 'Python Guide', 29.99])
    
    # Read custom format
    with open(custom_csv, 'r') as file:
        reader = csv.reader(file, delimiter=';', quotechar='"')
        print("Custom format data:")
        for row in reader:
            print(f"  {row}")
    
    # Cleanup
    os.unlink(csv_file)
    os.unlink(dict_csv_file)
    os.unlink(custom_csv)

# JSON file operations
def demonstrate_json_operations():
    """Demonstrate JSON file operations."""
    
    import json
    
    print("=== JSON File Operations ===")
    
    json_file = "data.json"
    
    # Sample data
    data = {
        "users": [
            {
                "id": 1,
                "name": "Alice Johnson",
                "email": "alice@example.com",
                "preferences": {
                    "theme": "dark",
                    "language": "en",
                    "notifications": True
                }
            },
            {
                "id": 2,
                "name": "Bob Smith",
                "email": "bob@example.com",
                "preferences": {
                    "theme": "light",
                    "language": "es",
                    "notifications": False
                }
            }
        ],
        "metadata": {
            "version": "1.0",
            "created": "2024-01-01",
            "total_users": 2
        }
    }
    
    # Write JSON file
    with open(json_file, 'w') as file:
        json.dump(data, file, indent=2)
    
    print("Created JSON file with user data")
    
    # Read JSON file
    with open(json_file, 'r') as file:
        loaded_data = json.load(file)
    
    print(f"\nLoaded {loaded_data['metadata']['total_users']} users")
    for user in loaded_data['users']:
        print(f"  {user['name']} ({user['email']})")
    
    # Pretty print JSON
    print("\n=== Pretty Printed JSON ===")
    print(json.dumps(data, indent=2, sort_keys=True))
    
    # Working with JSON strings
    print("\n=== JSON String Operations ===")
    
    # Convert to JSON string
    json_string = json.dumps(data['users'][0])
    print(f"JSON string: {json_string}")
    
    # Parse JSON string
    parsed_user = json.loads(json_string)
    print(f"Parsed user: {parsed_user}")
    
    # Handle custom objects
    print("\n=== Custom JSON Serialization ===")
    
    from datetime import datetime, date
    
    class DateTimeEncoder(json.JSONEncoder):
        """Custom encoder for datetime objects."""
        
        def default(self, obj):
            if isinstance(obj, (datetime, date)):
                return obj.isoformat()
            return super().default(obj)
    
    class Person:
        def __init__(self, name, birth_date):
            self.name = name
            self.birth_date = birth_date
        
        def to_dict(self):
            return {
                'name': self.name,
                'birth_date': self.birth_date
            }
    
    # Create person with date
    person = Person("Charlie", date(1990, 5, 15))
    
    # Serialize with custom encoder
    person_json = json.dumps(person.to_dict(), cls=DateTimeEncoder)
    print(f"Person JSON: {person_json}")
    
    # Cleanup
    os.unlink(json_file)

# Pathlib for modern file operations
def demonstrate_pathlib():
    """Demonstrate pathlib for modern file operations."""
    
    from pathlib import Path
    import shutil
    
    print("=== Pathlib Operations ===")
    
    # Create Path objects
    current_dir = Path.cwd()
    home_dir = Path.home()
    
    print(f"Current directory: {current_dir}")
    print(f"Home directory: {home_dir}")
    
    # Path construction
    file_path = current_dir / "test_file.txt"
    data_dir = current_dir / "data" / "processed"
    
    print(f"File path: {file_path}")
    print(f"Data directory: {data_dir}")
    
    # Path properties
    print(f"\nPath properties:")
    print(f"  Name: {file_path.name}")
    print(f"  Suffix: {file_path.suffix}")
    print(f"  Stem: {file_path.stem}")
    print(f"  Parent: {file_path.parent}")
    print(f"  Parts: {file_path.parts}")
    
    # Create directories
    test_dir = current_dir / "test_pathlib"
    test_dir.mkdir(exist_ok=True)
    
    sub_dir = test_dir / "subdir" / "deep"
    sub_dir.mkdir(parents=True, exist_ok=True)
    
    print(f"\nCreated directory: {test_dir}")
    
    # File operations with pathlib
    test_file = test_dir / "sample.txt"
    
    # Write file
    test_file.write_text("Hello from pathlib!\nLine 2\nLine 3")
    
    # Read file
    content = test_file.read_text()
    print(f"\nFile content:\n{content}")
    
    # File information
    print(f"\nFile information:")
    print(f"  Exists: {test_file.exists()}")
    print(f"  Is file: {test_file.is_file()}")
    print(f"  Is directory: {test_file.is_dir()}")
    print(f"  Size: {test_file.stat().st_size} bytes")
    
    # List directory contents
    print(f"\nDirectory contents:")
    for item in test_dir.iterdir():
        print(f"  {item.name} ({'dir' if item.is_dir() else 'file'})")
    
    # Glob patterns
    print(f"\nGlob patterns:")
    
    # Create more test files
    (test_dir / "file1.txt").write_text("File 1")
    (test_dir / "file2.txt").write_text("File 2")
    (test_dir / "data.csv").write_text("CSV data")
    (test_dir / "script.py").write_text("Python script")
    
    # Find all .txt files
    txt_files = list(test_dir.glob("*.txt"))
    print(f"  .txt files: {[f.name for f in txt_files]}")
    
    # Find all files recursively
    all_files = list(test_dir.rglob("*"))
    print(f"  All files recursively: {[f.name for f in all_files if f.is_file()]}")
    
    # Path manipulation
    print(f"\n=== Path Manipulation ===")
    
    original_path = Path("documents/projects/python/main.py")
    print(f"Original: {original_path}")
    
    # Change suffix
    backup_path = original_path.with_suffix(".py.bak")
    print(f"Backup: {backup_path}")
    
    # Change name
    test_path = original_path.with_name("test.py")
    print(f"Test: {test_path}")
    
    # Resolve path
    resolved = test_file.resolve()
    print(f"Resolved: {resolved}")
    
    # Relative path
    try:
        relative = test_file.relative_to(current_dir)
        print(f"Relative: {relative}")
    except ValueError:
        print("Cannot create relative path")
    
    # Cleanup
    shutil.rmtree(test_dir)

# Run demonstrations
if __name__ == "__main__":
    demonstrate_basic_file_operations()
    print("\n" + "="*50 + "\n")
    
    demonstrate_advanced_file_operations()
    print("\n" + "="*50 + "\n")
    
    demonstrate_csv_operations()
    print("\n" + "="*50 + "\n")
    
    demonstrate_json_operations()
    print("\n" + "="*50 + "\n")
    
    demonstrate_pathlib()
```

## ⚠️ Exception Handling

### Basic Exception Handling

```python
# Basic try-except blocks
def demonstrate_basic_exceptions():
    """Demonstrate basic exception handling patterns."""
    
    print("=== Basic Exception Handling ===")
    
    # Simple try-except
    try:
        result = 10 / 0
        print(f"Result: {result}")
    except ZeroDivisionError:
        print("Error: Cannot divide by zero!")
    
    # Multiple exception types
    def process_user_input(user_input):
        """Process user input with multiple exception handling."""
        try:
            # Try to convert to integer
            number = int(user_input)
            
            # Try mathematical operation
            result = 100 / number
            
            # Try list access
            data = [1, 2, 3, 4, 5]
            value = data[number]
            
            return f"Success: {result}, Value: {value}"
            
        except ValueError:
            return "Error: Input must be a valid number"
        except ZeroDivisionError:
            return "Error: Number cannot be zero"
        except IndexError:
            return "Error: Number is out of range for list access"
        except Exception as e:
            return f"Unexpected error: {e}"
    
    # Test different inputs
    test_inputs = ["5", "abc", "0", "10", "2"]
    
    print("\nTesting user input processing:")
    for input_val in test_inputs:
        result = process_user_input(input_val)
        print(f"  Input '{input_val}': {result}")
    
    # Catching multiple exceptions in one block
    def handle_multiple_exceptions(data, index, divisor):
        """Handle multiple exceptions in single block."""
        try:
            result = data[index] / divisor
            return result
        except (IndexError, ZeroDivisionError, TypeError) as e:
            return f"Error occurred: {type(e).__name__}: {e}"
    
    print("\nTesting multiple exception handling:")
    test_cases = [
        ([1, 2, 3], 1, 2),    # Success
        ([1, 2, 3], 5, 2),    # IndexError
        ([1, 2, 3], 1, 0),    # ZeroDivisionError
        ([1, 2, 3], 1, "a"),  # TypeError
    ]
    
    for data, index, divisor in test_cases:
        result = handle_multiple_exceptions(data, index, divisor)
        print(f"  {data}[{index}] / {divisor} = {result}")

# Exception hierarchy and specific handling
def demonstrate_exception_hierarchy():
    """Demonstrate exception hierarchy and specific handling."""
    
    print("\n=== Exception Hierarchy ===")
    
    # Custom exception classes
    class ValidationError(Exception):
        """Base validation error."""
        pass
    
    class EmailValidationError(ValidationError):
        """Email validation specific error."""
        pass
    
    class PasswordValidationError(ValidationError):
        """Password validation specific error."""
        pass
    
    def validate_email(email):
        """Validate email format."""
        if not isinstance(email, str):
            raise EmailValidationError("Email must be a string")
        
        if '@' not in email:
            raise EmailValidationError("Email must contain @ symbol")
        
        if '.' not in email:
            raise EmailValidationError("Email must contain a dot")
        
        parts = email.split('@')
        if len(parts) != 2:
            raise EmailValidationError("Email must have exactly one @ symbol")
        
        username, domain = parts
        if not username or not domain:
            raise EmailValidationError("Email must have both username and domain")
        
        return True
    
    def validate_password(password):
        """Validate password strength."""
        if not isinstance(password, str):
            raise PasswordValidationError("Password must be a string")
        
        if len(password) < 8:
            raise PasswordValidationError("Password must be at least 8 characters")
        
        if not any(c.isupper() for c in password):
            raise PasswordValidationError("Password must contain uppercase letter")
        
        if not any(c.islower() for c in password):
            raise PasswordValidationError("Password must contain lowercase letter")
        
        if not any(c.isdigit() for c in password):
            raise PasswordValidationError("Password must contain digit")
        
        return True
    
    def register_user(email, password):
        """Register user with validation."""
        try:
            validate_email(email)
            validate_password(password)
            return f"User registered successfully with email: {email}"
        
        except EmailValidationError as e:
            return f"Email validation failed: {e}"
        
        except PasswordValidationError as e:
            return f"Password validation failed: {e}"
        
        except ValidationError as e:
            return f"General validation error: {e}"
        
        except Exception as e:
            return f"Unexpected error: {e}"
    
    # Test user registration
    test_users = [
        ("user@example.com", "StrongPass123"),  # Valid
        ("invalid.email", "StrongPass123"),     # Invalid email
        ("user@example.com", "weak"),           # Invalid password
        (123, "StrongPass123"),                 # Invalid email type
        ("user@example.com", 123),              # Invalid password type
    ]
    
    print("Testing user registration:")
    for email, password in test_users:
        result = register_user(email, password)
        print(f"  {email}, {password}: {result}")
    
    # Exception chaining
    print("\n=== Exception Chaining ===")
    
    def process_data(data):
        """Process data with exception chaining."""
        try:
            # Simulate processing that might fail
            if not data:
                raise ValueError("Data cannot be empty")
            
            # Simulate another operation
            result = int(data) * 2
            return result
            
        except ValueError as original_error:
            # Chain exceptions to preserve original error
            raise RuntimeError("Failed to process data") from original_error
    
    def handle_processing():
        """Handle data processing with chained exceptions."""
        try:
            result = process_data("")
            return result
        except RuntimeError as e:
            print(f"Processing error: {e}")
            print(f"Original cause: {e.__cause__}")
            return None
    
    handle_processing()

# Advanced exception handling patterns
def demonstrate_advanced_exception_handling():
    """Demonstrate advanced exception handling patterns."""
    
    print("\n=== Advanced Exception Handling ===")
    
    # Using else and finally clauses
    def file_processor(filename, operation="read"):
        """Process file with complete exception handling."""
        file_handle = None
        
        try:
            print(f"Opening file: {filename}")
            file_handle = open(filename, 'r' if operation == "read" else 'w')
            
            if operation == "read":
                content = file_handle.read()
                print(f"Read {len(content)} characters")
                return content
            else:
                file_handle.write("Sample content")
                print("Content written successfully")
                return True
                
        except FileNotFoundError:
            print(f"Error: File '{filename}' not found")
            return None
            
        except PermissionError:
            print(f"Error: Permission denied for file '{filename}'")
            return None
            
        except IOError as e:
            print(f"Error: I/O error occurred: {e}")
            return None
            
        else:
            # Executed only if no exception occurred
            print("File operation completed successfully")
            
        finally:
            # Always executed, regardless of exceptions
            if file_handle and not file_handle.closed:
                file_handle.close()
                print("File handle closed")
    
    # Create a test file
    test_filename = "test_file.txt"
    with open(test_filename, 'w') as f:
        f.write("Test content for exception handling")
    
    # Test file operations
    print("Testing file operations:")
    file_processor(test_filename, "read")
    print()
    file_processor("nonexistent.txt", "read")
    print()
    
    # Context manager for automatic resource management
    print("=== Context Managers ===")
    
    class DatabaseConnection:
        """Simulated database connection context manager."""
        
        def __init__(self, host, port):
            self.host = host
            self.port = port
            self.connected = False
        
        def __enter__(self):
            """Enter context manager."""
            print(f"Connecting to {self.host}:{self.port}")
            self.connected = True
            return self
        
        def __exit__(self, exc_type, exc_val, exc_tb):
            """Exit context manager."""
            if exc_type is not None:
                print(f"Exception occurred: {exc_type.__name__}: {exc_val}")
            
            if self.connected:
                print("Closing database connection")
                self.connected = False
            
            # Return False to propagate exceptions
            return False
        
        def execute_query(self, query):
            """Execute a database query."""
            if not self.connected:
                raise RuntimeError("Not connected to database")
            
            if "DROP" in query.upper():
                raise ValueError("DROP statements not allowed")
            
            return f"Query executed: {query}"
    
    # Using context manager
    try:
        with DatabaseConnection("localhost", 5432) as db:
            result1 = db.execute_query("SELECT * FROM users")
            print(f"  {result1}")
            
            # This will raise an exception
            result2 = db.execute_query("DROP TABLE users")
            print(f"  {result2}")
            
    except Exception as e:
        print(f"Caught exception: {e}")
    
    # Exception suppression
    print("\n=== Exception Suppression ===")
    
    from contextlib import suppress
    
    def risky_operation(value):
        """Operation that might fail."""
        if value < 0:
            raise ValueError("Negative values not allowed")
        return value * 2
    
    # Without suppression
    print("Without suppression:")
    for value in [5, -3, 10]:
        try:
            result = risky_operation(value)
            print(f"  {value} -> {result}")
        except ValueError as e:
            print(f"  {value} -> Error: {e}")
    
    # With suppression
    print("\nWith suppression:")
    for value in [5, -3, 10]:
        with suppress(ValueError):
            result = risky_operation(value)
            print(f"  {value} -> {result}")
    
    # Cleanup
    os.unlink(test_filename)

# Exception logging and debugging
def demonstrate_exception_logging():
    """Demonstrate exception logging and debugging techniques."""
    
    import logging
    import traceback
    import sys
    
    print("\n=== Exception Logging ===")
    
    # Configure logging
    logging.basicConfig(
        level=logging.DEBUG,
        format='%(asctime)s - %(levelname)s - %(message)s'
    )
    
    logger = logging.getLogger(__name__)
    
    def divide_numbers(a, b):
        """Divide numbers with comprehensive error logging."""
        try:
            logger.debug(f"Attempting to divide {a} by {b}")
            result = a / b
            logger.info(f"Division successful: {a} / {b} = {result}")
            return result
            
        except ZeroDivisionError as e:
            logger.error(f"Division by zero: {a} / {b}")
            logger.exception("Full traceback:")
            raise
            
        except Exception as e:
            logger.critical(f"Unexpected error in division: {e}")
            logger.exception("Full traceback:")
            raise
    
    # Test with logging
    print("Testing division with logging:")
    try:
        result = divide_numbers(10, 2)
        print(f"Result: {result}")
    except Exception:
        print("Division failed")
    
    try:
        result = divide_numbers(10, 0)
        print(f"Result: {result}")
    except Exception:
        print("Division by zero handled")
    
    # Manual traceback handling
    print("\n=== Manual Traceback Handling ===")
    
    def process_with_detailed_error(data):
        """Process data with detailed error information."""
        try:
            # Simulate complex processing
            step1 = data[0]
            step2 = int(step1)
            step3 = 100 / step2
            step4 = [1, 2, 3][step2]
            
            return f"Processing successful: {step4}"
            
        except Exception as e:
            # Get detailed exception information
            exc_type, exc_value, exc_traceback = sys.exc_info()
            
            # Format traceback
            tb_lines = traceback.format_exception(exc_type, exc_value, exc_traceback)
            tb_string = ''.join(tb_lines)
            
            # Log detailed information
            error_info = {
                'exception_type': exc_type.__name__,
                'exception_message': str(exc_value),
                'traceback': tb_string,
                'input_data': data
            }
            
            print(f"Detailed error information:")
            for key, value in error_info.items():
                if key == 'traceback':
                    print(f"  {key}:\n{value}")
                else:
                    print(f"  {key}: {value}")
            
            return None
    
    # Test with different error conditions
    test_cases = [
        ["5"],          # Success
        [],             # IndexError
        ["abc"],        # ValueError
        ["0"],          # ZeroDivisionError
        ["5"],          # IndexError in final step
    ]
    
    for i, test_data in enumerate(test_cases):
        print(f"\nTest case {i + 1}: {test_data}")
        result = process_with_detailed_error(test_data)
        if result:
            print(f"  Result: {result}")

# Exception handling in competitive programming
def demonstrate_competitive_programming_exceptions():
    """Demonstrate exception handling patterns for competitive programming."""
    
    print("\n=== Competitive Programming Exception Handling ===")
    
    def safe_input_reader():
        """Safe input reader for competitive programming."""
        def read_int():
            """Read integer with error handling."""
            try:
                return int(input().strip())
            except (ValueError, EOFError):
                return None
        
        def read_ints():
            """Read multiple integers from a line."""
            try:
                return list(map(int, input().split()))
            except (ValueError, EOFError):
                return []
        
        def read_string():
            """Read string with error handling."""
            try:
                return input().strip()
            except EOFError:
                return ""
        
        def read_float():
            """Read float with error handling."""
            try:
                return float(input().strip())
            except (ValueError, EOFError):
                return None
        
        return {
            'int': read_int,
            'ints': read_ints,
            'string': read_string,
            'float': read_float
        }
    
    # Safe mathematical operations
    def safe_math_operations():
        """Safe mathematical operations for competitive programming."""
        
        def safe_divide(a, b):
            """Safe division operation."""
            try:
                return a / b
            except ZeroDivisionError:
                return float('inf') if a > 0 else float('-inf')
        
        def safe_sqrt(x):
            """Safe square root operation."""
            try:
                if x < 0:
                    return complex(0, abs(x) ** 0.5)
                return x ** 0.5
            except Exception:
                return None
        
        def safe_log(x, base=None):
            """Safe logarithm operation."""
            import math
            try:
                if base is None:
                    return math.log(x)
                return math.log(x, base)
            except (ValueError, ZeroDivisionError):
                return None
        
        def safe_factorial(n):
            """Safe factorial calculation."""
            try:
                if n < 0 or not isinstance(n, int):
                    return None
                
                result = 1
                for i in range(1, n + 1):
                    result *= i
                    if result > 10**18:  # Prevent overflow
                        return None
                
                return result
            except Exception:
                return None
        
        return {
            'divide': safe_divide,
            'sqrt': safe_sqrt,
            'log': safe_log,
            'factorial': safe_factorial
        }
    
    # Array operations with bounds checking
    def safe_array_operations():
        """Safe array operations for competitive programming."""
        
        def safe_get(arr, index, default=None):
            """Safe array element access."""
            try:
                return arr[index]
            except (IndexError, TypeError):
                return default
        
        def safe_set(arr, index, value):
            """Safe array element setting."""
            try:
                if 0 <= index < len(arr):
                    arr[index] = value
                    return True
                return False
            except (IndexError, TypeError):
                return False
        
        def safe_slice(arr, start, end=None):
            """Safe array slicing."""
            try:
                if end is None:
                    return arr[start:]
                return arr[start:end]
            except (IndexError, TypeError):
                return []
        
        def safe_search(arr, target):
            """Safe linear search."""
            try:
                return arr.index(target)
            except (ValueError, TypeError):
                return -1
        
        return {
            'get': safe_get,
            'set': safe_set,
            'slice': safe_slice,
            'search': safe_search
        }
    
    # Test safe operations
    print("Testing safe operations:")
    
    math_ops = safe_math_operations()
    
    # Test safe division
    print("\nSafe division:")
    test_divisions = [(10, 2), (10, 0), (-10, 0)]
    for a, b in test_divisions:
        result = math_ops['divide'](a, b)
        print(f"  {a} / {b} = {result}")
    
    # Test safe square root
    print("\nSafe square root:")
    test_sqrts = [9, -4, 0, 16]
    for x in test_sqrts:
        result = math_ops['sqrt'](x)
        print(f"  sqrt({x}) = {result}")
    
    # Test safe array operations
    array_ops = safe_array_operations()
    test_array = [1, 2, 3, 4, 5]
    
    print(f"\nSafe array operations on {test_array}:")
    
    # Safe get
    for index in [2, 10, -1]:
        result = array_ops['get'](test_array, index, "NOT_FOUND")
        print(f"  get[{index}] = {result}")
    
    # Safe search
    for target in [3, 10]:
        result = array_ops['search'](test_array, target)
        print(f"  search({target}) = {result}")

# Run all demonstrations
if __name__ == "__main__":
    demonstrate_basic_exceptions()
    demonstrate_exception_hierarchy()
    demonstrate_advanced_exception_handling()
    demonstrate_exception_logging()
    demonstrate_competitive_programming_exceptions()
```

## 🔄 Context Managers and Resource Management

### Built-in Context Managers

```python
import tempfile
import threading
import time
from contextlib import contextmanager, ExitStack

def demonstrate_context_managers():
    """Demonstrate various context manager patterns."""
    
    print("=== Built-in Context Managers ===")
    
    # File context manager
    with tempfile.NamedTemporaryFile(mode='w+', delete=False) as temp_file:
        temp_file.write("Temporary file content\n")
        temp_file.write("This will be cleaned up automatically\n")
        temp_filename = temp_file.name
    
    # Read the temporary file
    with open(temp_filename, 'r') as file:
        content = file.read()
        print(f"Temporary file content:\n{content}")
    
    # Clean up
    import os
    os.unlink(temp_filename)
    
    # Threading lock context manager
    print("\n=== Threading Lock Context Manager ===")
    
    shared_resource = []
    lock = threading.Lock()
    
    def worker(worker_id):
        """Worker function using context manager for locking."""
        with lock:
            # Critical section
            current_length = len(shared_resource)
            time.sleep(0.01)  # Simulate work
            shared_resource.append(f"Worker {worker_id}")
            print(f"Worker {worker_id}: Added item, length now {current_length + 1}")
    
    # Create and start threads
    threads = []
    for i in range(5):
        thread = threading.Thread(target=worker, args=(i,))
        threads.append(thread)
        thread.start()
    
    # Wait for all threads to complete
    for thread in threads:
        thread.join()
    
    print(f"Final shared resource: {shared_resource}")

# Custom context managers
def demonstrate_custom_context_managers():
    """Demonstrate custom context manager creation."""
    
    print("\n=== Custom Context Managers ===")
    
    # Class-based context manager
    class TimerContext:
        """Context manager to measure execution time."""
        
        def __init__(self, description="Operation"):
            self.description = description
            self.start_time = None
        
        def __enter__(self):
            """Enter the context."""
            print(f"Starting {self.description}")
            self.start_time = time.time()
            return self
        
        def __exit__(self, exc_type, exc_val, exc_tb):
            """Exit the context."""
            end_time = time.time()
            duration = end_time - self.start_time
            
            if exc_type is not None:
                print(f"{self.description} failed after {duration:.4f} seconds")
                print(f"Exception: {exc_type.__name__}: {exc_val}")
            else:
                print(f"{self.description} completed in {duration:.4f} seconds")
            
            # Don't suppress exceptions
            return False
    
    # Test timer context manager
    with TimerContext("File processing"):
        # Simulate some work
        time.sleep(0.1)
        data = [i**2 for i in range(1000)]
        result = sum(data)
        print(f"  Processed {len(data)} items, sum = {result}")
    
    # Function-based context manager using @contextmanager
    @contextmanager
    def database_transaction():
        """Simulate database transaction context manager."""
        print("BEGIN TRANSACTION")
        transaction_successful = False
        
        try:
            yield "transaction_object"
            transaction_successful = True
            print("COMMIT TRANSACTION")
        
        except Exception as e:
            print(f"ROLLBACK TRANSACTION due to error: {e}")
            raise
        
        finally:
            if not transaction_successful:
                print("Transaction was not successful")
    
    # Test database transaction
    print("\n=== Database Transaction Context Manager ===")
    
    # Successful transaction
    try:
        with database_transaction() as tx:
            print("  Executing SQL operations...")
            print("  INSERT INTO users VALUES ('Alice', 25)")
            print("  UPDATE accounts SET balance = balance + 100")
            # Transaction succeeds
    except Exception as e:
        print(f"Transaction failed: {e}")
    
    # Failed transaction
    try:
        with database_transaction() as tx:
            print("  Executing SQL operations...")
            print("  INSERT INTO users VALUES ('Bob', 30)")
            raise ValueError("Simulated database error")
    except Exception as e:
        print(f"Transaction failed: {e}")
    
    # Resource pool context manager
    @contextmanager
    def resource_pool(pool_size=3):
        """Manage a pool of resources."""
        resources = [f"Resource_{i}" for i in range(pool_size)]
        acquired_resources = []
        
        def acquire_resource():
            if resources:
                resource = resources.pop()
                acquired_resources.append(resource)
                print(f"  Acquired {resource}")
                return resource
            else:
                raise RuntimeError("No resources available")
        
        def release_resource(resource):
            if resource in acquired_resources:
                acquired_resources.remove(resource)
                resources.append(resource)
                print(f"  Released {resource}")
        
        pool = {
            'acquire': acquire_resource,
            'release': release_resource,
            'available': lambda: len(resources),
            'acquired': lambda: len(acquired_resources)
        }
        
        try:
            yield pool
        finally:
            # Release all acquired resources
            for resource in acquired_resources[:]:
                release_resource(resource)
            print(f"  Pool cleanup: {len(resources)} resources returned")
    
    # Test resource pool
    print("\n=== Resource Pool Context Manager ===")
    
    with resource_pool(2) as pool:
        print(f"Pool initialized with {pool['available']()} resources")
        
        # Acquire resources
        r1 = pool['acquire']()
        r2 = pool['acquire']()
        
        print(f"Resources available: {pool['available']()}")
        print(f"Resources acquired: {pool['acquired']()}")
        
        # Release one resource
        pool['release'](r1)
        
        print(f"After releasing {r1}:")
        print(f"  Available: {pool['available']()}")
        print(f"  Acquired: {pool['acquired']()}")

# ExitStack for managing multiple context managers
def demonstrate_exit_stack():
    """Demonstrate ExitStack for managing multiple context managers."""
    
    print("\n=== ExitStack for Multiple Context Managers ===")
    
    # Multiple file operations
    def process_multiple_files(filenames):
        """Process multiple files using ExitStack."""
        
        # Create test files
        for i, filename in enumerate(filenames):
            with open(filename, 'w') as f:
                f.write(f"Content of file {i+1}\n")
                f.write(f"Filename: {filename}\n")
        
        # Process files using ExitStack
        with ExitStack() as stack:
            files = []
            
            # Open all files
            for filename in filenames:
                try:
                    file_obj = stack.enter_context(open(filename, 'r'))
                    files.append((filename, file_obj))
                    print(f"Opened {filename}")
                except IOError as e:
                    print(f"Failed to open {filename}: {e}")
            
            # Process all open files
            total_lines = 0
            for filename, file_obj in files:
                lines = file_obj.readlines()
                total_lines += len(lines)
                print(f"  {filename}: {len(lines)} lines")
            
            print(f"Total lines processed: {total_lines}")
        
        # Clean up test files
        for filename in filenames:
            try:
                os.unlink(filename)
            except OSError:
                pass
    
    # Test multiple file processing
    test_files = ["file1.txt", "file2.txt", "file3.txt"]
    process_multiple_files(test_files)
    
    # Dynamic context manager management
    @contextmanager
    def conditional_timer(condition, description):
        """Timer that only runs if condition is True."""
        if condition:
            start_time = time.time()
            print(f"Starting timed operation: {description}")
            
        try:
            yield condition
        finally:
            if condition:
                end_time = time.time()
                print(f"Timed operation completed in {end_time - start_time:.4f}s")
    
    print("\n=== Conditional Context Managers ===")
    
    # Use ExitStack to conditionally enter context managers
    conditions = [True, False, True]
    descriptions = ["Fast operation", "Skipped operation", "Slow operation"]
    
    with ExitStack() as stack:
        active_timers = []
        
        for condition, description in zip(conditions, descriptions):
            timer = stack.enter_context(conditional_timer(condition, description))
            if timer:
                active_timers.append(description)
        
        print(f"Active timers: {active_timers}")
        
        # Simulate work
        time.sleep(0.05)
        
        print("Work completed")

# Advanced context manager patterns
def demonstrate_advanced_patterns():
    """Demonstrate advanced context manager patterns."""
    
    print("\n=== Advanced Context Manager Patterns ===")
    
    # Reentrant context manager
    class ReentrantLock:
        """Reentrant lock context manager."""
        
        def __init__(self):
            self._lock = threading.RLock()
            self._count = 0
        
        def __enter__(self):
            self._lock.acquire()
            self._count += 1
            print(f"  Lock acquired (count: {self._count})")
            return self
        
        def __exit__(self, exc_type, exc_val, exc_tb):
            self._count -= 1
            print(f"  Lock released (count: {self._count})")
            self._lock.release()
            return False
    
    # Test reentrant lock
    print("Reentrant Lock:")
    
    reentrant_lock = ReentrantLock()
    
    def nested_function():
        """Function that acquires the same lock."""
        with reentrant_lock:
            print("    Inside nested function")
            time.sleep(0.01)
    
    with reentrant_lock:
        print("  Outer context")
        nested_function()
        print("  Back to outer context")
    
    # Suppressing specific exceptions
    from contextlib import suppress
    
    print("\n=== Exception Suppression ===")
    
    def risky_operations():
        """Perform operations that might fail."""
        operations = [
            ("Division by zero", lambda: 1/0),
            ("Valid operation", lambda: 2*3),
            ("Index error", lambda: [1, 2, 3][10]),
            ("Another valid operation", lambda: "hello".upper()),
            ("Type error", lambda: "string" + 5)
        ]
        
        results = []
        
        for description, operation in operations:
            with suppress(ZeroDivisionError, IndexError, TypeError):
                result = operation()
                results.append((description, result))
                print(f"  ✓ {description}: {result}")
            
            # This runs whether exception was suppressed or not
            print(f"    Processed: {description}")
        
        return results
    
    successful_results = risky_operations()
    print(f"\nSuccessful operations: {len(successful_results)}")
    
    # Closing context manager
    from contextlib import closing
    
    print("\n=== Closing Context Manager ===")
    
    class NetworkConnection:
        """Simulated network connection."""
        
        def __init__(self, host, port):
            self.host = host
            self.port = port
            self.connected = False
        
        def connect(self):
            """Connect to the network."""
            print(f"Connecting to {self.host}:{self.port}")
            self.connected = True
        
        def send_data(self, data):
            """Send data over the connection."""
            if not self.connected:
                raise RuntimeError("Not connected")
            print(f"Sending: {data}")
        
        def close(self):
            """Close the connection."""
            if self.connected:
                print(f"Closing connection to {self.host}:{self.port}")
                self.connected = False
    
    # Use closing() to ensure close() is called
    with closing(NetworkConnection("example.com", 80)) as conn:
        conn.connect()
        conn.send_data("Hello, server!")
        conn.send_data("Goodbye!")
    
    print("Connection automatically closed")

# Run demonstrations
if __name__ == "__main__":
    demonstrate_context_managers()
    demonstrate_custom_context_managers()
    demonstrate_exit_stack()
    demonstrate_advanced_patterns()
```

## 🎯 Practice Exercises

### Exercise 1: Log File Analyzer

```python
def create_log_analyzer():
    """
    Create a log file analyzer that:
    1. Reads log files safely with proper exception handling
    2. Parses different log formats (Apache, Python, custom)
    3. Handles corrupted or incomplete log entries
    4. Generates summary reports with error statistics
    5. Uses context managers for file operations
    """
    # Your implementation here
    pass
```

### Exercise 2: Data Pipeline with Error Recovery

```python
def build_data_pipeline():
    """
    Build a data processing pipeline that:
    1. Reads data from multiple sources (CSV, JSON, databases)
    2. Processes data with transformation functions
    3. Handles various data errors gracefully
    4. Implements retry mechanisms for transient failures
    5. Logs all operations and errors comprehensively
    """
    # Your implementation here
    pass
```

### Exercise 3: Configuration Manager

```python
def create_config_manager():
    """
    Create a configuration management system that:
    1. Loads configuration from multiple formats
    2. Validates configuration values with custom exceptions
    3. Provides fallback mechanisms for missing values
    4. Implements hot-reloading with file watching
    5. Uses context managers for configuration sections
    """
    # Your implementation here
    pass
```

## 📚 Summary and Best Practices

### File I/O Best Practices

**Always Use Context Managers:**
```python
# Good
with open('file.txt', 'r') as f:
    content = f.read()

# Avoid
f = open('file.txt', 'r')
content = f.read()
f.close()  # Easy to forget or skip due to exception
```

**Handle Encoding Properly:**
```python
# Specify encoding explicitly
with open('file.txt', 'r', encoding='utf-8') as f:
    content = f.read()

# Handle encoding errors
with open('file.txt', 'r', encoding='utf-8', errors='replace') as f:
    content = f.read()
```

**Use Pathlib for Modern Path Operations:**
```python
from pathlib import Path

# Modern approach
file_path = Path('data') / 'file.txt'
if file_path.exists():
    content = file_path.read_text()

# Older approach
import os
file_path = os.path.join('data', 'file.txt')
if os.path.exists(file_path):
    with open(file_path, 'r') as f:
        content = f.read()
```

### Exception Handling Guidelines

| Principle | Good Practice | Avoid |
|-----------|--------------|-------|
| Specificity | Catch specific exceptions | Bare `except:` clauses |
| Granularity | Handle exceptions at appropriate level | Catching too broadly |
| Information | Log meaningful error messages | Silent failures |
| Recovery | Provide recovery mechanisms | Ignoring exceptions |
| Resources | Clean up resources properly | Resource leaks |

**Exception Handling Hierarchy:**
1. **Catch specific exceptions first**
2. **Use exception chaining for context**
3. **Log exceptions appropriately**
4. **Clean up resources in finally blocks**
5. **Re-raise when appropriate**

### Common File Operations Patterns

**Safe File Reading:**
```python
def safe_read_file(filename, default=None):
    """Safely read file with error handling."""
    try:
        with open(filename, 'r', encoding='utf-8') as f:
            return f.read()
    except FileNotFoundError:
        return default
    except PermissionError:
        logging.error(f"Permission denied: {filename}")
        return default
    except UnicodeDecodeError:
        logging.error(f"Encoding error: {filename}")
        return default
```

**Atomic File Writing:**
```python
def atomic_write(filename, content):
    """Write file atomically to prevent corruption."""
    temp_filename = filename + '.tmp'
    try:
        with open(temp_filename, 'w', encoding='utf-8') as f:
            f.write(content)
        os.rename(temp_filename, filename)
    except Exception:
        if os.path.exists(temp_filename):
            os.unlink(temp_filename)
        raise
```

### Context Manager Best Practices

**Use Built-in Context Managers:**
- `open()` for files
- `threading.Lock()` for synchronization
- `suppress()` for expected exceptions
- `closing()` for objects with close() method

**Create Custom Context Managers for:**
- Resource management
- State management
- Timing operations
- Transaction-like operations

**Context Manager Checklist:**
- [ ] Properly implement `__enter__` and `__exit__`
- [ ] Handle exceptions appropriately
- [ ] Clean up resources in `__exit__`
- [ ] Document expected usage
- [ ] Consider reentrant behavior

### Performance Considerations

**File I/O Optimization:**
- Use buffered I/O for large files
- Read in chunks for memory efficiency
- Use binary mode when appropriate
- Consider memory mapping for large files

**Exception Handling Performance:**
- Exceptions are expensive - don't use for control flow
- Cache exception objects when possible
- Use EAFP (Easier to Ask for Forgiveness than Permission)
- Profile exception-heavy code

### Testing Exception Handling

**Use pytest.raises:**
```python
import pytest

def test_division_by_zero():
    with pytest.raises(ZeroDivisionError):
        result = 1 / 0

def test_custom_exception():
    with pytest.raises(ValueError, match="Invalid input"):
        validate_input("")
```

**Test Exception Messages:**
```python
def test_exception_message():
    with pytest.raises(ValueError) as exc_info:
        raise ValueError("Specific error message")
    
    assert "Specific error message" in str(exc_info.value)
```

### Next Steps

After mastering file I/O and exception handling:
1. Learn about [Modules and Packages](./15-modules-packages.md)
2. Study advanced I/O operations (asyncio, streaming)
3. Explore logging frameworks in depth
4. Practice with real-world data processing projects
5. Learn about testing exception scenarios

---

**Remember**: Robust error handling and proper file operations are essential for building reliable applications. Always anticipate what can go wrong and handle it gracefully!
