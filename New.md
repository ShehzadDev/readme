#################################################################### -*- org -*-
                      WELCOME TO THE TRAINING LAB: GDB & C!
################################################################################

To read these instructions and work at the same time, I recommend you start
multiple SSH sessions (start PuTTy multiple times, or open several terminals).
One session can look at this file in emacs, and you can put an X in each box [ ]
to help you keep track of your progress.

* Extract the files needed for the lab

$ cd ~/
$ tar xvf ~prof/traininglab-part2-handout.tar.bz2
$ cd traininglab-part2

* Part 1: GDB

Go to ~/traininglab-part2.  All the files you are going to produce will be in that
folder.  It will be useful to open two sessions to our server to complete this
part: one to execute commands, one to write the answer files.

- [ ]  Compile bug.c with debug symbol (-g), activating all warnings (-Wall):

     $ gcc -g -Wall bug.c -o bug

- [ ]  Run

     $ ./bug 8 lorem ipsum dolor

  and store its output in the file "bug_output".  Recall the use of ">" from
  last week to redirect the output of a program to a file.

- [ ]  Read the man page of strtoul (man strtoul) to understand what it does,
  and change the call to strtoul in bug.c so that it reads numbers in
  hexadecimal (base 16).  Recompile with:

     $ gcc -Wall -g bug.c -o bug

- [ ]  Run

     $ ./bug

   and

   $ ./bug 0xB arg1 arg2 arg3 arg4 arg5 arg6 arg7 arg8 arg9 arg10 arg11

  and store the two outputs in the file "bug_output2"

- [ ]  Run

     $ gdb ./bug

   Enter the Text User Interface (TUI) by typing Control-x followed by 1.
   This displays the code of the main, and waits for the program to be run.

   Run the program (command `r' followed by Enter).  This runs the program
   with no arguments (as if you had run ./bug).

- [ ]  Hit Ctrl-l to refresh the display, that is now garbled by the output of
  the program.

- [ ]  Put a breakpoint on line 13 (command `b bug.c:13' followed by Enter).

- [ ] The breakpoint command "b" can take, as argument, a location as a line
  number or a function name.  The command has many more options.  Use "help b"
  to get instant documentation on the command "b".  Read the documentation and
  write in the file "bug_doc" what happens when no location is provided.

- [ ]  Now run the program in GDB with some arguments, using, in GDB:

        (gdb) r 8 lorem ipsum dolor

      This provides 4 arguments to our executable: 8 lorem ipsum dolor.

- [ ]  When the program breaks, print the value of the pointers:
     - argv
     - argv[0]
     - argv[8]
     and write these values in a file "bug_prints".

     Use command `p argv', for instance, to print a value.  Note that all of
  them are pointers (memory addresses), but that GDB smartly tries to display
  objects of type char* (i.e., pointer to a byte), such as argv[0], as strings.
  It does so by fetching the bytes at the address, then the next, the next,
  and so on, until reaching a 0 byte (or reaching 200 nonzero bytes).

- [ ]  Execute one more line of code using "n" followed by Enter.

- [ ]  Now print:
  - the value of idx that was just computed; print it in hexadecimal using
    command `p/x idx' (the /x indicates hexadecimal).
  - the first byte of argv[0] (using `p/x **argv', or `p/x *argv[0]', or
    `p/x argv[0][0]', which are all the same!).
  - the address of argv (using `p &argv').  Since argv is a variable, it has
    indeed an address!  This is independent from the fact that argv itself
    contains an address (which is just an 8-byte value).
  - the byte at address 0x42.  To do so, we want to tell GDB to see 0x42 (a
    number) as a pointer to a byte; the syntax is the same as in C:
     "(char*) 0x42".  We then want to look in memory at that address, so we
     dereference it, using * as in C.  The final command is thus:

      (gdb) p *((char*) 0x42).

  Add what GDB prints in each case to the file "bug_prints".

- [ ]  Delete the breakpoint (d 1)

- [ ]  Re run with command `r 9999999 arg1'.

- [ ]  GDB shows an error message; copy/paste it to file "bug_error", and add to
  that file ONE sentence explaining what caused this error in the code.

- [ ]  Exit GDB, and fix the file bug.c by printing an error message instead of
  crashing.

* Part 2: C

Read and complete the file strings.c, using GDB as needed to debug your program.
*You should not modify the main function,* which runs a few tests and shows
whether you obtained the correct values.  You are NOT allowed to call any
external function.

ANY discovered attempt at finding help online will result in an immediate
failing grade for the whole class.  Use our Discord server, emails, office
hours, when you need help; I'm here for that.

You must compile using:

  $ gcc -Wall -Werror -g strings.c -o ./strings
