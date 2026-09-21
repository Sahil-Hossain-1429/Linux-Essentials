# File & Directory Permissions

Linux uses a permission system to control **who can read, write, or execute files and directories**.

Understanding permissions is important because Linux can have many users accessing the same system, and permissions determine what each user is allowed to do.

---

## 1. Permission Types

There are **three basic types of permissions**:

| Permission | Symbol | Value | Meaning          |
| ---------- | -----: | ----: | ---------------- |
| Read       |    `r` |   `4` | Allows reading   |
| Write      |    `w` |   `2` | Allows modifying |
| Execute    |    `x` |   `1` | Allows executing |

These permissions can be applied to three different classes of users:

| User class   | Symbol | Meaning                             |
| ------------ | -----: | ----------------------------------- |
| User / Owner |    `u` | The owner of the file or directory  |
| Group        |    `g` | Users belonging to the file's group |
| Others       |`o`/`a` | All or Other                        |


So the permission system can be thought of as:

```text
                 Permissions
                     │
        ┌────────────┼────────────┐
        │            │            │
       User         Group       Others
        │            │            │
      rwx          rwx          rwx
```

---

# 2. Understanding `ls -lh` Permissions

The `ls -lh` command displays detailed information about files and directories.

For example:

```bash
ls -lh
```

Example output:

```text
drwxrwxr-x 2 nexus nexus 4.0K Sep 21 02:38 Test
-rw-rw-r-- 1 nexus nexus 3.6K Sep 21 02:38 test.sh
```

The first part of each line contains the permission information:

```text
drwxrwxr-x
-rw-rw-r--
```

---

## 2.1 Breaking Down the Permission String

Consider:

```text
drwxrwxr-x
```

It can be divided into four parts:

```text
d rwx rwx r-x
│ │   │   │
│ │   │   └── Others
│ │   └────── Group
│ └────────── Owner
└──────────── File type
```
The first character tells us the **file type**.

The remaining nine characters represent permissions.

---

## 2.2 The First Character — File Type

The first character indicates what type of filesystem object it is.

| Character | Meaning       |
| --------- | ------------- |
| `-`       | Regular file  |
| `d`       | Directory     |
| `l`       | Symbolic link |

For example:

```text
drwxrwxr-x
```

starts with `d`, so it is a **directory**.

Whereas:

```text
-rw-rw-r--
```

starts with `-`, so it is a **regular file**.

---

# 3. The Nine Permission Characters

After the file-type character, there are **nine permission positions**.

For example:

```text
-rw-rw-r--
```

Break it down:

```text
- | rw- | rw- | r--
  |     |     |
  |     |     └── Others
  |     └──────── Group
  └────────────── Owner
```

Each group contains three positions:

```text
r w x
```

They represent:

| Position | Permission |
| -------- | ---------- |
| 1st      | Read       |
| 2nd      | Write      |
| 3rd      | Execute    |

If a permission is missing, Linux displays `-`.

For example:

```text
rwx
```

means:

```text
read    ✓
write   ✓
execute ✓
```

While:

```text
r--
```

means:

```text
read    ✓
write   ✗
execute ✗
```

---

# 4. Understanding User, Group, and Others

Consider this permission string:

```text
-rwxrw-r--
```

It can be divided into:

```text
- | rwx | rw- | r--
    │     │     │
    │     │     └── Others
    │     └──────── Group
    └────────────── Owner
```

Therefore:

| Class        | Permissions | Meaning              |
| ------------ | ----------- | -------------------- |
| User / Owner | `rwx`       | Read, write, execute |
| Group        | `rw-`       | Read and write       |
| Others       | `r--`       | Read only            |

This is the basic pattern to remember:

```text
-rwx rw- r--
 │   │   │
 │   │   └── Others
 │   └────── Group
 └────────── Owner
```

---

# 5. File Owner and Group

A typical `ls -lh` output looks like this:

```text
-rw-rw-r-- 1 nexus nexus 3.6K Sep 21 02:38 test.sh
```

The relevant information is:

```text
-rw-rw-r-- 1 nexus nexus
             │     │
             │     └── Group
             └──────── Owner
```

In this example:

* Owner: `nexus`
* Group: `nexus`

The owner and group determine which permission set applies to a user.

---

# 6. Permission Meaning for Files

For **regular files**, permissions generally mean:

| Permission | Meaning                              |
| ---------- | ------------------------------------ |
| `r`        | Read the contents of the file        |
| `w`        | Modify the contents of the file      |
| `x`        | Execute the file as a program/script |

For example:

```text
-rwxr--r--
```

means:

```text
Owner  → read + write + execute
Group  → read
Others → read
```

---

# 7. Permission Meaning for Directories

Directory permissions have an important distinction.

For a directory:

| Permission | Meaning                                            |
| ---------- | -------------------------------------------------- |
| `r`        | List the directory contents                        |
| `w`        | Create, delete, or rename entries in the directory |
| `x`        | Enter/traverse the directory                       |

For example:

```text
drwxr-xr-x
```

means:

```text
Owner  → read + write + execute
Group  → read + execute
Others → read + execute
```

### Important

The meaning of `r`, `w`, and `x` depends on whether the object is a **file** or a **directory**.

For a file:

```text
r → read file contents
w → modify file contents
x → execute file
```

For a directory:

```text
r → list contents
w → create/delete/rename entries
x → enter/traverse directory
```

---

# 8. `chmod`

`chmod` stands for **change mode**.

It is used to change the permissions of files and directories.

Basic syntax:

```bash
chmod [options] permissions file
```

For example:

```bash
chmod u+x test.sh
```

This adds execute permission for the owner of `test.sh`.

There are two common ways to use `chmod`:

1. **Symbolic mode**
2. **Numeric / Octal mode**

---

# 9. Symbolic Mode

Symbolic mode uses letters to specify:

* **Who** should be affected
* **What operation** should be performed
* **Which permission** should be changed

The basic structure is:

```text
chmod [who][operator][permission] file
```

For example:

```bash
chmod u+x test.sh
```

means:

```text
u → user/owner
+ → add permission
x → execute
```

Therefore:

> Add execute permission for the owner of `test.sh`.

---

## 9.1 User Classes

| Symbol | Meaning      |
| ------ | ------------ |
| `u`    | User / owner |
| `g`    | Group        |
| `o`/`a`    | Others / All users       |


Example:

```bash
chmod u+x test.sh
```

Add execute permission for the owner.

```bash
chmod g+x test.sh
```

Add execute permission for the group.

```bash
chmod o+x test.sh
```

Add execute permission for others.

```bash
chmod a+x test.sh
```

Add execute permission for everyone.

---

# 10. Symbolic Operators

There are three important operators:

| Operator | Meaning                  |
| -------- | ------------------------ |
| `+`      | Add permission           |
| `-`      | Remove permission        |
| `=`      | Set the exact permission |

### Add permission

```bash
chmod g+r test.sh
```

Adds read permission for the group.

### Remove permission

```bash
chmod g-r test.sh
```

Removes read permission from the group.

### Set exact permission

```bash
chmod u=rwx test.sh
```

Sets the owner's permissions to exactly:

```text
rwx
```

This is different from `+`.

For example:

```bash
chmod u+x test.sh
```

means:

> Add execute permission while keeping the owner's existing permissions.

Whereas:

```bash
chmod u=x test.sh
```

means:

> Set the owner's permissions to only execute.

So if the original permissions were:

```text
-rw-r--r--
```

then:

```bash
chmod u+x test.sh
```

results in:

```text
-rwxr--r--
```

But:

```bash
chmod u=x test.sh
```

results in:

```text
--wx? 
```

More precisely, the owner permission becomes only `x`, so the complete permission string becomes:

```text
---? 
```

For clarity, use `ls -lh` to verify the exact result after changing permissions.

---

# 11. Combining Symbolic Permissions

Multiple changes can be made in a single command.

For example:

```bash
chmod u+rwx,g+rx,o+r test.sh
```

This means:

```text
Owner  → add read, write, execute
Group  → add read, execute
Others → add read
```

The resulting permissions would be:

```text
-rwxr-xr--
```

Another example:

```bash
chmod u+x,g-x,o-r test.sh
```

means:

```text
Owner  → add execute
Group  → remove execute
Others → remove read
```

---

# 12. Numeric / Octal Mode

The second common way to use `chmod` is **numeric mode**, also called **octal mode**.

Each permission has a numeric value:

| Permission | Value |
| ---------- | ----: |
| `r`        |     4 |
| `w`        |     2 |
| `x`        |     1 |

The values are added together to produce a number from `0` to `7`.

---

## 12.1 Permission Values

| Permission | Calculation | Value |
| ---------- | ----------: | ----: |
| `---`      |         `0` |     0 |
| `--x`      |         `1` |     1 |
| `-w-`      |         `2` |     2 |
| `-wx`      |     `2 + 1` |     3 |
| `r--`      |         `4` |     4 |
| `r-x`      |     `4 + 1` |     5 |
| `rw-`      |     `4 + 2` |     6 |
| `rwx`      | `4 + 2 + 1` |     7 |

The most important values to memorize are:

```text
r = 4
w = 2
x = 1
```

Therefore:

```text
rwx = 4 + 2 + 1 = 7
rw- = 4 + 2     = 6
r-x = 4 + 1     = 5
r-- = 4
-wx = 2 + 1     = 3
-w- = 2
--x = 1
--- = 0
```

---

# 13. Understanding Three-Digit `chmod` Numbers

A three-digit numeric permission has three positions:

```text
chmod ABC file
       │││
       ││└── Others
       │└─── Group
       └──── Owner
```

For example:

```bash
chmod 754 test.sh
```

means:

```text
7 → Owner
5 → Group
4 → Others
```

Convert each number:

```text
7 = rwx
5 = r-x
4 = r--
```

Therefore:

```text
-rwxr-xr--
```

The permission table is:

| User class | Number | Permission |
| ---------- | -----: | ---------- |
| Owner      |    `7` | `rwx`      |
| Group      |    `5` | `r-x`      |
| Others     |    `4` | `r--`      |

---

# 14. Example: `chmod 444`

Consider:

```bash
chmod 444 test.sh
```

Each `4` means:

```text
4 = read
```

Therefore:

```text
Owner  → r--
Group  → r--
Others → r--
```

Result:

```text
-r--r--r-- test.sh
```

Everyone can read the file, but nobody has write or execute permission through these permission bits.

---

# 15. Example: `chmod 744`

Consider:

```bash
chmod 744 test.sh
```

Break it down:

```text
7 → Owner
4 → Group
4 → Others
```

Convert the values:

```text
7 = rwx
4 = r--
4 = r--
```

Result:

```text
-rwxr--r-- test.sh
```

Therefore:

| User class | Permissions            |
| ---------- | ---------------------- |
| Owner      | Read + Write + Execute |
| Group      | Read                   |
| Others     | Read                   |

---

# 16. Example: `chmod 764`

Consider:

```bash
chmod 764 test.sh
```

Break it down:

```text
7 → Owner
6 → Group
4 → Others
```

Convert the values:

```text
7 = rwx
6 = rw-
4 = r--
```

Result:

```text
-rwxrw-r-- test.sh
```

Therefore:

| User class | Number | Permissions |
| ---------- | -----: | ----------- |
| Owner      |    `7` | `rwx`       |
| Group      |    `6` | `rw-`       |
| Others     |    `4` | `r--`       |

---

# 17. More Useful `chmod` Examples

## Give the owner execute permission

```bash
chmod u+x test.sh
```

Before:

```text
-rw-r--r--
```

After:

```text
-rwxr--r--
```

---

## Remove write permission from others

```bash
chmod o-w test.sh
```

---

## Give the group read and execute permissions

```bash
chmod g+rx test.sh
```

---

## Give everyone read permission

```bash
chmod a+r test.sh
```

---

## Give the owner full permissions

```bash
chmod u=rwx test.sh
```

---

## Set owner to full permissions and everyone else to read-only

```bash
chmod 744 test.sh
```

Result:

```text
-rwxr--r--
```

---

## Make a shell script executable

Suppose we have:

```bash
test.sh
```

Initially:

```text
-rw-r--r-- test.sh
```

Try to execute it:

```bash
./test.sh
```

If the execute permission is not set, the system can refuse execution.

Add execute permission:

```bash
chmod u+x test.sh
```

Now:

```text
-rwxr--r-- test.sh
```

The owner can execute the script.

The script can be run now:

```bash
./test.sh
```

---

# 18. Symbolic Mode vs Numeric Mode

Both methods change permissions, but they are useful in different situations.

| Feature                    | Symbolic Mode    | Numeric / Octal Mode    |
| -------------------------- | ---------------- | ----------------------- |
| Example                    | `chmod u+x file` | `chmod 744 file`        |
| Easy to understand         | Yes              | Requires knowing values |
| Add one permission         | Excellent        | Less convenient         |
| Remove one permission      | Excellent        | Less convenient         |
| Set complete permissions   | Possible         | Very convenient         |
| Common for precise changes | Yes              | Yes                     |

### Symbolic mode

Use symbolic mode to make a specific change:

```bash
chmod u+x test.sh
```

### Numeric mode

Use numeric mode when complete desired permission is known

```bash
chmod 755 test.sh
```

---

# 19. Common Permission Patterns

These permission patterns appear frequently in Linux:

| Numeric | Symbolic    | Meaning                                   |
| ------: | ----------- | ----------------------------------------- |
|   `000` | `---------` | No permissions                            |
|   `400` | `r--------` | Owner can read                            |
|   `600` | `rw-------` | Owner can read/write                      |
|   `644` | `rw-r--r--` | Owner read/write, everyone else read      |
|   `700` | `rwx------` | Owner has full permissions                |
|   `755` | `rwxr-xr-x` | Owner full, group/others read/execute     |
|   `764` | `rwxrw-r--` | Owner full, group read/write, others read |
|   `777` | `rwxrwxrwx` | Everyone has full permissions             |

> **Note:** `777` grants all three basic permission bits to everyone. It should not be used automatically just because a program or file is having permission problems.

---

# 20. Quick Permission Conversion


For example:

```text
chmod 755 file
```

Start with:

```text
7   5   5
│   │   │
│   │   └── Others
│   └────── Group
└────────── Owner
```

Then convert:

```text
7 = 4 + 2 + 1 = rwx
5 = 4 + 1     = r-x
5 = 4 + 1     = r-x
```

Therefore:

```text
755
 ↓
rwxr-xr-x
```

---

# 21. A Simple Mental Model

When reading Linux permissions, always follow these three steps:

### Step 1 — Identify the object

Look at the first character:

```text
- → file
d → directory
l → symbolic link
```

### Step 2 — Split the permissions

Ignore the first character and divide the remaining nine characters into three groups:

```text
rwx | rwx | rwx
 │     │     │
 │     │     └── Others
 │     └──────── Group
 └────────────── Owner
```

### Step 3 — Read each permission

```text
r → read
w → write
x → execute
- → permission not granted
```

For example:

```text
-rwxr-xr--
```

becomes:

```text
File
 │
 ├── Owner  → rwx
 ├── Group  → r-x
 └── Others → r--
```

---

# 22. Quick Reference

## Permission Symbols

| Symbol | Meaning                |
| ------ | ---------------------- |
| `r`    | Read                   |
| `w`    | Write                  |
| `x`    | Execute                |
| `-`    | Permission not granted |

## User Classes

| Symbol | Meaning      |
| ------ | ------------ |
| `u`    | User / Owner |
| `g`    | Group        |
| `o`    | Others       |
| `a`    | All          |

## Symbolic Operators

| Operator | Meaning           |
| -------- | ----------------- |
| `+`      | Add permission    |
| `-`      | Remove permission |
| `=`      | Set permission    |

## Numeric Values

| Permission | Value |
| ---------- | ----: |
| `---`      |   `0` |
| `--x`      |   `1` |
| `-w-`      |   `2` |
| `-wx`      |   `3` |
| `r--`      |   `4` |
| `r-x`      |   `5` |
| `rw-`      |   `6` |
| `rwx`      |   `7` |

---

# 23. Command Reference

| Command            | Purpose                             | Example               |
| ------------------ | ----------------------------------- | --------------------- |
| `ls -lh`            | Display detailed file information   | `ls -lh`               |
| `chmod u+x file`   | Add execute permission for owner    | `chmod u+x test.sh`   |
| `chmod g+r file`   | Add read permission for group       | `chmod g+r test.sh`   |
| `chmod o-w file`   | Remove write permission from others | `chmod o-w test.sh`   |
| `chmod a+r file`   | Add read permission for everyone    | `chmod a+r test.sh`   |
| `chmod u=rwx file` | Set owner's permissions to `rwx`    | `chmod u=rwx test.sh` |
| `chmod 644 file`   | Set `rw-r--r--`                     | `chmod 644 test.txt`  |
| `chmod 755 file`   | Set `rwxr-xr-x`                     | `chmod 755 test.sh`   |
| `chmod 777 file`   | Set `rwxrwxrwx`                     | `chmod 777 file`      |

---

# Summary

Linux permissions answer three questions:

```text
WHO?
 ├── User / Owner (u)
 ├── Group (g)
 └── Others (o)

WHAT?
 ├── Read (r)
 ├── Write (w)
 └── Execute (x)

HOW?
 ├── Symbolic mode
 │   └── chmod u+x file
 │
 └── Numeric mode
     └── chmod 755 file
```

The most important concepts to remember are:

```text
r = 4
w = 2
x = 1
```

and:

```text
-rwxr-xr--
 │   │   │
 │   │   └── Others
 │   └────── Group
 └────────── Owner
```
