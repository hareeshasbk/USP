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
