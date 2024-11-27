# ProcDump 
ProcDump for Mac provides a convenient way for Mac developers to create core dumps of their application based on performance triggers. ProcDump for Mac is part of [Sysinternals](https://sysinternals.com).

# Installation & Usage

## Requirements
* Minimum OS: Sierra

## Install ProcDump
To install ProcDump for Mac, you'll need to install [Homebrew](https://brew.sh) if you haven't already.

1. Add the Sysinternals tap:
   ```bash
   brew tap Microsoft/sysinternalstap
   ```
   
1. Install individual Sysinternals tools:
   ```bash
   brew install procdump
   ```

## Build
ProcDump for Mac is based on the ProcDump for Linux code base which is located [here](BUILD.md).

## Usage
```
Capture Usage: 
   procdump [-n Count]
            [-s Seconds]
            [-c|-cl CPU_Usage]
            [-m|-ml Commit_Usage1[,Commit_Usage2...]]
            [-tc Thread_Threshold]
            [-fc FileDescriptor_Threshold]
            [-pf Polling_Frequency]
            [-o]
            [-log syslog|stdout]
            {
             {{[-w] Process_Name | PID} [Dump_File | Dump_Folder]}
            }

Options:
   -n      Number of dumps to write before exiting.
   -s      Consecutive seconds before dump is written (default is 10).
   -c      CPU threshold above which to create a dump of the process.
   -cl     CPU threshold below which to create a dump of the process.
   -tc     Thread count threshold above which to create a dump of the process.
   -fc     File descriptor count threshold above which to create a dump of the process.
   -pf     Polling frequency.
   -o      Overwrite existing dump file.
   -log    Writes extended ProcDump tracing to the specified output stream (syslog or stdout).
   -w      Wait for the specified process to launch if it's not running.```

### Examples
> The following examples all target a process with pid == 1234

The following will create a core dump immediately.
```
sudo procdump 1234
```
The following will create 3 core dumps 10 seconds apart.
```
sudo procdump -n 3 1234
```
The following will create 3 core dumps 5 seconds apart.
```
sudo procdump -n 3 -s 5 1234
```
The following will create a core dump each time the process has CPU usage >= 65%, up to 3 times, with at least 10 seconds between each dump.
```
sudo procdump -c 65 -n 3 1234
```
The following will create a core dump each time the process has CPU usage >= 65%, up to 3 times, with at least 5 seconds between each dump.
```
sudo procdump -c 65 -n 3 -s 5 1234
```
The following will create a core dump when CPU usage is outside the range [10,65].
```
sudo procdump -cl 10 -c 65 1234
```
The following will create a core dump when CPU usage is >= 65% or memory usage is >= 100 MB.
```
sudo procdump -c 65 -m 100 1234
```

# License
Copyright (c) Microsoft Corporation. All rights reserved.

Licensed under the MIT License.
