# **Lab Testing and Debugging Guide**

This guide outlines the steps required to test and debug the `bug.c` and `strings.c` programs using GDB. It also includes the necessary documentation of changes and outputs as per the requirements.

## **Part 1: GDB Testing**

### **1. Compile `bug.c` with Debug Symbols and Warnings**
Compile the `bug.c` program with debug symbols enabled and warnings displayed.
```bash
gcc -g -Wall bug.c -o bug
```
- **Output**: No changes required.

### **2. Run the Program and Redirect Output**
Run the compiled program with specific arguments and redirect the output to `bug_output` file.
```bash
./bug 8 lorem ipsum dolor > bug_output
```
- **Output**: `bug_output` file should contain the program's output.

### **3. Modify `strtoul` to Read in Hexadecimal**
Change the `strtoul` function call in `bug.c` to read numbers in base 16.
```c
uint64_t idx = strtoul(argv[1], &endarg, 16);  // Change base to 16
```
- **Documentation**: Add a comment in `bug.c` explaining that the base has been changed to 16.

### **4. Recompile with Debug Symbols and Warnings**
Recompile `bug.c` to incorporate the change.
```bash
gcc -Wall -g bug.c -o bug
```
- **Output**: No further changes required.

### **5. Run the Program with No Arguments and Redirect Output**
Run the program without any arguments and redirect the output to `bug_output2`.
```bash
./bug > bug_output2
```
- **Output**: `bug_output2` file should contain the program's output when run without arguments.

### **6. Run the Program with Hexadecimal Input and Redirect Output**
Run the program with hexadecimal input and append the output to `bug_output2`.
```bash
./bug 0xB arg1 arg2 arg3 arg4 arg5 arg6 arg7 arg8 arg9 arg10 arg11 >> bug_output2
```
- **Output**: The output should be appended to the `bug_output2` file.

### **7. Start GDB**
Start a GDB session with the `bug` executable.
```bash
gdb ./bug
```

### **8. Enter TUI Mode in GDB**
- **Command**: Press `Ctrl+x` followed by `1`.
- **Purpose**: Switch to GDB's TUI mode for better visibility of the source code.

### **9. Run the Program in GDB**
Run the program in GDB without arguments.
```gdb
r
```

### **10. Refresh Display**
- **Command**: Press `Ctrl+l`.
- **Purpose**: Refresh the TUI display for clarity.

### **11. Set a Breakpoint on Line 13**
Set a breakpoint at line 13 of `bug.c`.
```gdb
b bug.c:13
```

### **12. Document the Behavior of Breakpoint Command**
- **Command**: In GDB, type the following to understand the `b` command behavior.
```gdb
help b
```
- **Documentation**: Write the output of this command and an explanation in the `bug_doc` file.

### **13. Run the Program with Arguments in GDB**
Run the program in GDB with the following arguments.
```gdb
r 8 lorem ipsum dolor
```

### **14. Print the Values of the Pointers**
Print the values of various pointers.
```gdb
p argv
p argv[0]
p argv[8]
```
- **Output**: Save the output of these commands in the `bug_prints` file.

### **15. Add Printed Values to `bug_prints`**
Document the printed values in the `bug_prints` file.

### **16. Execute One More Line of Code in GDB**
Move to the next line of code in GDB.
```gdb
n
```

### **17. Print in Hexadecimal and Other Values**
Print the following values in hexadecimal format and other information.
```gdb
p/x idx              // Print idx in hexadecimal
p/x **argv           // Print first byte of argv[0]
p &argv              // Print the address of argv
p *((char*) 0x42)    // Print the byte at address 0x42
```
- **Output**: Save the output in the `bug_prints` file.

### **18. Add Printed Values to `bug_prints`**
Document all the printed values from the previous step in the `bug_prints` file.

### **19. Delete the Breakpoint**
Delete the breakpoint set earlier.
```gdb
d 1
```

### **20. Rerun the Program with a New Argument**
Rerun the program in GDB with a large argument.
```gdb
r 9999999 arg1
```
- **Output**: Document the error message in the `bug_error` file.

### **21. Copy Error Message and Explanation to `bug_error`**
- Copy the GDB error message.
- Add a one-sentence explanation for the cause (e.g., "The error occurred due to an out-of-bounds array access.") in the `bug_error` file.

### **22. Fix the Code in `bug.c`**
Modify `bug.c` to print an error message instead of crashing.
```c
if (idx >= argc) {
    fprintf(stderr, "Error: Index out of bounds.\n");
    return 1;
}
```
- **Documentation**: Document this change in the `bug_error` file as well.

---

## **Part 2: C Testing**

### **1. Compile the `strings.c` File**
Compile the `strings.c` program with warnings and errors enabled.
```bash
gcc -Wall -Werror -g strings.c -o ./strings
```
- **Output**: No changes required unless compilation errors occur.

### **2. Run the Compiled Program**
Run the compiled `strings` program to check its outputs.
```bash
./strings
```
- **Output**: Check if the program behaves as expected. No file output required.

### **3. Use GDB to Debug the Program**
Start a GDB session to identify bugs.
```bash
gdb ./strings
```

### **4. Set Breakpoints and Step Through the Code**
Set breakpoints in suspected areas and step through the code to analyze behavior.
- **Commands**: Use `b`, `n`, and `s` commands in GDB.

### **5. Adjust Functions in `strings.c` Based on Analysis**
Based on the GDB analysis, make necessary adjustments to the functions in `strings.c`.
- **Documentation**: Document all changes in the code with appropriate comments.

---

By following these steps and documenting your actions in the specified files (`bug_output`, `bug_output2`, `bug_doc`, `bug_prints`, `bug_error`), you will be able to successfully complete the lab as instructed.
