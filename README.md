# Ex.No:1a  			Study of Socket Programming

## Aim: 
To implement  the concept  of  Socket Programming
## Introduction:
Introduction to Socket Programming

Socket programming is a method used in computer networks to enable communication between two devices (processes) over a network using endpoints called sockets.

🔹 Definition

A socket is an endpoint for sending and receiving data across a network. Socket programming allows a client-server architecture, where:

The server waits for requests
The client initiates communication
🔹 Key Concept

Socket programming uses protocols like:

TCP (Transmission Control Protocol) → Reliable, connection-oriented
UDP (User Datagram Protocol) → Faster, connectionless
## Understanding Socket Programming:
	Socket programming involves the use of sockets, which serve as endpoints for communication. A socket is identified by an IP address and a port number, and it facilitates data transfer between a client and a server. The two main types of sockets are Stream Sockets, which provide a reliable, connection-oriented communication, and Datagram Sockets, which are connectionless and suitable for scenarios where reliability is less critical.
## Key Concepts in Socket Programming:
1.Sockets
•	A socket is a software representation of a communication endpoint in a network.
•	It is identified by an IP address and a port number.
•	Sockets can be classified into two main types: Stream Sockets and Datagram Sockets.
•	Stream Sockets provide a reliable, connection-oriented communication, while Datagram Sockets are connectionless and operate in a best-effort mode.

2. Client-Server Model

•	Socket programming typically follows the client-server model.
•	The server listens for incoming connections from clients, while clients initiate connections to the server.
•	Servers are passive, waiting for connection requests, and clients are active, initiating communication.

3, TCP/IP Protocol:

TCP/IP Protocol

TCP/IP (Transmission Control Protocol / Internet Protocol) is the fundamental communication protocol suite used for data transmission over networks, including the Internet.

🔹 Definition

TCP/IP is a set of protocols that define how data is sent, received, addressed, and routed between computers in a network.

🔹 Main Components
TCP (Transmission Control Protocol)
Provides reliable, connection-oriented communication
Ensures:
Data is delivered without errors
Packets are in order
Lost data is retransmitted
IP (Internet Protocol)
Handles addressing and routing of packets
Uses IP addresses (e.g., 192.168.1.1) to identify devices
Delivers packets using a best-effort (unreliable) method

4.Basic Socket Functions:

•	Socket programming involves a set of functions provided by the operating system or programming language to create, bind, listen, accept, connect, send, and receive data through sockets.
•	Examples of functions include socket(), bind(), listen(), accept(), connect(), send(), and recv().

## Server-Side Operations:

•	Servers create a socket using socket() and bind it to a specific IP address and port using bind().
•	They then listen for incoming connections with listen() and accept connections with accept().
•	Once a connection is establi
•	shed, servers can send and receive data using send() and recv().

## Client –Server Operations

Clients create a socket using socket() and connect to a server using connect().
After establishing a connection, clients can send and receive data using send() and recv().

## Use Cases of Socket Programming:
Socket programming finds applications in various domains, including web development, file transfer protocols, online gaming, and real-time communication. It is the foundation for protocols like HTTP, FTP, and SMTP, which power the internet. Socket programming enables the development of both server and client applications, facilitating the exchange of information between devices in a networked environment.

## PROGRAMMING:
```
import socket
import threading
import time

HOST = "127.0.0.1"
PORT = 5002


# -------------------- SERVER --------------------
def server():
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

    # Allow reuse of same port
    s.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)

    s.bind((HOST, PORT))
    s.listen(1)

    print("Server is waiting for connection...")

    conn, addr = s.accept()
    print("Connected by:", addr)

    count = 0

    while count < 3:
        data = conn.recv(1024).decode()

        if not data:
            print("Client disconnected.")
            break

        print("Client says:", data)

        reply = input("Server reply: ")
        conn.send(reply.encode())

        count += 1

    print("Server is ending...")

    conn.send("Server is end.".encode())

    conn.close()
    s.close()


# -------------------- CLIENT --------------------
def client():
    time.sleep(1)  # Wait for server to start

    c = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

    # Retry connection until server is ready
    while True:
        try:
            c.connect((HOST, PORT))
            print("Client connected to server.")
            break
        except ConnectionRefusedError:
            print("Waiting for server...")
            time.sleep(1)

    while True:
        message = input("Client message: ")
        c.send(message.encode())

        response = c.recv(1024).decode()

        if response.lower() == "server is end.":
            print(response)
            break

        print("Server says:", response)

    c.close()


# -------------------- THREADS --------------------
server_thread = threading.Thread(target=server)
client_thread = threading.Thread(target=client)

server_thread.start()
client_thread.start()

server_thread.join()
client_thread.join()

print("Chat closed successfully.")


```

## OUTPUT IMAGE:
<img width="1916" height="1076" alt="image" src="https://github.com/user-attachments/assets/49660f98-50b9-4ece-a656-9818a5a919b8" />


## Example Use Cases:

1.	Web servers: Web servers use socket programming to handle incoming HTTP requests from clients, serving web pages and content.
2.	Chat Application: Instant messaging and chat applications use sockets to enable real-time communication between users.
3.	File Transfer Protocol: Protocols like FTP (File Transfer Protocol) utilize socket programming for transferring files between a client and a server.
4.	Networked Games: Online multiplayer games rely on socket programming to facilitate communication between game clients and servers.
5.	RPC mechanisms: which allow processes to execute code on a remote server, often use socket programming for communication.


## Result:
Thus the study of Socket Programming Completed Successfully
