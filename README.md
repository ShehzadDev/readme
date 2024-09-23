# Manual for GDB & C Training Lab

## Overview

This document serves as a comprehensive manual for the GDB & C Training Lab, detailing the steps taken to complete the assignment, along with instructions on how to test the functionality of the implemented solutions.

## 1. Implementation Summary

### Part 1: Debugging `bug.c` with GDB

1. **Initial Compilation and Testing:**
   - Compiled `bug.c` with debugging symbols (`-g`) and all warnings enabled (`-Wall`).
   - Tested the program with various inputs to identify errors in the index processing logic.

2. **Understanding and Modifying `strtoul`:**
   - Analyzed the `strtoul` function using its manual page (`man strtoul`).
   - Updated the `strtoul` call to interpret the index as a hexadecimal number (base 16).

3. **Using GDB to Debug and Inspect Values:**
   - Set breakpoints and used GDB commands to inspect variable values, including pointers and memory addresses.
   - Executed commands to print the `argv` array, individual arguments, and hexadecimal representations.
   - Identified and documented the issue causing the program to crash with large indices.

4. **Error Handling Improvement:**
   - Modified the program to handle out-of-bounds index values gracefully by printing an error message instead of crashing.

### Part 2: Implementing String Functions in `strings.c`

1. **Function Implementations:**
   - Implemented custom versions of common string functions without using any external library functions. These include:
     - `my_strlen`: Calculates the length of a string.
     - `my_strcmp`: Compares two strings.
     - `my_strchr`: Locates the first occurrence of a character in a string.
     - `my_strrchr`: Locates the last occurrence of a character in a string.
     - `my_strrepl`: Replaces occurrences of a character in a string with another character.

2. **Ensured Correctness:**
   - Used GDB to debug and verify the correctness of each function, ensuring they produce the expected outputs as defined in the `main` function of `strings.c`.

## 2. Testing Instructions

To validate the functionality of the implemented solutions, follow these steps:

### Part 1: Testing `bug.c`

1. **Compile the `bug.c` File:**
   ```bash
   gcc -g -Wall bug.c -o bug
   ```

2. **Test the Program with Various Inputs:**
   - **With a Valid Index:**
     ```bash
     ./bug 2 lorem ipsum dolor
     ```
     - Expected Output: 
     ```
     This is argument 2: lorem
     ```
   
   - **With an Out-of-Bounds Index:**
     ```bash
     ./bug 9999999 arg1
     ```
     - Expected Output: An error message indicating an invalid index.
     - Error: Index 9999999 is out of bounds. Maximum index allowed is 2.

3. **Debug the Program using GDB:**
   - Start GDB:
     ```bash
     gdb ./bug
     ```
   - Set a breakpoint and run:
     ```bash
     (gdb) b bug.c:13
     (gdb) r 8 lorem ipsum dolor
     ```
   - Print values of interest:
     ```bash
     (gdb) p argv
     (gdb) p argv[0]
     (gdb) p/x idx
     ```
   - Verify that the printed values match expected values as documented.

### Part 2: Testing `strings.c`

1. **Compile the `strings.c` File:**
   ```bash
   gcc -Wall -Werror -g strings.c -o ./strings
   ```

2. **Run the Program and Check Outputs:**
   - The main function of `strings.c` will automatically run several tests and output whether the implemented functions are correct.

3. **Verify Each Function Manually:**
   - For each implemented function, manually verify correctness by calling the function with different inputs and comparing the outputs to expected results.

   - Example:
     ```c
     int len = my_strlen("Hello, World!");
     printf("Length: %d\n", len); // Should print: Length: 13
     ```

4. **Debug with GDB (Optional):**
   - Use GDB to set breakpoints inside each function to step through and verify their behavior:
     ```bash
     gdb ./strings
     (gdb) b my_strlen
     (gdb) r
     ```

### Additional Commands to Verify Symbol Information

1. **Compile the `strings.c` File with Optimization and Remove `main`:**
   ```bash
   gcc -Dmain='static xmain [[ maybe_unused ]]' strings.c -O3 -c
   ```

2. **Check Symbol Information Using `readelf`:**
   ```bash
   readelf --syms strings.o -W
   ```
   This command lists all the symbols in the `strings.o` object file. Symbols marked as `UND` (undefined) indicate external dependencies, which should not be present if no external functions were used.

3. **Expected Symbol Table Output:**
   ```
   Symbol table '.symtab' contains 11 entries:
      Num:    Value          Size Type    Bind   Vis      Ndx Name
      0: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT  UND 
      1: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS strings.c
      2: 0000000000000000     0 SECTION LOCAL  DEFAULT    1 .text
      3: 0000000000000000     0 SECTION LOCAL  DEFAULT    5 .rodata.str1.1
      4: 0000000000000000    26 FUNC    GLOBAL DEFAULT    1 my_strlen
      5: 0000000000000020    62 FUNC    GLOBAL DEFAULT    1 my_strcmp
      6: 0000000000000060    35 FUNC    GLOBAL DEFAULT    1 my_strchr
      7: 0000000000000090    39 FUNC    GLOBAL DEFAULT    1 my_strrchr
      8: 00000000000000c0   132 FUNC    GLOBAL DEFAULT    1 my_strrepl
      9: 0000000000000000     0 NOTYPE  GLOBAL DEFAULT  UND getenv
     10: 0000000000000000     0 NOTYPE  GLOBAL DEFAULT  UND strlen
   ```

   **Note:** The entries for `getenv` and `strlen` should not be present in the final symbol table if all external function calls have been successfully removed.

## 3. Deliverables

1. **Source Files:**
   - `bug.c`: Original buggy program with improvements for error handling.
   - `strings.c`: Contains all the implemented string functions.

2. **Documentation Files:**
   - `bug_output`: Output of `bug.c` with initial testing.
   - `bug_output2`: Output of `bug.c` after modifying `strtoul`.
   - `bug_prints`: Outputs of various GDB commands.
   - `bug_error`: Error message with explanation for out-of-bounds index handling.
   - `bug_doc`: Documentation for the `b` command in GDB.

3. **Compiled Executables:**
   - `bug`: Executable for the `bug.c` file.
   - `strings`: Executable for the `strings.c` file.

4. **Object File:**
   - `strings.o`: Compiled object file without `main` for symbol verification.

