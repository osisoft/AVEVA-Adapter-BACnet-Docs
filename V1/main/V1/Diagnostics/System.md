---
uid: System
---

# System

The Diagnostics.System dynamic type includes the following values which are logged in a stream with the id System.Diagnostics.
This diagnostic stream contains system level information related to the host platform that the adapter is running on.

| Type       | Property                            | Description                                                                       |
| ---------- | ----------------------------------- |  --------------------------------------------------------------------------------- |
| **string** | timestamp                           | Timestamp of event                                                                |
| **int**    | ProcessIdentifier                   | Process id of the host process                                                    |
| **string** | StartTime                           | Time at which the host process started                                            |
| **long**   | WorkingSet                          | Amount of physical memory in bytes, allocated for the host process                |
| **double** | TotalProcessorTime (uom=s)          | Total processor time for the host process expressed in seconds                    |
| **double** | TotalUserProcessorTime (uom=s)      | User processor time for the host process expressed in seconds                     |
|**double**  | TotalPrivilegedProcessorTime (uom=s)| Privileged processor time for the host process expressed in seconds               |
| **int**    | ThreadCount                         | Number of threads in the host process                                             |
| **int**    | HandleCount                         | Number of handles opened by the host process                                      |
| **double** | ManagedMemorySize (uom=MB)          | Number of bytes currently thought to be allocated in managed memory               |
| **double** | PrivateMemorySize (uom=MB)          | Amount of paged memory, in bytes, allocated for the host process                  |
| **double** | PeakPagedMemorySize (uom=MB)        | Maximum amount of memory in the virtual memory paging file, in bytes, used by the host process.|
| **double** | StorageTotalSize (uom=MB)           | Total size of the storage medium in use by the system                             |
| **double** | StorageFreeSpace (uom=MB)           | Free space available                                                              |

Each adapter component produces its own diagnostics streams.
