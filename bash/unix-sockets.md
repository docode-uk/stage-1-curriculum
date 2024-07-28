# UNIX Sockets

## Introduction
Applications require a way to communicate with eachother: for example, a web app needs to get a list of users from a database, or a messaging app needs to send a message to a friend. This process is known as "Inter-Process Communication" (IPC), and this can be achieved in many ways.

One could implement IPC by saving a message to a file, and having another file/user read from it. This would be slow, insecure, and have issues when more than one person tries to write to the file at the same time.

Another way would be to use [pipes](https://man7.org/linux/man-pages/man2/pipe.2.html) or [named pipes/FIFOs](https://man7.org/linux/man-pages/man7/fifo.7.html) to communicate between processes. These are obviously faster, but are also unidirectional and the input/output can only be consumed by one process at a time.

[Shared Memory (SHM)](https://man7.org/linux/man-pages/man7/shm_overview.7.html) offers another way to communicate between processes, but it is more complex to implement and manage - and can add security risks.

[UNIX Sockets](https://man7.org/linux/man-pages/man7/unix.7.html) offer a convenient way to communicate _bidirectionally_ between processes, and can be setup with added security features - and are the UNIX standard for IPC.


## Types of UNIX Sockets

The family of UNIX sockets is `AF_UNIX` (or `AF_LOCAL`), and they are identified by a file path. As a Unix convention, most sockets are created in the `/var/run` directory, but can live anywhere on the filesystem.

There are two types of UNIX sockets: `stream` and `datagram`.

----
## Questions