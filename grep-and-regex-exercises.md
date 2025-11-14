# Grep and Regular Expressions - Exercises
## Exercise 1: Basic Grep Usage
  
Using `sample.log`, complete the following tasks:

 1. Search for "error" (case-sensitive) - this should find lowercase "error" only

2. Search for "error" (case-insensitive) - this should find ERROR, error, etc.

3. Count how many lines contain "error" (case-insensitive)

4. Search for "INFO" and count the results

---
  ## Exercise 2: Grep Options

Using `sample.log`, complete the following tasks:

  1. Find all ERROR lines with line numbers

2. Find all lines that do NOT contain " INFO"

3. Show 1 line before and after each ERROR line (context)

---
## Exercise 3: Basic Regex Patterns

Using `sample.log`, complete the following tasks:
  
1. Find lines containing timestamps (pattern: `[YYYY-MM-DD HH:MM:SS]`)

2. Find lines that contain "cat" or "cot" or "cut" (use `.` to match any character)

3. Find lines contaiing "WARNING" or "warning" (use `|` with extended regex)

4. Find lines starting with "#" (comments)


---
## Exercise 4: Character Classes and Quantifiers

Using `sample.log`, complete the following tasks:

1. Find all lines containing digits (numbers)

2. Find lines containing phone numbers in format 09123456789 (two digits, dash, then nine digits)

3. Find lines with exactly 3 digits (standalone numbers like 123 or 456)

---

## Exercise 5: Advanced Patterns and RealWorld Applications

Using `sample.log`, complete the following tasks:

1. Find email addresses (pattern: text@text.text)

2. Find all ERROR or WARNING messages (case-insensitive) with line numbers

3. Find lines that contain timestamps AND are ERROR messages

4. Create a simple script that counts errors, warnings, and info messages separately


---
## Bonus Challenge

Create a script that:

1. Reads `sample.log`

2. Extracts all email addresses and saves them to `emails.txt`

3. Extracts all phone numbers and saves them to `phones.txt`

4. Generates a summary report showing counts of each
