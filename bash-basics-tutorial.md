# Bash Basics Tutorial

  

## Table of Contents

1. [Introduction](#introduction)

2. [Getting Started with the Terminal](#getting-started-with-the-terminal)

3. [Basic Navigation Commands](#basic-navigation-commands)

4. [File Operations](#file-operations)

5. [Viewing File Contents](#viewing-file-contents)

6. [Variables and Environment](#variables-and-environment)

7. [Introduction to Bash Scripting](#introduction-to-bash-scripting)

8. [Input/Output Redirection](#inputoutput-redirection)

9. [Conditional Statements](#conditional-statements)

10. [Loops](#loops)

11. [Functions](#functions)

12. [Exercises](#exercises)

---
  
## Introduction

### What is Bash?

**Bash** (Bourne-Again SHell) is a command-line interpreter, or shell, for Unix-like operating systems. According to the [GNU Bash Manual](https://www.gnu.org/software/bash/manual/bash.html), Bash is:

A command interpreter that provides a user interface to system utilities

A programming language that allows combining commands to create powerful scripts

The default shell on most Linux distributions and macOS

---
## Getting Started with the Terminal

### Opening a Terminal

in Linux Press `Ctrl+Alt+T` or search for "Terminal" in applications

### Understanding the Prompt

When you open a terminal, you'll see something like this:

```bash

user@computer:~$

```

This is called the prompt. It shows:

- Your username

- Your computer name

- Your current directory (`~` means your home directory)

- A `$` symbol (or `#` for root user) indicating you're ready to type commands

---
## Basic Navigation Commands

### `pwd` - Print Working Directory

Shows your current location in the file system.

```bash

# Display the current directory path

pwd

# Output example: /home/username/Documents

```

### `ls` - List Directory Contents

Lists files and directories in the current location.

```bash

# List files and directories

ls

# List with detailed information (permissions, size, date)

ls -l

# List all files including hidden ones (starting with .)

ls -a

# Combine options: detailed list with hidden files

ls -la

# List files in a specific directory

ls /home/username/Documents

```

### `cd` - Change Directory

Moves you to a different directory.

```bash
# Go to your home directory

cd ~

# or simply

cd

# Go to a specific directory

cd /home/username/Documents

# Go to a subdirectory (relative path)

cd Documents/Projects

# Go up one directory level

cd ..

# Go up two directory levels

cd ../..

# Go to the previous directory you were in

cd -
```

### `mkdir` - Make Directory

Creates a new directory (folder).

```bash
# Create a single directory
mkdir my_folder

# Create multiple directories

mkdir folder1 folder2 folder3

# Create nested directories (parent directories created if needed)

mkdir -p parent/child/grandchild


# Create a directory with a space in the name (use quotes)

mkdir "my folder"
```

### `rmdir` - Remove Directory

Removes an empty directory.

```bash
# Remove an empty directory

rmdir empty_folder
  
# Note: rmdir only works on empty directories

# For directories with content, use: rm -r directory_name

```

---
## File Operations


### `touch` - Create Empty File

Creates a new empty file or updates the timestamp of an existing file.

```bash
# Create a new empty file
touch myfile.txt

# Create multiple files
touch file1.txt file2.txt file3.txt

# Create a file with a space in the name
touch "my file.txt"

```

### `cp` - Copy Files and Directories

Copies files or directories to another location.

```bash
# Copy a file to another location
cp source.txt destination.txt

# Copy a file to a directory
cp file.txt /home/username/Documents/

# Copy a directory recursively (including all contents)
cp -r source_directory destination_directory

# Copy with verbose output (shows what's being copied)
cp -v file.txt backup/

```

### `mv` - Move or Rename Files

Moves files to a new location or renames them

```bash
# Rename a file
mv oldname.txt newname.txt

# Move a file to a directory
mv file.txt /home/username/Documents/

# Move a directory
mv old_folder /home/username/Documents/new_location/

# Move multiple files

mv file1.txt file2.txt destination_directory/

```

### `rm` - Remove Files

Deletes files and directories.

```bash
# Delete a file
rm file.txt

# Delete multiple files
rm file1.txt file2.txt file3.txt

# Delete a directory and all its contents (recursive)
rm -r directory_name

# Delete with confirmation prompt
rm -i file.txt

# Force delete without confirmation (use with caution!)
rm -f file.txt

# Delete directory recursively with force
rm -rf directory_name

```
  

**Warning**: `rm -rf` is very powerful and can delete files permanently. Always double-check the path before using it!

---
## Viewing File Contents

### `cat` - Concatenate and Display

Displays the entire contents of a file.

```bash
# Display file contents
cat filename.txt

# Display multiple files
cat file1.txt file2.txt
  
# Display with line numbers
cat -n filename.txt

```

### `less` - View File Page by Page

Opens a file in a pager, allowing you to scroll through large files.

```bash
# Open file in less
less filename.txt

# Navigation in less:

# - Space: next page

# - b: previous page

# - q: quit

# - /pattern: search for pattern

# - n: next match

# - h: help

```

### `head` - Display First Lines

Shows the first few lines of a file (default: 10 lines).

```bash
# Display first 10 lines
head filename.txt

# Display first 20 lines

head -n 20 filename.txt

# or

head -20 filename.txt

```

### `tail` - Display Last Lines

Shows the last few lines of a file (default: 10 lines).

```bash
# Display last 10 lines
tail filename.txt

# Display last 20 lines

tail -n 20 filename.txt

# Follow file updates in real-time (useful for log files)

tail -f logfile.txt

# Press Ctrl+C to stop following

```

---
## Variables and Environment

### Creating Variables

Variables store data that can be used later in your scripts or commands.

```bash
# Create a variable (no spaces around =)
name="John Doe"

# Create a variable with a number

age=25

# Access variable value using $ or ${}

echo $name

echo ${name}

# Use variable in a command

echo "Hello, $name"

```

**Important Rules:**

- No spaces around the = sign
- Variable names are case-sensitive
- Use quotes for values with spaces
- Access variables with `$variable_name` or `${variable_name}`
### Environment Variables

These are system-wide variables available to all programs.


```bash
# Display your username
echo $USER

# Display your home directory

echo $HOME

# Display current directory

echo $PWD

# Display your shell

echo $SHELL

# Display PATH (directories where programs are searched)

echo $PATH

# Set an environment variable for current session

export MY_VAR="value"

# Make it permanent (add to ~/.bashrc or ~/.bash_profile)

```
### Command Substitution

You can store the output of a command in a variable.

```bash
# Store current date in a variable

current_date=$(date)

echo "Today is: $current_date"

# Alternative syntax using backticks (older style)

current_date=`date`

# Store command output

files=$(ls)

echo "Files: $files"

# Count files in directory

file_count=$(ls | wc -l)

echo "Number of files: $file_count"

```

---
## Introduction to Bash Scripting

### Creating Your First Script

A Bash script is a file containing a series of commands that can be executed.

**Step 1: Create a script file**

```bash
# Create a new file
touch my_script.sh
```

**Step 2: Add the shebang line**

The shebang (`#!/bin/bash`) tells the system which interpreter to use.

```bash
#!/bin/bash
# This is my first bash script
echo "Hello, World!"
```

**Step 3: Make it executable**
  
```bash
# Give execute permission
chmod +x my_script.sh
```

**Step 4: Run the script**

```bash
# Method 1: Execute directly
./my_script.sh

# Method 2: Run with bash explicitly
bash my_script.sh
```

### Comments

Comments help explain your code. They start with `#` and are ignored by Bash.

```bash

#!/bin/bash

# This is a single-line comment

# This script demonstrates comments

echo "Hello"  # Inline comment

# Multi-line comments can be done like this:

# Line 1

# Line 2

# Line 3

```

### File Permissions

Understanding file permissions is important for security.

```bash

# View file permissions

ls -l filename.txt

# Output example: -rw-r--r-- 1 user group 1234 Jan 1 12:00 filename.txt

# Permission breakdown:

# -rw-r--r--

# - = file type (- for file, d for directory)

# rw- = owner permissions (read, write, no execute)

# r-- = group permissions (read only)

# r-- = others permissions (read only)

# r --> read
# w --> write
# x --> execute

# Change permissions using chmod:

chmod +x script.sh      # Add execute permission

chmod -x script.sh      # Remove execute permission

chmod 755 script.sh     # rwxr-xr-x (owner: all, others: read+execute)

chmod 644 file.txt      # rw-r--r-- (owner: read+write, others: read)

```

---
## Input Output Redirection

### Output Redirection (`>`)

Saves command output to a file (overwrites existing content).

```bash

# Save output to a file

echo "Hello" > output.txt

# List files and save to a file
ls > file_list.txt

# Note: This overwrites the file if it exists!

```

### Append Redirection (`>>`)

Adds output to the end of a file without overwriting.


```bash

# Append to a file

echo "Line 1" >> log.txt

echo "Line 2" >> log.txt

echo "Line 3" >> log.txt

  

# Now log.txt contains all three lines

```

### Input Redirection (`<`)

Reads input from a file instead of keyboard.

```bash

# Count words in a file

wc -w < document.txt

# Sort lines from a file

sort < unsorted.txt

```

### Pipes (`|`)

Pipes connect the output of one command to the input of another.

```bash

# List files and count them

ls | wc -l

# Search for a pattern in file contents

cat file.txt | grep "pattern"

# List files, filter, and save

ls -la | grep ".txt" > text_files.txt

# Chain multiple commands

cat file.txt | grep "error" | sort | uniq

```

### Standard Error Redirection

Commands have two output streams: standard output (stdout) and standard error (stderr).

```bash
# Redirect standard error to a file

command 2> error.log

# Redirect both stdout and stderr to a file

command > output.log 2>&1

# Or using newer syntax

command &> output.log

# Append both streams

command >> output.log 2>&1

```

---
## Conditional Statements

### `if` Statement

Execute commands based on conditions.

**Basic Syntax:**

```bash
if [ condition ]; then
    # commands to execute if condition is true
fi

```

**Example:**

```bash
#!/bin/bash
number=10

if [ $number -eq 10 ]; then

    echo "Number is 10"
    
fi

```

### Comparison Operators

**For Numbers:**

- `-eq`: equal to

- `-ne`: not equal to

- `-lt`: less than

- `-le`: less than or equal to

- `-gt`: greater than

- `-ge`: greater than or equal to

**For Strings:**

- =: equal to

- `!=`: not equal to

- `-z`: string is empty (zero length)

- `-n`: string is not empty

**For Files:**

- `-f`: file exists and is a regular file

- `-d`: directory exists

- `-e`: file or directory exists

- `-r`: file is readable

- `-w`: file is writable

- `-x`: file is executable 

### `if-else` Statement

```bash
#!/bin/bash

age=18

if [ $age -ge 18 ]; then

    echo "You are an adult"

else

    echo "You are a minor"

fi

```

### `if-elif-else` Statement

  

```bash
#!/bin/bash

score=85

if [ $score -ge 90 ]; then

    echo "Grade: A"

elif [ $score -ge 80 ]; then

    echo "Grade: B"

elif [ $score -ge 70 ]; then

    echo "Grade: C"

else

    echo "Grade: F"

fi

```

### Logical Operators


```bash
#!/bin/bash

age=25

name="John"

  

# AND operator (&&)

if [ $age -ge 18 ] && [ "$name" = "John" ]; then

    echo "Condition met"

fi

  

# OR operator (||)

if [ $age -lt 18 ] || [ $age -gt 65 ]; then

    echo "Special age group"

fi

  

# NOT operator (!)

if [ ! -f "file.txt" ]; then

    echo "File does not exist"

fi

```

### `case` Statement

Useful for multiple conditions based on a single value.


```bash
#!/bin/bash

day="Monday"

  

case $day in

    Monday)

        echo "Start of work week"

        ;;

    Friday)

        echo "TGIF!"

        ;;

    Saturday|Sunday)

        echo "Weekend!"

        ;;

    *)

        echo "Regular day"

        ;;

esac

```

---
  
## Loops

### `for` Loop

Iterates over a list of items.

**Basic Syntax:**

```bash
for variable in list; do

    # commands

done
```

  

**Examples:**

```bash
#!/bin/bash

# Loop through a list of items

for fruit in apple banana orange; do

    echo "I like $fruit"

done

  

# Loop through files in current directory

for file in *.txt; do

    echo "Processing $file"

done

  

# Loop through numbers (using brace expansion)

for i in {1..5}; do

    echo "Number: $i"

done

  

# Loop with C-style syntax

for ((i=1; i<=5; i++)); do

    echo "Count: $i"

done

  

# Loop through command output

for user in $(cat users.txt); do

    echo "User: $user"

done

```


### `while` Loop


Repeats commands while a condition is true.

```bash
#!/bin/bash

# Basic while loop

counter=1

while [ $counter -le 5 ]; do

    echo "Count: $counter"

    counter=$((counter + 1))

done

  

# Read file line by line

while IFS= read -r line; do

    echo "Line: $line"

done < file.txt

  

# Infinite loop (until broken)

while true; do

    echo "Press Ctrl+C to stop"

    sleep 1

done

```
  
### `until` Loop

Repeats commands until a condition becomes true (opposite of while).

```bash
#!/bin/bash

counter=1

until [ $counter -gt 5 ]; do

    echo "Count: $counter"

    counter=$((counter + 1))

done

```

### Loop Control

```bash
#!/bin/bash

# break: exit the loop

for i in {1..10}; do

    if [ $i -eq 5 ]; then

        break  # Exit loop when i equals 5

    fi

    echo $i

done

  

# continue: skip to next iteration

for i in {1..10}; do

    if [ $i -eq 5 ]; then

        continue  # Skip iteration when i equals 5

    fi

    echo $i

done

```

---
## Functions

Functions allow you to group commands for reuse.
### Basic Function Syntax

```bash
#!/bin/bash

# Define a function

function_name() {

    # commands

}

  

# Or alternative syntax

function function_name {

    # commands

}

```

### Function Examples

```bash
#!/bin/bash

# Simple function

greet() {

    echo "Hello, World!"

}

  

# Call the function

greet

  

# Function with parameters

greet_person() {

    local name=$1  # $1 is the first argument

    echo "Hello, $name!"

}

  

greet_person "Alice"

greet_person "Bob"

  

# Function with multiple parameters

add() {

    local num1=$1

    local num2=$2

    local sum=$((num1 + num2))

    echo "Sum: $sum"

}

  

add 5 3

  

# Function with return value (using exit status)

check_file() {

    if [ -f "$1" ]; then

        return 0  # Success

    else

        return 1  # Failure

    fi

}

  

if check_file "test.txt"; then

    echo "File exists"

else

    echo "File does not exist"

fi

  

# Function that returns a value (using echo)

get_full_name() {

    local first=$1

    local last=$2

    echo "$first $last"

}

  

full_name=$(get_full_name "John" "Doe")

echo "Full name: $full_name"

```

### Variable Scope

```bash
#!/bin/bash

global_var="I'm global"

my_function() {

    local local_var="I'm local"

    echo "Inside function: $global_var"

    echo "Inside function: $local_var"

}

my_function

echo "Outside function: $global_var"

echo "Outside function: $local_var"  # This will be empty

```


---
## Exercises

### Exercise 1: Basic Commands

Create a directory called `practice` in your home directory, then:

1. Navigate into it

2. Create three files: `file1.txt`, `file2.txt`, `file3.txt`

3. List all files to verify they were created

4. Display the contents of `file1.txt` using `cat` (it will be empty)

5. Remove `file3.txt`

### Exercise 2: Variables and Redirection

Write a script that:

1. Stores your name in a variable

2. Stores today's date in a variable

3. Creates a file called `info.txt`

4. Writes your name and date to the file

### Exercise 3: Conditional Statements

Write a script that:

1. Asks the user to enter a number (use `read` command)

2. Checks if the number is positive, negative, or zero

3. Displays an appropriate message

### Exercise 4: Loops

Write a script that:

1. Creates a directory called `numbers`

2. Creates 10 files named `file1.txt` through `file10.txt` in that directory

3. Writes the corresponding number (1-10) into each file

### Exercise 5: Functions

Write a script with a function that:

1. Takes a filename as an argument

2. Checks if the file exists

3. If it exists, displays its size

4. If it doesn't exist, creates it and writes "Created on $(date)" to it

### Exercise 6: Combining Concepts

Write a script that:

1. Creates a `logs` directory

2. Creates 5 log files named `log1.txt` through `log5.txt`

3. Each log file should contain 3 lines with timestamps and messages

4. Use a function to generate log entries

5. Count and display the total number of log files created

## References

  

- [GNU Bash Manual](https://www.gnu.org/software/bash/manual/bash.html)

- [Bash Guide for Beginners](https://tldp.org/LDP/Bash-Beginners-Guide/html/)