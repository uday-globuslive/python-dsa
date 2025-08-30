# Comments and Documentation

## 🎯 Objective
Master the art of writing clear, meaningful comments and comprehensive documentation that enhances code readability, maintainability, and collaboration.

## 📖 Overview

Good documentation is as important as good code. Comments and documentation serve as communication tools between developers, including your future self. In Python, there are multiple ways to document code: inline comments, block comments, docstrings, and external documentation. Understanding when and how to use each type effectively is crucial for professional software development.

## 🔍 Types of Comments and Documentation

### 1. Inline Comments

Inline comments appear on the same line as code and explain specific implementation details.

```python
# Good inline comments - explain the "why", not the "what"
user_age = 25
tax_rate = 0.08  # State sales tax rate for California

# Calculate compound interest with monthly compounding
final_amount = principal * (1 + annual_rate/12)**(12 * years)

# Use binary search for O(log n) performance on sorted array
result = binary_search(sorted_numbers, target)

# Handle edge case where division by zero could occur
average = total / count if count > 0 else 0
```

```python
# Bad inline comments - state the obvious
user_age = 25  # Set user age to 25
x = x + 1      # Increment x by 1
print("Hello") # Print hello
```

### 2. Block Comments

Block comments explain larger sections of code or complex algorithms.

```python
# Calculate the optimal portfolio allocation using Modern Portfolio Theory
# This implementation uses the mean-variance optimization approach:
# 1. Calculate expected returns for each asset
# 2. Compute the covariance matrix of returns
# 3. Solve the quadratic optimization problem
# 4. Apply constraints (weights sum to 1, no short selling)

expected_returns = calculate_expected_returns(price_data)
covariance_matrix = calculate_covariance_matrix(price_data)
constraints = create_optimization_constraints(num_assets)
optimal_weights = solve_portfolio_optimization(
    expected_returns, covariance_matrix, constraints
)
```

```python
# Complex algorithm explanation with step-by-step breakdown
def dijkstra_shortest_path(graph, start_node, end_node):
    """
    Implementation of Dijkstra's algorithm for finding shortest paths.
    
    Algorithm steps:
    1. Initialize distances to all nodes as infinity, except start (0)
    2. Create a priority queue with all nodes
    3. While queue is not empty:
       a. Extract node with minimum distance
       b. For each neighbor, calculate tentative distance
       c. If tentative distance < current distance, update it
    4. Return the shortest path distance and route
    """
    
    # Step 1: Initialize distances and previous nodes tracking
    distances = {node: float('infinity') for node in graph.nodes}
    distances[start_node] = 0
    previous_nodes = {node: None for node in graph.nodes}
    
    # Step 2: Create priority queue (min-heap) with all unvisited nodes
    unvisited_nodes = PriorityQueue()
    for node in graph.nodes:
        unvisited_nodes.put((distances[node], node))
    
    # Step 3: Main algorithm loop
    while not unvisited_nodes.empty():
        # Step 3a: Extract node with minimum distance
        current_distance, current_node = unvisited_nodes.get()
        
        # Skip if we've already found a shorter path to this node
        if current_distance > distances[current_node]:
            continue
        
        # Stop if we reached the destination
        if current_node == end_node:
            break
        
        # Step 3b & 3c: Check all neighbors and update distances
        for neighbor, weight in graph.get_neighbors(current_node):
            tentative_distance = distances[current_node] + weight
            
            if tentative_distance < distances[neighbor]:
                distances[neighbor] = tentative_distance
                previous_nodes[neighbor] = current_node
                unvisited_nodes.put((tentative_distance, neighbor))
    
    # Step 4: Reconstruct and return the shortest path
    return reconstruct_path(previous_nodes, start_node, end_node)
```

### 3. Docstrings

Docstrings are Python's built-in documentation mechanism using triple quotes.

#### Function Docstrings

```python
def calculate_loan_payment(principal, annual_rate, years, payment_frequency=12):
    """
    Calculate monthly payment for a fixed-rate loan using the standard formula.
    
    This function implements the standard loan payment formula:
    M = P * [r(1+r)^n] / [(1+r)^n - 1]
    
    Where:
    - M = Monthly payment
    - P = Principal amount
    - r = Monthly interest rate
    - n = Total number of payments
    
    Args:
        principal (float): The loan principal amount in dollars.
            Must be positive.
        annual_rate (float): Annual interest rate as a decimal (e.g., 0.05 for 5%).
            Must be non-negative.
        years (int): Loan term in years. Must be positive.
        payment_frequency (int, optional): Number of payments per year.
            Defaults to 12 (monthly payments). Common values: 12, 24, 52.
    
    Returns:
        float: The payment amount per period, rounded to 2 decimal places.
    
    Raises:
        ValueError: If principal <= 0, years <= 0, or payment_frequency <= 0.
        TypeError: If any argument is not a number.
    
    Examples:
        >>> calculate_loan_payment(200000, 0.05, 30)
        1073.64
        
        >>> calculate_loan_payment(50000, 0.035, 5, 12)
        911.61
        
        >>> calculate_loan_payment(10000, 0.0, 2)  # Zero interest
        416.67
    
    Note:
        For zero interest rates, the function automatically uses simple
        division: principal / total_payments.
    """
    # Input validation
    if not all(isinstance(x, (int, float)) for x in [principal, annual_rate, years]):
        raise TypeError("All arguments must be numeric")
    
    if principal <= 0:
        raise ValueError("Principal must be positive")
    
    if years <= 0:
        raise ValueError("Loan term must be positive")
    
    if payment_frequency <= 0:
        raise ValueError("Payment frequency must be positive")
    
    # Handle zero interest rate case
    if annual_rate == 0:
        return round(principal / (years * payment_frequency), 2)
    
    # Calculate payment using standard formula
    monthly_rate = annual_rate / payment_frequency
    total_payments = years * payment_frequency
    
    # Apply loan payment formula
    numerator = monthly_rate * (1 + monthly_rate) ** total_payments
    denominator = (1 + monthly_rate) ** total_payments - 1
    payment = principal * (numerator / denominator)
    
    return round(payment, 2)
```

#### Class Docstrings

```python
class BankAccount:
    """
    A bank account class that manages account balance and transactions.
    
    This class provides a simple interface for banking operations including
    deposits, withdrawals, and balance inquiries. It maintains transaction
    history and enforces business rules like minimum balance requirements.
    
    Attributes:
        account_number (str): Unique identifier for the account.
        account_holder (str): Name of the account holder.
        balance (float): Current account balance in dollars.
        minimum_balance (float): Minimum required balance (default: 0).
        transaction_history (list): List of all transactions as dictionaries.
        is_active (bool): Whether the account is currently active.
    
    Class Attributes:
        TRANSACTION_FEE (float): Fee charged for each transaction ($1.50).
        OVERDRAFT_FEE (float): Fee for overdraft attempts ($35.00).
        MAX_DAILY_WITHDRAWALS (int): Maximum withdrawals per day (6).
    
    Examples:
        >>> account = BankAccount("12345", "John Doe", 1000.0)
        >>> account.deposit(500.0)
        True
        >>> account.get_balance()
        1500.0
        >>> account.withdraw(200.0)
        True
        >>> account.get_balance()
        1300.0
    
    Note:
        All monetary amounts should be provided as floats with up to 2
        decimal places representing dollars and cents.
    """
    
    # Class constants
    TRANSACTION_FEE = 1.50
    OVERDRAFT_FEE = 35.00
    MAX_DAILY_WITHDRAWALS = 6
    
    def __init__(self, account_number, account_holder, initial_balance=0.0, minimum_balance=0.0):
        """
        Initialize a new bank account.
        
        Args:
            account_number (str): Unique account identifier.
            account_holder (str): Name of the account holder.
            initial_balance (float, optional): Starting balance. Defaults to 0.0.
            minimum_balance (float, optional): Minimum required balance. Defaults to 0.0.
        
        Raises:
            ValueError: If initial_balance < minimum_balance or if any amount is negative.
            TypeError: If account_number or account_holder is not a string.
        """
        if not isinstance(account_number, str) or not isinstance(account_holder, str):
            raise TypeError("Account number and holder name must be strings")
        
        if initial_balance < 0 or minimum_balance < 0:
            raise ValueError("Balances cannot be negative")
        
        if initial_balance < minimum_balance:
            raise ValueError("Initial balance cannot be below minimum balance")
        
        self.account_number = account_number
        self.account_holder = account_holder
        self.balance = round(initial_balance, 2)
        self.minimum_balance = round(minimum_balance, 2)
        self.transaction_history = []
        self.is_active = True
        self._daily_withdrawals = 0
        self._last_withdrawal_date = None
        
        # Record initial deposit if balance > 0
        if initial_balance > 0:
            self._record_transaction("INITIAL_DEPOSIT", initial_balance, "Account opening")
    
    def deposit(self, amount, description="Deposit"):
        """
        Deposit money into the account.
        
        Args:
            amount (float): Amount to deposit (must be positive).
            description (str, optional): Transaction description.
        
        Returns:
            bool: True if deposit was successful, False otherwise.
        
        Raises:
            ValueError: If amount is not positive.
            TypeError: If amount is not a number.
            RuntimeError: If account is not active.
        """
        if not self.is_active:
            raise RuntimeError("Cannot deposit to inactive account")
        
        if not isinstance(amount, (int, float)):
            raise TypeError("Deposit amount must be a number")
        
        if amount <= 0:
            raise ValueError("Deposit amount must be positive")
        
        # Apply transaction fee
        net_deposit = amount - self.TRANSACTION_FEE
        if net_deposit <= 0:
            return False  # Transaction fee exceeds deposit amount
        
        self.balance += net_deposit
        self.balance = round(self.balance, 2)
        
        self._record_transaction("DEPOSIT", net_deposit, description)
        return True
    
    def withdraw(self, amount, description="Withdrawal"):
        """
        Withdraw money from the account.
        
        Enforces daily withdrawal limits, minimum balance requirements,
        and applies appropriate fees.
        
        Args:
            amount (float): Amount to withdraw (must be positive).
            description (str, optional): Transaction description.
        
        Returns:
            bool: True if withdrawal was successful, False otherwise.
        
        Raises:
            ValueError: If amount is not positive.
            TypeError: If amount is not a number.
            RuntimeError: If account is not active.
        """
        if not self.is_active:
            raise RuntimeError("Cannot withdraw from inactive account")
        
        if not isinstance(amount, (int, float)):
            raise TypeError("Withdrawal amount must be a number")
        
        if amount <= 0:
            raise ValueError("Withdrawal amount must be positive")
        
        # Check daily withdrawal limit
        if self._check_daily_withdrawal_limit():
            return False
        
        # Calculate total amount including fees
        total_amount = amount + self.TRANSACTION_FEE
        
        # Check if withdrawal would violate minimum balance
        if (self.balance - total_amount) < self.minimum_balance:
            # Apply overdraft fee and record failed attempt
            self.balance -= self.OVERDRAFT_FEE
            self._record_transaction("OVERDRAFT_FEE", -self.OVERDRAFT_FEE, 
                                   f"Failed withdrawal attempt: ${amount}")
            return False
        
        # Process successful withdrawal
        self.balance -= total_amount
        self.balance = round(self.balance, 2)
        self._increment_daily_withdrawals()
        
        self._record_transaction("WITHDRAWAL", -amount, description)
        return True
    
    def get_balance(self):
        """
        Get the current account balance.
        
        Returns:
            float: Current balance rounded to 2 decimal places.
        """
        return round(self.balance, 2)
    
    def get_transaction_history(self, limit=None):
        """
        Retrieve transaction history for the account.
        
        Args:
            limit (int, optional): Maximum number of recent transactions to return.
                If None, returns all transactions.
        
        Returns:
            list: List of transaction dictionaries, most recent first.
                Each dictionary contains: timestamp, type, amount, description, balance_after.
        """
        history = sorted(self.transaction_history, 
                        key=lambda x: x['timestamp'], reverse=True)
        
        if limit is not None and limit > 0:
            return history[:limit]
        
        return history
    
    def _record_transaction(self, transaction_type, amount, description):
        """
        Record a transaction in the account history.
        
        Args:
            transaction_type (str): Type of transaction (DEPOSIT, WITHDRAWAL, etc.).
            amount (float): Transaction amount (positive for credits, negative for debits).
            description (str): Transaction description.
        """
        from datetime import datetime
        
        transaction = {
            'timestamp': datetime.now(),
            'type': transaction_type,
            'amount': round(amount, 2),
            'description': description,
            'balance_after': round(self.balance, 2)
        }
        
        self.transaction_history.append(transaction)
    
    def _check_daily_withdrawal_limit(self):
        """
        Check if daily withdrawal limit has been reached.
        
        Returns:
            bool: True if limit reached, False otherwise.
        """
        from datetime import date
        
        today = date.today()
        
        # Reset counter if it's a new day
        if self._last_withdrawal_date != today:
            self._daily_withdrawals = 0
            self._last_withdrawal_date = today
        
        return self._daily_withdrawals >= self.MAX_DAILY_WITHDRAWALS
    
    def _increment_daily_withdrawals(self):
        """Increment the daily withdrawal counter."""
        from datetime import date
        
        today = date.today()
        if self._last_withdrawal_date != today:
            self._daily_withdrawals = 0
            self._last_withdrawal_date = today
        
        self._daily_withdrawals += 1
    
    def __str__(self):
        """
        Return a string representation of the account.
        
        Returns:
            str: Human-readable account information.
        """
        status = "Active" if self.is_active else "Inactive"
        return (f"BankAccount({self.account_number}): "
                f"{self.account_holder}, Balance: ${self.balance:.2f}, "
                f"Status: {status}")
    
    def __repr__(self):
        """
        Return a detailed string representation for debugging.
        
        Returns:
            str: Detailed account information for debugging.
        """
        return (f"BankAccount(account_number='{self.account_number}', "
                f"account_holder='{self.account_holder}', "
                f"balance={self.balance}, minimum_balance={self.minimum_balance}, "
                f"is_active={self.is_active})")
```

#### Module Docstrings

```python
"""
Financial Calculator Module

This module provides a comprehensive set of financial calculation functions
for common personal and business finance operations including loans, investments,
retirement planning, and tax calculations.

The module is designed to be both educational and practical, with clear
implementations of standard financial formulas and extensive documentation
for learning purposes.

Key Features:
    - Loan and mortgage calculations
    - Investment growth and compound interest
    - Retirement planning tools
    - Tax calculation utilities
    - Risk assessment functions

Usage Example:
    >>> import financial_calculator as fc
    >>> monthly_payment = fc.calculate_loan_payment(200000, 0.05, 30)
    >>> future_value = fc.compound_interest(10000, 0.07, 10)
    >>> retirement_goal = fc.retirement_planning(current_age=30, retirement_age=65, 
    ...                                          current_savings=50000, monthly_contribution=500)

Dependencies:
    - math: For mathematical operations
    - datetime: For date calculations
    - typing: For type hints

Author: Financial Calculator Team
Version: 2.1.0
Created: 2024-01-15
Last Modified: 2024-01-20

License:
    MIT License - See LICENSE file for details
"""

import math
from datetime import datetime, date
from typing import Optional, List, Dict, Tuple, Union

# Module constants
DEFAULT_COMPOUND_FREQUENCY = 12  # Monthly compounding
DAYS_PER_YEAR = 365.25  # Average including leap years
MONTHS_PER_YEAR = 12

# Tax brackets for 2024 (example - would be updated annually)
FEDERAL_TAX_BRACKETS_2024 = [
    (0, 11000, 0.10),
    (11000, 44725, 0.12),
    (44725, 95375, 0.22),
    (95375, 182050, 0.24),
    (182050, 231250, 0.32),
    (231250, 578125, 0.35),
    (578125, float('inf'), 0.37)
]
```

## 📝 Documentation Standards and Best Practices

### PEP 257 Docstring Conventions

```python
def calculate_compound_interest(principal, rate, time, frequency=1):
    """Calculate compound interest using the standard formula.
    
    The compound interest formula is: A = P(1 + r/n)^(nt)
    Where A is the final amount, P is principal, r is annual rate,
    n is compounding frequency, and t is time in years.
    
    Args:
        principal (float): Initial investment amount.
        rate (float): Annual interest rate as decimal.
        time (float): Investment period in years.
        frequency (int): Compounding frequency per year.
    
    Returns:
        float: Final amount after compound interest.
    """
    return principal * (1 + rate/frequency) ** (frequency * time)

class Investment:
    """Represents an investment portfolio with tracking capabilities."""
    
    def __init__(self, name):
        """Initialize investment with a name."""
        self.name = name
    
    def add_position(self, symbol, shares, price):
        """Add a stock position to the portfolio."""
        pass
```

### Google Style Docstrings

```python
def calculate_portfolio_performance(positions, start_date, end_date):
    """Calculate the performance metrics for an investment portfolio.
    
    This function analyzes portfolio performance over a specified time period,
    calculating key metrics including total return, annualized return, volatility,
    and Sharpe ratio.
    
    Args:
        positions (List[Dict[str, Union[str, float]]]): List of portfolio positions.
            Each position should be a dictionary with keys:
            - 'symbol' (str): Stock ticker symbol
            - 'shares' (float): Number of shares owned
            - 'purchase_price' (float): Price per share at purchase
            - 'purchase_date' (str): Purchase date in 'YYYY-MM-DD' format
        start_date (str): Analysis start date in 'YYYY-MM-DD' format.
        end_date (str): Analysis end date in 'YYYY-MM-DD' format.
    
    Returns:
        Dict[str, float]: Performance metrics containing:
            - 'total_return': Total return as decimal (e.g., 0.15 for 15%)
            - 'annualized_return': Annualized return rate
            - 'volatility': Portfolio volatility (standard deviation)
            - 'sharpe_ratio': Risk-adjusted return metric
            - 'max_drawdown': Maximum decline from peak
    
    Raises:
        ValueError: If date format is invalid or end_date <= start_date.
        KeyError: If required position keys are missing.
        TypeError: If positions is not a list or contains non-dict elements.
    
    Example:
        >>> positions = [
        ...     {'symbol': 'AAPL', 'shares': 100, 'purchase_price': 150.0, 
        ...      'purchase_date': '2023-01-01'},
        ...     {'symbol': 'GOOGL', 'shares': 50, 'purchase_price': 2800.0,
        ...      'purchase_date': '2023-01-15'}
        ... ]
        >>> metrics = calculate_portfolio_performance(positions, '2023-01-01', '2023-12-31')
        >>> print(f"Total Return: {metrics['total_return']:.2%}")
        Total Return: 24.50%
    
    Note:
        This function requires internet access to fetch current stock prices.
        Historical price data is retrieved from Yahoo Finance API.
    """
    # Implementation would go here
    pass
```

### Sphinx/reStructuredText Style

```python
def monte_carlo_simulation(initial_value, annual_return, volatility, years, simulations=1000):
    """
    Run Monte Carlo simulation for investment projections.
    
    Simulates potential investment outcomes using random sampling based on
    historical return distributions to provide probability-based projections.
    
    :param initial_value: Starting investment amount
    :type initial_value: float
    :param annual_return: Expected annual return rate (as decimal)
    :type annual_return: float
    :param volatility: Annual volatility (standard deviation of returns)
    :type volatility: float
    :param years: Investment time horizon in years
    :type years: int
    :param simulations: Number of simulation runs to perform
    :type simulations: int
    :returns: Dictionary with simulation results including percentiles and statistics
    :rtype: Dict[str, Union[float, List[float]]]
    :raises ValueError: if any parameter is negative or simulations < 1
    :raises TypeError: if parameters are not numeric types
    
    .. note::
       Uses normal distribution for return modeling. Real market returns
       may exhibit fat tails and skewness not captured by this model.
    
    .. warning::
       Monte Carlo simulations are probabilistic models and should not be
       used as guarantees of future performance.
    
    Example:
        >>> results = monte_carlo_simulation(10000, 0.07, 0.15, 30, 10000)
        >>> print(f"Median projection: ${results['percentile_50']:,.2f}")
        >>> print(f"10th percentile: ${results['percentile_10']:,.2f}")
        >>> print(f"90th percentile: ${results['percentile_90']:,.2f}")
    """
    import random
    import statistics
    
    if any(x < 0 for x in [initial_value, volatility, years]):
        raise ValueError("Initial value, volatility, and years must be non-negative")
    
    if simulations < 1:
        raise ValueError("Number of simulations must be at least 1")
    
    results = []
    
    for _ in range(simulations):
        current_value = initial_value
        
        for year in range(years):
            # Generate random return based on normal distribution
            random_return = random.gauss(annual_return, volatility)
            current_value *= (1 + random_return)
        
        results.append(current_value)
    
    # Calculate statistics
    results.sort()
    
    return {
        'mean': statistics.mean(results),
        'median': statistics.median(results),
        'std_dev': statistics.stdev(results),
        'min': min(results),
        'max': max(results),
        'percentile_10': results[int(0.10 * len(results))],
        'percentile_25': results[int(0.25 * len(results))],
        'percentile_50': results[int(0.50 * len(results))],
        'percentile_75': results[int(0.75 * len(results))],
        'percentile_90': results[int(0.90 * len(results))],
        'all_results': results
    }
```

## 🔧 Advanced Documentation Techniques

### Type Hints with Documentation

```python
from typing import List, Dict, Optional, Union, Tuple, Callable
from datetime import datetime

def process_financial_data(
    data: List[Dict[str, Union[float, str, datetime]]],
    filters: Optional[Dict[str, Union[str, float]]] = None,
    aggregation_func: Callable[[List[float]], float] = sum,
    include_metadata: bool = True
) -> Tuple[List[Dict[str, Union[float, str]]], Dict[str, Union[int, float]]]:
    """
    Process and aggregate financial data with optional filtering.
    
    Takes raw financial data records and applies filters, aggregations,
    and transformations to produce clean, analyzed results suitable for
    reporting or further analysis.
    
    Args:
        data: List of financial records. Each record must be a dictionary
            containing at minimum 'amount' (float) and 'date' (datetime).
            Additional fields like 'category', 'description' are optional.
            
        filters: Optional filtering criteria. Supported filter keys:
            - 'min_amount' (float): Minimum transaction amount
            - 'max_amount' (float): Maximum transaction amount  
            - 'category' (str): Exact category match
            - 'start_date' (str): Start date in 'YYYY-MM-DD' format
            - 'end_date' (str): End date in 'YYYY-MM-DD' format
            
        aggregation_func: Function to aggregate numeric values.
            Must accept List[float] and return float. Common options:
            - sum: Total of all values (default)
            - statistics.mean: Average value
            - statistics.median: Median value
            - max/min: Maximum/minimum value
            
        include_metadata: Whether to include processing metadata in results.
            If True, returns additional statistics about the processing.
    
    Returns:
        A tuple containing:
        - Processed data records (filtered and cleaned)
        - Metadata dictionary with processing statistics:
            * 'records_processed': Number of input records
            * 'records_filtered': Number of records after filtering
            * 'total_amount': Aggregated amount using aggregation_func
            * 'processing_time': Time taken in seconds
            * 'filters_applied': List of filters that were applied
    
    Raises:
        TypeError: If data is not a list or contains non-dictionary elements.
        ValueError: If required fields are missing from data records.
        KeyError: If aggregation_func is not callable.
    
    Example:
        >>> import statistics
        >>> from datetime import datetime
        >>> 
        >>> sample_data = [
        ...     {'amount': 100.0, 'date': datetime(2024, 1, 1), 'category': 'food'},
        ...     {'amount': 50.0, 'date': datetime(2024, 1, 2), 'category': 'transport'},
        ...     {'amount': 200.0, 'date': datetime(2024, 1, 3), 'category': 'food'}
        ... ]
        >>> 
        >>> filters = {'category': 'food', 'min_amount': 75.0}
        >>> processed, metadata = process_financial_data(
        ...     sample_data, 
        ...     filters, 
        ...     statistics.mean
        ... )
        >>> 
        >>> print(f"Processed {metadata['records_filtered']} records")
        >>> print(f"Average amount: ${metadata['total_amount']:.2f}")
        Processed 2 records
        Average amount: $150.00
    """
    import time
    from datetime import datetime
    
    start_time = time.time()
    
    # Input validation
    if not isinstance(data, list):
        raise TypeError("Data must be a list")
    
    if not callable(aggregation_func):
        raise TypeError("Aggregation function must be callable")
    
    # Validate data structure
    for i, record in enumerate(data):
        if not isinstance(record, dict):
            raise TypeError(f"Record {i} is not a dictionary")
        
        if 'amount' not in record or 'date' not in record:
            raise ValueError(f"Record {i} missing required fields 'amount' or 'date'")
    
    # Apply filters if provided
    filtered_data = data.copy()
    applied_filters = []
    
    if filters:
        if 'min_amount' in filters:
            filtered_data = [r for r in filtered_data if r['amount'] >= filters['min_amount']]
            applied_filters.append(f"min_amount >= {filters['min_amount']}")
        
        if 'max_amount' in filters:
            filtered_data = [r for r in filtered_data if r['amount'] <= filters['max_amount']]
            applied_filters.append(f"max_amount <= {filters['max_amount']}")
        
        if 'category' in filters:
            filtered_data = [r for r in filtered_data if r.get('category') == filters['category']]
            applied_filters.append(f"category == '{filters['category']}'")
        
        # Date filtering would be implemented here
        # ... additional filter logic
    
    # Process and clean data
    processed_records = []
    amounts = []
    
    for record in filtered_data:
        # Clean and validate record
        cleaned_record = {
            'amount': round(float(record['amount']), 2),
            'date': record['date'],
            'category': record.get('category', 'uncategorized'),
            'description': record.get('description', '').strip()
        }
        
        processed_records.append(cleaned_record)
        amounts.append(cleaned_record['amount'])
    
    # Calculate aggregation
    total_amount = aggregation_func(amounts) if amounts else 0.0
    
    # Prepare metadata
    processing_time = time.time() - start_time
    metadata = {
        'records_processed': len(data),
        'records_filtered': len(processed_records),
        'total_amount': round(total_amount, 2),
        'processing_time': round(processing_time, 4),
        'filters_applied': applied_filters
    }
    
    if not include_metadata:
        return processed_records, {}
    
    return processed_records, metadata
```

### Documentation for Complex Algorithms

```python
class RedBlackTree:
    """
    Implementation of a Red-Black Tree data structure.
    
    A Red-Black Tree is a self-balancing binary search tree where each node
    contains an extra bit to store its color (red or black). These color bits
    are used to ensure the tree remains approximately balanced during insertions
    and deletions.
    
    Red-Black Tree Properties:
        1. Every node is either red or black
        2. The root is black
        3. All leaves (NIL nodes) are black
        4. If a node is red, then both its children are black
        5. For each node, all simple paths from the node to descendant leaves
           contain the same number of black nodes
    
    These properties ensure that the longest path from root to leaf is no more
    than twice as long as the shortest path, guaranteeing O(log n) operations.
    
    Time Complexities:
        - Search: O(log n)
        - Insert: O(log n) 
        - Delete: O(log n)
        - Min/Max: O(log n)
    
    Space Complexity: O(n)
    
    Attributes:
        root (Node): Root node of the tree
        nil (Node): Sentinel node representing all leaves
        size (int): Number of nodes in the tree
    
    Example:
        >>> tree = RedBlackTree()
        >>> tree.insert(10)
        >>> tree.insert(5)
        >>> tree.insert(15)
        >>> print(tree.search(10))  # Returns the node containing 10
        >>> print(tree.size)        # Prints 3
    """
    
    class Node:
        """
        Node class for Red-Black Tree.
        
        Each node stores a key-value pair, color information, and pointers
        to parent and children nodes.
        
        Attributes:
            key: The key stored in this node
            value: The value associated with the key
            color: Either 'RED' or 'BLACK' 
            parent: Reference to parent node
            left: Reference to left child
            right: Reference to right child
        """
        
        def __init__(self, key, value=None, color='RED'):
            """
            Initialize a new node.
            
            Args:
                key: Key for this node
                value: Value associated with key (defaults to key if None)
                color: Node color, either 'RED' or 'BLACK' (default: 'RED')
            """
            self.key = key
            self.value = value if value is not None else key
            self.color = color
            self.parent = None
            self.left = None
            self.right = None
    
    def __init__(self):
        """Initialize an empty Red-Black Tree."""
        # Create sentinel nil node (always black)
        self.nil = self.Node(key=None, color='BLACK')
        self.nil.left = self.nil
        self.nil.right = self.nil
        self.nil.parent = self.nil
        
        # Root initially points to nil
        self.root = self.nil
        self.size = 0
    
    def insert(self, key, value=None):
        """
        Insert a new key-value pair into the tree.
        
        This method implements the standard Red-Black Tree insertion algorithm:
        1. Insert the node using standard BST insertion
        2. Color the new node red
        3. Fix any Red-Black Tree violations using rotations and recoloring
        
        The fixing process ensures all Red-Black Tree properties are maintained
        while keeping the tree balanced.
        
        Args:
            key: Key to insert (must be comparable)
            value: Value to associate with key (defaults to key if None)
        
        Raises:
            TypeError: If key is not comparable
        
        Time Complexity: O(log n)
        Space Complexity: O(1)
        
        Example:
            >>> tree = RedBlackTree()
            >>> tree.insert(10, "ten")
            >>> tree.insert(5, "five") 
            >>> tree.insert(15, "fifteen")
        """
        # Step 1: Create new node (initially red)
        new_node = self.Node(key, value, 'RED')
        new_node.left = self.nil
        new_node.right = self.nil
        
        # Step 2: Standard BST insertion
        parent = self.nil
        current = self.root
        
        # Find the correct position for the new node
        while current != self.nil:
            parent = current
            if new_node.key < current.key:
                current = current.left
            elif new_node.key > current.key:
                current = current.right
            else:
                # Key already exists, update value
                current.value = new_node.value
                return
        
        # Set parent relationship
        new_node.parent = parent
        
        # Determine if new node is left or right child
        if parent == self.nil:
            self.root = new_node  # Tree was empty
        elif new_node.key < parent.key:
            parent.left = new_node
        else:
            parent.right = new_node
        
        self.size += 1
        
        # Step 3: Fix Red-Black Tree violations
        self._insert_fixup(new_node)
    
    def _insert_fixup(self, node):
        """
        Fix Red-Black Tree violations after insertion.
        
        This method handles the cases where Red-Black Tree properties
        might be violated after inserting a red node. The violations
        occur when a red node has a red parent (property 4 violation).
        
        The algorithm handles three main cases:
        1. Uncle is red: Recolor parent, uncle, and grandparent
        2. Uncle is black and node is "inside": Rotate to make it "outside"
        3. Uncle is black and node is "outside": Rotate and recolor
        
        Args:
            node: The newly inserted node that might cause violations
        
        Time Complexity: O(log n) - at most O(log n) iterations
        """
        # Continue while there's a red-red violation
        while node.parent.color == 'RED':
            
            # Case A: Parent is left child of grandparent
            if node.parent == node.parent.parent.left:
                uncle = node.parent.parent.right
                
                # Case 1: Uncle is red
                if uncle.color == 'RED':
                    node.parent.color = 'BLACK'           # Parent becomes black
                    uncle.color = 'BLACK'                 # Uncle becomes black  
                    node.parent.parent.color = 'RED'      # Grandparent becomes red
                    node = node.parent.parent              # Move up the tree
                
                # Cases 2 & 3: Uncle is black
                else:
                    # Case 2: Node is right child (inside case)
                    if node == node.parent.right:
                        node = node.parent
                        self._left_rotate(node)
                    
                    # Case 3: Node is left child (outside case)
                    node.parent.color = 'BLACK'           # Parent becomes black
                    node.parent.parent.color = 'RED'      # Grandparent becomes red
                    self._right_rotate(node.parent.parent) # Rotate grandparent
            
            # Case B: Parent is right child of grandparent (symmetric to Case A)
            else:
                uncle = node.parent.parent.left
                
                # Case 1: Uncle is red
                if uncle.color == 'RED':
                    node.parent.color = 'BLACK'
                    uncle.color = 'BLACK'
                    node.parent.parent.color = 'RED'
                    node = node.parent.parent
                
                # Cases 2 & 3: Uncle is black
                else:
                    # Case 2: Node is left child (inside case)
                    if node == node.parent.left:
                        node = node.parent
                        self._right_rotate(node)
                    
                    # Case 3: Node is right child (outside case)
                    node.parent.color = 'BLACK'
                    node.parent.parent.color = 'RED'
                    self._left_rotate(node.parent.parent)
        
        # Ensure root is always black (property 2)
        self.root.color = 'BLACK'
    
    def _left_rotate(self, node):
        """
        Perform left rotation around the given node.
        
        Left rotation transforms the tree structure:
        
        Before rotation:     After rotation:
              x                   y
             / \                 / \
            α   y               x   γ
               / \             / \
              β   γ           α   β
        
        This operation preserves the BST property while changing the tree
        structure to help maintain Red-Black Tree balance.
        
        Args:
            node: Node to rotate around (x in the diagram above)
        
        Time Complexity: O(1)
        """
        # Right child becomes the new root of this subtree
        new_root = node.right
        
        # Move β subtree to become x's right child
        node.right = new_root.left
        if new_root.left != self.nil:
            new_root.left.parent = node
        
        # Update parent relationships
        new_root.parent = node.parent
        if node.parent == self.nil:
            self.root = new_root
        elif node == node.parent.left:
            node.parent.left = new_root
        else:
            node.parent.right = new_root
        
        # Make x the left child of y
        new_root.left = node
        node.parent = new_root
    
    def _right_rotate(self, node):
        """
        Perform right rotation around the given node.
        
        Right rotation is symmetric to left rotation:
        
        Before rotation:     After rotation:
              y                   x
             / \                 / \
            x   γ               α   y
           / \                     / \
          α   β                   β   γ
        
        Args:
            node: Node to rotate around (y in the diagram above)
        
        Time Complexity: O(1)
        """
        # Left child becomes the new root of this subtree
        new_root = node.left
        
        # Move β subtree to become y's left child
        node.left = new_root.right
        if new_root.right != self.nil:
            new_root.right.parent = node
        
        # Update parent relationships
        new_root.parent = node.parent
        if node.parent == self.nil:
            self.root = new_root
        elif node == node.parent.right:
            node.parent.right = new_root
        else:
            node.parent.left = new_root
        
        # Make y the right child of x
        new_root.right = node
        node.parent = new_root
```

## ⚠️ Common Documentation Mistakes

### Mistake 1: Obvious Comments

```python
# Bad: Comments that state the obvious
x = x + 1  # Increment x by 1
user_name = input("Enter name: ")  # Get user name
if age >= 18:  # If age is greater than or equal to 18
    print("Adult")  # Print "Adult"

# Good: Comments that explain why or provide context
x += 1  # Move to next position in the array
user_name = input("Enter name: ").strip()  # Remove whitespace for consistency
if age >= LEGAL_ADULT_AGE:  # Check if user meets legal requirements
    grant_adult_privileges(user)
```

### Mistake 2: Outdated Documentation

```python
# Bad: Documentation that doesn't match implementation
def calculate_tax(income, rate):
    """Calculate tax based on income and rate.
    
    Args:
        income (float): Annual income
        rate (float): Tax rate as percentage (e.g., 15 for 15%)
    
    Returns:
        float: Tax amount
    """
    # Implementation actually expects rate as decimal!
    return income * rate  # rate should be 0.15, not 15

# Good: Documentation matches implementation
def calculate_tax(income, rate):
    """Calculate tax based on income and rate.
    
    Args:
        income (float): Annual income in dollars
        rate (float): Tax rate as decimal (e.g., 0.15 for 15%)
    
    Returns:
        float: Tax amount in dollars
    
    Example:
        >>> calculate_tax(50000, 0.15)
        7500.0
    """
    return income * rate
```

### Mistake 3: Missing Edge Cases in Documentation

```python
# Bad: Doesn't document edge cases or limitations
def divide_numbers(a, b):
    """Divide two numbers.
    
    Returns:
        float: Result of division
    """
    return a / b  # What happens when b is 0?

# Good: Documents edge cases and error conditions
def divide_numbers(a, b):
    """Divide two numbers with proper error handling.
    
    Args:
        a (float): Dividend (number to be divided)
        b (float): Divisor (number to divide by)
    
    Returns:
        float: Result of a divided by b
    
    Raises:
        ValueError: If b is zero (division by zero)
        TypeError: If arguments are not numeric
    
    Examples:
        >>> divide_numbers(10, 2)
        5.0
        >>> divide_numbers(7, 3)
        2.3333333333333335
        >>> divide_numbers(5, 0)
        Traceback (most recent call last):
        ValueError: Cannot divide by zero
    """
    if not isinstance(a, (int, float)) or not isinstance(b, (int, float)):
        raise TypeError("Arguments must be numeric")
    
    if b == 0:
        raise ValueError("Cannot divide by zero")
    
    return a / b
```

## 🎯 Tools and Automation

### Using Docstring Tools

```python
# Example for use with tools like sphinx, pydoc, or help()

def complex_calculation(data, method='average', weights=None):
    """
    Perform complex statistical calculations on data.
    
    .. versionadded:: 1.2.0
    
    .. versionchanged:: 1.3.0
       Added support for weighted calculations
    
    .. deprecated:: 1.4.0
       Use `statistical_analysis()` instead
    
    .. seealso::
       :func:`statistical_analysis`
       :func:`simple_calculation`
    
    .. warning::
       This function will be removed in version 2.0
    """
    pass

# Generate documentation automatically
if __name__ == "__main__":
    help(complex_calculation)  # Shows formatted docstring
```

### Documentation Testing with Doctest

```python
def fibonacci(n):
    """
    Calculate the nth Fibonacci number.
    
    The Fibonacci sequence starts with 0, 1 and each subsequent number
    is the sum of the previous two numbers.
    
    Args:
        n (int): Position in sequence (0-indexed)
    
    Returns:
        int: The nth Fibonacci number
    
    Raises:
        ValueError: If n is negative
        TypeError: If n is not an integer
    
    Examples:
        >>> fibonacci(0)
        0
        >>> fibonacci(1)
        1
        >>> fibonacci(5)
        5
        >>> fibonacci(10)
        55
        >>> [fibonacci(i) for i in range(8)]
        [0, 1, 1, 2, 3, 5, 8, 13]
        
        # Test error cases
        >>> fibonacci(-1)
        Traceback (most recent call last):
        ValueError: n must be non-negative
        >>> fibonacci(1.5)
        Traceback (most recent call last):
        TypeError: n must be an integer
    """
    if not isinstance(n, int):
        raise TypeError("n must be an integer")
    
    if n < 0:
        raise ValueError("n must be non-negative")
    
    if n <= 1:
        return n
    
    # Use iterative approach for efficiency
    a, b = 0, 1
    for _ in range(2, n + 1):
        a, b = b, a + b
    
    return b

# Run doctests
if __name__ == "__main__":
    import doctest
    doctest.testmod(verbose=True)
```

## 📚 Summary and Best Practices

### Documentation Checklist
- [ ] Every public function/class has a docstring
- [ ] Docstrings explain purpose, not just implementation
- [ ] All parameters and return values are documented
- [ ] Error conditions and exceptions are documented
- [ ] Examples are provided for complex functions
- [ ] Comments explain "why", not "what"
- [ ] Documentation is kept up-to-date with code changes
- [ ] Complex algorithms include step-by-step explanations

### Key Principles
1. **Write for your future self** - Document as if you'll need to understand this code in 6 months
2. **Explain the why, not the what** - Code shows what happens, comments should explain why
3. **Keep it current** - Outdated documentation is worse than no documentation
4. **Be specific** - Vague documentation helps no one
5. **Use examples** - Show how functions should be used
6. **Document edge cases** - Explain what happens in unusual situations

### Next Steps
- Practice writing comprehensive docstrings
- Learn to use documentation generation tools (Sphinx, MkDocs)
- Set up automated documentation testing with doctest
- Review and improve documentation in existing projects
- Study well-documented open source projects for examples

---

**Remember**: Good documentation is an investment in code maintainability and team collaboration. It makes your code more professional, easier to debug, and more valuable to others (including your future self)!
