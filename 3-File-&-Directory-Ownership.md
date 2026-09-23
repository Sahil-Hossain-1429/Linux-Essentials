# Linux File Ownership: `chown` and `chgrp`

Linux provides commands for changing the **owner** and **group ownership** of files and directories.

| Command | Purpose                                            | Changes     |
| ------- | -------------------------------------------------- | ----------- |
| `chown` | Changes the owner of a file or directory           | User owner  |
| `chgrp` | Changes the group ownership of a file or directory | Group owner |

---

## 1. `chown`

The `chown` command changes the **owner** of a file or directory.

### Syntax

```bash
chown <owner> <file>
```

### Example

```bash
chown root test.sh
```

Before running the command:

```text
-rwxrw-r-- 1 nexus nexus 19 Sep 21 02:57 test.sh
```

| Field | Before  |
| ----- | ------- |
| Owner | `nexus` |
| Group | `nexus` |

After running:

```bash
chown root test.sh
```

The file becomes:

```text
-rwxrw-r-- 1 root nexus 19 Sep 21 02:57 test.sh
```

| Field | After   |
| ----- | ------- |
| Owner | `root`  |
| Group | `nexus` |

**Result:** Only the **file owner** changes from `nexus` to `root`. The group remains `nexus`.

### Changing Both Owner and Group

`chown` can also change both the owner and group at the same time.

```bash
chown root:root test.sh
```

Before:

```text
-rwxrw-r-- 1 nexus nexus 19 Sep 21 02:57 test.sh
```

After:

```text
-rwxrw-r-- 1 root root 19 Sep 21 02:57 test.sh
```

The `root:root` format means:

```text
owner:group
```

---

## 2. `chgrp`

The `chgrp` command changes the **group ownership** of a file or directory.

### Syntax

```bash
chgrp <group> <file>
```

### Example

```bash
chgrp root test.sh
```

Before running the command:

```text
-rwxrw-r-- 1 root nexus 19 Sep 21 02:57 test.sh
```

| Field | Before  |
| ----- | ------- |
| Owner | `root`  |
| Group | `nexus` |

After running:

```bash
chgrp root test.sh
```

The file becomes:

```text
-rwxrw-r-- 1 root root 19 Sep 21 02:57 test.sh
```

| Field | After  |
| ----- | ------ |
| Owner | `root` |
| Group | `root` |

**Result:** Only the **group ownership** changes from `nexus` to `root`. The owner remains `root`.

---

## `chown` vs `chgrp`

| Feature                      | `chown`                  | `chgrp`                |
| ---------------------------- | ------------------------ | ---------------------- |
| Changes file owner           | Yes                      | No                     |
| Changes group ownership      | Yes                      | Yes                    |
| Changes both owner and group | Yes                      | No                     |
| Example                      | `chown root test.sh`     | `chgrp root test.sh`   |
| Owner syntax                 | `owner` or `owner:group` | Not applicable         |
| Main purpose                 | Change ownership         | Change group ownership |

### Quick Reference

```bash
# Change owner
chown root test.sh

# Change group
chgrp root test.sh

# Change both owner and group
chown root:root test.sh
```

### Reading File Ownership

A typical `ls -l` output looks like:

```text
-rwxrw-r-- 1 root root 19 Sep 21 02:57 test.sh
```

The relevant section is:

```text
-rwxrw-r-- 1 root root
             │    │
             │    └── Group
             └─────── Owner
```
