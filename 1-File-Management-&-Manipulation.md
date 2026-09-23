# Linux Terminal Commands — Beginner Cheat Sheet

> **Topic:** File Management Manipulation

---

## 1. Navigation & Location

Commands used to determine the current location in the filesystem and navigate between directories.

| Command          | Full Form               | Purpose                                                                                    | Example    |
| ---------------- | ----------------------- | ------------------------------------------------------------------------------------------ | ---------- |
| `pwd`            | Print Working Directory | Displays the absolute path of the current working directory.                               | `pwd`      |
| `cd`             | Change Directory        | Changes the current working directory. With no argument, it changes to the home directory. | `cd`       |
| `cd ..`          | —                       | Moves one level up to the parent directory.                                                | `cd ..`    |
| `cd <directory>` | Change Directory        | Changes to the specified directory.                                                        | `cd /home` |

### `pwd`

**Print Working Directory**

Displays the absolute path of the current working directory.

```bash
pwd
```

Example output:

```text
/home/nexus
```

`pwd` answers the question:

> **Where is the current working directory?**

---

### `cd`

**Change Directory**

Changes the current working directory.

When used without an argument, `cd` changes to the current user's home directory.

```bash
cd
```

For example:

```text
/home/nexus
```

---

### `cd ..`

Moves one directory level upward to the **parent directory**.

For example, if the current directory is:

```text
/home/nexus/Documents
```

then:

```bash
cd ..
```

changes the current directory to:

```text
/home/nexus
```

---

### `cd <directory>`

Changes to a specified directory.

```bash
cd /home
```

Both absolute and relative paths can be used.

---

# 2. Listing Files & Directories

The `ls` command is used to inspect the contents of directories.

| Command  | Purpose                                               |
| -------- | ----------------------------------------------------- |
| `ls`     | Lists files and directories                           |
| `ls -a`  | Lists all entries, including hidden files             |
| `ls -l`  | Displays a detailed long-format listing               |
| `ls -lh` | Displays a detailed listing with human-readable sizes |
| `ls -R`  | Recursively lists contents of subdirectories          |

---

### `ls`

**List**

Lists files and directories in the current directory.

```bash
ls
```

Example output:

```text
Desktop  Documents  Downloads  Music  Pictures  Projects  Public
Templates  Videos
```

---

### `ls -a`

The `-a` option means **all**.

It displays all directory entries, including hidden files and directories.

```bash
ls -a
```

Example output:

```text
.  ..  .bashrc  .cache  Desktop  Documents  Downloads
```

In Linux, filenames beginning with `.` are treated as hidden by convention.

Examples:

```text
.bashrc
.cache
```

> **Note:** Hidden does not mean protected or encrypted. It simply means that the filename begins with `.` and is not displayed by a normal `ls` command.

---

### `ls -l`

The `-l` option produces a **long-format listing** containing additional information about each entry.

```bash
ls -l
```

Example:

```text
drwxr-xr-x  2 nexus nexus  4096 Sep 17 02:44 Documents
drwxr-xr-x  2 nexus nexus  4096 Sep 17 04:35 Downloads
```

The output can contain information such as:

* File type
* Permissions
* Number of hard links
* Owner
* Group
* Size
* Modification date and time
* Filename

The permission field will be covered in more detail when studying Linux file permissions.

---

### `ls -lh`

Combines:

* `-l` → Long format
* `-h` → Human-readable sizes

```bash
ls -lh
```

Example:

```text
total 36K
drwxr-xr-x 2 nexus nexus 4.0K Sep 17 02:44 Desktop
drwxr-xr-x 2 nexus nexus 4.0K Sep 17 02:44 Documents
drwxr-xr-x 2 nexus nexus 4.0K Sep 17 04:35 Downloads
```

The `-h` option makes file sizes easier to read.

For example:

```text
4096     → 4.0K
1048576  → 1.0M
```

---

### `ls -R`

The `-R` option means **recursive**.

It displays the contents of the specified directory and then continues into its subdirectories.

```bash
ls -R TestDirectory
```

Example:

```text
TestDirectory:
TestSubDirectory  testSubfile1.txt  testSubfile2.txt

TestDirectory/TestSubDirectory:
```

Directory structure:

```text
TestDirectory/
└── TestSubDirectory/
```

A recursive operation continues through the directory tree and its descendants.

---

# 3. Creating Files

### `touch`

Creates an empty file if the specified file does not already exist.

```bash
touch test.txt
```

This creates:

```text
test.txt
```

### Important detail

`touch` is primarily used to **change file timestamps**. If the specified file does not exist, an empty file is created.

Therefore:

```bash
touch test.txt
```

can either:

* Create `test.txt` if it does not exist.
* Update its timestamps if it already exists.

---

# 4. Creating Directories

### `mkdir`

**Make Directory**

Creates a new directory.

```bash
mkdir testDirectory
```

This creates:

```text
testDirectory/
```

---

# 5. Displaying & Writing Text

### `echo`

Displays text to standard output.

```bash
echo "Hello World"
```

Output:

```text
Hello World
```

`echo` is commonly used to print text or generate text that can be redirected into files.

---

### `echo` + `>`

The `>` operator is called **output redirection**.

It redirects the output of a command into a file.

```bash
echo "Hello World" > test.txt
```

Instead of displaying the text on the terminal, the output is written to:

```text
test.txt
```

> **Important:** `>` creates the destination file if necessary and **overwrites existing contents**.

For example:

```bash
echo "First line" > test.txt
echo "Second line" > test.txt
```

The final contents of `test.txt` will be:

```text
Second line
```

---

# 6. Reading & Concatenating Files

### `cat`

**Concatenate**

Reads files and writes their contents to standard output. It can also be used to concatenate multiple files.

For a single file:

```bash
cat test.txt
```

If `test.txt` contains:

```text
Hello World
```

the command outputs:

```text
Hello World
```

---

### `cat` + `>`

The contents of one file can be redirected into another file:

```bash
cat test.txt > anotherTest.txt
```

This writes the contents of `test.txt` into `anotherTest.txt`.

> **Important:** `>` overwrites the destination file if it already exists.

---

# 7. Copying Files & Directories

### `cp`

**Copy**

Copies files or directories from one location to another.

```bash
cp test.txt Desktop/
```

This copies:

```text
test.txt
```

into:

```text
Desktop/
```

The original file remains in its original location.

### Basic syntax

```bash
cp <source> <destination>
```

Example:

```bash
cp file.txt /home/nexus/Documents/
```

---

# 8. Moving & Renaming

### `mv`

**Move**

Moves files or directories from one location to another.

```bash
mv file.txt Test/
```

This moves:

```text
file.txt
```

into:

```text
Test/
```

Unlike `cp`, the original file is no longer present at its previous location.

---

### `mv` for Renaming

`mv` can also be used to rename files and directories.

```bash
mv test.txt renamedTest.txt
```

This changes:

```text
test.txt
```

to:

```text
renamedTest.txt
```

The source and destination are in the same directory, so the operation effectively becomes a rename.

> **Key idea:** Linux uses `mv` for both moving and renaming files and directories.

---

# 9. Removing Files & Directories

### `rm`

**Remove**

Removes files.

```bash
rm test.txt
```

This removes:

```text
test.txt
```

> **Warning:** `rm` normally does not move files to a graphical recycle bin or trash. Deleted files may not be easily recoverable.

---

### `rm -R`

The `-R` option means **recursive**.

It allows `rm` to remove a directory and its contents recursively.

```bash
rm -R Test
```

For example:

```text
Test/
├── file1.txt
├── file2.txt
└── SubDirectory/
    └── file3.txt
```

A recursive removal can remove the entire directory tree.

> **Warning:** Recursive `rm` commands should be used carefully. An incorrect path can result in significant data loss.

---

### `rmdir`

**Remove Directory**

Removes empty directories.

```bash
rmdir Test
```

If `Test` contains files or subdirectories, `rmdir` normally refuses to remove it.

This makes `rmdir` useful when a directory should only be removed if it is empty.

---

# 10. Getting Information About Commands

### `whatis`

Provides a short description of a command by looking up its manual-page description.

```bash
whatis mv
```

Example output:

```text
mv (1) - move (rename) files
```

`whatis` is useful for quickly identifying the purpose of an unfamiliar command.

For more detailed documentation, the `man` command can be used:

```bash
man mv
```

---

# Quick Reference

| Command    | Category    | Description                                             |
| ---------- | ----------- | ------------------------------------------------------- |
| `pwd`      | Navigation  | Displays the current working directory                  |
| `ls`       | Listing     | Lists files and directories                             |
| `ls -a`    | Listing     | Lists all entries, including hidden entries             |
| `ls -l`    | Listing     | Displays detailed file information                      |
| `ls -lh`   | Listing     | Displays detailed information with human-readable sizes |
| `ls -R`    | Listing     | Recursively lists directory contents                    |
| `cd`       | Navigation  | Changes to the home directory                           |
| `cd ..`    | Navigation  | Moves to the parent directory                           |
| `cd <dir>` | Navigation  | Changes to a specified directory                        |
| `touch`    | Files       | Creates an empty file or updates timestamps             |
| `echo`     | Text        | Displays text to standard output                        |
| `cat`      | Files       | Displays or concatenates file contents                  |
| `mkdir`    | Directories | Creates a directory                                     |
| `cp`       | Files       | Copies files or directories                             |
| `mv`       | Files       | Moves or renames files or directories                   |
| `rm`       | Files       | Removes files                                           |
| `rm -R`    | Directories | Recursively removes directories and their contents      |
| `rmdir`    | Directories | Removes empty directories                               |
| `whatis`   | Help        | Provides a short description of a command               |

---

# Important Options

| Option | Meaning        | Example           |
| ------ | -------------- | ----------------- |
| `-a`   | All            | `ls -a`           |
| `-l`   | Long format    | `ls -l`           |
| `-h`   | Human-readable | `ls -lh`          |
| `-R`   | Recursive      | `ls -R` / `rm -R` |

---

# Command Categories

```text
                    LINUX TERMINAL
                          │
        ┌─────────────────┼─────────────────┐
        │                 │                 │
    NAVIGATION         MANAGE            INSPECT
        │                 │                 │
   pwd, cd            mkdir              ls
   cd ..              touch              cat
                      cp
                      mv
                      rm
                      rmdir
        │
        └─────────────────┐
                          │
                     TEXT & HELP
                          │
                    echo, whatis
```

The commands covered so far provide the basic operations required to:

**navigate the filesystem → inspect directories → create files and directories → display and write text → read file contents → copy and move files → rename files → remove files and directories → obtain basic command information.**
