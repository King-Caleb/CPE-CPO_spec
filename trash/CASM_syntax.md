# CASM Official Syntax Specification

# Sections
.const:
    # Defines constants
    # Format: <label> <type> "<value>"
    # Types: int, latin, utf8, float, bool
    # Examples:
    pi float "3.14159"
    flag bool true
    hello utf8 "Hello World\n"
    char latin "A"

.var:
    # Defines variables
    # Format: <label> <type>
    # Types: int, latin, utf8, float, bool
    counter int
    name utf8

.code:
    # Code section contains instructions, global labels, and external references

    # External function imports
    # Format: extern <function_name> @ <module_path>
    extern malloc @ std\mem
    extern print @ std\io
    extern exit @ std\io

    # Global entry points
    # Format: global <label>
    global _start
    global print
    global exit

# Labels
<label>:
    # Labels mark locations in code for jumps or calls
    # Format: <label_name>:

# Instructions
CASM is a register-based assembly
Registers: rax, rbx, rcx, rdx, r9
Basic Instructions:
mov <reg> <reg|var|const>
    # Moves value into register

call <label|extern>
    # Calls a function or label

len <reg> <const|var>
    # Loads length of string/array into register

test <reg> <reg|const>
    # Compares two values, sets flags

cmove <reg1> <reg2>
    # Conditional move if zero flag is set

# System or module calls
invoke
    # Special opcode: 0F 05
    # Uses r9 to determine operation (like syscall)

# Example instruction usage
_start:
    mov rcx hello_ptr
    call get_ptr
    mov rcx rax
    len rdx hello
    call print
    mov rcx 0
    call exit

# Operand rules
1. <reg> must be one of: rax, rbx, rcx, rdx, r9
2. <const> can be a literal constant defined in .const
3. <var> must be defined in .var

# Types
1. int: integer numbers
2. float: floating point numbers
latin: single European only letters
utf8: UTF-8 string literals
bool: true or false

# Sections summary
1. .const : constants
2. .var   : variables
3. .code  : executable instructions, global labels, externs
