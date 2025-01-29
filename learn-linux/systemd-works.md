### What is Systemd?

**Systemd** is like the traffic manager for your Linux system. It’s a modern tool that organizes and supervises how different parts of your system start and run. Imagine it as a smarter, faster way to handle tasks compared to older methods. Instead of doing things one after the other, systemd can get multiple tasks going at the same time, making your computer start up quicker and respond faster. It uses something called “units” to keep everything in order – like `services`, `sockets`, and `devices` – helping your system run smoothly.

### What is the Linux Systemctl Command?

Now, imagine you have a remote control for your Linux system – that’s what `systemctl` is. It’s like your boss for telling the system what to do. With this tool, you can start, stop, or restart services (think of them like programs running in the background). Want something to start automatically when your computer turns on? `systemctl` helps with that too. It’s also good for checking how things are going – like looking at logs or figuring out what other things a service needs to work properly. So, if you’re in charge of a Linux system, `systemctl` is your go-to tool for keeping things organized and running well.

`systemd` is designed to improve the boot process and manage system services more efficiently than traditional init systems like SysVinit. Here's a detailed explanation of how `systemd` works:

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

### 10. Integration with Other Tools

- **Compatibility**: `systemd` is designed to be compatible with existing tools and scripts. It can run traditional init scripts and integrates with other system components like udev for device management.

### Several Command-line manage system services

  | command-line | description |
  | --- | --- |
  | `systemctl list-units --type service --all` | see all available services |
  | `systemctl start [service-name]` | Starting services |
  | `systemctl stop [service-name]` | Stopping services |
  | `systemctl enable [service-name]` | Enabling services |
  | `systemctl disable [service-name]` | Disabling services |
  | `systemctl restart [service-name]` | Restarting services |
  | `systemctl status [service-name]` | Viewing status of services |
  | `systemctl reload [service-name]` | Reloading services |
  | `systemctl mask [service-name]` | Masking services |
  | `systemctl unmask [service-name]` | Unmasking services |
  | `systemctl set-default [service-name]` | Changing the Default Target (Example: If we want to change the default target to graphical.target (which will start the graphical user interface).) |
  | `systemctl list-unit-files` |  Listing Unit Files |
  | `systemctl mask [unit-file]` |  Masking Unit Files |
  | `systemctl unmask [unit-file]` |  Unmasking Unit Files |

  | Options | Description | Syntax |  
  | --- | --- | --- |  
  | `–version` | This option displays the version number of the systemctl command. | `systemctl --version` | 
  | `–help` | This option displays the help manual for systemctl, including a list of available options and commands | `systemctl --help` |   
  | `–type` | The argument in this case should be comma-separated list of unit types such as service and socket. | `systemctl --type=service` |   
  | `–all` | This option lists all available units, including those that are inactive. | `systemctl --all` |   
  | `–failed` | This option lists all units that have failed. | `systemctl --failed` |   
  | –user | talk to service manager of calling user, instead of system. | systemctl --user |
  | `–force` | This option forces the service to start or stop, even if it has dependencies that are not yet started or stopped. | `systemctl stop --force httpd.service` |
  | `–no-block` | This option starts or stops the service without blocking the shell, allowing the user to continue to use the shell while the service is starting or stopping. | `systemctl start --no-block httpd.service` |
  | `–state` | This option is used to filter the output based on the specified unit state. You can specify one or more-unit states separated by commas, such as active, inactive, failed, and activating. For example: to list all the failed units. | `systemctl list-units --state=failed` |
  | `-r, –recursive` | This option is used to show units of local containers as well. For example: to list all units including those in local containers. | `systemctl list-units --recursive` |
  | `–show-types` | This option is used to show the types of sockets along with showing sockets. For example: to show the types of all sockets. | `systemctl list-sockets --show-types` |
  | `–job-mode=` | This option controls how to deal with already queued jobs in case of queuing a new job. There are three available modes:replace: replace already queued jobs with the new one. fail: cancel the new job and return failure if there are already queued jobs. isolate: queue the new job and isolate it from the other jobs. For example: to use the replace mode. | `systemctl isolate graphical.target --job-mode=replace` |
  | `-i, –ignore-inhibitors` | This option is used to ignore inhibitor locks when requesting a system shutdown or sleep state. For example: to ignore inhibitor locks when requesting a system shutdown. | `systemctl poweroff --ignore-inhibitors` |
  | `-q, –quiet` | This option is used to suppress the printing of results of various commands and the hints about the truncated lines. For example: to reload the systemctl daemon without showing any output. | `systemctl daemon-reload --quiet` |
  | `–no-wall` | This option is used to not send a wall message before power-off, halt, or reboot. For example: to halt the system without sending a wall message. | `systemctl halt --no-wall` |