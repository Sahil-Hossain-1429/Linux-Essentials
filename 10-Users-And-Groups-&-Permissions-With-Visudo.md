# Linux User and Group Management Commands

Linux provides several commands for managing users, groups, and administrative privileges.

## 1. User Management

| Command                                    | Purpose                                                                 | Example                                         |
| ------------------------------------------ | ----------------------------------------------------------------------- | ----------------------------------------------- |
| `useradd`                                  | Creates a new user or modifies default settings for newly created users | `sudo useradd nexus`                            |
| `useradd -m -c "nexus" -s /bin/bash nexus` | Creates a user with a home directory, comment, and Bash shell           | `sudo useradd -m -c "nexus" -s /bin/bash nexus` |
| `usermod -aG`                              | Adds an existing user to one or more supplementary groups               | `sudo usermod -aG developers nexus`             |
| `userdel -r`                               | Deletes a user and removes the user's home directory and mail spool     | `sudo userdel -r nexus`                         |
| `su username`                              | Switches to another user account                                        | `su nexus`                                      |

---

# 2. `useradd`

The `useradd` command creates a new user account or modifies the default settings used when creating new users.

### Basic Syntax

```bash
useradd [options] username
```

### Basic Example

```bash
sudo useradd nexus
```

This creates a user named `nexus`.

Depending on the system configuration, a home directory may not be created automatically.

### Creating a User with a Home Directory and Bash Shell

```bash
sudo useradd -m -c "nexus" -s /bin/bash nexus
```

| Option      | Meaning                                    |
| ----------- | ------------------------------------------ |
| `-m`        | Creates the user's home directory          |
| `-c`        | Adds a comment or description for the user |
| `-s`        | Specifies the user's login shell           |
| `/bin/bash` | Sets Bash as the login shell               |
| `nexus`     | Name of the new user                       |

The resulting account can look like:

```text
Username: nexus
Home:     /home/nexus
Shell:    /bin/bash
Comment:  nexus
```

### Setting a Password

A password can be assigned after creating the account:

```bash
sudo passwd nexus
```

The command prompts for a new password.

---

# 3. `usermod -aG`

The `usermod` command modifies an existing user account.

The `-aG` options are commonly used to add a user to supplementary groups.

### Example

```bash
sudo usermod -aG developers nexus
```

This adds `nexus` to the `developers` group.

| Option       | Meaning                                              |
| ------------ | ---------------------------------------------------- |
| `-a`         | Append the user to the existing supplementary groups |
| `-G`         | Specify supplementary groups                         |
| `developers` | Group name                                           |
| `nexus`      | Username                                             |

### Important Note

The `-a` option is important when adding a user to an existing group.

For example:

```bash
sudo usermod -aG developers nexus
```

preserves existing supplementary group memberships.

Without `-a`:

```bash
sudo usermod -G developers nexus
```

the supplementary group list is replaced with the specified group list.

---

# 4. `userdel -r`

The `userdel` command deletes a user account.

The `-r` option also removes the user's home directory and mail spool.

### Example

```bash
sudo userdel -r nexus
```

This removes:

```text
User account
    +
Home directory
    +
Mail spool
```

### Without `-r`

```bash
sudo userdel nexus
```

The user account is removed, but the user's home directory may remain.

> **Caution:** `userdel -r` permanently removes the user's home directory and its contents.

---

# 5. `su`

The `su` command is used to switch to another user account.

### Syntax

```bash
su username
```

### Example

```bash
su nexus
```

This starts a shell as the `nexus` user and normally requests the `nexus` user's password.

### Switching to a Login Shell

A common form is:

```bash
su - nexus
```

The `-` creates a login shell and loads the target user's login environment.

| Command      | Purpose                                      |
| ------------ | -------------------------------------------- |
| `su nexus`   | Switches to the `nexus` user                 |
| `su - nexus` | Switches to `nexus` with a login environment |

The login-shell form is often preferable when working interactively as another user.

---

# 6. `groupadd`

The `groupadd` command creates a new group.

### Syntax

```bash
groupadd groupname
```

### Example

```bash
sudo groupadd developers
```

This creates a group named `developers`.

A user can then be added to the group:

```bash
sudo usermod -aG developers nexus
```

The relationship can be represented as:

```text
developers
    │
    ├── nexus
    ├── alice
    └── bob
```

Groups make it possible to manage permissions for multiple users collectively.

---

# 7. `groups`

The `groups` command displays the groups associated with a user.

### Example

```bash
groups nexus
```

Possible output:

```text
nexus : nexus developers
```

This indicates that `nexus` belongs to the `nexus` and `developers` groups.

For the currently logged-in user:

```bash
groups
```

---

# 8. `sudo visudo`

`visudo` is a utility used to safely edit the `sudoers` configuration.

The `sudoers` configuration controls which users and groups can execute commands with elevated privileges through `sudo`.

### Command

```bash
sudo visudo
```

This opens the sudoers configuration using the system's configured editor.

A typical rule can look like:

```text
nexus ALL=(ALL:ALL) ALL
```

This allows the `nexus` user to execute commands through `sudo`, subject to the configured sudo policy.

### Why Use `visudo`?

The sudoers configuration is security-sensitive.

`visudo` checks the syntax before applying the configuration, helping prevent an invalid sudoers file from causing administrative problems.

> **Important:** Directly editing `/etc/sudoers` with a normal text editor is discouraged. `visudo` should be used for editing the sudoers configuration.

---

# 9. Complete Example

The following sequence demonstrates a typical user and group-management workflow.

### Step 1: Create a Group

```bash
sudo groupadd developers
```

### Step 2: Create a User

```bash
sudo useradd -m -c "Nexus Developer" -s /bin/bash nexus
```

### Step 3: Set the User's Password

```bash
sudo passwd nexus
```

### Step 4: Add the User to the Group

```bash
sudo usermod -aG developers nexus
```

### Step 5: Verify Group Membership

```bash
groups nexus
```

Possible output:

```text
nexus : nexus developers
```

### Step 6: Switch to the User

```bash
su - nexus
```

### Step 7: Return to the Previous Shell

```bash
exit
```

The complete workflow:

```text
Create group
     │
     ▼
groupadd developers
     │
     ▼
Create user
     │
     ▼
useradd -m ... nexus
     │
     ▼
Set password
     │
     ▼
passwd nexus
     │
     ▼
Add user to group
     │
     ▼
usermod -aG developers nexus
     │
     ▼
Verify membership
     │
     ▼
groups nexus
```

---

# 10. Quick Reference

| Command                  | Main Purpose                                    |
| ------------------------ | ----------------------------------------------- |
| `useradd`                | Create a user account                           |
| `useradd -m ...`         | Create a user with a home directory             |
| `passwd`                 | Set or change a user's password                 |
| `usermod`                | Modify an existing user                         |
| `usermod -aG group user` | Add a user to a supplementary group             |
| `userdel`                | Delete a user account                           |
| `userdel -r`             | Delete a user and the home directory            |
| `su username`            | Switch to another user                          |
| `su - username`          | Switch to another user with a login environment |
| `groupadd`               | Create a group                                  |
| `groups`                 | Display group memberships                       |
| `visudo`                 | Safely edit the sudoers configuration           |

---

# 11. Key Points to Remember

* `useradd` → creates a user.
* `usermod` → modifies an existing user.
* `userdel` → deletes a user.
* `passwd` → manages a user's password.
* `groupadd` → creates a group.
* `usermod -aG` → adds a user to supplementary groups.
* `groups` → displays group membership.
* `su` → switches to another user.
* `sudo` → executes commands with elevated privileges according to sudo policy.
* `visudo` → safely edits the sudoers configuration.
* `-m` with `useradd` → creates a home directory.
* `-s` with `useradd` → specifies the login shell.
* `-aG` with `usermod` → adds supplementary group membership without replacing existing memberships.
* `-r` with `userdel` → removes the user's home directory along with the account.
