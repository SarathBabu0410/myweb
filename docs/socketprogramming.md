
# Socket programming
Socket programming is a fundamental concept in network communication that enables the exchange of data between two entities over a network. Sockets provide a standard mechanism for processes running on different devices to communicate seamlessly. In socket programming, a socket represents an endpoint for sending or receiving data across a computer network.

## Key concepts in socket programming:

* Server and Client:

    The server is a program or device that provides services or resources.
    The client is a program or device that requests services or resources from the server.

* Socket Creation:

    Sockets are created using programming interfaces, such as the Berkeley Sockets API in Unix-like systems.
    A server creates a socket to listen for incoming connections, while a client creates a socket to initiate a connection to the server.

* Socket Binding:

    The server binds its socket to a specific address and port to listen for incoming connections.
    The client specifies the server's address and port when connecting.

* Connection Establishment:

    The server listens for incoming connections, and the client initiates a connection request.
    Once a connection is established, data can be exchanged between the server and client.

* Data Transfer:

    Data is transferred between the server and client using methods like send() and recv() in programming languages like Python or C.
    Sockets provide a bi-directional communication channel for data exchange.

* Socket Closing:

    Sockets are closed after data transfer is complete or when the connection is no longer needed.
    Proper socket closure ensures the release of resources and termination of the connection.

Socket programming is widely used in various applications, including web development, network protocols, and distributed systems. It provides a flexible and efficient way for applications to communicate and share information across a network.

## UDP socket client-server program in Python
### UDP Server

``` bash   
import socket

# Define server address and port
server_address = ('localhost', 12345)

# Create a UDP socket
server_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

# Bind the socket to the server address
server_socket.bind(server_address)

print(f"Server listening on {server_address}")

while True:
    # Receive data from the client
    data, client_address = server_socket.recvfrom(1024)
    print(f"Received message from {client_address}: {data.decode()}")

    # Echo the message back to the client
    server_socket.sendto(data, client_address)
```

### UDP Client
``` bash
import socket

# Define server address and port
server_address = ('localhost', 12345)

# Create a UDP socket
client_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

while True:
    # Get user input
    message = input("Enter message to send to server (type 'exit' to quit): ")

    if message.lower() == 'exit':
        break

    # Send the message to the server
    client_socket.sendto(message.encode(), server_address)

    # Receive the echoed message from the server
    data, _ = client_socket.recvfrom(1024)
    print(f"Received echoed message: {data.decode()}")

# Close the socket
client_socket.close()
```



# How to achieve parallelism



## Python thread
Python, a thread is a lightweight, independent sequence of instructions that can run concurrently with other threads within the same process. Threads enable concurrent execution, allowing tasks to progress simultaneously and make efficient use of resources. Python provides a built-in threading module, which facilitates the creation, management, and synchronization of threads.

### Reading exercise

[threading — Thread-based parallelismThread](https://docs.python.org/3/library/threading.html)

## Example
``` bash
def sender():
# HELLO MESSAGE SENDER THREAD
    while True:
        sock = socket.socket(socket.AF_INET, socket.SOCK_DGRAM, socket.IPPROTO_UDP)
        sock.setsockopt(socket.IPPROTO_IP, socket.IP_MULTICAST_TTL, 2)
        sock.setsockopt(socket.SOL_SOCKET,socket.SO_BROADCAST,1)
        message="HELLO|"
        encmessage=message.encode()
        sock.sendto(encmessage, ('192.168.1.255', 3400))
        time.sleep(0.8)

def receiver ():
# HELLO MESSAGE RECEIVER FUNCTION THREAD
    UDP_IP = ""
    UDP_PORT = 3400
    sock = socket.socket(socket.AF_INET,socket.SOCK_DGRAM) # UDP
    sock.bind((UDP_IP, UDP_PORT))
    while True:
        data, addr = sock.recvfrom(1024) 
        data=data.decode()
        print(data)

fList=list()
fList.append(receiver)
fList.append(sender)

for funct in fList:
    th=Thread(target=funct)
    th.setDaemon(True)
    th.start()
```