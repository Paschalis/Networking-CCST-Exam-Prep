# CCST Networking Exam Preparation

This repository provides resources and examples for preparing for the CCST Networking exam. It includes study notes, practice questions, Packet Tracer files, and network performance testing examples using `iperf3`.

## Network Performance Testing with iperf3

`iperf3` is a tool for measuring network bandwidth. Below are some examples of how to use `iperf3` for various network performance tests.

### Basic Bandwidth Test

**Situation:** You want to measure the maximum bandwidth between a client and a server on a local network.

**On the server:**
```bash
iperf3 -s
```

**On the client:**
```bash
iperf3 -c <server_ip>
```

### Bandwidth Test with Custom Time Interval

**Situation:**  You need to measure bandwidth over a specific period.

**On the server:**
```bash
iperf3 -s
```

**On the client:**
```bash
iperf3 -c <server_ip> -t 60
```
 
### Test with Bandwidth Limiting

**Situation:**  You want to simulate network conditions by limiting bandwidth.

**On the server:**
```bash
iperf3 -s
```

**On the client:**
```bash
iperf3 -c <server_ip> -b 10M
```

### TCP Bandwidth Test with Custom Port

**Situation:** You need to measure TCP bandwidth on a specific port.

**On the server:**
```bash
iperf3 -s
```

**On the client:**
```bash
iperf3 -c <server_ip> -p 5001
```

### UDP Bandwidth Test with Custom Port

**Situation:** You need to measure UDP bandwidth and observe packet loss.

**On the server:**
```bash
iperf3 -s -u
```

**On the client:**
```bash
iperf3 -c <server_ip> -u  -p 5201
```

### SCTP Bandwidth Test with Custom Port

**On the server:**
```bash
iperf3 -s -p 5001 -t 30 -i 10 --sctp
```

**On the client:**
```bash
iperf3 -c <server_ip> -p 5001 -t 30 -i 10 --sctp
```

### Testing with Zero-Copy Mode

Situation: You want to test performance using the zero-copy mode for potentially improved throughput.

**On the server:**
```bash
iperf3 -s -Z
```

**On the client:**
```bash
iperf3 -c <server_ip> -Z
```

### Test with Different Window Size

Situation: You want to test how changing the TCP window size affects performance.

**On the server:**
```bash
iperf3 -s
```

**On the client:**
```bash
iperf3 -c <server_ip> -w 64K
```

### Multi-Client Testing

Situation: You want to test bandwidth from multiple clients simultaneously to see how the server handles concurrent connections.


**On the server:**
```bash
iperf3 -s
```

**On the client:**
```bash
iperf3 -c <server_ip> -P 5
```

### Reverse Test Mode

Situation: You want the server to act as the client and the client to act as the server, often used to test the reverse path bandwidth.


**On the server:**
```bash
iperf3 -s
```

**On the client:**
```bash
iperf3 -c <server_ip> -R
```


### UDP Test with Custom Packet Size

Situation: You need to test how different packet sizes affect performance.

**On the server:**
```bash
iperf3 -s -u
```

**On the client:**
```bash
iperf3 -c <server_ip> -u -l 1024
```


















