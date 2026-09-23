# Linux Shells

A **shell** is a command-line interpreter that provides an interface between a user and the operating system.

There are several different shells available on Linux systems, including:

* Bash
* Zsh
* Dash
* Fish
* KornShell (Ksh)
* PowerShell

On many Debian-based systems, including Debian and Ubuntu, **Bash** is commonly used as the default interactive shell.

---

# 1. Checking the Current Shell

The `$SHELL` environment variable can be used to display the user's default login shell.

### Command

```bash
echo $SHELL
```

### Example Output

```text
/bin/bash
```

This indicates that the default login shell is **Bash**.

### Bash

| Item           | Information        |
| -------------- | ------------------ |
| **Name**       | Bash               |
| **Full form**  | Bourne Again SHell |
| **Executable** | `/bin/bash`        |
| **Type**       | Command-line shell |

### Important Note

`$SHELL` generally represents the user's **default login shell**. It does not always indicate the shell currently running in every situation.

For example, a Bash session started from another shell can still have `$SHELL` set to the original login shell.

---

# 2. Listing Available Shells

The file `/etc/shells` contains a list of shells that are considered valid login shells on the system.

### Command

```bash
cat /etc/shells
```

### Example Output

```text
/bin/sh
/usr/bin/sh
/bin/bash
/usr/bin/bash
/bin/rbash
/usr/bin/rbash
/usr/bin/dash
/usr/bin/tmux
/bin/zsh
/usr/bin/zsh
/usr/bin/pwsh
/opt/microsoft/powershell/7/pwsh
/usr/bin/screen
```

The exact list depends on the installed software and the Linux distribution.

### Common Shells

| Shell             | Description                                    |
| ----------------- | ---------------------------------------------- |
| `/bin/sh`         | Generic POSIX-compatible shell interface       |
| `/bin/bash`       | Bourne Again SHell                             |
| `/bin/dash`       | Debian Almquist Shell; lightweight POSIX shell |
| `/bin/zsh`        | Z Shell                                        |
| `/bin/rbash`      | Restricted Bash shell                          |
| `/usr/bin/pwsh`   | PowerShell                                     |
| `/usr/bin/tmux`   | Terminal multiplexer; not normally a shell     |
| `/usr/bin/screen` | Terminal multiplexer; not normally a shell     |

### Important Note

Not every entry that appears in `/etc/shells` necessarily represents a traditional shell. Some systems may include programs that can be used as login programs or command interpreters.

---

# 3. Changing the Login Shell with `chsh`

The `chsh` command changes the **login shell** associated with a user account.

### Full Form

**`chsh` = change shell**

### Basic Syntax

```bash
chsh [options] [username]
```

### Example

```bash
chsh
```

The command may prompt for the desired login shell.

A shell path can also be specified explicitly:

```bash
chsh -s /bin/zsh
```

Here:

| Part       | Meaning                 |
| ---------- | ----------------------- |
| `chsh`     | Changes the login shell |
| `-s`       | Specifies the new shell |
| `/bin/zsh` | New login shell         |

---

# 4. Checking Available Shells Before Using `chsh`

Before changing the login shell, the available login shells can be checked with:

```bash
cat /etc/shells
```

For example:

```text
/bin/bash
/bin/zsh
/bin/dash
```

A shell path from the available list can then be selected.

### Example

To change the login shell to Zsh:

```bash
chsh -s /bin/zsh
```

The current password may be requested depending on the system configuration.

---

# 5. Applying and Verifying the Shell Change

Changing the login shell does not necessarily replace the shell process of an already-running terminal session.

A new login session can be started by logging out and logging back in.

After starting a new session, the login shell can be checked with:

```bash
echo $SHELL
```

### Example

```bash
echo $SHELL
```

Output:

```text
/bin/zsh
```

This indicates that `/bin/zsh` is configured as the login shell.

### Alternative Verification

The account's configured login shell can also be checked with:

```bash
getent passwd "$USER"
```

Example:

```text
nexus:x:1001:1001::/home/nexus:/bin/zsh
```

The final field contains the configured login shell:

```text
/bin/zsh
```

---

# Bash Configuration Files

Bash uses several configuration and history files in the user's home directory.

Common files include:

| File              | Main Purpose                                             |
| ----------------- | -------------------------------------------------------- |
| `~/.bash_aliases` | Stores custom Bash aliases                               |
| `~/.bash_history` | Stores previously executed Bash commands                 |
| `~/.bash_logout`  | Contains commands executed when a Bash login shell exits |
| `~/.bashrc`       | Configures interactive Bash shells                       |

The `~` symbol represents the current user's home directory.

For example:

```text
~/.bashrc
```

usually refers to:

```text
/home/nexus/.bashrc
```

---

# 6. `.bash_aliases`

The `.bash_aliases` file is commonly used to store **custom Bash aliases**.

An alias creates a shorter name for a command or command sequence.

### Example

```bash
alias ll='ls -lah'
```

After defining the alias:

```bash
ll
```

is equivalent to:

```bash
ls -lah
```

### Typical Purpose

```text
~/.bash_aliases
```

can contain frequently used aliases:

```bash
alias ll='ls -lah'
alias la='ls -A'
alias ..='cd ..'
```

### Relationship with `.bashrc`

On many Debian-based systems, `.bashrc` contains logic that loads `.bash_aliases` if the file exists.

A typical configuration may look like:

```bash
if [ -f ~/.bash_aliases ]; then
    . ~/.bash_aliases
fi
```

The `.` means **source**, which loads the contents of the file into the current shell.

---

# 7. `.bash_history`

The `.bash_history` file stores previously executed Bash commands.

### Location

```text
~/.bash_history
```

For example:

```bash
cat ~/.bash_history
```

may display entries such as:

```text
ls
pwd
cd /var/log
cat /etc/os-release
whoami
```

### Why It Is Useful

Bash history allows previously executed commands to be:

* Reviewed
* Reused
* Searched
* Retrieved with the Up Arrow key

For example:

```bash
history
```

displays commands from the current shell's history.

### Important Note

The exact behavior of command history depends on Bash configuration and shell settings. The `.bash_history` file is commonly written when a Bash session exits.

---

# 8. `.bash_logout`

The `.bash_logout` file contains commands that Bash can execute when a **login shell exits**.

### Location

```text
~/.bash_logout
```

For example:

```bash
cat ~/.bash_logout
```

A system may contain commands such as:

```bash
clear
```

When the login shell exits, those commands can be executed automatically.

### Typical Purpose

The file can be used for cleanup tasks or terminal-related actions that should occur when a login shell terminates.

### Important Note

`.bash_logout` is associated with **login shells**. It is not executed every time an ordinary interactive Bash shell exits.

---

# 9. `.bashrc`

The `.bashrc` file is one of the most important Bash configuration files for interactive shells.

### Location

```text
~/.bashrc
```

It commonly contains configuration for:

* Aliases
* Shell functions
* Environment-related settings
* Prompt customization
* Shell options
* Command completion
* Other interactive Bash settings

### Example

A `.bashrc` file may contain:

```bash
alias ll='ls -lah'

PS1='\u@\h:\w\$ '
```

The first line creates an alias.

The second line customizes the Bash prompt.

---

# `.bashrc` vs `.bash_logout` vs `.bash_history` vs `.bash_aliases`

| File            | Easy Explanation            | Main Purpose                           |
| --------------- | --------------------------- | -------------------------------------- |
| `.bash_aliases` | "Shortcut commands"         | Stores aliases                         |
| `.bash_history` | "Command record"            | Stores command history                 |
| `.bash_logout`  | "Exit actions"              | Runs commands when a login shell exits |
| `.bashrc`       | "Interactive Bash settings" | Configures interactive Bash sessions   |

### Simple Mental Model

```text
                    Bash
                     │
          ┌──────────┼──────────┐
          │          │          │
       .bashrc   .bash_aliases  .bash_history
          │          │          │
     Shell setup   Shortcuts   Command history
          │
          │
     .bash_logout
          │
     Exit actions
```

---

# Quick Reference

| Command / File     | Purpose                                           |
| ------------------ | ------------------------------------------------- |
| `echo $SHELL`      | Displays the configured login shell               |
| `cat /etc/shells`  | Lists valid login shells configured on the system |
| `chsh`             | Changes the login shell                           |
| `chsh -s /bin/zsh` | Sets Zsh as the login shell                       |
| `whoami`           | Displays the current username                     |
| `~/.bash_aliases`  | Stores Bash aliases                               |
| `~/.bash_history`  | Stores Bash command history                       |
| `~/.bash_logout`   | Contains commands for login-shell logout          |
| `~/.bashrc`        | Configures interactive Bash sessions              |

## Key Concept

A simple way to remember the four Bash files is:

```text
.bashrc       → Configure the interactive shell
.bash_aliases → Define command shortcuts
.bash_history → Remember previous commands
.bash_logout  → Perform actions when a login shell exits
```

These files are generally located in the user's home directory:

```text
~/
├── .bash_aliases
├── .bash_history
├── .bash_logout
└── .bashrc
```
