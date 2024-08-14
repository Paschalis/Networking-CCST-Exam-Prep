# CCST Networking Exam Preparation

This repository provides resources and examples for preparing for the CCST Networking exam. It includes study notes, practice questions, Packet Tracer files, and network performance testing examples using `iperf3`.




<p align="center"><em>(click on them to expand)</em></p>

<ol style="line-height: 2;">
   
   <li><details>
   <summary><strong>Network Performance Testing with iperf3</strong></summary>
   
  `iperf3` is a tool for measuring network bandwidth. Below are some examples of how to use `iperf3` for various network performance tests.

  ## Basic Bandwidth Test

  **Situation:** You want to measure the maximum bandwidth between a client and a server on a local network.

  **On the server:**
  ```bash
  iperf3 -s
  ```

  **On the client:**
  ```bash
  iperf3 -c <server_ip>
  ```

  ## Bandwidth Test with Custom Time Interval

  **Situation:**  You need to measure bandwidth over a specific period.

  **On the server:**
  ```bash
  iperf3 -s
  ```

  **On the client:**
  ```bash
  iperf3 -c <server_ip> -t 60
  ```
  
  ## Test with Bandwidth Limiting

  **Situation:**  You want to simulate network conditions by limiting bandwidth.

  **On the server:**
  ```bash
  iperf3 -s
  ```

  **On the client:**
  ```bash
  iperf3 -c <server_ip> -b 10M
  ```

  ## TCP Bandwidth Test with Custom Port

  **Situation:** You need to measure TCP bandwidth on a specific port.

  **On the server:**
  ```bash
  iperf3 -s
  ```

  **On the client:**
  ```bash
  iperf3 -c <server_ip> -p 5001
  ```

  ## UDP Bandwidth Test with Custom Port

  **Situation:** You need to measure UDP bandwidth and observe packet loss.

  **On the server:**
  ```bash
  iperf3 -s -u
  ```

  **On the client:**
  ```bash
  iperf3 -c <server_ip> -u  -p 5201
  ```

  ## SCTP Bandwidth Test with Custom Port

  **On the server:**
  ```bash
  iperf3 -s -p 5001 -t 30 -i 10 --sctp
  ```

  **On the client:**
  ```bash
  iperf3 -c <server_ip> -p 5001 -t 30 -i 10 --sctp
  ```

  ## Testing with Zero-Copy Mode

  Situation: You want to test performance using the zero-copy mode for potentially improved throughput.

  **On the server:**
  ```bash
  iperf3 -s -Z
  ```

  **On the client:**
  ```bash
  iperf3 -c <server_ip> -Z
  ```

  ## Test with Different Window Size

  Situation: You want to test how changing the TCP window size affects performance.

  **On the server:**
  ```bash
  iperf3 -s
  ```

  **On the client:**
  ```bash
  iperf3 -c <server_ip> -w 64K
  ```

  ## Multi-Client Testing

  Situation: You want to test bandwidth from multiple clients simultaneously to see how the server handles concurrent connections.


  **On the server:**
  ```bash
  iperf3 -s
  ```

  **On the client:**
  ```bash
  iperf3 -c <server_ip> -P 5
  ```

  ## Reverse Test Mode

  Situation: You want the server to act as the client and the client to act as the server, often used to test the reverse path bandwidth.


  **On the server:**
  ```bash
  iperf3 -s
  ```

  **On the client:**
  ```bash
  iperf3 -c <server_ip> -R
  ```


  ## UDP Test with Custom Packet Size

  Situation: You need to test how different packet sizes affect performance.

  **On the server:**
  ```bash
  iperf3 -s -u
  ```

  **On the client:**
  ```bash
  iperf3 -c <server_ip> -u -l 1024
  ```

  ---
   </details></li>



   
   
   <li><details>
   <summary><strong>Network Protocols: FTP, SFTP, TFTP, NTP and ICMP</strong></summary>
   

  ## FTP (File Transfer Protocol)

  **Overview:**
  FTP is a standard network protocol used to transfer files between a client and a server over a network. It operates on TCP/IP and typically uses port 21 for control commands and port 20 for data transfer.

  **Basic Commands and Examples:**

  - **Starting the FTP Server:**
    - **On Linux:**
      ```bash
      sudo apt-get install vsftpd
      sudo systemctl start vsftpd
      ```
    - **On Windows:**
      Install and configure FileZilla Server.

  - **Connecting to an FTP Server:**
    - **From a command-line client:**
      ```bash
      ftp <server_ip>
      ```
      Enter username and password when prompted.

    - **Using FileZilla Client:**
      - Open FileZilla.
      - Enter the server IP, port 21, username, and password in the Quickconnect bar.

  - **Common Commands:**
    - **List Files:**
      ```bash
      ls
      ```
    - **Upload File:**
      ```bash
      put <local_file>
      ```
    - **Download File:**
      ```bash
      get <remote_file>
      ```

  **Configuration Example:**
  Ensure your server settings disallow anonymous logins and only allow authenticated users.

  ---

  ## SFTP (Secure File Transfer Protocol)

  **Overview:**
  SFTP is a secure protocol for transferring files over a network, using SSH (Secure Shell) to encrypt data and commands. It operates on port 22.

  **Basic Commands and Examples:**

  - **Setting Up SFTP on Linux:**
    - Install OpenSSH server:
      ```bash
      sudo apt-get install openssh-server
      ```
    - Start the SSH service:
      ```bash
      sudo systemctl start ssh
      ```

  - **Connecting to an SFTP Server:**
    - **From a command-line client:**
      ```bash
      sftp <username>@<server_ip>
      ```
      Enter the password when prompted.

    - **Using WinSCP (Windows):**
      - Open WinSCP.
      - Enter the server IP, port 22, username, and password.

  - **Common Commands:**
    - **Upload File:**
      ```bash
      put <local_file>
      ```
    - **Download File:**
      ```bash
      get <remote_file>
      ```

  **Configuration Example:**
  Ensure your `sshd_config` file allows SFTP and restricts users to their home directories for security.

  ---

  ## TFTP (Trivial File Transfer Protocol)

  **Overview:**
  TFTP is a simpler version of FTP used for transferring files with minimal overhead. It operates on UDP port 69 and is typically used for tasks like network booting.

  **Basic Commands and Examples:**

  - **Installing and Starting TFTP Server on Linux:**
    - Install `tftpd-hpa`:
      ```bash
      sudo apt-get install tftpd-hpa
      ```
    - Edit the configuration file `/etc/default/tftpd-hpa` to set the directory and options.
    - Start the TFTP service:
      ```bash
      sudo systemctl start tftpd-hpa
      ```

  - **Connecting to a TFTP Server:**
    - **From a command-line client:**
      ```bash
      tftp <server_ip>
      ```

  - **Common Commands:**
    - **Upload File:**
      ```bash
      put <local_file>
      ```
    - **Download File:**
      ```bash
      get <remote_file>
      ```

  **Configuration Example:**
  Configure the TFTP server to restrict access to a specific directory and ensure that it has read/write permissions.

  ---

  ## NTP (Network Time Protocol)

  **Overview:**
  NTP is used to synchronize the clocks of computers over a network. It operates on UDP port 123 and ensures that time is consistent across all devices.

  **Basic Commands and Examples:**

  - **Installing and Configuring NTP Server on Linux:**
    - Install `ntp`:
      ```bash
      sudo apt-get install ntp
      ```
    - Configure `/etc/ntp.conf` to set up NTP servers and access restrictions.
    - Start the NTP service:
      ```bash
      sudo systemctl start ntp
      ```

  - **Synchronizing Time with an NTP Server:**
    - **On a Linux client:**
      ```bash
      sudo ntpdate <server_ip>
      ```
    - **On a Windows client:**
      - Go to **Date and Time Settings**.
      - Select **Add clocks for different time zones** and **Internet Time** tab to synchronize.

  **Configuration Example:**
  Ensure that your NTP server configuration allows for accurate time synchronization and restricts access to trusted clients only.

  ---
## ICMP (Internet Control Message Protocol)

**Overview:**
ICMP is used for sending error messages and operational information about network conditions. It operates alongside IP and is crucial for network diagnostics and troubleshooting.

**Basic Commands and Examples:**

### `ping`

The `ping` command checks the reachability of a host on a network and measures round-trip time.

- **Basic Usage:**
  - **Linux/Windows:**
    ```bash
    ping <host_or_ip>
    ```
  - Example:
    ```bash
    ping google.com
    ```

- **Specify Number of Packets (Linux):**
  - **Linux:**
    ```bash
    ping -c 5 <host_or_ip>
    ```
  - Example:
    ```bash
    ping -c 5 google.com
    ```
  - This sends 5 packets and then stops.

- **Specify Packet Size (Linux/Windows):**
  - **Linux:**
    ```bash
    ping -s 1000 <host_or_ip>
    ```
  - **Windows:**
    ```cmd
    ping -l 1000 <host_or_ip>
    ```
  - Example:
    ```bash
    ping -s 1000 google.com
    ```

- **Specify Time To Live (TTL) (Linux):**
  - **Linux:**
    ```bash
    ping -t 64 <host_or_ip>
    ```
  - Example:
    ```bash
    ping -t 64 google.com
    ```

- **Flood Ping (Linux):**
  - **Linux:**
    ```bash
    ping -f <host_or_ip>
    ```
  - Example:
    ```bash
    ping -f google.com
    ```
  - This sends packets as fast as possible (use with caution).

### `traceroute` (Linux) / `tracert` (Windows)

The `traceroute` command (Linux) and `tracert` command (Windows) trace the path packets take to a destination, showing each hop along the way.

- **Basic Usage:**
  - **Linux:**
    ```bash
    traceroute <host_or_ip>
    ```
  - **Windows:**
    ```cmd
    tracert <host_or_ip>
    ```
  - Example:
    ```bash
    traceroute google.com
    ```
  - Example:
    ```cmd
    tracert google.com
    ```

- **Specify Maximum Number of Hops:**
  - **Linux:**
    ```bash
    traceroute -m 20 <host_or_ip>
    ```
  - **Windows:**
    ```cmd
    tracert -h 20 <host_or_ip>
    ```
  - Example:
    ```bash
    traceroute -m 20 google.com
    ```
  - Example:
    ```cmd
    tracert -h 20 google.com
    ```

- **Show Numeric IP Addresses Only:**
  - **Linux:**
    ```bash
    traceroute -n <host_or_ip>
    ```
  - **Windows:**
    ```cmd
    tracert -d <host_or_ip>
    ```
  - Example:
    ```bash
    traceroute -n google.com
    ```
  - Example:
    ```cmd
    tracert -d google.com
    ```

- **Use a Specific Network Interface (Linux):**
  - **Linux:**
    ```bash
    traceroute -i <interface> <host_or_ip>
    ```
  - Example:
    ```bash
    traceroute -i eth0 google.com
    ```

- **Change the Default Packet Size (Linux):**
  - **Linux:**
    ```bash
    traceroute -s 1000 <host_or_ip>
    ```
  - Example:
    ```bash
    traceroute -s 1000 google.com
    ```


   </details></li>


   

