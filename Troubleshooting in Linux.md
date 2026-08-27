Here is the complete step-by-step breakdown of every command, concept, and Linux troubleshooting scenario demonstrated by Praveen Singampalli in his [Debugging & Troubleshooting in Linux](https://www.youtube.com/watch?v=LwcvrEQzg6o) video.

---

### Step 1: Initial System Health Check

* **`sudo su`** [[01:37](https://www.youtube.com/watch?v=LwcvrEQzg6o&t=97)]: Switches from a regular user to the `root` administrative user to run elevated troubleshooting commands.
* **`uptime`** [[01:52](https://www.youtube.com/watch?v=LwcvrEQzg6o&t=112)]: Checks how long the system has been running, the total number of connected users, and system load averages over 1, 5, and 15 minutes.

---

### Step 2: CPU Troubleshooting & Process Analysis

* **`top`** [[02:17](https://www.youtube.com/watch?v=LwcvrEQzg6o&t=137)]: Displays real-time process monitoring, showing system CPU utilization, memory distribution, and active process metrics:
* **PID:** Process ID
* **USER:** Owner of the process
* **PR & NI:** Priority level and Nice value
* **VIRT / RES / SHR:** Virtual, Resident (physical memory), and Shared memory usage
* **%CPU & %MEM:** Percentages of CPU and Memory consumed by each process
* **TIME+ & COMMAND:** CPU runtime and the executed binary command


* **`htop`** [[03:19](https://www.youtube.com/watch?v=LwcvrEQzg6o&t=199)]: An interactive, user-friendly process viewer (requires pre-installation on Amazon Linux/EC2).
* **`ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%cpu | head`** [[04:03](https://www.youtube.com/watch?v=LwcvrEQzg6o&t=243)]: Sorts all running system processes strictly by top CPU consumption and displays the top results including PID, Parent PID (PPID), Command, Memory, and CPU utilization.

---

### Step 3: Memory Issues & Analysis

* **`free -m`** [[05:27](https://www.youtube.com/watch?v=LwcvrEQzg6o&t=327)]: Displays available, total, and used system RAM and swap space in megabytes (MB).
* **`vmstat 1`** [[06:01](https://www.youtube.com/watch?v=LwcvrEQzg6o&t=361)]: Provides virtual memory statistics refreshed every 1 second, showing active processes (r/b), memory usage (swpd, free, buff, cache), I/O block counts (bi/bo), system interrupts/context switches (in/cs), and detailed CPU usage states (us, sy, id, wa, st).

---

### Step 4: Disk & I/O Bottlenecks

* **`df -h`** [[07:12](https://www.youtube.com/watch?v=LwcvrEQzg6o&t=432)]: Displays disk space availability across all mounted filesystems in human-readable format (e.g., GB/MB).
* **`du -sh /*`** [[08:03](https://www.youtube.com/watch?v=LwcvrEQzg6o&t=483)]: Summarizes disk space usage per directory across the Linux file system hierarchy (`/bin`, `/boot`, `/dev`, `/etc`, `/home`, `/var`, etc.).
* **`iostat -x 1`** [[09:28](https://www.youtube.com/watch?v=LwcvrEQzg6o&t=568)]: Refreshes detailed extended I/O statistics every 1 second, tracking read/write throughput, device usage, and CPU wait states (`%iowait`).

---

### Step 5: Network Troubleshooting

* **`netstat -tulnp`** [[10:28](https://www.youtube.com/watch?v=LwcvrEQzg6o&t=628)]: Scans and lists active TCP (`-t`) and UDP (`-u`) listening ports (`-l`) along with numeric addresses (`-n`) and associated Process IDs/names (`-p`).
* **`ss -tulpn`** [[11:46](https://www.youtube.com/watch?v=LwcvrEQzg6o&t=706)]: Modern, faster alternative to `netstat` for analyzing socket connections and listening ports.
* **`ping [www.google.com](https://www.google.com)`** [[12:19](https://www.youtube.com/watch?v=LwcvrEQzg6o&t=739)]: Tests basic network reachability to remote hosts via ICMP packets.
* **`curl [www.google.com](https://www.google.com)`** [[12:19](https://www.youtube.com/watch?v=LwcvrEQzg6o&t=739)]: Fetches external web content over HTTP/HTTPS to verify internet connectivity.

---

### Step 6: Log File Analysis

* **`journalctl -xe`** [[12:32](https://www.youtube.com/watch?v=LwcvrEQzg6o&t=752)]: Retrieves system logs using `systemd-journald`, automatically jumping to the end (`-e`) and explaining system error events in detail (`-x`).
* **`tail -f /var/log/syslog`** [[13:20](https://www.youtube.com/watch?v=LwcvrEQzg6o&t=800)]: Streams the latest entries of system logs in real-time.

---

### Step 7: Service Management & Configuration Checks

* **`systemctl status <service_name>`** [[13:50](https://www.youtube.com/watch?v=LwcvrEQzg6o&t=830)]: Checks operational status and active runtime logs of system services (e.g., `jenkins`).
* **`systemctl start <service_name>`** / **`systemctl restart <service_name>`**: Starts or restarts specific background services.

---

### Step 8: Advanced Debugging

* **`pstack <PID>`** [[14:39](https://www.youtube.com/watch?v=LwcvrEQzg6o&t=879)]: Prints the stack trace of a running process by its PID.
* **`strace`** [[14:39](https://www.youtube.com/watch?v=LwcvrEQzg6o&t=879)]: Intercepts and logs system calls executed by a process.
* **`lsof`** [[15:03](https://www.youtube.com/watch?v=LwcvrEQzg6o&t=903)]: Lists all open files and active network connections associated with running processes.
* **`tcpdump`** [[15:11](https://www.youtube.com/watch?v=LwcvrEQzg6o&t=911)]: Captures and analyzes network packets traversing network interfaces.
