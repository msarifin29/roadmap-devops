`systemd` is a system and service manager for Linux operating systems, which has become the de facto standard for many Linux distributions. It is designed to improve the boot process and manage system services more efficiently than traditional init systems like SysVinit. Here's a detailed explanation of how `systemd` works:

### 1. Core Concepts

- **Units**: `systemd` manages system resources through units, which are configuration files that describe resources such as services, sockets, devices, mounts, and more. Each unit file has a specific type (e.g., .`service`, .`socket`, .`device`).
- **Dependencies**: Units can have dependencies on other units, ensuring that resources are started and stopped in the correct order.
- **Targets**: Targets are special units that group other units together, similar to runlevels in SysVinit but more flexible.

### 2. Unit Files

- **Location**: Unit files are typically located in `/usr/lib/systemd/system/` for system-provided units and `/etc/systemd/system/` for user-defined or customized units.
- **Structure**: A unit file is a plain text file with sections and key-value pairs. For example, a service unit file might look like this:

```bash
[Unit]
Description=Example Service
After=network.target

[Service]
ExecStart=/usr/bin/example-service
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

### 3. Service Management

- **Starting and Stopping Services**: You can start, stop, restart, and check the status of services using systemctl commands:
```bash
systemctl start example.service
systemctl stop example.service
systemctl restart example.service
systemctl status example.service
```
- **Enabling and Disabling Services**: To enable a service to start at boot, or disable it:

### 4. Targets

- **Default Target**: The default target is analogous to the default runlevel in SysVinit. You can set the default target with:
```bash
systemctl set-default multi-user.target
```
- **Switching Targets**: You can switch to a different target temporarily:
```bash
systemctl isolate graphical.target
```

### 5. Dependency Management

-  **Ordering**: `systemd` uses dependencies to ensure that units are started and stopped in the correct order. For example, a service that requires networking to be up will have a dependency on `network.target`.
- **Parallelization**: `systemd` can start units in parallel if they do not have dependencies on each other, speeding up the boot process.

### 6. Journaling and Logging

- **Journald**: `systemd` includes `journald`, a logging daemon that collects and stores logging data. You can view logs using:
```bash
journalctl
```
- **Log Filtering**: You can filter logs by unit, priority, time, and more:
```bash
journalctl -u example.service
journalctl -p err
journalctl --since "2023-10-01" --until "2023-10-02"
```

### 7. Socket Activation
- **Socket Units**: `systemd` can manage sockets and start services on-demand when a connection is made to the socket. This is useful for services that do not need to run continuously.
- **Example**: A socket unit file might look like this:
```bash
[Unit]
Description=Example Socket

[Socket]
ListenStream=12345
Accept=yes

[Install]
WantedBy=sockets.target
```

### 8. Timer Units
- **Timers**: `systemd` can manage cron-like jobs using timer units. Timers can be used to schedule tasks to run at specific times or intervals.
- **Example**: A timer unit file might look like this:
```bash
[Unit]
Description=Run example service daily

[Timer]
OnCalendar=daily
Persistent=true

[Install]
WantedBy=timers.target
```

### 9. System State Management

- **System States**: systemd can manage different system states such as poweroff, reboot, and suspend:
```bash
systemctl poweroff
systemctl reboot
systemctl suspend
```

Below is the list of some useful systemd utilities along with a brief description of what they do:

- `systemctl`: It Controls the systemd system and services.
- `journalctl`: Used To manage journal, systemd’s own logging system
- `hostnamectl`: Can Control hostname.
- `localectl`: Helps Configure system local and keyboard layout.
- `timedatectl`: Used to Set time and date.
- `systemd-cgls` : It Shows cgroup contents.
- `systemadm`: It is a Front-end for systemctl command.

| comaand-line | description |
| `systemctl list-units --type service --all` | see all available services |
| `systemctl start [service-name]` | start a service |
| `systemctl stop [service-name]` | stop a service |
| `systemctl restart [service-name]` | restart a service |

### 10. Integration with Other Tools

- **Compatibility**: `systemd` is designed to be compatible with existing tools and scripts. It can run traditional init scripts and integrates with other system components like udev for device management.

