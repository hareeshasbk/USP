Set 6

---

## Q1: Why are internal commands faster than external commands?

**Internal commands** are built into the shell itself (e.g., `cd`, `echo`, `pwd`).

They are faster because:

* They **do not create a new process**
* They **do not require disk access** to load a program
* They execute **directly inside the shell**

**External commands** (e.g., `ls`, `grep`, `cat`) are stored as separate executable files and require:

* Forking a new process
* Loading the program from disk

---

## Q2: Recursively compress files and generate a compression report

### Shell Script

```sh
#!/bin/bash

DIR=$1
ARCHIVE="compressed.tar.gz"
REPORT="compression_report.txt"

# Size before compression
BEFORE=$(du -sh "$DIR" | awk '{print $1}')

# Compress directory recursively
tar -czf $ARCHIVE $DIR

# Size after compression
AFTER=$(du -sh $ARCHIVE | awk '{print $1}')

# Generate report
echo "Compression Report" > $REPORT
echo "Directory: $DIR" >> $REPORT
echo "Size before compression: $BEFORE" >> $REPORT
echo "Size after compression: $AFTER" >> $REPORT
echo "Archive name: $ARCHIVE" >> $REPORT

echo "Compression completed. Report generated."
```

### Usage

```sh
./compress.sh myfolder
```

---

## Q3: Display unique categories from `sales.txt`

**If categories are in the 3rd column:**

```sh
cut -d',' -f3 sales.txt | sort | uniq
```

**Alternative (recommended):**

```sh
awk -F',' '{print $3}' sales.txt | sort -u
```

> Change `-f3` or `{print $3}` if the category column is different.

---

## Q4: Shell script to calculate the perimeter of a rectangle

### Script

```sh
#!/bin/bash

echo "Enter length:"
read l

echo "Enter breadth:"
read b

perimeter=$((2 * (l + b)))

echo "Perimeter of rectangle: $perimeter"
```

---

## Q5: Shell script using a function to find square of a number

### Script

```sh
#!/bin/bash

square() {
    result=$(( $1 * $1 ))
    echo "Square of $1 is $result"
}

echo "Enter a number:"
read num

square $num
```

---

If you want, I can also:

* Convert these into **very short exam answers**
* Rewrite them for **Linux viva** or **practical record format**

---
Set 4


Q1:Why is PATH considered an important environment variable? Demonstrate with an
example.
Q2: Create a recursive ZIP archive of a directory and identify the largest file before
compression.
Q3: Extract the 2nd and 4th columns from a CSV file employees.txt.
Q4: Write a shell script to count the number of occurrences of a word in a file.
Q5:Write a shell script to stop printing numbers when it reaches 7.


Here are **clear, exam-oriented answers** with examples and shell scripts.

---

## Q1: Why is PATH considered an important environment variable? Demonstrate with an example.

**PATH** is an environment variable that tells the shell **where to look for executable programs**.

### Why it is important:

* Allows running commands **without specifying full path**
* Saves time and improves usability
* Enables execution of user-defined programs

### Example:

```sh
echo $PATH
```

If `/bin` is in PATH, you can run:

```sh
ls
```

Without PATH, you must specify:

```sh
/bin/ls
```

### Adding a directory to PATH:

```sh
export PATH=$PATH:/home/user/scripts
```

---

## Q2: Create a recursive ZIP archive of a directory and identify the largest file before compression

### Command to find the largest file:

```sh
find mydir -type f -exec du -h {} + | sort -hr | head -n 1
```

### Create recursive ZIP archive:

```sh
zip -r mydir.zip mydir
```

✔ `-r` → recursive compression

---

## Q3: Extract the 2nd and 4th columns from a CSV file `employees.txt`

### Using `cut`:

```sh
cut -d',' -f2,4 employees.txt
```

### Using `awk`:

```sh
awk -F',' '{print $2, $4}' employees.txt
```

---

## Q4: Write a shell script to count the number of occurrences of a word in a file

### Script:

```sh
#!/bin/bash

echo "Enter word:"
read word

echo "Enter filename:"
read file

count=$(grep -o -w "$word" "$file" | wc -l)

echo "Occurrences of '$word': $count"
```

---

## Q5: Write a shell script to stop printing numbers when it reaches 7

### Script:

```sh
#!/bin/bash

for i in {1..10}
do
    if [ $i -eq 7 ]
    then
        break
    fi
    echo $i
done
```

---

If you want, I can:

* Shorten answers for **2–3 mark questions**
* Rewrite scripts in **POSIX sh**
* Prepare a **lab record / viva explanation**



Below are clear, exam-style answers with commands and scripts.


---

Q1: Explain why UNIX treats everything as a file

UNIX follows the philosophy “everything is a file” to provide a simple, uniform interface to system resources.

Regular files, directories, devices, pipes, and sockets are all accessed using the same system calls (open, read, write, close)

This reduces complexity for programmers

Device I/O (keyboard, disk, printer) is handled just like file I/O

Enables powerful features like redirection and piping


Example:

Keyboard → /dev/tty

Hard disk → /dev/sda

Processes → /proc


This design makes UNIX flexible, consistent, and modular.


---

Q2: List all files recursively with inode numbers and compress files with read and write permissions

(a) List all files recursively with inode numbers

ls -R -i

Or using find (more powerful):

find . -print -inum


---

(b) Compress files that have read and write permissions

If read & write for owner (rw-------):

find . -type f -perm -600 -exec gzip {} \;

If read & write for all users (rw-rw-rw-):

find . -type f -perm -666 -exec gzip {} \;


---

Q3: Merge two files side by side and replace a word globally

Merge two files side by side

paste file1 file2

Replace a word globally in a file

sed -i 's/oldword/newword/g' filename

Example:

sed -i 's/Linux/UNIX/g' file1


---

Q4: Write a shell script to compare two numbers and display exit status

#!/bin/bash

read -p "Enter first number: " a
read -p "Enter second number: " b

if [ $a -gt $b ]; then
    echo "First number is greater"
    exit 0
elif [ $a -lt $b ]; then
    echo "Second number is greater"
    exit 1
else
    echo "Both numbers are equal"
    exit 2
fi

Check exit status:

echo $?


---

Q5: Write a shell script to perform arithmetic operations on two numbers

#!/bin/bash

read -p "Enter first number: " a
read -p "Enter second number: " b

echo "Addition: $((a + b))"
echo "Subtraction: $((a - b))"
echo "Multiplication: $((a * b))"
echo "Division: $((a / b))"
echo "Modulus: $((a % b))"


---

If you want, I can also rewrite these in short exam answers, with comments, or POSIX-only syntax.

https://chatgpt.com/share/696dd490-6018-8007-ac61-dcf3e9c47a2f


https://chatgpt.com/share/696dd4ca-709c-8007-8bb4-a4e3649fdf40