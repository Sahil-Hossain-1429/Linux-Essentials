# Linux Terminal Keyboard Shortcuts & Screen Control

> **Environment:** Ubuntu/Debian and common terminal emulators

---

## 1. Opening & Closing the Terminal

| Shortcut           | Action         | Description                                                            |
| ------------------ | -------------- | ---------------------------------------------------------------------- |
| `Ctrl + Alt + T`   | Open Terminal  | Opens a new terminal window in many Ubuntu/Debian desktop environments |
| `Ctrl + Shift + W` | Close Terminal | Closes the current terminal window or tab in many terminal emulators   |

### `Ctrl + Alt + T`

Opens a new terminal window.

```text
Ctrl + Alt + T
```

> **Note:** This shortcut is commonly configured in Ubuntu and some Debian-based desktop environments. The exact shortcut may vary depending on the desktop environment and system configuration.

---

### `Ctrl + Shift + W`

Closes the current terminal window or tab in many terminal emulators.

```text
Ctrl + Shift + W
```

> **Note:** Terminal shortcuts are provided by the terminal emulator and may differ between applications.

---

# 2. Controlling Running Commands

### `Ctrl + C`

Sends an **interrupt signal (`SIGINT`)** to the foreground process.

```text
Ctrl + C
```

It is commonly used to stop a command or program that is currently running in the terminal.

For example:

```bash
ping google.com
```

Pressing:

```text
Ctrl + C
```

normally stops the running `ping` process.

> **Important:** `Ctrl + C` does not necessarily "stop anything" in every situation. It sends `SIGINT` to the foreground process, and the process can potentially handle or ignore the signal.

---

# 3. Clearing the Terminal

### `Ctrl + L`

Clears the visible terminal screen.

```text
Ctrl + L
```

The terminal display is cleared while the command history remains available.

`Ctrl + L` is generally equivalent to running:

```bash
clear
```

---

### `clear`

Clears the visible contents of the terminal.

```bash
clear
```

After execution, the terminal provides a clean screen for continued work.

> **Important:** `clear` does not delete command history or remove files. It only clears the visible terminal display.

---

# 4. Command Autocompletion

### `Tab`

Pressing `Tab` activates **shell autocompletion**.

```text
Tab
```

It can be used to:

* Complete commands
* Complete filenames
* Complete directory names
* Display possible matches when multiple completions exist

For example, if the directory contains:

```text
Documents
Downloads
```

typing:

```bash
cd Doc
```

and pressing:

```text
Tab
```

may complete the command to:

```bash
cd Documents
```

Autocompletion reduces typing and helps avoid spelling mistakes.

---

# Quick Reference

| Shortcut / Command | Category        | Action                                         |
| ------------------ | --------------- | ---------------------------------------------- |
| `Ctrl + Alt + T`   | Terminal        | Opens a new terminal                           |
| `Ctrl + Shift + W` | Terminal        | Closes the current terminal window/tab         |
| `Ctrl + C`         | Process Control | Sends `SIGINT` to the foreground process       |
| `Ctrl + L`         | Terminal        | Clears the visible terminal screen             |
| `Tab`              | Shell           | Autocompletes commands, files, and directories |
| `clear`            | Command         | Clears the visible terminal screen             |

---

# Shortcut vs Command

It is useful to distinguish between **keyboard shortcuts** and **shell commands**.

### Keyboard shortcuts

These are key combinations interpreted by the terminal emulator or shell:

```text
Ctrl + C
Ctrl + L
Ctrl + Alt + T
Ctrl + Shift + W
Tab
```

### Shell commands

These are programs or shell built-ins executed by entering text into the terminal:

```bash
clear
pwd
ls
cd
mkdir
```

For example:

```text
Ctrl + L
```

and:

```bash
clear
```

both provide a way to clear the visible terminal screen, but they are not the same mechanism.

---

# Summary

```text
TERMINAL SHORTCUTS
│
├── Opening / Closing
│   ├── Ctrl + Alt + T  → Open terminal
│   └── Ctrl + Shift + W → Close terminal/tab
│
├── Process Control
│   └── Ctrl + C → Interrupt foreground process
│
├── Screen Control
│   └── Ctrl + L → Clear visible screen
│
└── Shell Assistance
    └── Tab → Autocompletion
```
