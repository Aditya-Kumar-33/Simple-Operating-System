# Custom Linux Process Management Suite

A low-level, three-part system written in C that simulates core components of an operating system. This project demonstrates practical systems programming skills using process management, ELF loading, inter-process communication, and CPU scheduling.

---

## Project Structure

### 1. **ELF Loader (`loader.c`)**

A minimal ELF executable loader that bypasses `execve`, manually loads the binary into memory, and jumps to its entry point.

* **Key Features**:

  * Parses ELF headers and maps segments with `mmap()`
  * Loads `.text`, `.data`, and `.bss` into memory with appropriate permissions
  * Jumps directly to program's entry point (`e_entry`)

* **Skills Highlighted**:

  * ELF binary parsing
  * Manual memory mapping and segment protection
  * Low-level execution control without standard process launching

### 2. **Custom Shell (`shell.c`)**

A simple interactive shell to execute commands. Integrates directly with the scheduler.

* **Key Features**:

  * Parses and submits commands to the scheduler via a shared queue
  * Accepts priority-based submissions using: `submit ./a.out [priority]`
  * Gracefully shuts down and prints statistics on `Ctrl+C`

* **Skills Highlighted**:

  * Command parsing
  * Signal handling
  * Shared memory communication

### 3. **Round-Robin Scheduler (`scheduler.c`)**

A process scheduler that uses shared memory and semaphores to simulate round-robin CPU scheduling.

* **Key Features**:

  * Allocates `nprocs` CPUs, each running in time slices (`tslice`)
  * Uses `SIGSTOP` and `SIGCONT` to pause/resume processes
  * Tracks execution time, wait time, and process statistics
  * Synchronizes with the shell using `mmap()` and POSIX semaphores

* **Skills Highlighted**:

  * Process scheduling algorithms
  * IPC: shared memory, semaphores
  * Signal-based process control (`kill`, `waitpid`, `SIGSTOP`, `SIGCONT`)

---

## Technologies Used

* C
* Linux system calls
* POSIX shared memory + semaphores
* ELF binary format
* Signals and process control

---


## Notes

* Designed for Linux-based systems.
* No external libraries or frameworks used.
* Makefile provided for easy compilation.
