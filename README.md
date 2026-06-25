# UDP Broadcast Messaging System

A simple Python-based UDP Broadcast Messaging System that allows a host device to send broadcast messages to all devices connected on the same Local Area Network (LAN).

This project demonstrates practical networking concepts such as UDP communication, socket programming, network broadcasting, and message logging. It was developed and tested using Kali Linux and Windows systems connected to the same network.

---

## Project Overview

The objective of this project is to broadcast messages from a sender device to multiple receiver devices connected to the same network.

The sender transmits a UDP broadcast packet, and all devices running the receiver application can receive and display the message along with the sender's IP address and timestamp.

### Key Features

* UDP Broadcast Communication
* Cross-platform support (Linux and Windows)
* Real-time message delivery
* Sender IP identification
* Date and Time logging
* Simple and lightweight implementation using Python sockets

---

## Technologies Used

* Python 3
* Socket Programming
* UDP Protocol
* Kali Linux
* Windows Command Prompt

---

## Project Structure

```text
BroadcastProject/
│
├── broadcaster.py      # Sends broadcast messages
├── listener.py         # Receives broadcast messages
├── logs.txt            # Optional log file
└── README.md
```

---

## Network Architecture

```text
                    +----------------+
                    | Sender Device  |
                    |  (Kali Linux)  |
                    +--------+-------+
                             |
                             |
                   UDP Broadcast Message
                             |
       ------------------------------------------------
       |                                              |
       |                                              |
+------+-------+                            +---------+------+
| Receiver 1   |                            | Receiver 2     |
| Kali Linux   |                            | Windows 10     |
+--------------+                            +----------------+
```

---

## Sender Code

The sender broadcasts a message to all devices on the network using UDP.

```python
import socket

PORT = 5000

message = input("Enter message: ")

sock = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

sock.setsockopt(
    socket.SOL_SOCKET,
    socket.SO_BROADCAST,
    1
)

sock.sendto(
    message.encode(),
    ('255.255.255.255', PORT)
)

print("Broadcast sent")
```

---

## Receiver Code

The receiver listens on UDP port 5000 and displays incoming messages with timestamps.

```python
import socket
from datetime import datetime

HOST = ''
PORT = 5000

sock = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
sock.bind((HOST, PORT))

print("Listening on port 5000...")

while True:
    data, addr = sock.recvfrom(1024)

    timestamp = datetime.now().strftime("%d-%m-%Y %H:%M:%S")

    print("\n------------------------")
    print(f"Date & Time : {timestamp}")
    print(f"Sender      : {addr[0]}")
    print(f"Message     : {data.decode()}")
    print("------------------------")
```

---

## How to Run

### Step 1: Start the Receiver

On the receiving device:

```bash
python listener.py
```

Expected output:

```text
Listening on port 5000...
```

---

### Step 2: Send a Broadcast Message

On the sender device:

```bash
python broadcaster.py
```

Enter a message:

```text
Enter message: Hello Network
```

Output:

```text
Broadcast sent
```

---

### Step 3: Receive the Message

Receiver output:

```text
Date & Time : 24-06-2026 22:28:15

Sender      : 10.212.40.215
Message     : Hello! How are you? This message is to test message broadcast!
```

---

## Screenshots

### Sender Device (Kali Linux)

Shows execution of `broadcaster.py` and successful broadcast transmission.

### Receiver Device (Kali Linux)

Shows incoming messages received through UDP broadcast communication.

### Receiver Device (Windows)

Shows successful reception of messages along with sender IP address and timestamp.

---

## Learning Outcomes

This project helped in understanding:

* UDP Communication
* Socket Programming
* Network Broadcasting
* IP Addressing
* Cross-platform Communication
* Basic Cybersecurity Networking Concepts

---

## Future Enhancements

* Private messaging using TCP
* Device discovery
* Message encryption
* Authentication system
* GUI-based interface
* Message history storage
* Multi-user chat support

---

## Author

Developed as a Networking and Cybersecurity Learning Project using Python Socket Programming.
