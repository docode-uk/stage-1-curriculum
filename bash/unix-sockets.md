# UNIX Sockets

## Introduction
Applications require a way to communicate with eachother: for example, a web app needs to get a list of users from a database, or a messaging app needs to send a message to a friend. This process is known as "Inter-Process Communication" (IPC), and this can be achieved in many ways.

One could implement IPC by saving a message to a file, and having another file/user read from it. This would be slow, insecure, and have issues when more than one person tries to write to the file at the same time.

Another way would be to use [pipes](https://man7.org/linux/man-pages/man2/pipe.2.html) or [named pipes/FIFOs](https://man7.org/linux/man-pages/man7/fifo.7.html) to communicate between processes. These are obviously faster, but are also unidirectional and the input/output can only be consumed by one process at a time.

[Shared Memory (SHM)](https://man7.org/linux/man-pages/man7/shm_overview.7.html) offers another way to communicate between processes, but it is more complex to implement and manage - and can add security risks.

[UNIX Sockets](https://man7.org/linux/man-pages/man7/unix.7.html) offer a convenient way to communicate _bidirectionally_ between processes, and can be setup with added security features - and are the UNIX standard for IPC.


## Types of UNIX Sockets

Unix sockets (known by the Address Family `AF_UNIX` or `AF_LOCAL`) are identified by a file path. As a Unix convention, most sockets are created in the `/var/run` directory, but can live anywhere on the filesystem.

There are two types of Unix sockets: `stream` and `datagram` - these streams are not exclusive to Unix sockets, and you will find them not just with Unix sockets, but also with the standard IP addresses (part of the family `AF_INET` - i.e. IPv4 addresses); you might already know the implementation of Transmission Control Protocol (TCP) for streams, and User Datagram Protocol (UDP) for datagrams - but this chapter is focused on Unix sockets only.

All the transfer of data occurrs within the kernel - no data reaches the network stack.

### Streams

Steams are also known as **connection based** sockets: this means that each peer in a connection (i.e. a server or client) is aware that a connection has been made, and that message has been received by the other party. With this one can send a continue _stream_ (of an arbritary length) of bytes. This is very useful where a guarantee that a message has been successfully sent: like an email for example.

### Datagrams

Datagrams are also known as **connection-less** sockets: i.e. the other party never knows if the other has left. A datagram is a discrete message with boundaries - there is a beginning, body, and end to each one.

A nice analogy I have stolen from [this Stackoverflow response](https://stackoverflow.com/a/4688899) makes it a lot easier to visualise:

> A stream socket is like a phone call -- one side places the call, the other answers, you say hello to each other (SYN/ACK in TCP), and then you exchange information. Once you are done, you say goodbye (FIN/ACK in TCP). If one side doesn't hear a goodbye, they will usually call the other back since this is an unexpected event; usually the client will reconnect to the server. There is a guarantee that data will not arrive in a different order than you sent it, and there is a reasonable guarantee that data will not be damaged.

> A datagram socket is like passing a note in class. Consider the case where you are not directly next to the person you are passing the note to; the note will travel from person to person. It may not reach its destination, and it may be modified by the time it gets there. If you pass two notes to the same person, they may arrive in an order you didn't intend, since the route the notes take through the classroom may not be the same, one person might not pass a note as fast as another, etc.

> So you use a stream socket when having information in order and intact is important. File transfer protocols are a good example here. You don't want to download some file with its contents randomly shuffled around and damaged!

**Note well**: An important distinction to make with Unix datagram packets (compared to _network sockets_) is that the order of the packets are guaranteed, and the order will remain the same - but the analogy still holds!

## An example
We can create a quick example of how this works using python; although any language (including `ba/sh`) would be more than suffice here, although python has some advantages we can get into later (specifically - looking at contexts)!

```python
# server.py
import socket

with socket.socket(socket.AF_UNIX, socket.SOCK_STREAM) as sock:
    sock.bind("/tmp/docode.sock")
    sock.listen()
    conn, address = sock.accept()
    with conn:
        while True:
            data = conn.recv(1024)
            print(f"Got connection with message: {data}")
            if not data:
                break
            conn.sendall(data)
```

```python
# client.py
import socket

with socket.socket(socket.AF_UNIX, socket.SOCK_STREAM) as sock:
    sock.connect("/tmp/docode.sock")
    sock.sendall(b"Hello, docode!")
    data = sock.recv(1024)

print(f"Received {data!r}")
```



----
## Questions