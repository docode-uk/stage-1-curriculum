# UNIX Sockets

## Introduction
Applications require a way to communicate with eachother: for example, a web app needs to get a list of users from a database, or a messaging app needs to send a message to a friend. This process is known as "Inter-Process Communication" (IPC), and this can be achieved in many ways.

One could implement IPC by saving a message to a file, and having another file/user read from it. This would be slow, insecure, and have issues when more than one person tries to write to the file at the same time.

Another way would be to use [pipes](https://man7.org/linux/man-pages/man2/pipe.2.html) or [named pipes/FIFOs](https://man7.org/linux/man-pages/man7/fifo.7.html) to communicate between processes. These are obviously faster, but are also unidirectional and the input/output can only be consumed by one process at a time.

[Shared Memory (SHM)](https://man7.org/linux/man-pages/man7/shm_overview.7.html) offers another way to communicate between processes, but it is more complex to implement and manage - and can only be used by processes on the same machine.

[UNIX Sockets](https://man7.org/linux/

----
## Questions