# State

 Applications often make use of state information to simplify what is going on. For example

* Keeping file pointers to current file location
* Keeping current mouse position
* Keeping current customer value

In a distributed system, such state information may be kept in the client, in the server, or in both.

The important point is to whether one process is keeping state information about itself or about the other process. One process may keep as much state information about itself as it wants, without causing any problems. If it needs to keep information about the state of the other process, then problems arise: the process' actual knowledge of the state of the other may become incorrect. This can be caused by loss of messages (in UDP), by failure to update, or by s/w errors.

An example is reading a file. In single process applications the file handling code runs as part of the application. It maintains a table of open files and the location in each of them. Each time a read or write is done this file location is updated. In the DCE file system, the file server keeps track of a client's open files, and where the client's file pointer is. If a message could get lost (but DCE uses TCP) these could get out of synch. If the client crashes, the server must eventually timeout on the client's file tables and remove them. 
