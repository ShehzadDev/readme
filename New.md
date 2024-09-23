# WELCOME TO THE TRAINING LAB: GDB & C!

To read these instructions and work at the same time, consider starting multiple SSH sessions. One session can view this file, while another can execute commands.

## Extract the files needed for the lab

```bash
$ cd ~/
$ tar xvf ~prof/traininglab-part2-handout.tar.bz2
$ cd traininglab-part2
```

## Part 1: GDB

1. Go to `~/traininglab-part2`. Open two sessions: one for executing commands, another for writing answer files.

2. Compile `bug.c` with debug symbols and warnings:

   ```bash
   $ gcc -g -Wall bug.c -o bug
   ```

3. Run the program and store its output:

   ```bash
   $ ./bug 8 lorem ipsum dolor > bug_output
   ```

4. Read the man page of `strtoul` and change its call in `bug.c` to read numbers in hexadecimal (base 16). Recompile:

   ```bash
   $ gcc -Wall -g bug.c -o bug
   ```

5. Run the program with two different inputs and store the outputs:

   ```bash
   $ ./bug > bug_output2
   $ ./bug 0xB arg1 arg2 arg3 arg4 arg5 arg6 arg7 arg8 arg9 arg10 arg11 >> bug_output2
   ```

6. Start GDB:

   ```bash
   $ gdb ./bug
   ```

   Enter TUI mode with `Ctrl-x` followed by `1`.

7. Run the program without arguments:

   - Hit `Ctrl-l` to refresh the display.
   - Set a breakpoint on line 13:

     ```
     (gdb) b bug.c:13
     ```

8. Use `help b` to get documentation on the breakpoint command and write the findings in `bug_doc`.

9. Run the program with arguments:

   ```
   (gdb) r 8 lorem ipsum dolor
   ```

10. Print the values of the pointers:

    ```
    (gdb) p argv
    (gdb) p argv[0]
    (gdb) p argv[8]
    ```

    Write these values in `bug_prints`.

11. Execute one more line of code using `n`.

12. Print the following:

    - Value of `idx` in hexadecimal: 

      ```
      (gdb) p/x idx
      ```

    - First byte of `argv[0]`:

      ```
      (gdb) p/x *argv[0]
      ```

    - Address of `argv`:

      ```
      (gdb) p &argv
      ```

    - Byte at address `0x42`:

      ```
      (gdb) p *((char*) 0x42)
      ```

    Add the results to `bug_prints`.

13. Delete the breakpoint:

    ```
    (gdb) d 1
    ```

14. Rerun with:

    ```
    (gdb) r 9999999 arg1
    ```

    Copy/paste the error message to `bug_error` and explain the cause.

15. Exit GDB and fix `bug.c` to print an error message instead of crashing.

## Part 2: C

Read and complete `strings.c`, using GDB as needed for debugging. Do not modify the main function. You are NOT allowed to call any external functions.

Compile using:

```bash
$ gcc -Wall -Werror -g strings.c -o ./strings
```

--- 

Feel free to ask if you need any more adjustments!
