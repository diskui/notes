
## foreword
ints are not integers, floats are not reals.

c doesn't check the bound when deal with array (and map...)

Shift operations associate from left to right, so `x << j << k` is equivalent to `(x << j) << k`.

In C, addition and subtraction have higher precedence than shifts, so the expression `1<<2+3<<4` will be `1 << (2+3) << 4`.

when in trouble, put in parentheses.

when both size and type need to be casted, the size comes first.

the aligning only takes place with primitive, but don't with clustered type.

## data representation
tow ways to get the negatibe of a two's complement number x:

* -x =  ~x + 1
* let k be the position of right-most 1 of x, then x has the form [Xw-1,Xw-2...,Xk+1,1,0...], and the bit pattern of the negation of x is [~Xw-1,~Xw-2...,~Xk+1,1,0...]

to compute the product of two's complement number :

* sign extend the numbers to twice as many bits
* do elementary multiplication
* take the correct protion of the result

When casting from float or double to int, the value will be rounded **toward zero**, and the value may overflow. On Intel-compatible microprocessors machines, all indefinite numbers will be represented as T_Min.

Floating-point arithmetic must be used carefully, for its limited range and precision.

Floating-point number arithmetic doesn't support associative 
law.

## machine level programing

the processes of compiling a c program:
* preprocess (expand the source code with things declared in `#include` and `#define`)
* generate assembly code (file.c -> file.s)
* the assembler convert the assembly into object-code file(file.s -> file.o)
* the linker links all the object-codes and library functions, and then generate the final executable file(file.o -> file)

there are some instructions for copying and generating 1-, 2-, 4-, and 8-bytes values, when the destinations of these instructions are registers, the instructions that deal with 1- and 2-bytes quantities will keep the remaining bytes unchanged, while those who deal with 4-bytes quantities will set all remaining bytes to 0.

x86-64 imposes the restriction that a move instruction can't have both operands refer to momery location, so copying a value from a memory location to another needs two instructions: firstly move the source value to a register, and then copy from that register to destination.

the regular `movq` instruction can only have immediate source operand that can be represented as a 32-bit two's complement number. this value is then sign extended to a 64-bit value for the destination. the `movabsq` instruction can have arbitrary immediate value for its source operand and its destination must be a register.

instructions in the `MOVZ` class will fill out the remaining bytes of the destination by zero, while instructions in the `MOVS` class will fill out them by sign bit. each instruction name in these classes have two size designators as its two final characters -- the first specifying the size of source operand, and the second specifying the size of destination.

`movzlq` (move a 4-byte source value to a 8-byte destination with zero filling out) does not exist, for this movement can be implemented using a `movl` instruction with a register as a destination operand.

the `cltq` instruction has no operands -- it always use `%eax` as its source operand and `%rax` as its destination operand with sign-extension, ie `movslq %eax,%rax`.

the two operands of a binary instrucion can't be both memory locations (just as `mov`). when the second operand of a binary instruction is a memory location, the processor will read the value of it first, and write back it after the operation.

there are two names of left shift instruction: `SAL` and `SHL`, and they have same effect. However, there are two different right shift instrucions, `SAR` for arithmetic right shift (fill out sign bit), and `SHR` for logical right shift (fill out zero).

the `lea` instruction does alter the conditional code, since it's used for address computing.

the logical instructions will set carry and overflow codes to zero, the shift instrucitons will set overflow code to zero and carry code to the last bit that just shifted out.

the `inc` and `dec` instructions will keep carry flag unchanged.

single byte conditional move is not supported.

gcc mostly use conditional control transfers because it's safer, the conditional move will raise an error if one of the expressions to be evaluated is not valid.

the `->` operator is just the combination of `(*p).object`

`void *` type represents a generic pointer.

the `molloc` function will return a generic pointer, so it's common to cast it to a pointer of a specific type.

pointer types **are not** part of mechine code, it's just an abstraction of c to help programs to avoid address errors.

the `&` operator (create a pointer) can be applied to any **lvalue**.

casting from one type of pointer to another changes its type but not its value. one effect of casting is to change any scaling of pointer arithmetic.

pointers can also point to functions.

```c
//function prototype
int fun(int x, int * p);
//declare and assign a pointer to this function
int (*fp)(int ,int *);
fp = fun;
//invoke this function with pointer
int y = 1;
int result = fp(3,&y);
```
the parentheses around `*fp` is required, otherwise the statement turns into: `(int *) fp(int,int*);` which will be interpreted as a function prototype.

function `fgets` is a better version of `gets`, for it has an argument indicates the max number of bytes to read.

when a function contains a combination of integers, pointers and floating number arguments, the pointers and integers will be passed by common registers, and the floating numbers will be passed by XMMn.

AVX floating-point operations can't have immediate values as operand (unlike integer arithmetic).

## Memory Hierarchy

SRAM is used in cache memories while DRAM is used for main memories and flame buffers.

## Linker

linker's symbol rules:
* multiple strong symbols are not allowed, otherwise error
* given a strong symbol and multiple symtols, choose the strong one
* if there are multiple weak symbols, pick an arbitrary one(can be overridden by `gcc -fno-common`)

some rules about global varialbe:
* avoid it if you can
* initialize it if you define one
* use `extern` if you reference an external global variable

## Exception Control Flow

the difference between `SIGINT` and `SIGKILL` is that  the latter can't override or ignore.

kernel sends a signal to a process by updating some bits of it's context.

signals are not queued, there can be at most **one** pending signal (signal sent while not received) for a particular type. the subsequent signals sent to a particular process after a pending signal will be discarded.

```bash
# to kill a process
/bin/kill -9 pid

#to kill all processes of a process group:
/bin/kill -9 -pgrpid
```

`ctrl + c` (and `ctrl + z`) will send a `SIGINT` (and `SIGSTP`) to all jobs in the foreground **process group**.

user code handlers and main program are **concurrent** and they **share** the global variables, so be careful to write them.

guidelines for writing safe handlers:

* keep your handlers as simple as possible
* call only `async-signal-safe` function in your handlers
* save and restore `errno` on entry and exit
* protect accesses to shared data structure by temporarily blocking all signals
* declare global variables as volatile
  * to prevent compiler from store them in register
* declare global flags as volatile `sig_atomic_t`

function is `async-signal-safe` if either **reentrant** or **non-interruptible by signals**.

a pending signal can merely indicates that there are **at least** one signal has arrived.

signals can't be used to count the occurrence of events in other processes.

## System-Level I/O

A file is just a sequence of bytes.

Every time you make a system call you should check the return value.

You should check the return value even if you are just closing a file.

To access the file metadata of a file you should use Unix I/O, and standard I/O is not appropriate to use when network programing.

don't use `scanf` to read binary files.

## Virtual Memory

