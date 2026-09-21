# Linux Commands: `grep` and `man`

## 1. `grep`

### Purpose

`grep` searches for lines that match a specified **pattern** in text.

### Basic Syntax

```bash
grep [options] "pattern" file
```

| Component   | Description                                       |
| ----------- | ------------------------------------------------- |
| `grep`      | The command used to search for matching lines     |
| `[options]` | Optional flags that modify the command's behavior |
| `"pattern"` | The text or pattern to search for                 |
| `file`      | The file in which the search is performed         |

---

### Method 1: Using `grep` Directly

A file can be searched directly with `grep`.

**Example:**

```bash
grep "World" test.sh
```

If `test.sh` contains:

```text
echo "Hello World"
```

The matching line is displayed:

```text
echo "Hello World"
```

---

### Method 2: Using `grep` with a Pipe

A pipe (`|`) sends the **standard output** of one command to the **standard input** of another command.

**Example:**

```bash
cat /etc/passwd | grep "nexus"
```

In this example:

1. `cat /etc/passwd` displays the contents of `/etc/passwd`.
2. The pipe (`|`) passes that output to `grep`.
3. `grep "nexus"` searches the received output for lines containing `nexus`.
4. Only matching lines are displayed.

---

## Case Sensitivity

By default, `grep` is **case-sensitive**.

For example:

```bash
grep "world" test.sh
```

If the file contains:

```text
echo "Hello World"
```

there is no match because:

```text
world
```

and

```text
World
```

have different capitalization.

### Case-Insensitive Search

The `-i` option makes the search **case-insensitive**.

**Example:**

```bash
grep -i "world" test.sh
```

This matches :

```text
world
World
WORLD
WoRlD
```

### Common `grep` Options

| Option | Meaning                                | Example                     |
| ------ | -------------------------------------- | --------------------------- |
| `-i`   | Case-insensitive search                | `grep -i "world" test.sh`   |
| `-n`   | Show line numbers                      | `grep -n "World" test.sh`   |
| `-v`   | Show lines that do **not** match       | `grep -v "World" test.sh`   |
| `-r`   | Search recursively through directories | `grep -r "World" ./project` |
| `-w`   | Match a complete word                  | `grep -w "World" test.sh`   |

---

## 2. `man`

### Purpose

`man` stands for **manual**.

The `man` command displays the manual page for a command. Manual pages provide information such as the command's purpose, syntax, options, and usage examples.

### Basic Syntax

```bash
man command
```

### Example

```bash
man grep
```

This opens the manual page for `grep`.

Other examples include:

```bash
man ls
man cp
man mv
man mkdir
```

### Useful Navigation Keys inside man

| Key        | Action                         |
| ---------- | ------------------------------ |
| `Space`    | Move forward one page          |
| `b`        | Move backward one page         |
| `↑` / `↓`  | Move up or down                |
| `/pattern` | Search for a pattern           |
| `n`        | Move to the next search result |
| `q`        | Quit the manual page           |

---

## Quick Reference

| Command   | Purpose                         | Example                     |
| --------- | ------------------------------- | --------------------------- |
| `grep`    | Search for matching lines       | `grep "World" test.sh`      |
| `grep -i` | Search without considering case | `grep -i "world" test.sh`   |
| `grep -n` | Search and display line numbers | `grep -n "World" test.sh`   |
| `grep -v` | Display non-matching lines      | `grep -v "World" test.sh`   |
| `grep -r` | Search recursively              | `grep -r "World" ./project` |
| `man`     | Display a command's manual      | `man grep`                  |

> **Key concept:**
> `grep` is primarily used for **searching text**, while `man` is used for **learning how commands work**.
