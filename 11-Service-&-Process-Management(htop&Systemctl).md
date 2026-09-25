# Linux Process and System Monitoring Commands

The following commands are commonly used to monitor processes, memory usage, and system services in Linux.

| Command     | Description                                                                                                                                                                     | Example                |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- |
| `top`       | Displays a real-time view of running Linux processes, including CPU and memory usage.                                                                                           | `top`                  |
| `htop`      | Provides an interactive and user-friendly process viewer with real-time CPU, memory, and process information.                                                                   | `htop`                 |
| `free`      | Displays information about total, used, free, shared, cached, and available system memory.                                                                                      | `free -h`              |
| `ps`        | Displays information about currently running processes. It is useful for obtaining a snapshot of active processes. For continuous updates, `top` or `htop` can be used instead. | `ps aux`               |
| `systemctl` | Controls and manages the `systemd` system and service manager, including starting, stopping, restarting, and checking the status of services.                                   | `systemctl status ssh` |

## Quick Reference

| Command                      | Common Use                           |
| ---------------------------- | ------------------------------------ |
| `top`                        | Real-time process monitoring         |
| `htop`                       | Interactive process monitoring       |
| `free -h`                    | Memory usage and availability        |
| `ps aux`                     | List currently running processes     |
| `systemctl status <service>` | Check the status of a system service |

