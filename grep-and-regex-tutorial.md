# Grep and Regular Expressions Tutorial

## Table of Contents
1. [Introduction to Grep](#introduction-to-grep)
2. [Basic Grep Usage](#basic-grep-usage)
3. [Essential Grep Options](#essential-grep-options)
4. [Introduction to Regular Expressions](#introduction-to-regular-expressions)
5. [Basic Regex Patterns](#basic-regex-patterns)
6. [Using Regex with Grep](#using-regex-with-grep)
7. [Practical Examples](#practical-examples)
8. [Exercises](#exercises)

---

## Introduction to Grep

### What is Grep?

Grep (Global Regular Expression Print) is a powerful command-line tool that searches for patterns in text. It's one of the most useful tools for working with files and command output.

Why use grep
- Find specific text in files quickly
- Filter log files for errors or warnings
- Search through code for functions or variables
- Extract information from large files
- Combine with other commands using pipes

### Basic Syntax

```bash
grep [options] pattern [file(s)]
```

- `pattern`: The text to search for (can be plain text or a regular expression)
- `file(s)`: One or more files to search (optional - can read from stdin)

---

## Basic Grep Usage

### Searching in a File

The simplest use of grep is searching for text in a file.

```bash
# Search for "error" in a file
grep "error" logfile.txt

# This displays all lines containing "error"
```

**Example:**
If `logfile.txt` contains:
```
System started successfully
Error: connection failed
Processing data
Error: timeout occurred
Task completed
```

Running `grep "error" logfile.txt` outputs:
```
Error: connection failed
Error: timeout occurred
```

### Searching Multiple Files

You can search across multiple files at once.

```bash
# Search in multiple files
grep "pattern" file1.txt file2.txt file3.txt

# Search in all .txt files
grep "pattern" *.txt
```

### Using Grep with Pipes

Grep works great with pipes to filter command output.

```bash
# List files and filter for .txt files
ls -la | grep "\.txt"

# Display file and filter lines
cat large_file.txt | grep "pattern"

# Chain multiple commands
cat file.txt | grep "error" | sort
```

---

## Essential Grep Options

### `-i` - Case-Insensitive Search

Ignore case differences when searching.

```bash
# Match error, Error, ERROR, etc.
grep -i "error" logfile.txt
```

### `-n` - Show Line Numbers

Display line numbers along with matching lines.

```bash
grep -n "error" logfile.txt
# Output: 5:Error: connection failed
```

### `-v` - Invert Match

Show lines that do NOT match the pattern.

```bash
# Show all lines except those containing "error"
grep -v "error" logfile.txt
```

### `-c` - Count Matches

Show only the count of matching lines.

```bash
grep -c "error" logfile.txt
# Output: 2
```

### `-r` - Recursive Search

Search recursively through directories.

```bash
# Search in current directory and all subdirectories
grep -r "pattern" .

# Search in specific directory
grep -r "function" /path/to/code
```

### `-E` - Extended Regular Expressions

Enable extended regex syntax (needed for advanced patterns).

```bash
# Use extended regex for patterns like | (OR)
grep -E "error|warning" logfile.txt
```

### `-w` - Word Boundaries

Match whole words only, not parts of words.

```bash
# Matches "error" but not "errors" or "terror"
grep -w "error" file.txt
```

### Combining Options

You can combine multiple options together.

```bash
# Case-insensitive, show line numbers, recursive search
grep -rin "error" /path/to/directory

# Extended regex, whole word, show context
grep -EwC 2 "error|warning" logfile.txt
```

---

## Introduction to Regular Expressions

### What are Regular Expressions?

Regular Expressions (regex) are a pattern-matching language that lets you describe what text you're looking for, rather than specifying exact text.

Why learn regex?
- Search for patterns instead of exact text
- Find phone numbers, emails, dates, etc.
- Extract specific data from logs
- Validate input formats

### Basic Concept

Think of regex as a way to describe patterns:
- `cat` matches the literal text "cat"
- `c.t` matches "cat", "cot", "cut" (`.` = any character)
- `ca*t` matches "ct", "cat", "caat" (`*` = zero or more)

---

## Basic Regex Patterns

### `.` (Dot) - Any Character

Matches any single character except a newline.

```bash
# Pattern: c.t matches cat, cot, cut, c1t, etc.
grep "c.t" file.txt
```

### `*` - Zero or More

Matches zero or more occurrences of the preceding character.

```bash
# Pattern: ca*t matches ct, cat, caat, caaat, etc.
grep "ca*t" file.txt
```

### `+` - One or More

Matches one or more occurrences (requires `-E` flag).

```bash
# Pattern: ca+t matches cat, caat, but NOT ct
grep -E "ca+t" file.txt
```

### `?` - Zero or One

Matches zero or one occurrence (requires `-E` flag).

```bash
# Pattern: colou?r matches color or colour
grep -E "colou?r" file.txt
```

### `^` - Start of Line

Matches the beginning of a line.

```bash
# Find lines starting with "Error"
grep "^Error" file.txt
```

### `$` - End of Line

Matches the end of a line.

```bash
# Find lines ending with "failed"
grep "failed$" file.txt
```

### `[...]` - Character Class

Matches any single character from the set.

```bash
# Match any vowel
grep "[aeiou]" file.txt

# Match any digit
grep "[0-9]" file.txt

# Match any letter
grep "[a-zA-Z]" file.txt
```

### `[^...]` - Negated Character Class

Matches any character NOT in the set.

```bash
# Match any non-digit character
grep "[^0-9]" file.txt
```

### `{n}` - Exactly N Times

Matches exactly n occurrences (requires `-E` flag).

```bash
# Match exactly 3 digits
grep -E "[0-9]{3}" file.txt
```

### `{n,m}` - Between N and M Times

Matches between n and m occurrences (requires `-E` flag).

```bash
# Match 2 to 4 digits
grep -E "[0-9]{2,4}" file.txt
```

### `|` - Alternation (OR)

Matches one pattern OR another (requires `-E` flag).

```bash
# Match "error" OR "warning"
grep -E "error|warning" file.txt
```

### `(...)` - Groups

Groups patterns together (requires `-E` flag).

```bash
# Match "cat" or "dog"
grep -E "(cat|dog)" file.txt
```

### Escaping Special Characters

Use `\` to match literal special characters.

```bash
# Match a literal dot
grep "file\.txt" file.txt

# Match a literal asterisk
grep "2\*3" file.txt
```

---

## Using Regex with Grep

### Basic vs Extended Regex

Basic grep supports:
- `.`, `*`, `^`, `$`
- Character classes `[...]`
- Escaped metacharacters

Extended regex (`-E` flag) adds:
- `+`, `?`, `|`
- `{n}`, `{n,m}`, `{n,}`
- Groups `(...)`

### Common Combinations

```bash
# Case-insensitive regex search
grep -iE "error|warning" file.txt

# Regex with line numbers
grep -nE "^[0-9]+" file.txt

# Recursive regex search
grep -rE "pattern" /path/to/directory

# Count regex matches
grep -cE "pattern" file.txt
```

---

## Practical Examples

### Example 1: Finding Log Entries

```bash
# Find lines with timestamps [YYYY-MM-DD HH:MM:SS]
grep -E "\[[0-9]{4}-[0-9]{2}-[0-9]{2} [0-9]{2}:[0-9]{2}:[0-9]{2}\]" logfile.txt

# Find ERROR or WARNING messages
grep -iE "error|warning" logfile.txt
```

### Example 2: Extracting Data

```bash
# Find lines containing numbers
grep "[0-9]" file.txt

# Find lines with 3 or more digits
grep -E "[0-9]{3,}" file.txt

# Find lines starting with a number
grep "^[0-9]" file.txt
```

### Example 3: Email Addresses (Simplified)

```bash
# Find email addresses (simplified pattern)
grep -E "[a-zA-Z0-9._]+@[a-zA-Z0-9._]+\.[a-zA-Z]{2,}" file.txt
```

### Example 4: Common Patterns

```bash
# Find empty lines
grep "^$" file.txt

# Find lines starting with # (comments)
grep "^#" file.txt

# Find files ending in .txt
ls | grep "\.txt$"
```

---

## Exercises

**[Grep and Regular Expressions Exercises](grep-and-regex-exercises.md)**


## Quick Reference

### Common Grep Options
- `-i`: Case-insensitive
- `-n`: Show line numbers
- `-v`: Invert match
- `-c`: Count matches
- `-r`: Recursive search
- `-E`: Extended regex
- `-w`: Whole word match
- `-C n`: Show n lines of context

### Common Regex Patterns
- `.`: Any character
- `*`: Zero or more
- `+`: One or more (requires -E)
- `?`: Zero or one (requires -E)
- `^`: Start of line
- `$`: End of line
- `[abc]`: Character class
- `[^abc]`: Negated class
- `{n}`: Exactly n times (requires -E)
- `{n,m}`: Between n and m times (requires -E)
- `|`: OR (requires -E)
- `\.`: Literal dot

---

## References

- [GNU Grep Manual](https://www.gnu.org/software/grep/manual/grep.html)
- [GNU Bash Manual](https://www.gnu.org/software/bash/manual/bash.html)
- [Regular Expressions Info](https://www.regular-expressions.info/)

