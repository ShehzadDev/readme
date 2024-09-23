# GDB & C Training Lab Manual

## Overview

Welcome to the GDB & C Training Lab! This manual serves as your guide through the lab, providing step-by-step instructions for debugging a C program using GDB and implementing custom string functions in C. We’ll be delving into common debugging techniques, handling errors, and creating efficient C functions without external library dependencies. Let's dive in!

## Lab Setup

1. **Extract Lab Files:**
   - [x] Navigate to your home directory and extract the provided lab files:
     ```bash
     cd ~/
     tar xvf ~prof/traininglab-part2-handout.tar.bz2
     cd traininglab-part2
     ```
   - [x] Open multiple SSH sessions: one for command execution and another for editing answer files.

2. **Recommended Setup:**
   - [x] Keep multiple terminal windows open: one for writing/editing files, one for compiling, and another for running GDB.

---

## Part 1: Debugging `bug.c` with GDB

### Step 1: Initial Compilation and Testing

1. **Compile `bug.c` with Debug Symbols:**
   - [x] Use `-g` for debugging symbols and `-Wall` for all warnings. This helps catch issues early.
     ```bash
     gcc -g -Wall bug.c -o bug
     ```

2. **Run the Program with Test Inputs:**
   - [x] Identify logical errors and crashes:
     ```bash
     ./bug 2 lorem ipsum dolor
     ```

   - [x] Expect crashes or incorrect output with specific inputs. Take note!

### Step 2: Analyze and Update `strtoul` Call

1. **Update `strtoul` Usage:**
   - [x] Modify `bug.c` to interpret the index as a hexadecimal number (base 16).
   - Why? This prevents misinterpretation of input values.

2. **Recompile `bug.c`:**
   - [x] Don’t forget to include `-g` and `-Wall`:
     ```bash
     gcc -Wall -g bug.c -o bug
     ```

3. **Re-test with Multiple Inputs:**
   - [x] Check both valid and out-of-bounds indices:
     ```bash
     ./bug 0xB arg1 arg2 arg3 arg4 arg5 arg6 arg7 arg8 arg9 arg10 arg11
     ```

### Step 3: Debugging with GDB

1. **Start GDB Session:**
   - [x] Launch GDB with the compiled executable:
     ```bash
     gdb ./bug
     ```

2. **Set Up Logging:**
   - [x] Capture GDB output to a log file:
     ```bash
     set logging file bug_prints
     set logging on
     ```

3. **Set Breakpoints and Inspect Variables:**
   - [x] Breakpoints stop the program at a specific line for inspection:
     ```bash
     b bug.c:13
     r 8 lorem ipsum dolor
     ```

   - [x] Inspect pointers and indices:
     ```bash
     p argv
     p argv[0]
     p/x idx
     ```

4. **Delete Breakpoint and Re-run with Edge Cases:**
   - [x] Remove breakpoints and test edge cases:
     ```bash
     d 1
     r 9999999 arg1
     ```
   - [x] Identify out-of-bounds behavior and document the error message.

### Step 4: Implement Error Handling in `bug.c`

1. **Update Error Handling:**
   - [x] Modify `bug.c` to handle out-of-bounds indices by printing an error message instead of crashing.

2. **Recompile and Re-test:**
   - [x] Ensure the program behaves correctly with edge cases.

---

## Part 2: Implementing String Functions in `strings.c`

### Step 1: Implement Custom String Functions

1. **Write the Following Functions without External Libraries:**
   - [x] `my_strlen`: Calculates the length of a string.
   - [x] `my_strcmp`: Compares two strings lexicographically.
   - [x] `my_strchr`: Finds the first occurrence of a character.
   - [x] `my_strrchr`: Finds the last occurrence of a character.
   - [x] `my_strrepl`: Replaces all occurrences of a character.

2. **Ensure Correctness and Efficiency:**
   - [x] No external calls are allowed. Think carefully about edge cases (empty strings, non-existent characters, etc.).

### Step 2: Compile and Test `strings.c`

1. **Compile with Warnings and Debug Symbols:**
   - [x] This ensures all issues are caught at compile time:
     ```bash
     gcc -Wall -Werror -g strings.c -o ./strings
     ```

2. **Run the Program:**
   - [x] Check if your functions pass the pre-defined tests in the `main` function.

3. **Verify Outputs:**
   - [x] Manually verify the outputs of your functions to ensure correctness:
     ```c
     int len = my_strlen("Hello, World!");
     printf("Length: %d\n", len); // Expected: Length: 13
     ```

### Step 3: Optional Debugging with GDB

1. **Use GDB to Debug Functions:**
   - [x] Set breakpoints inside each function to inspect behavior:
     ```bash
     gdb ./strings
     b my_strlen
     r
     ```

2. **Step Through Code:**
   - [x] Use GDB commands like `step` (`s`), `next` (`n`), and `print` (`p`) to trace the execution flow and variable states.

---

## Part 3: Verification and Symbol Information

1. **Compile with Optimizations and Remove `main`:**
   - [x] Ensure no external functions are present in the object file:
     ```bash
     gcc -Dmain='static xmain [[ maybe_unused ]]' strings.c -O3 -c
     ```

2. **Check Symbols Using `readelf`:**
   - [x] Confirm that no external functions (like `getenv` or `strlen`) appear in the symbol table:
     ```bash
     readelf --syms strings.o -W
     ```

---

## Summary of Testing Instructions

### Testing `bug.c`

1. **Compile and Run `bug.c`:**
   - [x] Check for proper behavior with various indices:
     ```bash
     gcc -g -Wall bug.c -o bug
     ./bug 2 lorem ipsum dolor
     ./bug 9999999 arg1
     ```

2. **Debug and Log Outputs:**
   - [x] Use GDB to break at critical points and inspect variable states:
     ```bash
     gdb ./bug
     b bug.c:13
     r 8 lorem ipsum dolor
     ```

### Testing `strings.c`

1. **Compile and Run `strings.c`:**
   - [x] Ensure each function works as expected:
     ```bash
     gcc -Wall -Werror -g strings.c -o ./strings
     ./strings
     ```

2. **Debug as Needed:**
   - [x] Use GDB for any functions not behaving correctly.

---
