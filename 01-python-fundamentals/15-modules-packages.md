# Modules and Packages

## 🎯 Objective
Master Python's module and package system for creating reusable, maintainable, and scalable codebases. Learn to organize code effectively, manage dependencies, and build distributable packages essential for competitive programming and software development.

## 📖 Overview

Python's module and package system enables code organization, reusability, and namespace management. Understanding how to create, import, and distribute Python modules is crucial for building larger applications, competitive programming libraries, and collaborative projects.

## 📁 Module Basics

### Creating and Importing Modules

```python
# math_utils.py - A simple module
"""
Mathematical utility functions for common operations.

This module provides various mathematical functions that are commonly
used in competitive programming and general calculations.
"""

import math
from typing import List, Tuple, Optional

def factorial(n: int) -> int:
    """
    Calculate factorial of a number.
    
    Args:
        n: Non-negative integer
        
    Returns:
        Factorial of n
        
    Raises:
        ValueError: If n is negative
    """
    if n < 0:
        raise ValueError("Factorial is not defined for negative numbers")
    
    if n <= 1:
        return 1
    
    result = 1
    for i in range(2, n + 1):
        result *= i
    return result

def is_prime(n: int) -> bool:
    """
    Check if a number is prime.
    
    Args:
        n: Integer to check
        
    Returns:
        True if n is prime, False otherwise
    """
    if n < 2:
        return False
    
    if n == 2:
        return True
    
    if n % 2 == 0:
        return False
    
    for i in range(3, int(math.sqrt(n)) + 1, 2):
        if n % i == 0:
            return False
    
    return True

def gcd(a: int, b: int) -> int:
    """
    Calculate Greatest Common Divisor using Euclidean algorithm.
    
    Args:
        a: First integer
        b: Second integer
        
    Returns:
        GCD of a and b
    """
    while b:
        a, b = b, a % b
    return abs(a)

def lcm(a: int, b: int) -> int:
    """
    Calculate Least Common Multiple.
    
    Args:
        a: First integer
        b: Second integer
        
    Returns:
        LCM of a and b
    """
    return abs(a * b) // gcd(a, b) if a and b else 0

def fibonacci_sequence(n: int) -> List[int]:
    """
    Generate Fibonacci sequence up to n terms.
    
    Args:
        n: Number of terms to generate
        
    Returns:
        List of Fibonacci numbers
    """
    if n <= 0:
        return []
    
    if n == 1:
        return [0]
    
    fib = [0, 1]
    for i in range(2, n):
        fib.append(fib[i-1] + fib[i-2])
    
    return fib

def prime_factors(n: int) -> List[int]:
    """
    Find all prime factors of a number.
    
    Args:
        n: Number to factorize
        
    Returns:
        List of prime factors
    """
    factors = []
    d = 2
    
    while d * d <= n:
        while n % d == 0:
            factors.append(d)
            n //= d
        d += 1
    
    if n > 1:
        factors.append(n)
    
    return factors

# Module-level variables
PI = 3.14159265359
E = 2.71828182846
GOLDEN_RATIO = 1.61803398875

# Module initialization code
print(f"Math utilities module loaded. Constants available: PI={PI}, E={E}")

if __name__ == "__main__":
    # Test code that runs only when module is executed directly
    print("Testing math utilities...")
    
    # Test factorial
    print(f"5! = {factorial(5)}")
    
    # Test prime checking
    test_numbers = [2, 3, 4, 17, 25, 29]
    for num in test_numbers:
        print(f"{num} is {'prime' if is_prime(num) else 'not prime'}")
    
    # Test GCD and LCM
    a, b = 48, 18
    print(f"GCD({a}, {b}) = {gcd(a, b)}")
    print(f"LCM({a}, {b}) = {lcm(a, b)}")
    
    # Test Fibonacci
    print(f"First 10 Fibonacci numbers: {fibonacci_sequence(10)}")
    
    # Test prime factorization
    n = 60
    print(f"Prime factors of {n}: {prime_factors(n)}")
```

### Different Import Methods

```python
# import_examples.py - Demonstrating different import methods

# Method 1: Import entire module
import math_utils

print("=== Method 1: Import entire module ===")
result1 = math_utils.factorial(5)
print(f"math_utils.factorial(5) = {result1}")

# Access module constants
print(f"PI from math_utils: {math_utils.PI}")

# Method 2: Import specific functions
from math_utils import factorial, is_prime, gcd

print("\n=== Method 2: Import specific functions ===")
result2 = factorial(6)
print(f"factorial(6) = {result2}")

prime_check = is_prime(17)
print(f"is_prime(17) = {prime_check}")

gcd_result = gcd(24, 36)
print(f"gcd(24, 36) = {gcd_result}")

# Method 3: Import with aliases
from math_utils import fibonacci_sequence as fib, prime_factors as factors

print("\n=== Method 3: Import with aliases ===")
fib_numbers = fib(8)
print(f"fib(8) = {fib_numbers}")

factor_list = factors(100)
print(f"factors(100) = {factor_list}")

# Method 4: Import all (generally not recommended)
# from math_utils import *

# Method 5: Import module with alias
import math_utils as mu

print("\n=== Method 5: Import module with alias ===")
result5 = mu.lcm(12, 18)
print(f"mu.lcm(12, 18) = {result5}")

# Method 6: Conditional imports
try:
    import numpy as np
    HAS_NUMPY = True
    print("\n=== NumPy available ===")
except ImportError:
    HAS_NUMPY = False
    print("\n=== NumPy not available ===")

# Method 7: Import from specific path
import sys
import os

# Add custom path to sys.path
custom_path = os.path.join(os.getcwd(), "custom_modules")
if custom_path not in sys.path:
    sys.path.append(custom_path)

# Now can import from custom_modules directory
# import custom_module

# Method 8: Dynamic imports
def dynamic_import_demo():
    """Demonstrate dynamic importing."""
    
    # Import module by name
    module_name = "math_utils"
    
    # Using importlib
    import importlib
    
    module = importlib.import_module(module_name)
    result = module.factorial(4)
    print(f"\nDynamic import: {module_name}.factorial(4) = {result}")
    
    # Import specific function dynamically
    func_name = "is_prime"
    if hasattr(module, func_name):
        func = getattr(module, func_name)
        result = func(13)
        print(f"Dynamic function call: {func_name}(13) = {result}")
    
    # Reload module (useful for development)
    importlib.reload(module)
    print("Module reloaded")

dynamic_import_demo()

# Method 9: Lazy imports
class LazyImporter:
    """Lazy import class that imports modules only when needed."""
    
    def __init__(self, module_name):
        self.module_name = module_name
        self._module = None
    
    def __getattr__(self, name):
        if self._module is None:
            print(f"Lazy loading module: {self.module_name}")
            self._module = __import__(self.module_name)
        
        return getattr(self._module, name)

# Usage of lazy importer
lazy_math = LazyImporter('math')
print(f"\nLazy import: math.sqrt(16) = {lazy_math.sqrt(16)}")

# Demonstrating module search path
print("\n=== Module Search Path ===")
print("Python searches for modules in the following order:")
for i, path in enumerate(sys.path):
    print(f"  {i+1}. {path}")
```

### Module Attributes and Introspection

```python
# module_introspection.py - Exploring module attributes and introspection

import math_utils
import sys
import inspect

def explore_module(module):
    """Explore attributes and functions of a module."""
    
    print(f"=== Exploring Module: {module.__name__} ===")
    
    # Basic module information
    print(f"Module name: {module.__name__}")
    print(f"Module file: {getattr(module, '__file__', 'Built-in')}")
    print(f"Module doc: {module.__doc__[:100] if module.__doc__ else 'No documentation'}...")
    
    # List all attributes
    print(f"\nAll attributes ({len(dir(module))}):")
    attributes = dir(module)
    
    # Categorize attributes
    functions = []
    classes = []
    variables = []
    private_attrs = []
    
    for attr_name in attributes:
        if attr_name.startswith('_'):
            private_attrs.append(attr_name)
            continue
            
        attr = getattr(module, attr_name)
        
        if inspect.isfunction(attr):
            functions.append(attr_name)
        elif inspect.isclass(attr):
            classes.append(attr_name)
        else:
            variables.append(attr_name)
    
    print(f"  Functions: {functions}")
    print(f"  Classes: {classes}")
    print(f"  Variables: {variables}")
    print(f"  Private attributes: {private_attrs[:5]}{'...' if len(private_attrs) > 5 else ''}")
    
    # Function signatures
    print(f"\nFunction signatures:")
    for func_name in functions[:3]:  # Show first 3 functions
        func = getattr(module, func_name)
        sig = inspect.signature(func)
        print(f"  {func_name}{sig}")
        
        # Function documentation
        if func.__doc__:
            first_line = func.__doc__.split('\n')[0]
            print(f"    Doc: {first_line}")
    
    # Module variables with values
    print(f"\nModule variables:")
    for var_name in variables:
        var_value = getattr(module, var_name)
        print(f"  {var_name} = {var_value}")

def demonstrate_module_caching():
    """Demonstrate how Python caches imported modules."""
    
    print("\n=== Module Caching ===")
    
    # Check if module is in cache
    if 'math_utils' in sys.modules:
        print("math_utils is already in sys.modules cache")
        cached_module = sys.modules['math_utils']
        print(f"Cached module ID: {id(cached_module)}")
    
    # Import again - should get same object
    import math_utils as mu_again
    print(f"Re-imported module ID: {id(mu_again)}")
    print(f"Same object: {cached_module is mu_again}")
    
    # Show all cached modules
    print(f"\nTotal cached modules: {len(sys.modules)}")
    
    # Show some built-in modules
    builtin_modules = [name for name in sys.modules.keys() 
                      if not name.startswith('_') and '.' not in name]
    print(f"Some built-in modules: {builtin_modules[:10]}")

def demonstrate_module_reloading():
    """Demonstrate module reloading for development."""
    
    import importlib
    
    print("\n=== Module Reloading ===")
    
    # Show current module timestamp
    import os
    import time
    
    if hasattr(math_utils, '__file__') and math_utils.__file__:
        file_path = math_utils.__file__
        if file_path.endswith('.pyc'):
            file_path = file_path[:-1]  # Remove 'c' from .pyc
        
        if os.path.exists(file_path):
            mod_time = os.path.getmtime(file_path)
            print(f"Module file last modified: {time.ctime(mod_time)}")
    
    # Function to check if module changed
    def module_changed(module):
        """Check if module file has been modified."""
        if not hasattr(module, '__file__') or not module.__file__:
            return False
        
        file_path = module.__file__
        if file_path.endswith('.pyc'):
            file_path = file_path[:-1]
        
        if not os.path.exists(file_path):
            return False
        
        # Compare with cached modification time
        if not hasattr(module, '_cached_mtime'):
            module._cached_mtime = os.path.getmtime(file_path)
            return False
        
        current_mtime = os.path.getmtime(file_path)
        if current_mtime > module._cached_mtime:
            module._cached_mtime = current_mtime
            return True
        
        return False
    
    # Auto-reload function
    def auto_reload_module(module):
        """Automatically reload module if it has changed."""
        if module_changed(module):
            print(f"Module {module.__name__} has changed, reloading...")
            importlib.reload(module)
            return True
        return False
    
    # Test auto-reload
    reloaded = auto_reload_module(math_utils)
    print(f"Module reloaded: {reloaded}")

# Run demonstrations
if __name__ == "__main__":
    explore_module(math_utils)
    demonstrate_module_caching()
    demonstrate_module_reloading()
    
    # Explore built-in modules
    print("\n" + "="*50)
    explore_module(sys)
```

## 📦 Creating Packages

### Basic Package Structure

```python
# Package structure example:
# 
# competitive_programming/
# ├── __init__.py
# ├── algorithms/
# │   ├── __init__.py
# │   ├── sorting.py
# │   ├── searching.py
# │   └── graph.py
# ├── data_structures/
# │   ├── __init__.py
# │   ├── trees.py
# │   ├── heaps.py
# │   └── union_find.py
# └── utils/
#     ├── __init__.py
#     ├── input_parser.py
#     └── output_formatter.py

# competitive_programming/__init__.py
"""
Competitive Programming Library

A comprehensive Python package for competitive programming,
containing algorithms, data structures, and utilities.
"""

__version__ = "1.0.0"
__author__ = "Python DSA Course"
__email__ = "course@example.com"

# Import commonly used modules for convenience
from .algorithms import sorting, searching
from .data_structures import trees, heaps
from .utils import input_parser

# Package-level functions
def get_version():
    """Get package version."""
    return __version__

def list_algorithms():
    """List available algorithms."""
    algorithms = []
    
    # Get sorting algorithms
    if hasattr(sorting, '__all__'):
        algorithms.extend([f"sorting.{name}" for name in sorting.__all__])
    
    # Get searching algorithms  
    if hasattr(searching, '__all__'):
        algorithms.extend([f"searching.{name}" for name in searching.__all__])
    
    return algorithms

# Package initialization
print(f"Competitive Programming Library v{__version__} loaded")

# Define what gets imported with "from package import *"
__all__ = [
    'sorting',
    'searching', 
    'trees',
    'heaps',
    'input_parser',
    'get_version',
    'list_algorithms'
]
```

### Subpackage Example - Algorithms

```python
# competitive_programming/algorithms/__init__.py
"""
Algorithms subpackage containing sorting, searching, and graph algorithms.
"""

from . import sorting
from . import searching
from . import graph

__all__ = ['sorting', 'searching', 'graph']

# competitive_programming/algorithms/sorting.py
"""
Sorting algorithms for competitive programming.
"""

from typing import List, TypeVar, Callable, Optional

T = TypeVar('T')

def bubble_sort(arr: List[T]) -> List[T]:
    """
    Bubble sort implementation.
    
    Time Complexity: O(n²)
    Space Complexity: O(1)
    
    Args:
        arr: List to sort
        
    Returns:
        Sorted list
    """
    arr = arr.copy()
    n = len(arr)
    
    for i in range(n):
        swapped = False
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True
        
        if not swapped:
            break
    
    return arr

def quick_sort(arr: List[T]) -> List[T]:
    """
    Quick sort implementation.
    
    Time Complexity: O(n log n) average, O(n²) worst
    Space Complexity: O(log n)
    
    Args:
        arr: List to sort
        
    Returns:
        Sorted list
    """
    if len(arr) <= 1:
        return arr.copy()
    
    pivot = arr[len(arr) // 2]
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]
    
    return quick_sort(left) + middle + quick_sort(right)

def merge_sort(arr: List[T]) -> List[T]:
    """
    Merge sort implementation.
    
    Time Complexity: O(n log n)
    Space Complexity: O(n)
    
    Args:
        arr: List to sort
        
    Returns:
        Sorted list
    """
    if len(arr) <= 1:
        return arr.copy()
    
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])
    
    return _merge(left, right)

def _merge(left: List[T], right: List[T]) -> List[T]:
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

def counting_sort(arr: List[int], max_val: Optional[int] = None) -> List[int]:
    """
    Counting sort for integers.
    
    Time Complexity: O(n + k) where k is the range
    Space Complexity: O(k)
    
    Args:
        arr: List of integers to sort
        max_val: Maximum value in array (auto-detected if None)
        
    Returns:
        Sorted list
    """
    if not arr:
        return []
    
    if max_val is None:
        max_val = max(arr)
    
    min_val = min(arr)
    range_val = max_val - min_val + 1
    
    # Count occurrences
    count = [0] * range_val
    for num in arr:
        count[num - min_val] += 1
    
    # Build sorted array
    result = []
    for i, freq in enumerate(count):
        result.extend([i + min_val] * freq)
    
    return result

def heap_sort(arr: List[T]) -> List[T]:
    """
    Heap sort implementation.
    
    Time Complexity: O(n log n)
    Space Complexity: O(1)
    
    Args:
        arr: List to sort
        
    Returns:
        Sorted list
    """
    arr = arr.copy()
    n = len(arr)
    
    # Build max heap
    for i in range(n // 2 - 1, -1, -1):
        _heapify(arr, n, i)
    
    # Extract elements from heap
    for i in range(n - 1, 0, -1):
        arr[0], arr[i] = arr[i], arr[0]
        _heapify(arr, i, 0)
    
    return arr

def _heapify(arr: List[T], n: int, i: int):
    """Helper function for heap sort."""
    largest = i
    left = 2 * i + 1
    right = 2 * i + 2
    
    if left < n and arr[left] > arr[largest]:
        largest = left
    
    if right < n and arr[right] > arr[largest]:
        largest = right
    
    if largest != i:
        arr[i], arr[largest] = arr[largest], arr[i]
        _heapify(arr, n, largest)

# Algorithm benchmarking
def benchmark_sorting_algorithms(arr: List[int]) -> dict:
    """
    Benchmark all sorting algorithms.
    
    Args:
        arr: Array to sort
        
    Returns:
        Dictionary with timing results
    """
    import time
    
    algorithms = {
        'bubble_sort': bubble_sort,
        'quick_sort': quick_sort,
        'merge_sort': merge_sort,
        'heap_sort': heap_sort,
        'counting_sort': counting_sort if all(isinstance(x, int) for x in arr) else None
    }
    
    results = {}
    
    for name, func in algorithms.items():
        if func is None:
            continue
            
        # Time the algorithm
        start_time = time.time()
        try:
            sorted_arr = func(arr)
            end_time = time.time()
            
            # Verify correctness
            is_correct = sorted_arr == sorted(arr)
            
            results[name] = {
                'time': end_time - start_time,
                'correct': is_correct
            }
        except Exception as e:
            results[name] = {
                'time': float('inf'),
                'correct': False,
                'error': str(e)
            }
    
    return results

# Define public interface
__all__ = [
    'bubble_sort',
    'quick_sort', 
    'merge_sort',
    'counting_sort',
    'heap_sort',
    'benchmark_sorting_algorithms'
]

# competitive_programming/algorithms/searching.py
"""
Searching algorithms for competitive programming.
"""

from typing import List, TypeVar, Optional, Callable

T = TypeVar('T')

def linear_search(arr: List[T], target: T) -> int:
    """
    Linear search implementation.
    
    Time Complexity: O(n)
    Space Complexity: O(1)
    
    Args:
        arr: List to search
        target: Element to find
        
    Returns:
        Index of target, -1 if not found
    """
    for i, element in enumerate(arr):
        if element == target:
            return i
    return -1

def binary_search(arr: List[T], target: T) -> int:
    """
    Binary search implementation (assumes sorted array).
    
    Time Complexity: O(log n)
    Space Complexity: O(1)
    
    Args:
        arr: Sorted list to search
        target: Element to find
        
    Returns:
        Index of target, -1 if not found
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

def binary_search_leftmost(arr: List[T], target: T) -> int:
    """
    Find leftmost occurrence of target in sorted array.
    
    Args:
        arr: Sorted list to search
        target: Element to find
        
    Returns:
        Index of leftmost occurrence, -1 if not found
    """
    left, right = 0, len(arr) - 1
    result = -1
    
    while left <= right:
        mid = (left + right) // 2
        
        if arr[mid] == target:
            result = mid
            right = mid - 1  # Continue searching left
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return result

def binary_search_rightmost(arr: List[T], target: T) -> int:
    """
    Find rightmost occurrence of target in sorted array.
    
    Args:
        arr: Sorted list to search
        target: Element to find
        
    Returns:
        Index of rightmost occurrence, -1 if not found
    """
    left, right = 0, len(arr) - 1
    result = -1
    
    while left <= right:
        mid = (left + right) // 2
        
        if arr[mid] == target:
            result = mid
            left = mid + 1  # Continue searching right
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return result

def ternary_search(arr: List[T], target: T) -> int:
    """
    Ternary search implementation (assumes sorted array).
    
    Time Complexity: O(log₃ n)
    Space Complexity: O(1)
    
    Args:
        arr: Sorted list to search
        target: Element to find
        
    Returns:
        Index of target, -1 if not found
    """
    left, right = 0, len(arr) - 1
    
    while left <= right:
        # Divide into three parts
        mid1 = left + (right - left) // 3
        mid2 = right - (right - left) // 3
        
        if arr[mid1] == target:
            return mid1
        if arr[mid2] == target:
            return mid2
        
        if target < arr[mid1]:
            right = mid1 - 1
        elif target > arr[mid2]:
            left = mid2 + 1
        else:
            left = mid1 + 1
            right = mid2 - 1
    
    return -1

def exponential_search(arr: List[T], target: T) -> int:
    """
    Exponential search implementation.
    
    Time Complexity: O(log n)
    Space Complexity: O(1)
    
    Args:
        arr: Sorted list to search
        target: Element to find
        
    Returns:
        Index of target, -1 if not found
    """
    if not arr:
        return -1
    
    if arr[0] == target:
        return 0
    
    # Find range for binary search
    bound = 1
    while bound < len(arr) and arr[bound] < target:
        bound *= 2
    
    # Binary search in the range
    left = bound // 2
    right = min(bound, len(arr) - 1)
    
    return binary_search(arr[left:right+1], target) + left if binary_search(arr[left:right+1], target) != -1 else -1

def interpolation_search(arr: List[int], target: int) -> int:
    """
    Interpolation search for uniformly distributed sorted arrays.
    
    Time Complexity: O(log log n) average, O(n) worst
    Space Complexity: O(1)
    
    Args:
        arr: Sorted list of integers
        target: Integer to find
        
    Returns:
        Index of target, -1 if not found
    """
    left, right = 0, len(arr) - 1
    
    while left <= right and target >= arr[left] and target <= arr[right]:
        if left == right:
            return left if arr[left] == target else -1
        
        # Interpolation formula
        pos = left + ((target - arr[left]) * (right - left)) // (arr[right] - arr[left])
        
        if arr[pos] == target:
            return pos
        elif arr[pos] < target:
            left = pos + 1
        else:
            right = pos - 1
    
    return -1

# Define public interface
__all__ = [
    'linear_search',
    'binary_search',
    'binary_search_leftmost',
    'binary_search_rightmost', 
    'ternary_search',
    'exponential_search',
    'interpolation_search'
]
```

### Using Packages

```python
# package_usage_demo.py - Demonstrating package usage

print("=== Package Usage Demonstration ===")

# Method 1: Import entire package
import competitive_programming as cp

print(f"Package version: {cp.get_version()}")
print(f"Available algorithms: {cp.list_algorithms()}")

# Method 2: Import specific submodules
from competitive_programming.algorithms import sorting, searching
from competitive_programming.utils import input_parser

# Test sorting algorithms
test_array = [64, 34, 25, 12, 22, 11, 90]
print(f"\nOriginal array: {test_array}")

# Test different sorting algorithms
sorted_bubble = sorting.bubble_sort(test_array)
sorted_quick = sorting.quick_sort(test_array)
sorted_merge = sorting.merge_sort(test_array)

print(f"Bubble sort: {sorted_bubble}")
print(f"Quick sort: {sorted_quick}")
print(f"Merge sort: {sorted_merge}")

# Benchmark sorting algorithms
print("\n=== Sorting Algorithm Benchmark ===")
benchmark_results = sorting.benchmark_sorting_algorithms(test_array)
for algorithm, result in benchmark_results.items():
    if 'error' in result:
        print(f"{algorithm}: ERROR - {result['error']}")
    else:
        print(f"{algorithm}: {result['time']:.6f}s, Correct: {result['correct']}")

# Test searching algorithms
sorted_array = [1, 3, 5, 7, 9, 11, 13, 15, 17, 19]
target = 11

print(f"\n=== Searching Algorithms ===")
print(f"Searching for {target} in {sorted_array}")

linear_result = searching.linear_search(sorted_array, target)
binary_result = searching.binary_search(sorted_array, target)
ternary_result = searching.ternary_search(sorted_array, target)

print(f"Linear search result: {linear_result}")
print(f"Binary search result: {binary_result}")
print(f"Ternary search result: {ternary_result}")

# Test with duplicates
array_with_dups = [1, 2, 2, 2, 3, 4, 4, 5]
target_dup = 2

print(f"\nSearching for {target_dup} in {array_with_dups}")
leftmost = searching.binary_search_leftmost(array_with_dups, target_dup)
rightmost = searching.binary_search_rightmost(array_with_dups, target_dup)

print(f"Leftmost occurrence: {leftmost}")
print(f"Rightmost occurrence: {rightmost}")

# Method 3: Import specific functions
from competitive_programming.algorithms.sorting import quick_sort, merge_sort
from competitive_programming.algorithms.searching import binary_search

# Direct function usage
large_array = list(range(100, 0, -1))  # [100, 99, 98, ..., 1]
sorted_large = quick_sort(large_array)
search_result = binary_search(sorted_large, 50)

print(f"\nSorted large array (first 10): {sorted_large[:10]}")
print(f"Found 50 at index: {search_result}")

# Method 4: Dynamic package exploration
def explore_package(package):
    """Explore package structure dynamically."""
    
    import pkgutil
    import inspect
    
    print(f"\n=== Exploring Package: {package.__name__} ===")
    
    # Walk through package modules
    for importer, modname, ispkg in pkgutil.walk_packages(
        package.__path__, 
        package.__name__ + "."
    ):
        print(f"{'Package' if ispkg else 'Module'}: {modname}")
        
        # Try to import and explore
        try:
            module = importer.find_module(modname).load_module(modname)
            
            # List functions in module
            functions = [name for name, obj in inspect.getmembers(module) 
                        if inspect.isfunction(obj) and not name.startswith('_')]
            
            if functions:
                print(f"  Functions: {functions[:3]}{'...' if len(functions) > 3 else ''}")
        
        except Exception as e:
            print(f"  Error importing: {e}")

# Explore our package
try:
    explore_package(competitive_programming)
except Exception as e:
    print(f"Package exploration failed: {e}")

# Method 5: Package-level configuration
def configure_package():
    """Demonstrate package-level configuration."""
    
    # Check if package has configuration
    if hasattr(competitive_programming, 'config'):
        config = competitive_programming.config
        print(f"\nPackage configuration: {config}")
    
    # Set package-level options (if supported)
    # competitive_programming.set_debug_mode(True)
    # competitive_programming.set_optimization_level('high')
    
    print("\nPackage configured for optimal performance")

configure_package()

# Method 6: Package version and dependency checking
def check_package_info():
    """Check package information and dependencies."""
    
    print(f"\n=== Package Information ===")
    
    # Basic package info
    if hasattr(competitive_programming, '__version__'):
        print(f"Version: {competitive_programming.__version__}")
    
    if hasattr(competitive_programming, '__author__'):
        print(f"Author: {competitive_programming.__author__}")
    
    # Check for optional dependencies
    optional_deps = {
        'numpy': 'NumPy for numerical computations',
        'matplotlib': 'Matplotlib for plotting',
        'networkx': 'NetworkX for graph algorithms'
    }
    
    print(f"\nOptional dependencies:")
    for dep, description in optional_deps.items():
        try:
            __import__(dep)
            print(f"  ✓ {dep}: {description}")
        except ImportError:
            print(f"  ✗ {dep}: {description} (not installed)")

check_package_info()

# Method 7: Custom package finder
class CustomPackageFinder:
    """Custom package finder for specialized imports."""
    
    def __init__(self, base_package):
        self.base_package = base_package
    
    def find_algorithm(self, algorithm_name):
        """Find algorithm by name across all submodules."""
        
        import pkgutil
        import inspect
        
        for importer, modname, ispkg in pkgutil.walk_packages(
            self.base_package.__path__, 
            self.base_package.__name__ + "."
        ):
            if ispkg:
                continue
            
            try:
                module = importer.find_module(modname).load_module(modname)
                
                if hasattr(module, algorithm_name):
                    return getattr(module, algorithm_name)
                
            except Exception:
                continue
        
        return None
    
    def list_all_algorithms(self):
        """List all available algorithms."""
        
        import pkgutil
        import inspect
        
        algorithms = {}
        
        for importer, modname, ispkg in pkgutil.walk_packages(
            self.base_package.__path__, 
            self.base_package.__name__ + "."
        ):
            if ispkg:
                continue
            
            try:
                module = importer.find_module(modname).load_module(modname)
                
                # Get all functions
                functions = [name for name, obj in inspect.getmembers(module) 
                           if inspect.isfunction(obj) and not name.startswith('_')]
                
                if functions:
                    algorithms[modname] = functions
                
            except Exception:
                continue
        
        return algorithms

# Test custom package finder
finder = CustomPackageFinder(competitive_programming)

# Find specific algorithm
quick_sort_func = finder.find_algorithm('quick_sort')
if quick_sort_func:
    test_result = quick_sort_func([3, 1, 4, 1, 5])
    print(f"\nFound quick_sort: {test_result}")

# List all algorithms
all_algorithms = finder.list_all_algorithms()
print(f"\nAll available algorithms:")
for module, funcs in all_algorithms.items():
    print(f"  {module}: {len(funcs)} functions")
```

## 🎯 Practice Exercises

### Exercise 1: Data Processing Package

```python
def create_data_processing_package():
    """
    Create a data processing package with:
    1. File readers for different formats (CSV, JSON, XML)
    2. Data transformers and validators
    3. Statistical analysis modules
    4. Export utilities
    5. Configuration management
    """
    # Your implementation here
    pass
```

### Exercise 2: Algorithm Visualization Package

```python
def build_algorithm_visualization():
    """
    Build an algorithm visualization package with:
    1. Sorting algorithm animators
    2. Graph algorithm visualizers
    3. Data structure viewers
    4. Performance profilers
    5. Interactive demonstrations
    """
    # Your implementation here
    pass
```

### Exercise 3: Competitive Programming Toolkit

```python
def create_cp_toolkit():
    """
    Create a comprehensive competitive programming toolkit with:
    1. Template generators for different problem types
    2. Input/output handlers
    3. Common algorithm implementations
    4. Testing and benchmarking utilities
    5. Submission helpers
    """
    # Your implementation here
    pass
```

## 📚 Summary and Best Practices

### Module Organization Guidelines

**Single Responsibility:**
- Each module should have one clear purpose
- Group related functions and classes together
- Separate different concerns into different modules

**Naming Conventions:**
- Use lowercase with underscores for module names
- Choose descriptive, meaningful names
- Avoid conflicts with built-in modules

**Documentation:**
- Always include module docstrings
- Document all public functions and classes
- Provide usage examples

### Package Structure Best Practices

**Directory Organization:**
```
package_name/
├── __init__.py          # Package initialization
├── core/                # Core functionality
│   ├── __init__.py
│   └── module.py
├── utils/               # Utility functions
│   ├── __init__.py
│   └── helpers.py
├── tests/               # Test modules
│   ├── __init__.py
│   └── test_core.py
└── docs/                # Documentation
    └── README.md
```

**Import Strategy:**
- Use relative imports within packages
- Import only what you need
- Avoid circular imports
- Use `__all__` to control public interface

### Module and Package Checklist

**Module Development:**
- [ ] Clear module purpose and scope
- [ ] Comprehensive docstrings
- [ ] Proper error handling
- [ ] Unit tests included
- [ ] Performance considerations

**Package Development:**
- [ ] Logical directory structure
- [ ] Proper `__init__.py` files
- [ ] Version management
- [ ] Dependency handling
- [ ] Installation scripts

**Distribution Preparation:**
- [ ] setup.py or pyproject.toml
- [ ] README with usage examples
- [ ] License file
- [ ] Change log
- [ ] Documentation

### Import Performance Tips

**Lazy Imports:**
- Import modules only when needed
- Use local imports in functions for optional dependencies
- Consider dynamic imports for plugins

**Import Optimization:**
- Minimize imports in `__init__.py`
- Use `from module import specific_function`
- Avoid `import *` in production code

### Testing Modules and Packages

**Unit Testing:**
```python
import unittest
from your_package import your_module

class TestYourModule(unittest.TestCase):
    def test_function(self):
        result = your_module.function(input_data)
        self.assertEqual(result, expected_output)
```

**Integration Testing:**
```python
def test_package_integration():
    """Test that package components work together."""
    from your_package import module1, module2
    
    data = module1.process_data(raw_data)
    result = module2.analyze_data(data)
    
    assert result is not None
```

### Common Pitfalls to Avoid

1. **Circular Imports**: Design modules to avoid mutual dependencies
2. **Large `__init__.py`**: Keep package initialization lightweight
3. **Missing `__all__`**: Define public interface explicitly
4. **Relative Import Issues**: Use proper relative import syntax
5. **Module Path Problems**: Understand sys.path behavior

### Advanced Package Features

**Entry Points:**
```python
# setup.py
entry_points={
    'console_scripts': [
        'mycommand=mypackage.cli:main',
    ],
}
```

**Plugin Systems:**
```python
# Using entry points for plugins
import pkg_resources

for entry_point in pkg_resources.iter_entry_points('mypackage.plugins'):
    plugin = entry_point.load()
    plugin.register()
```

### Next Steps

After mastering modules and packages:
1. Learn about [Regular Expressions](./16-regular-expressions.md)
2. Study package distribution (PyPI, pip)
3. Explore advanced import mechanisms
4. Learn about namespace packages
5. Practice building real-world packages

---

**Remember**: Well-organized modules and packages are the foundation of maintainable Python applications. Focus on clear interfaces, good documentation, and logical organization!
