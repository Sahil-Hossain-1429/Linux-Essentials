# Linux Disk Space Commands: `du` and `df`

Linux provides several commands for checking disk and file-system space. Two commonly used commands are:

* `du` — estimates disk space used by files and directories.
* `df` — reports available and used space on mounted file systems.

---

## 1. `du` — Disk Usage

The `du` command estimates the amount of disk space used by files and directories.

### Basic Syntax

```bash
du [options] [file_or_directory]
```

### Common `du` Options

| Command    | Description                                                            |
| ---------- | ---------------------------------------------------------------------- |
| `du`       | Displays disk usage for files and directories.                         |
| `du -h`    | Displays disk usage in human-readable units such as `K`, `M`, and `G`. |
| `du -s`    | Displays only the total size of the specified file or directory.       |
| `du -sh`   | Displays the total size in a human-readable format.                    |
| `du -sh *` | Displays the total size of each item in the current directory.         |

### Example: `du -sh *`

```bash
du -sh *
```

Example output:

```text
4.0K    Desktop
4.0K    Documents
284K    Downloads
4.0K    Music
4.0K    Pictures
4.0K    Projects
4.0K    Public
4.0K    Templates
4.0K    Test2
12K     TestDirectory
4.0K    Videos
```

### Understanding the Output

Each line contains:

```text
SIZE    DIRECTORY
```

For example:

```text
284K    Downloads
```

This indicates that the `Downloads` directory uses approximately **284 KB of disk space**, including the files and subdirectories contained within it.

Another example:

```text
12K     TestDirectory
```

This indicates that `TestDirectory` uses approximately **12 KB**, including its contents.

### A More Practical Example

To check the total size of a specific directory:

```bash
du -sh ~/Downloads
```

Example:

```text
284K    /home/user/Downloads
```

This is useful when checking how much space a particular directory is consuming.

---

# 2. `df` — Disk Free Space

The `df` command reports disk-space usage for mounted file systems.

Unlike `du`, which focuses on **files and directories**, `df` focuses on **file systems and their available space**.

### Basic Syntax

```bash
df [options]
```

### Common `df` Options

| Command | Description                                               |
| ------- | --------------------------------------------------------- |
| `df`    | Displays file-system space usage in 1K blocks.            |
| `df -h` | Displays file-system space usage in human-readable units. |

---

## 3. `df` Example

Command:

```bash
df
```

Example output:

```text
Filesystem     1K-blocks     Used Available Use% Mounted on
udev             1905516        0   1905516   0% /dev
tmpfs             401036      964    400072   1% /run
/dev/sda1      205838128 28713332 167881492  15% /
tmpfs            2005164        4   2005160   1% /dev/shm
none                1024        0      1024   0% /run/credentials/systemd-journald.service
tmpfs            2005164       28   2005136   1% /tmp
none                1024        0      1024   0% /run/credentials/getty@tty1.service
tmpfs             401032      116    400916   0% /run/user/1001
```

### Output Columns

| Column       | Meaning                                         |
| ------------ | ----------------------------------------------- |
| `Filesystem` | Name of the file system or device.              |
| `1K-blocks`  | Total space available, measured in 1-KB blocks. |
| `Used`       | Amount of space currently in use.               |
| `Available`  | Amount of space currently available.            |
| `Use%`       | Percentage of space currently being used.       |
| `Mounted on` | Directory where the file system is mounted.     |

For example:

```text
/dev/sda1      205838128 28713332 167881492  15% /
```

This indicates that the `/dev/sda1` file system is mounted at `/` and is using approximately **15%** of its available space.

---

# 4. `df -h` — Human-Readable File-System Usage

The `-h` option makes the output easier to read by converting block counts into units such as KB, MB, GB, and TB.

Command:

```bash
df -h
```

Example output:

```text
Filesystem      Size  Used Avail Use% Mounted on
udev            1.9G     0  1.9G   0% /dev
tmpfs           392M  964K  391M   1% /run
/dev/sda1       197G   28G  161G  15% /
tmpfs           2.0G  4.0K  2.0G   1% /dev/shm
none            1.0M     0  1.0M   0% /run/credentials/systemd-journald.service
tmpfs           2.0G   28K  2.0G   1% /tmp
none            1.0M     0  1.0M   0% /run/credentials/getty@tty1.service
tmpfs           392M   116K  392M   0% /run/user/1001
```

For example:

```text
/dev/sda1       197G   28G  161G  15% /
```

This shows:

| Value  | Meaning                   |
| ------ | ------------------------- |
| `197G` | Total file-system size    |
| `28G`  | Space currently used      |
| `161G` | Space currently available |
| `15%`  | Percentage currently used |
| `/`    | Mount point               |

---

# 5. `du` vs `df`

Although both commands are related to disk space, they answer different questions.

| Command | Main Purpose              | Scope                 | Typical Question                                |
| ------- | ------------------------- | --------------------- | ----------------------------------------------- |
| `du`    | Estimates disk usage      | Files and directories | "Which directory is using the most space?"      |
| `df`    | Reports file-system usage | File systems          | "How much free space is available on the disk?" |

### Example

To investigate a directory:

```bash
du -sh ~/Downloads
```

To check overall file-system space:

```bash
df -h
```

A useful way to remember the difference is:

> **`du` → disk usage by files and directories**
> **`df` → disk free space on file systems**

---

# 6. Quick Reference

| Command    | Purpose                                               |
| ---------- | ----------------------------------------------------- |
| `du`       | Show estimated disk usage                             |
| `du -h`    | Show disk usage in human-readable units               |
| `du -s`    | Show only the total usage                             |
| `du -sh`   | Show total usage in human-readable format             |
| `du -sh *` | Show the size of each item in the current directory   |
| `df`       | Show file-system space usage                          |
| `df -h`    | Show file-system space usage in human-readable format |

## Commonly Used Commands

```bash
# Check the size of a directory
du -sh ~/Downloads

# Check the size of every item in the current directory
du -sh *

# Check file-system usage
df

# Check file-system usage in a human-readable format
df -h
```
