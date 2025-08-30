# Regular Expressions

## 🎯 Objective
Master Python's regular expression capabilities for pattern matching, text processing, and data validation. Essential for competitive programming string problems, data cleaning, and text analysis tasks.

## 📖 Overview

Regular expressions (regex) are powerful tools for pattern matching and text manipulation. They provide a concise way to search, match, and replace text based on patterns, making them invaluable for data processing, validation, and competitive programming problems involving strings.

## 🔤 Basic Regex Patterns

### Introduction to Regex

```python
import re
from typing import List, Optional, Tuple, Dict

def basic_regex_introduction():
    """Introduction to basic regular expression concepts."""
    
    print("=== Basic Regular Expression Introduction ===")
    
    # Simple pattern matching
    text = "Hello World! This is a test string with numbers 123 and symbols @#$."
    
    # 1. Literal matching
    pattern1 = "Hello"
    matches1 = re.findall(pattern1, text)
    print(f"Literal pattern '{pattern1}': {matches1}")
    
    # 2. Character classes
    pattern2 = r"[aeiou]"  # Vowels
    matches2 = re.findall(pattern2, text)
    print(f"Vowels pattern '{pattern2}': {matches2}")
    
    # 3. Digit matching
    pattern3 = r"\d+"  # One or more digits
    matches3 = re.findall(pattern3, text)
    print(f"Digits pattern '{pattern3}': {matches3}")
    
    # 4. Word boundaries
    pattern4 = r"\btest\b"  # Whole word "test"
    matches4 = re.findall(pattern4, text)
    print(f"Word boundary pattern '{pattern4}': {matches4}")
    
    # 5. Case insensitive matching
    pattern5 = r"hello"
    matches5 = re.findall(pattern5, text, re.IGNORECASE)
    print(f"Case insensitive '{pattern5}': {matches5}")

def character_classes_demo():
    """Demonstrate character classes and special sequences."""
    
    print("\n=== Character Classes and Special Sequences ===")
    
    test_string = "ABC123xyz!@# \t\n"
    
    patterns = {
        r"[A-Z]": "Uppercase letters",
        r"[a-z]": "Lowercase letters", 
        r"[0-9]": "Digits",
        r"[A-Za-z]": "All letters",
        r"[A-Za-z0-9]": "Alphanumeric",
        r"[^A-Za-z0-9]": "Non-alphanumeric",
        r"\w": "Word characters (letters, digits, underscore)",
        r"\W": "Non-word characters",
        r"\d": "Digits",
        r"\D": "Non-digits", 
        r"\s": "Whitespace",
        r"\S": "Non-whitespace",
        r".": "Any character except newline"
    }
    
    for pattern, description in patterns.items():
        matches = re.findall(pattern, test_string)
        print(f"{pattern:15} ({description}): {matches}")

def quantifiers_demo():
    """Demonstrate quantifiers for pattern repetition."""
    
    print("\n=== Quantifiers ===")
    
    test_strings = [
        "a",
        "aa", 
        "aaa",
        "aaaa",
        "b",
        "ab",
        "aab",
        "aaab",
        "aaaab"
    ]
    
    quantifier_patterns = {
        r"a": "Literal 'a'",
        r"a?": "Zero or one 'a'",
        r"a*": "Zero or more 'a'",
        r"a+": "One or more 'a'",
        r"a{2}": "Exactly 2 'a's",
        r"a{2,}": "2 or more 'a's",
        r"a{2,4}": "2 to 4 'a's",
        r"a+b": "One or more 'a' followed by 'b'"
    }
    
    for pattern, description in quantifier_patterns.items():
        print(f"\nPattern: {pattern} ({description})")
        for test_str in test_strings:
            match = re.fullmatch(pattern, test_str)
            print(f"  '{test_str}': {'✓' if match else '✗'}")

def anchors_and_boundaries():
    """Demonstrate anchors and word boundaries."""
    
    print("\n=== Anchors and Boundaries ===")
    
    text = """
    start of line
    middle content
    end of line
    """
    
    lines = text.strip().split('\n')
    
    anchor_patterns = {
        r"^start": "Line starts with 'start'",
        r"line$": "Line ends with 'line'", 
        r"^middle": "Line starts with 'middle'",
        r"\bof\b": "Whole word 'of'",
        r"\Bof\B": "'of' not as whole word",
        r"^.*content.*$": "Line containing 'content'"
    }
    
    for pattern, description in anchor_patterns.items():
        print(f"\nPattern: {pattern} ({description})")
        for i, line in enumerate(lines):
            line = line.strip()
            match = re.search(pattern, line)
            print(f"  Line {i+1} '{line}': {'✓' if match else '✗'}")

# Run basic demos
if __name__ == "__main__":
    basic_regex_introduction()
    character_classes_demo()
    quantifiers_demo()
    anchors_and_boundaries()
```

### Advanced Pattern Matching

```python
def groups_and_capturing():
    """Demonstrate groups and capturing in regex."""
    
    print("=== Groups and Capturing ===")
    
    # Basic grouping
    text = "Contact: John Doe at john.doe@email.com or call (555) 123-4567"
    
    # 1. Capturing groups
    email_pattern = r"(\w+)\.(\w+)@(\w+)\.(\w+)"
    email_match = re.search(email_pattern, text)
    
    if email_match:
        print("Email parts:")
        print(f"  Full match: {email_match.group(0)}")
        print(f"  First name: {email_match.group(1)}")
        print(f"  Last name: {email_match.group(2)}")
        print(f"  Domain: {email_match.group(3)}")
        print(f"  TLD: {email_match.group(4)}")
        print(f"  All groups: {email_match.groups()}")
    
    # 2. Named groups
    phone_pattern = r"\((?P<area>\d{3})\)\s(?P<prefix>\d{3})-(?P<line>\d{4})"
    phone_match = re.search(phone_pattern, text)
    
    if phone_match:
        print("\nPhone parts (named groups):")
        print(f"  Full match: {phone_match.group(0)}")
        print(f"  Area code: {phone_match.group('area')}")
        print(f"  Prefix: {phone_match.group('prefix')}")
        print(f"  Line number: {phone_match.group('line')}")
        print(f"  Group dict: {phone_match.groupdict()}")
    
    # 3. Non-capturing groups
    url_pattern = r"https?://(?:www\.)?(\w+)\.(\w+)"
    urls = ["http://example.com", "https://www.google.com", "http://test.org"]
    
    print("\nURL parsing with non-capturing groups:")
    for url in urls:
        match = re.search(url_pattern, url)
        if match:
            print(f"  {url} -> Domain: {match.group(1)}, TLD: {match.group(2)}")

def backreferences_and_lookarounds():
    """Demonstrate backreferences and lookaround assertions."""
    
    print("\n=== Backreferences and Lookarounds ===")
    
    # 1. Backreferences
    print("Backreferences:")
    
    # Find repeated words
    text1 = "This is is a test test sentence with repeated repeated words."
    repeated_pattern = r"\b(\w+)\s+\1\b"
    repeated_matches = re.findall(repeated_pattern, text1)
    print(f"  Repeated words: {repeated_matches}")
    
    # Find palindromes (simple)
    words = ["level", "hello", "radar", "python", "madam", "test"]
    palindrome_pattern = r"^(\w)(\w)?(\w)?\2\1$"  # 3-5 letter palindromes
    
    print("  Palindromes:")
    for word in words:
        if re.match(palindrome_pattern, word):
            print(f"    {word} ✓")
    
    # 2. Lookahead assertions
    print("\nLookahead assertions:")
    
    # Password validation (at least 8 chars, contains digit and uppercase)
    passwords = ["password", "Password1", "WEAK", "StrongPass123", "weak123"]
    password_pattern = r"^(?=.*[A-Z])(?=.*\d).{8,}$"
    
    for pwd in passwords:
        valid = re.match(password_pattern, pwd)
        print(f"  '{pwd}': {'Valid' if valid else 'Invalid'}")
    
    # 3. Lookbehind assertions
    print("\nLookbehind assertions:")
    
    # Find numbers preceded by $
    text2 = "Price: $19.99, Cost: 25.50, Sale: $9.99"
    price_pattern = r"(?<=\$)\d+\.?\d*"
    prices = re.findall(price_pattern, text2)
    print(f"  Prices: {prices}")
    
    # 4. Negative lookarounds
    print("\nNegative lookarounds:")
    
    # Find words not followed by exclamation
    text3 = "Hello! World test! Python rocks"
    no_exclamation_pattern = r"\w+(?!\!)"
    words_no_exclamation = re.findall(no_exclamation_pattern, text3)
    print(f"  Words not followed by '!': {words_no_exclamation}")

def greedy_vs_lazy():
    """Demonstrate greedy vs lazy quantifiers."""
    
    print("\n=== Greedy vs Lazy Quantifiers ===")
    
    html = '<div>Content 1</div><div>Content 2</div>'
    
    # Greedy matching
    greedy_pattern = r"<div>.*</div>"
    greedy_match = re.search(greedy_pattern, html)
    print(f"Greedy pattern: {greedy_pattern}")
    print(f"  Matches: '{greedy_match.group(0) if greedy_match else 'None'}'")
    
    # Lazy matching
    lazy_pattern = r"<div>.*?</div>"
    lazy_matches = re.findall(lazy_pattern, html)
    print(f"Lazy pattern: {lazy_pattern}")
    print(f"  Matches: {lazy_matches}")
    
    # More examples
    text = "Start...middle...end"
    
    patterns = {
        r"Start.*end": "Greedy: Start to end",
        r"Start.*?end": "Lazy: Start to end",
        r"\.+": "Greedy: dots",
        r"\.+?": "Lazy: dots"
    }
    
    for pattern, description in patterns.items():
        matches = re.findall(pattern, text)
        print(f"{description}: {matches}")

# Run advanced demos
if __name__ == "__main__":
    groups_and_capturing()
    backreferences_and_lookarounds()
    greedy_vs_lazy()
```

## 🔧 Regex Methods and Operations

### Core Regex Functions

```python
def core_regex_functions():
    """Demonstrate core regex functions in Python."""
    
    print("=== Core Regex Functions ===")
    
    text = "The quick brown fox jumps over the lazy dog. The fox is quick."
    
    # 1. re.search() - Find first match
    print("1. re.search() - Find first match:")
    pattern = r"fox"
    match = re.search(pattern, text)
    if match:
        print(f"   Found '{match.group()}' at position {match.start()}-{match.end()}")
        print(f"   Context: '{text[match.start()-5:match.end()+5]}'")
    
    # 2. re.match() - Match at beginning
    print("\n2. re.match() - Match at beginning:")
    start_pattern = r"The"
    match = re.match(start_pattern, text)
    print(f"   Matches start: {bool(match)}")
    
    wrong_start = r"quick"
    match = re.match(wrong_start, text)
    print(f"   Matches 'quick' at start: {bool(match)}")
    
    # 3. re.fullmatch() - Match entire string
    print("\n3. re.fullmatch() - Match entire string:")
    full_pattern = r"The.*dog\."
    match = re.fullmatch(full_pattern, text)
    print(f"   Full match: {bool(match)}")
    
    # 4. re.findall() - Find all matches
    print("\n4. re.findall() - Find all matches:")
    word_pattern = r"\bthe\b"
    matches = re.findall(word_pattern, text, re.IGNORECASE)
    print(f"   All 'the': {matches}")
    
    # 5. re.finditer() - Find all with match objects
    print("\n5. re.finditer() - Find all with match objects:")
    for i, match in enumerate(re.finditer(word_pattern, text, re.IGNORECASE)):
        print(f"   Match {i+1}: '{match.group()}' at {match.start()}-{match.end()}")
    
    # 6. re.split() - Split string by pattern
    print("\n6. re.split() - Split string by pattern:")
    sentence = "apple,banana;orange:grape|kiwi"
    fruits = re.split(r"[,;:|]", sentence)
    print(f"   Split by delimiters: {fruits}")
    
    # Advanced splitting with groups
    parts = re.split(r"([,;:|])", sentence)
    print(f"   Split keeping delimiters: {parts}")
    
    # 7. re.sub() - Replace matches
    print("\n7. re.sub() - Replace matches:")
    
    # Simple replacement
    replaced = re.sub(r"fox", "cat", text)
    print(f"   Replace 'fox' with 'cat': {replaced[:50]}...")
    
    # Replacement with groups
    date_text = "Today is 2024-01-15 and tomorrow is 2024-01-16"
    date_replaced = re.sub(r"(\d{4})-(\d{2})-(\d{2})", r"\2/\3/\1", date_text)
    print(f"   Date format change: {date_replaced}")
    
    # 8. re.subn() - Replace with count
    print("\n8. re.subn() - Replace with count:")
    result, count = re.subn(r"the", "THE", text, flags=re.IGNORECASE)
    print(f"   Replaced {count} occurrences")
    print(f"   Result: {result[:50]}...")

def compiled_patterns():
    """Demonstrate compiled regex patterns for better performance."""
    
    print("\n=== Compiled Patterns ===")
    
    # Compile patterns for reuse
    email_pattern = re.compile(r"\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b")
    phone_pattern = re.compile(r"\(?\d{3}\)?[-.\s]?\d{3}[-.\s]?\d{4}")
    url_pattern = re.compile(r"https?://[^\s]+")
    
    test_data = [
        "Contact me at john@example.com or call (555) 123-4567",
        "Visit https://www.python.org for more info",
        "Email: alice@test.org, Phone: 555.987.6543",
        "Check out http://github.com/python"
    ]
    
    print("Extracting information from text:")
    for i, text in enumerate(test_data):
        print(f"\nText {i+1}: {text}")
        
        emails = email_pattern.findall(text)
        phones = phone_pattern.findall(text)
        urls = url_pattern.findall(text)
        
        print(f"  Emails: {emails}")
        print(f"  Phones: {phones}")
        print(f"  URLs: {urls}")
    
    # Performance comparison
    print("\n=== Performance Comparison ===")
    import time
    
    text = "test@example.com " * 1000
    pattern_str = r"\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b"
    compiled_pattern = re.compile(pattern_str)
    
    # Test non-compiled
    start = time.time()
    for _ in range(1000):
        re.findall(pattern_str, text)
    non_compiled_time = time.time() - start
    
    # Test compiled
    start = time.time()
    for _ in range(1000):
        compiled_pattern.findall(text)
    compiled_time = time.time() - start
    
    print(f"Non-compiled: {non_compiled_time:.4f}s")
    print(f"Compiled: {compiled_time:.4f}s")
    print(f"Speedup: {non_compiled_time/compiled_time:.2f}x")

def regex_flags():
    """Demonstrate regex flags for different matching behaviors."""
    
    print("\n=== Regex Flags ===")
    
    text = """First Line
    Second Line with CAPS
    Third line
    Final LINE"""
    
    # re.IGNORECASE (re.I)
    print("1. re.IGNORECASE:")
    pattern = r"line"
    normal_matches = re.findall(pattern, text)
    ignore_case_matches = re.findall(pattern, text, re.IGNORECASE)
    print(f"   Normal: {normal_matches}")
    print(f"   Ignore case: {ignore_case_matches}")
    
    # re.MULTILINE (re.M) 
    print("\n2. re.MULTILINE:")
    start_pattern = r"^.*line"
    without_multiline = re.findall(start_pattern, text, re.IGNORECASE)
    with_multiline = re.findall(start_pattern, text, re.IGNORECASE | re.MULTILINE)
    print(f"   Without MULTILINE: {without_multiline}")
    print(f"   With MULTILINE: {with_multiline}")
    
    # re.DOTALL (re.S)
    print("\n3. re.DOTALL:")
    multiline_text = "Start\nMiddle\nEnd"
    dot_pattern = r"Start.*End"
    without_dotall = re.search(dot_pattern, multiline_text)
    with_dotall = re.search(dot_pattern, multiline_text, re.DOTALL)
    print(f"   Without DOTALL: {bool(without_dotall)}")
    print(f"   With DOTALL: {bool(with_dotall)}")
    
    # re.VERBOSE (re.X)
    print("\n4. re.VERBOSE:")
    
    # Complex pattern without verbose
    complex_pattern = r"(\d{1,3})\.(\d{1,3})\.(\d{1,3})\.(\d{1,3})"
    
    # Same pattern with verbose (more readable)
    verbose_pattern = r"""
        (\d{1,3})   # First octet
        \.          # Dot
        (\d{1,3})   # Second octet
        \.          # Dot  
        (\d{1,3})   # Third octet
        \.          # Dot
        (\d{1,3})   # Fourth octet
    """
    
    ip_address = "192.168.1.1"
    match1 = re.search(complex_pattern, ip_address)
    match2 = re.search(verbose_pattern, ip_address, re.VERBOSE)
    
    print(f"   IP pattern match: {bool(match1) and bool(match2)}")
    if match1:
        print(f"   Octets: {match1.groups()}")
    
    # Combining flags
    print("\n5. Combining flags:")
    combined_text = "HELLO\nWORLD"
    combined_pattern = r"^hello.*world$"
    
    no_flags = re.search(combined_pattern, combined_text)
    with_flags = re.search(combined_pattern, combined_text, 
                          re.IGNORECASE | re.DOTALL | re.MULTILINE)
    
    print(f"   No flags: {bool(no_flags)}")
    print(f"   Combined flags: {bool(with_flags)}")

# Run core function demos
if __name__ == "__main__":
    core_regex_functions()
    compiled_patterns()
    regex_flags()
```

### Text Processing Applications

```python
def data_validation():
    """Demonstrate regex for data validation."""
    
    print("=== Data Validation with Regex ===")
    
    # Email validation
    def validate_email(email):
        """Validate email address format."""
        pattern = r"^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$"
        return bool(re.match(pattern, email))
    
    # Phone number validation
    def validate_phone(phone):
        """Validate US phone number format."""
        pattern = r"^\(?\d{3}\)?[-.\s]?\d{3}[-.\s]?\d{4}$"
        return bool(re.match(pattern, phone))
    
    # Credit card validation (simple format check)
    def validate_credit_card(card):
        """Validate credit card number format."""
        # Remove spaces and hyphens
        clean_card = re.sub(r"[\s-]", "", card)
        
        patterns = {
            "Visa": r"^4\d{15}$",
            "MasterCard": r"^5[1-5]\d{14}$",
            "American Express": r"^3[47]\d{13}$",
            "Discover": r"^6(?:011|5\d{2})\d{12}$"
        }
        
        for card_type, pattern in patterns.items():
            if re.match(pattern, clean_card):
                return card_type
        return None
    
    # Password strength validation
    def validate_password(password):
        """Validate password strength."""
        criteria = {
            "length": len(password) >= 8,
            "uppercase": bool(re.search(r"[A-Z]", password)),
            "lowercase": bool(re.search(r"[a-z]", password)),
            "digit": bool(re.search(r"\d", password)),
            "special": bool(re.search(r"[!@#$%^&*(),.?\":{}|<>]", password)),
            "no_common": not re.search(r"(password|123456|qwerty)", password, re.IGNORECASE)
        }
        
        return criteria, sum(criteria.values())
    
    # Test data validation
    test_data = {
        "emails": [
            "user@example.com",
            "invalid.email",
            "test@domain.co.uk",
            "bad@.com",
            "good.email+tag@domain.org"
        ],
        "phones": [
            "(555) 123-4567",
            "555-123-4567",
            "555.123.4567",
            "5551234567",
            "invalid-phone"
        ],
        "credit_cards": [
            "4111 1111 1111 1111",  # Visa
            "5555-5555-5555-4444",  # MasterCard
            "378282246310005",       # Amex
            "6011111111111117",      # Discover
            "1234567890123456"       # Invalid
        ],
        "passwords": [
            "weakpass",
            "StrongPass123!",
            "NoNumbers!",
            "nocaps123!",
            "NOLOWER123!",
            "NoSpecial123"
        ]
    }
    
    # Test email validation
    print("Email validation:")
    for email in test_data["emails"]:
        valid = validate_email(email)
        print(f"  {email:25} {'✓' if valid else '✗'}")
    
    # Test phone validation
    print("\nPhone validation:")
    for phone in test_data["phones"]:
        valid = validate_phone(phone)
        print(f"  {phone:15} {'✓' if valid else '✗'}")
    
    # Test credit card validation
    print("\nCredit card validation:")
    for card in test_data["credit_cards"]:
        card_type = validate_credit_card(card)
        print(f"  {card:20} {card_type if card_type else '✗'}")
    
    # Test password validation
    print("\nPassword validation:")
    for password in test_data["passwords"]:
        criteria, score = validate_password(password)
        print(f"  {password:15} Score: {score}/6")
        failed = [k for k, v in criteria.items() if not v]
        if failed:
            print(f"    Missing: {', '.join(failed)}")

def text_extraction():
    """Demonstrate text extraction using regex."""
    
    print("\n=== Text Extraction ===")
    
    # Sample text with various data
    sample_text = """
    Dear Customer,
    
    Your order #ORD-12345 has been processed. The total amount of $199.99 
    will be charged to your card ending in 4567.
    
    Delivery address:
    John Doe
    123 Main Street, Apt 4B
    New York, NY 10001
    
    Expected delivery: January 15, 2024
    Tracking number: 1Z999AA1234567890
    
    For questions, contact us at support@store.com or call (800) 555-0123.
    Visit our website at https://www.store.com
    
    Best regards,
    Customer Service Team
    """
    
    # Extraction patterns
    extraction_patterns = {
        "Order Numbers": r"ORD-\d+",
        "Prices": r"\$\d+\.?\d*",
        "Credit Card": r"\d{4}",
        "Dates": r"[A-Z][a-z]+ \d{1,2}, \d{4}",
        "Phone Numbers": r"\(\d{3}\) \d{3}-\d{4}",
        "Email Addresses": r"\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b",
        "URLs": r"https?://[^\s]+",
        "Tracking Numbers": r"1Z[A-Z0-9]{16}",
        "ZIP Codes": r"\b\d{5}\b"
    }
    
    print("Extracting information from text:")
    for category, pattern in extraction_patterns.items():
        matches = re.findall(pattern, sample_text)
        print(f"  {category}: {matches}")
    
    # More complex extraction with groups
    print("\nComplex extraction with groups:")
    
    # Extract address components
    address_pattern = r"([A-Z][a-z]+ [A-Z][a-z]+)\n(\d+.*)\n([A-Z][a-z]+, [A-Z]{2} \d{5})"
    address_match = re.search(address_pattern, sample_text)
    
    if address_match:
        print("Address components:")
        print(f"  Name: {address_match.group(1)}")
        print(f"  Street: {address_match.group(2)}")
        print(f"  City/State/ZIP: {address_match.group(3)}")

def text_cleaning():
    """Demonstrate text cleaning with regex."""
    
    print("\n=== Text Cleaning ===")
    
    dirty_text = """
    <html><body>
    Hello    World!!!   This  is   a    TEST   string.
    
    
    It has     extra   spaces,    WEIRD   capitalization,
    and !!!! too   many  punctuation  marks????
    
    Also includes: email@example.com, phone (555) 123-4567,
    and URL https://example.com
    
    </body></html>
    """
    
    print("Original text:")
    print(repr(dirty_text))
    
    # Cleaning steps
    cleaned = dirty_text
    
    # 1. Remove HTML tags
    cleaned = re.sub(r"<[^>]+>", "", cleaned)
    print("\n1. After removing HTML tags:")
    print(repr(cleaned[:100] + "..."))
    
    # 2. Normalize whitespace
    cleaned = re.sub(r"\s+", " ", cleaned)
    print("\n2. After normalizing whitespace:")
    print(repr(cleaned[:100] + "..."))
    
    # 3. Remove extra punctuation
    cleaned = re.sub(r"[!?]{2,}", "!", cleaned)
    print("\n3. After reducing punctuation:")
    print(repr(cleaned[:100] + "..."))
    
    # 4. Normalize case (title case for sentences)
    sentences = re.split(r"[.!?]+", cleaned)
    normalized_sentences = []
    
    for sentence in sentences:
        sentence = sentence.strip()
        if sentence:
            # Capitalize first letter
            sentence = sentence[0].upper() + sentence[1:].lower()
            normalized_sentences.append(sentence)
    
    cleaned = ". ".join(normalized_sentences) + "."
    print("\n4. After case normalization:")
    print(cleaned)
    
    # 5. Extract and format structured data
    print("\n5. Extracted structured data:")
    
    # Remove personal information for privacy
    cleaned_privacy = re.sub(r"\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b", 
                            "[EMAIL]", cleaned)
    cleaned_privacy = re.sub(r"\(\d{3}\) \d{3}-\d{4}", 
                            "[PHONE]", cleaned_privacy)
    cleaned_privacy = re.sub(r"https?://[^\s]+", 
                            "[URL]", cleaned_privacy)
    
    print(f"Privacy-cleaned text: {cleaned_privacy}")

def log_parsing():
    """Demonstrate log file parsing with regex."""
    
    print("\n=== Log File Parsing ===")
    
    # Sample log entries
    log_entries = [
        "2024-01-15 10:30:45 [INFO] User john.doe logged in from 192.168.1.100",
        "2024-01-15 10:31:02 [ERROR] Failed login attempt for user admin from 10.0.0.50",
        "2024-01-15 10:31:15 [WARNING] High memory usage: 85% on server web-01",
        "2024-01-15 10:32:01 [INFO] Database backup completed successfully",
        "2024-01-15 10:32:30 [ERROR] Connection timeout to database server 10.0.0.100:5432",
        "2024-01-15 10:33:15 [INFO] User jane.smith uploaded file report.pdf (2.5MB)",
    ]
    
    # Log parsing pattern
    log_pattern = r"(\d{4}-\d{2}-\d{2}) (\d{2}:\d{2}:\d{2}) \[(\w+)\] (.+)"
    
    print("Parsed log entries:")
    parsed_logs = []
    
    for entry in log_entries:
        match = re.match(log_pattern, entry)
        if match:
            date, time, level, message = match.groups()
            parsed_log = {
                "date": date,
                "time": time,
                "level": level,
                "message": message
            }
            parsed_logs.append(parsed_log)
            print(f"  {date} {time} [{level:7}] {message}")
    
    # Analyze logs
    print(f"\nLog analysis:")
    
    # Count by log level
    level_counts = {}
    for log in parsed_logs:
        level = log["level"]
        level_counts[level] = level_counts.get(level, 0) + 1
    
    print(f"  Log levels: {level_counts}")
    
    # Extract IP addresses
    ip_pattern = r"\b\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}\b"
    all_ips = []
    
    for log in parsed_logs:
        ips = re.findall(ip_pattern, log["message"])
        all_ips.extend(ips)
    
    print(f"  IP addresses found: {set(all_ips)}")
    
    # Find error patterns
    error_logs = [log for log in parsed_logs if log["level"] == "ERROR"]
    print(f"  Error messages:")
    for error_log in error_logs:
        print(f"    {error_log['time']}: {error_log['message']}")

# Run text processing demos
if __name__ == "__main__":
    data_validation()
    text_extraction()
    text_cleaning()
    log_parsing()
```

## 🏆 Competitive Programming Applications

### String Processing Problems

```python
def competitive_programming_regex():
    """Demonstrate regex solutions for competitive programming problems."""
    
    print("=== Competitive Programming Regex Solutions ===")
    
    # Problem 1: Valid Parentheses (using regex approach)
    def is_valid_parentheses_regex(s):
        """Check if parentheses are valid using regex."""
        # Remove all non-parentheses characters
        parens = re.sub(r"[^(){}[\]]", "", s)
        
        # Repeatedly remove valid pairs
        prev_len = len(parens) + 1
        while len(parens) < prev_len:
            prev_len = len(parens)
            parens = re.sub(r"\(\)|\{\}|\[\]", "", parens)
        
        return len(parens) == 0
    
    # Test valid parentheses
    test_parentheses = [
        "()",
        "()[]{}",
        "(]",
        "([)]",
        "{[]}",
        "((()))",
        "({[})"
    ]
    
    print("Valid parentheses check:")
    for test in test_parentheses:
        result = is_valid_parentheses_regex(test)
        print(f"  '{test}': {'Valid' if result else 'Invalid'}")
    
    # Problem 2: Extract numbers from mixed string
    def extract_and_sum_numbers(text):
        """Extract all numbers from text and return their sum."""
        numbers = re.findall(r"-?\d+\.?\d*", text)
        return sum(float(num) for num in numbers)
    
    # Test number extraction
    mixed_strings = [
        "The price is $19.99 and tax is $2.50",
        "Temperature dropped from 25.5°C to -3.2°C", 
        "Array: [1, 2, 3, 4, 5] sum = 15",
        "No numbers here!",
        "Negative values: -100, -50.5, 200"
    ]
    
    print("\nNumber extraction and sum:")
    for text in mixed_strings:
        total = extract_and_sum_numbers(text)
        numbers = re.findall(r"-?\d+\.?\d*", text)
        print(f"  '{text}' -> Numbers: {numbers}, Sum: {total}")
    
    # Problem 3: Word frequency with case insensitive
    def word_frequency(text):
        """Count word frequency ignoring case and punctuation."""
        # Extract words only
        words = re.findall(r"\b[a-zA-Z]+\b", text.lower())
        
        frequency = {}
        for word in words:
            frequency[word] = frequency.get(word, 0) + 1
        
        return frequency
    
    # Test word frequency
    text = "The quick brown fox jumps over the lazy dog. The dog was really lazy!"
    freq = word_frequency(text)
    
    print(f"\nWord frequency in: '{text}'")
    for word, count in sorted(freq.items()):
        print(f"  '{word}': {count}")
    
    # Problem 4: Replace multiple delimiters
    def normalize_delimiters(text, delimiter=","):
        """Replace various delimiters with a standard one."""
        # Replace any sequence of delimiter characters with single delimiter
        normalized = re.sub(r"[,;|:\s]+", delimiter, text.strip())
        return normalized
    
    # Test delimiter normalization
    messy_data = [
        "apple,banana;orange:grape|kiwi",
        "red   blue  green    yellow",
        "data1;;;data2,,,data3|||data4",
        "a,b;c:d|e f g"
    ]
    
    print("\nDelimiter normalization:")
    for data in messy_data:
        normalized = normalize_delimiters(data)
        print(f"  '{data}' -> '{normalized}'")

def pattern_matching_problems():
    """Solve pattern matching problems common in competitive programming."""
    
    print("\n=== Pattern Matching Problems ===")
    
    # Problem 1: Check if string matches pattern with wildcards
    def wildcard_match(text, pattern):
        """Match text against pattern with * and ? wildcards."""
        # Convert wildcard pattern to regex
        regex_pattern = pattern.replace("*", ".*").replace("?", ".")
        regex_pattern = f"^{regex_pattern}$"
        
        return bool(re.match(regex_pattern, text))
    
    # Test wildcard matching
    wildcard_tests = [
        ("hello", "h*o"),      # True
        ("hello", "h?llo"),    # True  
        ("hello", "h?l?o"),    # True
        ("hello", "h*x"),      # False
        ("abc", "a?c"),        # True
        ("abc", "a??"),        # True
        ("abc", "a???"),       # False
    ]
    
    print("Wildcard pattern matching:")
    for text, pattern in wildcard_tests:
        result = wildcard_match(text, pattern)
        print(f"  '{text}' matches '{pattern}': {result}")
    
    # Problem 2: Find longest repeated substring
    def longest_repeated_substring(s):
        """Find the longest substring that appears at least twice."""
        max_length = 0
        longest_substr = ""
        
        # Check all possible substrings
        for i in range(len(s)):
            for j in range(i + 1, len(s) + 1):
                substr = s[i:j]
                
                # Use regex to find all occurrences
                pattern = re.escape(substr)
                matches = list(re.finditer(pattern, s))
                
                if len(matches) >= 2 and len(substr) > max_length:
                    max_length = len(substr)
                    longest_substr = substr
        
        return longest_substr
    
    # Test longest repeated substring
    repeat_tests = [
        "abcabcbb",
        "banana", 
        "aaaa",
        "abcdef",
        "abababab"
    ]
    
    print("\nLongest repeated substring:")
    for test in repeat_tests:
        result = longest_repeated_substring(test)
        print(f"  '{test}' -> '{result}'")
    
    # Problem 3: Count valid IP addresses
    def count_valid_ips(text):
        """Count valid IP addresses in text."""
        # IP address pattern: each octet is 0-255
        ip_pattern = r"\b(?:(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.){3}(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\b"
        
        valid_ips = re.findall(ip_pattern, text)
        return len(valid_ips), valid_ips
    
    # Test IP counting
    ip_text = """
    Valid IPs: 192.168.1.1, 10.0.0.1, 255.255.255.255
    Invalid IPs: 256.1.1.1, 192.168.1.256, 999.999.999.999
    Edge cases: 0.0.0.0, 127.0.0.1
    """
    
    count, ips = count_valid_ips(ip_text)
    print(f"\nValid IP addresses in text: {count}")
    for ip in ips:
        print(f"  {ip}")
    
    # Problem 4: Validate mathematical expressions
    def is_valid_math_expression(expr):
        """Check if mathematical expression has valid format."""
        # Remove spaces
        expr = re.sub(r"\s+", "", expr)
        
        # Pattern for valid math expression
        # Numbers, operators, parentheses
        pattern = r"^[0-9+\-*/().]+$"
        
        if not re.match(pattern, expr):
            return False
        
        # Check balanced parentheses
        if not is_valid_parentheses_regex(expr):
            return False
        
        # Check for valid operator placement
        # No consecutive operators, no operator at start/end (except -)
        if re.search(r"[+\-*/]{2,}", expr):
            return False
        
        if re.search(r"^[+*/]|[+\-*/]$", expr):
            return False
        
        return True
    
    # Test math expression validation
    math_expressions = [
        "2 + 3 * 4",
        "(2 + 3) * 4",
        "2 + + 3",          # Invalid: consecutive operators
        "2 + 3 *",          # Invalid: ends with operator
        "* 2 + 3",          # Invalid: starts with operator
        "-2 + 3",           # Valid: negative number
        "((2 + 3) * 4)",    # Valid: nested parentheses
        "2 + 3 (",          # Invalid: unbalanced parentheses
    ]
    
    print("\nMath expression validation:")
    for expr in math_expressions:
        valid = is_valid_math_expression(expr)
        print(f"  '{expr}': {'Valid' if valid else 'Invalid'}")

def string_transformation_problems():
    """Solve string transformation problems using regex."""
    
    print("\n=== String Transformation Problems ===")
    
    # Problem 1: Convert camelCase to snake_case
    def camel_to_snake(text):
        """Convert camelCase to snake_case."""
        # Insert underscore before uppercase letters
        snake = re.sub(r"([a-z0-9])([A-Z])", r"\1_\2", text)
        return snake.lower()
    
    # Problem 2: Convert snake_case to camelCase
    def snake_to_camel(text):
        """Convert snake_case to camelCase."""
        components = text.split("_")
        return components[0] + "".join(word.capitalize() for word in components[1:])
    
    # Test case conversions
    case_tests = [
        "camelCaseString",
        "snake_case_string", 
        "XMLHttpRequest",
        "simple",
        "already_snake",
        "alreadyCamel"
    ]
    
    print("Case conversions:")
    for test in case_tests:
        if "_" in test:
            camel = snake_to_camel(test)
            print(f"  {test} (snake) -> {camel} (camel)")
        else:
            snake = camel_to_snake(test)
            print(f"  {test} (camel) -> {snake} (snake)")
    
    # Problem 3: Remove consecutive duplicate characters
    def remove_consecutive_duplicates(text):
        """Remove consecutive duplicate characters."""
        return re.sub(r"(.)\1+", r"\1", text)
    
    # Test duplicate removal
    duplicate_tests = [
        "aabbccdd",
        "hello",
        "aaabbbcccdddeee",
        "abcccdeeef",
        "programming"
    ]
    
    print("\nRemove consecutive duplicates:")
    for test in duplicate_tests:
        result = remove_consecutive_duplicates(test)
        print(f"  '{test}' -> '{result}'")
    
    # Problem 4: Expand abbreviated words
    def expand_abbreviations(text):
        """Expand common abbreviations."""
        abbreviations = {
            r"\bdr\b": "doctor",
            r"\bmr\b": "mister", 
            r"\bms\b": "miss",
            r"\bprof\b": "professor",
            r"\betc\b": "et cetera",
            r"\bi\.e\.\b": "that is",
            r"\be\.g\.\b": "for example"
        }
        
        expanded = text
        for abbrev, full in abbreviations.items():
            expanded = re.sub(abbrev, full, expanded, flags=re.IGNORECASE)
        
        return expanded
    
    # Test abbreviation expansion
    abbrev_text = "Dr. Smith and Prof. Jones discussed the results, i.e., the findings were significant."
    expanded_text = expand_abbreviations(abbrev_text)
    
    print(f"\nAbbreviation expansion:")
    print(f"  Original: {abbrev_text}")
    print(f"  Expanded: {expanded_text}")
    
    # Problem 5: Format phone numbers
    def format_phone_number(phone):
        """Format phone number to standard format."""
        # Extract digits only
        digits = re.sub(r"\D", "", phone)
        
        if len(digits) == 10:
            # Format as (XXX) XXX-XXXX
            return re.sub(r"(\d{3})(\d{3})(\d{4})", r"(\1) \2-\3", digits)
        elif len(digits) == 11 and digits[0] == "1":
            # Format as +1 (XXX) XXX-XXXX
            return re.sub(r"1(\d{3})(\d{3})(\d{4})", r"+1 (\1) \2-\3", digits)
        else:
            return "Invalid phone number"
    
    # Test phone formatting
    phone_tests = [
        "5551234567",
        "555-123-4567",
        "(555) 123-4567",
        "1-555-123-4567",
        "15551234567",
        "123456"  # Invalid
    ]
    
    print("\nPhone number formatting:")
    for phone in phone_tests:
        formatted = format_phone_number(phone)
        print(f"  '{phone}' -> '{formatted}'")

# Run competitive programming demos
if __name__ == "__main__":
    competitive_programming_regex()
    pattern_matching_problems()
    string_transformation_problems()
```

## 🎯 Practice Exercises

### Exercise 1: Advanced Text Processor

```python
def create_text_processor():
    """
    Create an advanced text processing tool that:
    1. Extracts structured data from unformatted text
    2. Validates and formats various data types
    3. Cleans and normalizes text content
    4. Generates reports with regex-based analysis
    5. Handles multiple text formats and encodings
    """
    # Your implementation here
    pass
```

### Exercise 2: Log Analysis System

```python
def build_log_analyzer():
    """
    Build a comprehensive log analysis system that:
    1. Parses multiple log formats (Apache, nginx, custom)
    2. Extracts and analyzes error patterns
    3. Identifies security threats and anomalies
    4. Generates statistical reports
    5. Provides real-time monitoring capabilities
    """
    # Your implementation here
    pass
```

### Exercise 3: Data Validation Framework

```python
def create_validation_framework():
    """
    Create a flexible data validation framework that:
    1. Validates various data formats (emails, phones, URLs, etc.)
    2. Supports custom validation rules
    3. Provides detailed error messages
    4. Handles internationalization requirements
    5. Integrates with web forms and APIs
    """
    # Your implementation here
    pass
```

## 📚 Summary and Best Practices

### Regex Best Practices

**Performance Optimization:**
- Compile patterns for repeated use
- Use specific patterns instead of overly broad ones
- Avoid excessive backtracking with careful quantifier placement
- Use non-capturing groups when you don't need the captured content

**Readability and Maintenance:**
- Use raw strings (`r""`) for regex patterns
- Add comments for complex patterns using `re.VERBOSE`
- Break complex patterns into smaller, testable components
- Document regex patterns with clear explanations

**Common Pitfalls to Avoid:**
- Catastrophic backtracking with nested quantifiers
- Forgetting to escape special characters
- Using `.` when you mean literal dot
- Not considering edge cases in patterns

### Regex Cheat Sheet

| Pattern | Description | Example |
|---------|-------------|---------|
| `\d` | Digit | `\d+` matches "123" |
| `\w` | Word character | `\w+` matches "hello" |
| `\s` | Whitespace | `\s+` matches "   " |
| `^` | Start of string | `^Hello` matches start |
| `$` | End of string | `world$` matches end |
| `*` | Zero or more | `a*` matches "", "a", "aa" |
| `+` | One or more | `a+` matches "a", "aa" |
| `?` | Zero or one | `a?` matches "", "a" |
| `{n}` | Exactly n | `a{3}` matches "aaa" |
| `{n,m}` | n to m times | `a{2,4}` matches "aa" to "aaaa" |
| `[]` | Character class | `[abc]` matches "a", "b", or "c" |
| `()` | Capturing group | `(abc)` captures "abc" |
| `(?:)` | Non-capturing group | `(?:abc)` groups without capture |

### When to Use Regex

**Good Use Cases:**
- Pattern validation (emails, phones, etc.)
- Text extraction and parsing
- Simple find and replace operations
- Data cleaning and normalization
- Log file analysis

**When to Avoid Regex:**
- Parsing HTML/XML (use proper parsers)
- Complex nested structures
- Mathematical expressions (use parsers)
- When simple string methods suffice
- Performance-critical code with complex patterns

### Testing Regex Patterns

**Use Online Tools:**
- regex101.com for testing and explanation
- regexr.com for interactive testing
- regexpal.com for quick validation

**Write Unit Tests:**
```python
import unittest

class TestRegexPatterns(unittest.TestCase):
    def test_email_validation(self):
        pattern = r"^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$"
        
        valid_emails = ["test@example.com", "user.name@domain.co.uk"]
        invalid_emails = ["invalid.email", "test@", "@domain.com"]
        
        for email in valid_emails:
            self.assertTrue(re.match(pattern, email))
        
        for email in invalid_emails:
            self.assertFalse(re.match(pattern, email))
```

### Alternative Approaches

**When Regex Isn't Enough:**
- Use parsing libraries for structured data
- Combine regex with string methods
- Consider finite state machines for complex patterns
- Use specialized libraries for specific domains

### Next Steps

After mastering regular expressions:
1. Learn about [Decorators and Generators](./17-decorators-generators.md)
2. Study advanced text processing libraries
3. Explore natural language processing
4. Practice with real-world text processing projects
5. Learn about parsing theory and formal grammars

---

**Remember**: Regular expressions are powerful but can become complex quickly. Always prioritize readability and maintainability over cleverness!
