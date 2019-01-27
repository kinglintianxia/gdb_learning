# GDB Learning
> [RMS's gdb Debugger Tutorial](http://www.unknownroad.com/rtfm/gdbtut/)

------------
# ch01 How do I use gdb? 
- [x] 1.1 How do I compile with debugging symbols?
* Pass the `-g` flag to your compiler:
```shell
$ gcc -g program.c -o programname
```

- [x] 1.2 How do I run programs with the debugger?
* First start the debugger with your program name as the first argument.
```shell
$ gdb programname
```
* Next use the `run` command in gdb to start execution. Pass your arguments to this command. 
```shell
$ (gdb) run arg1 arg2 ...
```
- [x] 1.3 How do I restart a program running in the debugger?
* Use the `kill` command in gdb to stop execution. The you can use the run command as shown above to start it again. 
```shell
$ (gdb) kill
# Kill the program being debugged? (y or n) y
$ (gdb) run
```

- [x] 1.4 How do I exit the debugger?
* Use the `quit` command.
```shell
$ (gdb) quit
# The program is running. Exit anyway? (y or n) y
``` 

- [x] 1.5 How do I get help on debugger commands? 
* Use the `help` command.
```shell
$ (gdb) help
# List of classes of commands:
```

------------
# ch07 Example Debugging Sessions
- [x] **Infinite Loop Example**
```shell
$ gcc -g inf.c			# Compile the program with debugging flags.
$ gdb a.out				# Lets load up gdb.
$ run & ctrl+c			# Set off the infinite loop, then press `Ctrl-C` to send the program a SIGINT. 
$ backtrace				# We will use the `backtrace` command to examine the stack.
$ frame 1				# See is where we are in `main()`.
$ print c				# Check value of `c`.
$ next					# We use several `next` command to call stack back to `main()`.
$ n						# We run the next command several more times to watch the program execute. 
# Notice a pattern? The same two lines of code are executing over and over. Removing the `else` on line 13 will fix the bug.
$ quit					# Use the quit command.
```

- [x] **Segmentation Fault Example** 
```shell
$ gcc -g segfault.c		# Compile the program with debugging flags.
$ gdb a.out				# Lets load up gdb.
$ run					# run & type something, you will get `Program received signal SIGSEGV, Segmentation fault.` 
$ backtrace				# We will use the `backtrace` command to examine the stack.
$ frame 3				# See is where we are in `main()`, We crashed inside the call to `fgets`.
$ print buf				# The value of buf is `0x0`, which is the `NULL pointer`.
$ kill					# kill the currently-running invocation of our program.
$ break segfault.c:6	# set a breakpoint on `line 6`.
$ print buf				# After the call to `malloc`, buf is `NULL`. Well, the value of the expression 1 << 31 (the integer 1 right-shifted 31 times) is 429497295, or 4GB (gigabytes).
```

