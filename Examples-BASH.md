[[Hands-on Example]]
## 1. Overview of Operating Systems

### **Introduction to Operating Systems**

**Explanation:**
An operating system (OS) is software that manages computer hardware and software resources, providing services for computer programs. Key functions include managing processes, memory, storage, and providing a user interface.

### **Operating-System Structures**

**Explanation:**
Operating systems can be structured in various ways, such as monolithic kernels, microkernels, and modular architectures. Understanding these structures helps in comprehending how different components interact within the OS.

**Example:**
- **Monolithic Kernel vs. Microkernel:**
  - **Monolithic Kernel:** All OS services run in kernel space. Example: Linux.
  - **Microkernel:** Minimal kernel with services running in user space. Example: MINIX.

### **Linux Basic Commands**

**Explanation:**
Bash provides a powerful interface to interact with the Linux OS. Mastering basic commands is essential for efficient navigation and management.

**Examples:**
- **Navigating the File System:**
  ```bash
  pwd          # Print working directory
  ls -la       # List all files with detailed information
  cd /path/to/directory  # Change directory
  ```
- **File Operations:**
  ```bash
  cp source.txt destination.txt   # Copy files
  mv oldname.txt newname.txt      # Move/Rename files
  rm unwanted.txt                 # Remove files
  mkdir new_directory             # Create a new directory
  ```

### **Command-Line Interface (Shell)**

**Explanation:**
The shell is a command-line interpreter that provides a user interface for accessing the OS services. Bash (Bourne Again Shell) is one of the most popular shells in Linux.

**Example:**
- **Customizing the Bash Prompt:**
  ```bash
  export PS1="\u@\h \w\$ "   # Sets the prompt to user@host current_directory$
  ```
- **Basic Shell Scripting:**
  ```bash
  #!/bin/bash
  echo "Hello, World!"
  ```
  Save the above in a file `hello.sh`, make it executable with `chmod +x hello.sh`, and run it using `./hello.sh`.

---

## 2. Process Management

### **Processes and Threads**

**Explanation:**
A process is an instance of a running program. Threads are smaller units of a process that can run concurrently. Understanding processes and threads is crucial for managing applications and system resources.

### **Synchronization, Algorithms, and Deadlocks**

**Explanation:**
Synchronization ensures that multiple threads or processes can operate concurrently without conflicts. Deadlocks occur when processes are waiting indefinitely for resources.

### **Process Management System Calls in Linux**

**Explanation:**
System calls like `fork()`, `exec()`, and `wait()` are fundamental for creating and managing processes in Linux.

### **Bash Examples:**

- **Listing Processes:**
  ```bash
  ps aux        # Displays all running processes
  top           # Interactive process viewer
  ```
- **Managing Processes:**
  ```bash
  kill PID      # Terminate a process with the given PID
  pkill process_name  # Terminate processes by name
  ```
- **Background and Foreground Processes:**
  ```bash
  sleep 100 &   # Run sleep command in the background
  fg            # Bring the most recent background job to the foreground
  bg            # Resume a suspended job in the background
  ```
- **Creating a Simple Script to Manage Processes:**
  ```bash
  #!/bin/bash
  echo "Starting a background process..."
  sleep 300 &
  PID=$!
  echo "Process ID: $PID"
  echo "Killing the process..."
  kill $PID
  ```
  Save as `manage_process.sh`, make executable, and run to see process management in action.

---

## 3. CPU Scheduling

### **Scheduling Algorithms**

**Explanation:**
CPU scheduling algorithms determine the order in which processes access the CPU. Common algorithms include First-Come-First-Served (FCFS), Shortest Job Next (SJN), Round Robin (RR), and Priority Scheduling.

### **Scheduling in Linux**

**Explanation:**
Linux uses the Completely Fair Scheduler (CFS) by default, which aims to allocate CPU time fairly among all processes.

### **Bash Examples:**

- **Checking Process Priority:**
  ```bash
  ps -eo pid,comm,pri,ni  # Displays PID, command, priority, and nice value
  ```
- **Changing Process Priority:**
  ```bash
  renice -n 10 -p 1234    # Change the nice value of PID 1234 to 10
  ```
- **Understanding Scheduling Policies:**
  ```bash
  chrt -p 1234            # Display the scheduling policy and priority of PID 1234
  chrt -r -p 20 1234      # Set the scheduling policy to Round Robin with priority 20 for PID 1234
  ```
- **Example Script to Monitor CPU Usage:**
  ```bash
  #!/bin/bash
  while true; do
      clear
      echo "CPU Usage:"
      top -bn1 | grep "Cpu(s)"
      sleep 2
  done
  ```
  This script continuously monitors and displays CPU usage, reflecting how scheduling affects CPU allocation.

---

## 4. Memory Management

### **Main Memory and Virtual Memory**

**Explanation:**
Main memory (RAM) is the primary storage for active processes. Virtual memory allows the OS to use disk storage to extend apparent memory, enabling larger applications to run.

### **Page Replacement Algorithms**

**Explanation:**
When physical memory is full, the OS must decide which memory pages to swap out. Common algorithms include Least Recently Used (LRU), First-In-First-Out (FIFO), and Optimal.

### **Segmentation**

**Explanation:**
Segmentation divides memory into different segments based on logical divisions like code, data, and stack, allowing for more flexible memory management.

### **Memory Management System Calls in Linux**

**Explanation:**
System calls like `mmap()`, `munmap()`, `brk()`, and `sbrk()` are used for memory management in Linux.

### **Bash Examples:**

- **Monitoring Memory Usage:**
  ```bash
  free -h         # Displays memory usage in human-readable format
  vmstat 1        # Reports virtual memory statistics every second
  ```
- **Using `top` and `htop`:**
  ```bash
  top             # Interactive process viewer with memory stats
  htop            # Enhanced version of top (if installed)
  ```
- **Swapping Memory:**
  ```bash
  sudo swapon --show         # Show current swap spaces
  sudo swapoff /swapfile     # Disable a swap file
  sudo swapon /swapfile      # Enable a swap file
  ```
- **Example Script to Check Memory and Alert:**
  ```bash
  #!/bin/bash
  THRESHOLD=80
  while true; do
      USED=$(free | grep Mem | awk '{print $3/$2 * 100.0}')
      USED_INT=${USED%.*}
      if [ "$USED_INT" -gt "$THRESHOLD" ]; then
          echo "Memory usage is above $THRESHOLD%!"
      fi
      sleep 60
  done
  ```
  This script checks memory usage every minute and alerts if usage exceeds 80%.

---

## 5. Storage Management

### **Storage Structure**

**Explanation:**
Storage structure refers to how data is organized on storage devices. This includes file systems, directories, and data blocks.

### **File-System Interface**

**Explanation:**
The file-system interface allows users and programs to interact with files and directories through operations like reading, writing, and modifying.

### **File-System Implementation and Management**

**Explanation:**
File systems manage how data is stored, retrieved, and maintained on storage devices. Examples include ext4, XFS, and Btrfs in Linux.

### **I/O Systems**

**Explanation:**
I/O systems handle input and output operations between the computer and peripheral devices, ensuring efficient data transfer and device management.

### **Filesystem and I/O System Calls in Linux**

**Explanation:**
System calls like `open()`, `read()`, `write()`, `close()`, `mkdir()`, and `rmdir()` are fundamental for file and I/O operations in Linux.

### **Bash Examples:**

- **Navigating and Managing the File System:**
  ```bash
  ls -lh          # List files with human-readable sizes
  tree            # Display directory tree (if installed)
  du -sh /path    # Show disk usage of a directory
  ```
- **File Operations:**
  ```bash
  cp source.txt /destination/path/
  mv file.txt /new/location/
  rm -r directory/  # Remove a directory recursively
  ```
- **Disk Management:**
  ```bash
  df -h           # Display disk space usage
  fdisk -l        # List disk partitions (requires sudo)
  mount /dev/sdb1 /mnt/usb  # Mount a USB drive to /mnt/usb
  ```
- **Example Script to Backup a Directory:**
  ```bash
  #!/bin/bash
  SOURCE_DIR="/home/user/data"
  BACKUP_DIR="/home/user/backup"
  TIMESTAMP=$(date +"%Y%m%d_%H%M%S")
  tar -czf "$BACKUP_DIR/data_backup_$TIMESTAMP.tar.gz" "$SOURCE_DIR"
  echo "Backup completed at $TIMESTAMP"
  ```
  This script creates a compressed backup of the specified directory with a timestamp.

---

## 6. Advanced Topics

### **Protection and Security**

**Explanation:**
Protection mechanisms ensure that system resources are accessed only by authorized entities. Security involves safeguarding the system against threats and vulnerabilities.

### **Virtual Machines and Distributed Systems**

**Explanation:**
Virtual machines allow multiple OS instances to run on a single physical machine, providing isolation and efficient resource usage. Distributed systems consist of multiple interconnected computers that work together, enhancing performance and reliability.

### **Bash Examples:**

- **File Permissions and Ownership:**
  ```bash
  ls -l           # List files with permissions
  chmod 755 script.sh  # Change permissions of a script
  chown user:group file.txt  # Change ownership of a file
  ```
- **Secure Shell (SSH) Operations:**
  ```bash
  ssh user@remote_host    # Connect to a remote host via SSH
  scp file.txt user@remote_host:/path/  # Securely copy files to a remote host
  ```
- **Using `iptables` for Basic Firewall Configuration:**
  ```bash
  sudo iptables -L       # List current firewall rules
  sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT  # Allow SSH
  sudo iptables -A INPUT -j DROP   # Drop all other incoming traffic
  ```
- **Managing Virtual Machines with `VirtualBox` and `VBoxManage`:**
  ```bash
  VBoxManage list vms                     # List all VMs
  VBoxManage startvm "VM_Name" --type headless  # Start a VM in headless mode
  VBoxManage controlvm "VM_Name" poweroff  # Stop a VM
  ```
- **Working with Docker Containers (as an example of virtualization):**
  ```bash
  docker run -it ubuntu bash           # Run an Ubuntu container
  docker ps                            # List running containers
  docker stop container_id              # Stop a running container
  ```
- **Distributed Systems Example: Setting Up a Simple SSH Cluster Script:**
  ```bash
  #!/bin/bash
  SERVERS=("server1" "server2" "server3")
  for SERVER in "${SERVERS[@]}"; do
      ssh user@$SERVER 'uptime' &
  done
  wait
  echo "All servers have been queried."
  ```
  This script connects to multiple servers concurrently to retrieve their uptime, demonstrating basic distributed operations.

---

## **Additional Resources and Assignments**

To reinforce the concepts covered, consider the following assignments and resources:

### **Assignments:**
1. **Basic Command Line Tasks:**
   - Navigate directories, manipulate files, and use text processing commands (`grep`, `awk`, `sed`).

2. **Process Management Script:**
   - Create a script that monitors specific processes and restarts them if they are not running.

3. **Scheduling and Priority Assignment:**
   - Experiment with changing process priorities and observe the impact on system performance using `top`.

4. **Memory Monitoring Tool:**
   - Develop a Bash script that logs memory usage over time and alerts when usage exceeds a threshold.

5. **File Backup and Restoration:**
   - Write scripts to automate backing up important directories and restoring them from backups.

6. **Security Configuration:**
   - Set up basic firewall rules using `iptables` and secure SSH access with key-based authentication.

7. **Virtual Machine Management:**
   - Use `VBoxManage` or Docker to create, manage, and automate virtual environments.

### **Resources:**
 **Online Tutorials:**
- https://www.gnu.org/software/bash/manual/

- https://www.freecodecamp.org/news/bash-scripting-tutorial-linux-shell-script-and-command-line-for-beginners/

- https://linuxconfig.org/bash-scripting-tutorial-for-beginners

- https://github.com/herbertech/bash-intro-tutorial

- https://hpc.nmsu.edu/onboarding/linux/bash-script/

- https://github.com/PacktPublishing/Complete-Bash-Shell-Scripting-

