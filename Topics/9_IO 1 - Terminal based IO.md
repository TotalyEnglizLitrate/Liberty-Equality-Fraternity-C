# Terminal based IO
I'm sure by this point you have covered atleast printf/scanf in your classes so I won't go into much detail about what they do.
## Output functions

1. **printf()**: `printf()` is a versatile output function that can print formatted output to the standard output stream (`stdout`). It takes a format string as its first argument, followed by any number of additional arguments that are used to replace placeholders in the format string.

Example:
```c
int x = 10;
printf("The value of x is %d\n", x);
```
This code prints the string "The value of x is 10" to the screen, followed by a newline character.
printf returns the number of bytes successfully printed to the terminal, `-1` for a failure (usually an EOF error)

2. **puts()**: `puts()` is a simpler output function that prints a string followed by a newline character.

Example:
```c
puts("Hello, world!");
```
This code prints the string "Hello, world!" to the screen, followed by a newline character. puts also returns the number of characters written to stdout or -1 for an error

3. **putc()**: `putc()` is an output function that prints a single character.

Example:
```c
putc('A', stdout);
```
This code prints the character 'A' to the screen. (we'll touch on stdout in a bit), putc returns the character printed out or -1 for an error 

4. **putchar()**: `putchar()` is similar to `putc()`, but it only prints to the standard output stream (`stdout`).

Example:
```c
putchar('A'); // same as putc('A', stdout)
```
This code prints the character 'A' to the screen. putchar also has the same return type as putc

## Input functions

5. **scanf()**: `scanf()` is a versatile input function that can read formatted input from the standard input stream (`stdin`). It takes a format string as its first argument, followed by any number of additional arguments that are used to store the input values.

Example:
```c
int x;
scanf("%d", &x);
```
This code reads an integer from the user and stores it in the variable `x`. scanf returns the number of variables successfully read in and -1 for an EOF error

1. **gets()**:  `gets()` is an input function that read a line of input from the standard input stream (`stdin`) and stored it in a string.
```c
char name[10];
gets(name);
```
This code reads a string of upto 9 characters\* from the user and stores it in the variable `c`. It returns a pointer to the string it read in

2. **getc()**: `getc()` is an input function that reads a single character from the standard input stream (`stdin`).

Example:
```c
char c = getc(stdin);
```
This code reads a single character from the user and stores it in the variable `c`. it returns the character it reads in or EOF

3. **getchar()**: `getchar()` is similar to `getc()`, but it only reads from the standard input stream (`stdin`).

Example:
```c
char c = getchar();
```
This code reads a single character from the user and stores it in the variable `c`. same as getc

Note that `getchar()` is often used in preference to `getc()` because it is more concise and easier to read. However, `getc()` can be used to read from other input streams, such as files, whereas `getchar()` only reads from `stdin`.
#### Formatting strings for printf/scanf
In C, print/scan formatters are used to specify format of the input or output. Here are some of the most common formatters:

* **%c**: Character formatter. Used to print or scan a single character.
* **%d**: Decimal integer formatter. Used to print or scan a decimal(i.e base 10) integer.
* **%i**: Integer formatter. Used to print or scan an integer in decimal, octal, or hexadecimal format.
* **%e**: Exponential floating-point formatter. Used to print a floating-point number in exponential notation. (like 3.7e+7 = 3.7 \* 10 ^ 7)
* **%f**: Fixed-point floating-point formatter. Used to print a floating-point number in fixed-point notation.
* **%g**: General floating-point formatter. Used to print a floating-point number in either fixed-point or exponential notation, depending on the size of the number.
* **%o**: Octal integer formatter. Used to print or scan an integer in octal format.
* **%s**: String formatter. Used to print or scan a string of characters.
* **%u**: Unsigned decimal integer formatter. Used to print or scan an unsigned decimal integer.
* **%x**: Hexadecimal integer formatter. Used to print or scan an integer in hexadecimal format.
* **%p**: Pointer formatter. Used to print a pointer address.
* **%lf**: Long floating-point formatter. Used to print or scan a long floating-point number.
* **%ll**: Long long integer formatter. Used to print or scan a long long integer.
* **%hu**: Unsigned short integer formatter. Used to print or scan an unsigned short integer.
* **%h**: Short integer formatter. Used to print or scan a short integer.

Modifiers can be used with these formatters to specify additional formatting options, such as:
* **h**: Short modifier. Used to specify a short integer or unsigned short integer.
* **l**: Long modifier. Used to specify a long integer, unsigned long integer, or long floating-point number.
* **ll**: Long long modifier. Used to specify a long long integer or unsigned long long integer.
* **L**: Long double modifier. Used to specify a long double floating-point number.

For example:
* **%hd**: Short decimal integer formatter.
* **%lu**: Long unsigned decimal integer formatter.
* **%lld**: Long long decimal integer formatter.
* **%Lf**: Long double floating-point formatter.

Flags can also be used with these formatters to specify additional formatting options, such as:
* **+**: Plus sign flag. Used to always print a plus sign for positive numbers.
* **-**: Minus sign flag. Used to left-justify the output.
* **#**: Alternate form flag. Used to print an alternate form of the output, such as printing a leading zero for octal numbers.
* **0**: Zero padding flag. Used to pad the output with zeros instead of spaces.
* ****: Space flag. Used to print a space before the output if the number is positive.

For example:
* **%+d**: Decimal integer formatter with plus sign flag.
* **%-d**: Decimal integer formatter with minus sign flag.
* **%#x**: Hexadecimal integer formatter with alternate form flag.
* **%05d**: Decimal integer formatter with zero padding flag.

### Buffer overflows

The `gets()` function and the `%s` format specifier with `scanf()` can be dangerous to use in C programming because they can lead to buffer overflow vulnerabilities.

**gets():**
The `gets()` function does not perform any bounds checking on the input, which means that if the input is longer than the buffer, it will overflow the buffer and potentially cause the program to crash or execute arbitrary code.

For example:
```c
char buffer[10];
gets(buffer);
```
If the user enters a string longer than 9 characters (leaving room for the null terminator), it will overflow the buffer and write into memory that is not part of the buffer, potentially cause the program to crash if we overwrite a large amount of memory or worse, allow a malicious attacker to run arbitrary code by overwriting the next data and/or instructions that are placed after the buffer in memory.

**scanf() with %s:**

The `%s` format specifier with `scanf()` reads a string of characters from the standard input and stores it in a buffer. However, like `gets()`, it also does not perform bounds checking by default.

For example:
```c
char buffer[10];
scanf("%s", buffer);
```
If the user enters a string longer than 9 characters (leaving room for the null terminator), it will overflow the buffer and potentially cause the program to crash.

**Consequences:**

Buffer overflow vulnerabilities can have serious consequences, including:

* Program crashes: The program may crash or terminate unexpectedly, potentially causing data loss or corruption.
* Code execution: An attacker may be able to execute arbitrary code, potentially allowing them to gain unauthorised access to the system or steal sensitive data.
* Data corruption: The buffer overflow may cause data corruption, potentially leading to unexpected behaviour or errors.

We will look at alternatives to avoid this later, however there is a way to limit the amount of bytes read in when using scanf
```c
char buffer[10];
scanf("%9s", buffer);
```
### Extra tidbits
#### stdin, stdout, stderr
**Introduction to stdin, stdout, and stderr:**

In computing, `stdin`, `stdout`, and `stderr` are three standard streams that are used for input/output operations. They are:

* **stdin (Standard Input)**: The standard input stream, which is used to read input from the user or from a file. By default, `stdin` is connected to the keyboard.
* **stdout (Standard Output)**: The standard output stream, which is used to print output to the screen or to a file. By default, `stdout` is connected to the terminal.
* **stderr (Standard Error)**: The standard error stream, which is used to print error messages to the screen or to a file. By default, `stderr` is connected to the terminal.

**Default behavior in the terminal:**

In a terminal, `stdin`, `stdout`, and `stderr` are connected to the following devices by default:

* `stdin`: Keyboard
* `stdout`: Terminal
* `stderr`: Terminal

This means that when a program reads from `stdin`, it reads input from the keyboard. When a program writes to `stdout`, it prints output to the screen. When a program writes to `stderr`, it prints error messages to the screen.

**Modifying the default behaviour:**

We are allowed to modify the default behaviour of `stdin`, `stdout`, and `stderr` from their default connections to the keyboard and screen. This is useful in a variety of situations, such as:

* **Redirecting output to a file**: We can redirect the output of a program to a file instead of the screen. For example, `ls > file.txt` redirects the output of the `ls` command to a file named `file.txt`.
* **Redirecting input from a file**: We can redirect the input of a program to come from a file instead of the keyboard. For example, `sort < file.txt` redirects the input of the `sort` command to come from a file named `file.txt`.
* **Piping output to another program**: We can pipe the output of one program to the input of another program. For example, `ls | grep file` pipes the output of the `ls` command to the input of the `grep` command.
* **Logging error messages to a file**: We can redirect error messages to a file instead of the screen. For example, `program 2> error.log` redirects error messages from the `program` command to a file named `error.log` while keeping the stdout as the terminal.

We can modify the default behaviour of `stdin`, `stdout`, and `stderr` using various methods, such as:

* **Redirection operators**: `>`, `<`, `>>`, `<<`, `|`, etc.
* **File descriptors**: We can use file descriptors to redirect input/output operations to specific files or devices.
* **System calls**: We can use system calls, such as `open()`, `close()`, `read()`, and `write()`, to modify the default behaviour of `stdin`, `stdout`, and `stderr`.

**Why are we allowed to modify the default behaviour?**

We are allowed to modify the default behaviour of `stdin`, `stdout`, and `stderr` because it provides flexibility and power in using the command line and writing programs. By modifying the default behaviour, we can:

* **Automate tasks**: We can automate tasks by redirecting input/output operations to files or other programs.
* **Log error messages**: We can log error messages to files for debugging and troubleshooting purposes.
* **Improve productivity**: We can improve productivity by using pipes and redirection to perform complex tasks in a single command.
* **Write more efficient programs**: We can write more efficient programs by using system calls and file descriptors to modify the default behaviour of `stdin`, `stdout`, and `stderr` instead of printing output to the terminal and then do some convoluted stuff to pass that in to another program we cut the middle man and go straight from one program to another.

[[10_Compilation - a bit of theory & implementation detail|Next]]
