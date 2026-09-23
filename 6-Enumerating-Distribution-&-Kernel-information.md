# Linux Basic Commands

This section covers commonly used Linux commands for identifying users, groups, system information, CPU information, logged-in users, and searching for files and directories.

## 1. `whoami`

| Item        | Description                              |
| ----------- | ---------------------------------------- |
| **Command** | `whoami`                                 |
| **Purpose** | Prints the username of the current user. |
| **Syntax**  | `whoami`                                 |

### Example

```bash
whoami
```

**Output:**

```text
nexus
```

---

## 2. `hostname`

| Item        | Description                             |
| ----------- | --------------------------------------- |
| **Command** | `hostname`                              |
| **Purpose** | Displays or sets the system's hostname. |
| **Syntax**  | `hostname`                              |

### Example

```bash
hostname
```

**Output:**

```text
kali
```

### Note

Running `hostname` without an argument displays the current hostname.

---

## 3. `id`

| Item        | Description                                                                   |
| ----------- | ----------------------------------------------------------------------------- |
| **Command** | `id`                                                                          |
| **Purpose** | Displays the real and effective user ID (UID) and group ID (GID) information. |
| **Syntax**  | `id [username]`                                                               |

### Example

```bash
id
```

A typical output may look like:

```text
uid=1001(nexus) gid=1001(nexus) groups=1001(nexus),27(sudo),100(users)
```

### Important Information

| Field    | Meaning                         |
| -------- | ------------------------------- |
| `uid`    | User ID                         |
| `gid`    | Primary group ID                |
| `groups` | Groups associated with the user |

---

## 4. `groups`

| Item        | Description                                 |
| ----------- | ------------------------------------------- |
| **Command** | `groups`                                    |
| **Purpose** | Displays the groups associated with a user. |
| **Syntax**  | `groups [username]`                         |

### Example

```bash
groups nexus
```

**Output:**

```text
nexus : nexus sudo users
```

This indicates that the `nexus` user belongs to the following groups:

* `nexus`
* `sudo`
* `users`

---

## 5. `lsb_release -a`

| Item          | Description                                       |
| ------------- | ------------------------------------------------- |
| **Command**   | `lsb_release`                                     |
| **Option**    | `-a`                                              |
| **Purpose**   | Displays distribution-specific Linux information. |
| **Full form** | Linux Standard Base Release                       |

### Example

```bash
lsb_release -a
```

**Output:**

```text
No LSB modules are available.
Distributor ID:	Kali
Description:	Kali GNU/Linux Rolling
Release:	2026.3
Codename:	kali-rolling
```

### Option

`-a` stands for **all** and displays all available distribution information.

---

## 6. `lscpu`

| Item        | Description                                      |
| ----------- | ------------------------------------------------ |
| **Command** | `lscpu`                                          |
| **Purpose** | Displays information about the CPU architecture. |
| **Syntax**  | `lscpu`                                          |

### Example

```bash
lscpu
```

Typical information includes:

* CPU architecture
* CPU model
* Number of CPUs
* Number of cores
* Number of threads
* CPU frequency
* Virtualization support
* Cache information

---

## 7. `uname`

| Item        | Description                                                        |
| ----------- | ------------------------------------------------------------------ |
| **Command** | `uname`                                                            |
| **Purpose** | Displays the system name and information about the current kernel. |
| **Syntax**  | `uname [option]`                                                   |

### Example

```bash
uname
```

**Example output:**

```text
Linux
```

### Useful Options

| Option | Description                        |
| ------ | ---------------------------------- |
| `-s`   | Kernel name                        |
| `-r`   | Kernel release                     |
| `-v`   | Kernel version                     |
| `-m`   | Machine hardware architecture      |
| `-a`   | Displays all available information |

### Example

```bash
uname -a
```

---

## 8. `who`

| Item        | Description                                                        |
| ----------- | ------------------------------------------------------------------ |
| **Command** | `who`                                                              |
| **Purpose** | Displays information about users currently logged into the system. |
| **Syntax**  | `who`                                                              |

### Example

```bash
who
```

Typical output:

```text
nexus    tty1    2026-09-23 09:15
```

The output can contain information such as the username, terminal, login date, and login time.

---

# File and Directory Searching

## 9. `find`

| Item             | Description                                                      |
| ---------------- | ---------------------------------------------------------------- |
| **Command**      | `find`                                                           |
| **Purpose**      | Searches for files and directories within a directory hierarchy. |
| **Basic syntax** | `find [path] [expression]`                                       |

The `find` command can search based on several properties, including:

* Filename
* File type
* Permissions
* Owner
* Group
* File size
* Modification time

---

## 10. Searching for Files with `sudo`

The following command searches the entire filesystem for regular files:

```bash
sudo find / -type f
```

| Part      | Meaning                                        |
| --------- | ---------------------------------------------- |
| `sudo`    | Executes the command with elevated privileges. |
| `find`    | Searches for files and directories.            |
| `/`       | Starts the search from the root directory.     |
| `-type f` | Restricts the search to regular files.         |

### Searching for Directories

```bash
sudo find / -type d
```

Here, `-type d` restricts the search to directories.

---

## 11. Searching for a Specific File

For example, a configuration file named `proxychains.conf` can be searched for with:

```bash
sudo find / -type f -name "proxychains.conf"
```

A possible result:

```text
/etc/proxychains4.conf
```

Permission-related messages may also appear during a search:

```text
find: '/run/user/1001/gvfs': Permission denied
```

### Why Does `Permission denied` Appear?

Some directories may not be accessible even during a filesystem-wide search. Running the command with `sudo` provides additional privileges, but certain virtual, mounted, or restricted filesystems can still produce permission-related messages.

---

# Searching by File Permissions

The `find` command can also search for files based on their permissions.

For example, consider a file with the following permissions:

```text
r--r--r--
```

These permissions correspond to numeric mode:

```text
444
```

A search can be performed without knowing the filename.

## 12. Permission Search — Numeric Mode

```bash
find /home -type f -perm 444
```

| Part        | Meaning                                        |
| ----------- | ---------------------------------------------- |
| `find`      | Searches the filesystem.                       |
| `/home`     | Starts the search from `/home`.                |
| `-type f`   | Searches only regular files.                   |
| `-perm 444` | Searches for files with permission mode `444`. |

### Example Result

```text
/home/nexus/TestDirectory/test.sh
```

---

## 13. Permission Search — Symbolic Mode

The same permission condition can be expressed using symbolic notation:

```bash
find /home -type f -perm u=r,g=r,o=r
```

| Permission | Meaning                      |
| ---------- | ---------------------------- |
| `u=r`      | Owner has read permission.   |
| `g=r`      | Group has read permission.   |
| `o=r`      | Others have read permission. |

This corresponds to:

```text
r--r--r--
```

and:

```text
444
```

---

# `find` Command Reference

| Command                                | Purpose                                                                       |
| -------------------------------------- | ----------------------------------------------------------------------------- |
| `find / -type f`                       | Search for regular files from the root directory.                             |
| `find / -type d`                       | Search for directories from the root directory.                               |
| `sudo find / -type f`                  | Search for regular files with elevated privileges.                            |
| `sudo find / -type d`                  | Search for directories with elevated privileges.                              |
| `find /home -type f -name "file.txt"`  | Search for a specific filename.                                               |
| `find /home -type f -perm 444`         | Search for regular files with permission mode `444`.                          |
| `find /home -type f -perm u=r,g=r,o=r` | Search for regular files where owner, group, and others have read permission. |

## Quick Reference

| Command          | Main Use                         |
| ---------------- | -------------------------------- |
| `whoami`         | Current username                 |
| `hostname`       | System hostname                  |
| `id`             | User and group IDs               |
| `groups`         | User's groups                    |
| `lsb_release -a` | Linux distribution information   |
| `lscpu`          | CPU information                  |
| `uname -a`       | Kernel and system information    |
| `who`            | Currently logged-in users        |
| `find`           | Search for files and directories |
