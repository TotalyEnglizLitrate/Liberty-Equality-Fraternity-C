### Note
Before we start, I am assuming a 64 bit system when discussing the sizes of the the datatypes, it might differ on 32 bit or lower systems. you can look up the differences if you so desire.

# Variable declaration and initialization
**What are Variables?**
Variables are named memory locations that store data of a specific type. They act as containers for values that can be manipulated throughout a program.

**Declaration Syntax**
The basic syntax for declaring a variable is: `<datatype> <variable_name>;`
When declaring a variable, you're telling the compiler:
- What type of data will be stored
- A name to reference that memory location
- Allocating memory for that specific type - inferred size from the datatype

**Initialization Syntax**
Assigning a value to a declared variable `<variable_name> = <value>;`

You can declare and initialize a variable in one go, like `<datatype> <variable_name> = <value>;`

We'll expand on declaring/initializing variables at the end of this topic.
# But what are datatypes?
I'm pretty sure, regardless of your background you have come across the idea that everything is just binary in computers, but how do you represent all the stuff we need to store that are not numbers? Well, we created standards that say this number means this in the context of `x`.

As an example we created ASCII codes for encoding text as numbers, 65 corresponds to `A`, 66 - `B` and so on. Similarly everything we need to represent can and are being represent as a bunch of binary. So everything you are going to be using is just a bunch of bits wearing a trench coat pretending to be something else.

Now to the actual built in basic, datatypes,
- `int` & it's variants
- `float`
- `double`
- `char`
- `void`

# Integers
`int` is how an integer datatype is represented in C. it takes up 4 bytes (or 32 bits) of storage and is stored in the [two's complement format](https://en.wikipedia.org/wiki/Two%27s_complement).

There are a few variations on the integer datatype, namely
- `unsigned int`
- `long int`
- `long long int`
- `unsigned long int`
- `unsigned long long int`
- `short int`
- `short unsigned int`

`unsigned int`'s are exactly what you would expect them to be, integers without sign, i.e non-negative integers. they also take up 4 bytes.

On a 64 bit system, there is no difference between (both signed and unsigned) `long` and `long long` integers, they both take up 64 bits, but in the days of 16 bit systems and the like, `int` was 2 bytes, `long int` 4 bytes and `long long int`'s were 8 bytes.

`short int`/`short unsigned int`
Opposite to long, a short int is smaller than a normal int, a `short int` takes up 2 bytes (16 bits) of space.

`long int`s and `long long int`s can also be denoted as `long` and `long long` for convenience, Similarly, there's `unsigned long`,  `unsigned long long`,  `short` & `unsigned short`.

```c
int age = 25;                   // Basic integer
unsigned int population = 50000;// Non-negative integer
short studentCount = 32;         // Smaller range integer
long bigNumber = 2147483647;     // Larger integer range
```

| Type                               | Size            | Lower bound                      | Upper bound                         |
| ---------------------------------- | --------------- | -------------------------------- | ----------------------------------- |
| `int`                              | 4 bytes/32 bits | -2147483648 $(-2^{31})$          | 2147483647 $(2^{31} - 1)$           |
| `unsigned int`                     | 4 bytes/32 bits | 0                                | 4294967295 $(2^{32} - 1)$           |
| `long`/`long long`                 | 8 bytes/64 bits | -9223372036854775808 $(-2^{63})$ | 9223372036854775807 $(2^{63} - 1)$  |
| `unsigned long/unsgined long long` | 8 bytes/64 bits | 0                                | 18446744073709551615 $(2^{64} - 1)$ |
| `short`                            | 2 bytes/16 bits | -32768 $(-2^{15})$               | 32767 $(2^{15} - 1)$                |
| `unsigned short`                   | 2 bytes/16 bits | 0                                | 65535 $(2^{16} - 1)$                |

You also have the option to use binary, octal and hexadecimal representation of integers.
binary - prefix with `0b`, e.g `0b1170750101` = 53
octal - prefix with `0o`, e.g `0o31246` = 12870
hex - prefix with `0x`, e.g `0x1ba3` = 7075


**Little and Big Endian-ness of an integer**
A little bit of background is that, a single unit of memory in your RAM is 1 byte, i.e 8 bits. And since all of the integer datatypes take up more than 1 byte, we have options as to how to store it. Obviously it has to be broken down into chunks of 1 byte/8 bits each but we have an option as to how they are ordered. i.e if the first chunk comes first and the last chunk last, or vice versa, the first chunk last and the last chunk first.

This ordering is known as the little/big endian-ness of a given system.
- Big Endian is how you would normally order, higher values to lower values.
- Little endian is lower values to higher values.

Most modern systems use little endian representation, for reasons I will explain later.

## Floating point numbers (Fractional/Real numbers)
As you undoubtedly know, there are more to numbers than just integers, namely the real numbers. They are implemented/represented in C according to the [IEEE 754 format](https://en.wikipedia.org/wiki/IEEE_754). for the uninitiated, the IEEE standard for floating points is just scientific notation in disguise.

The and `float`/`double` datatypes are used to represent these values in C, where `float` is of 32 bits and `double` 64.

A few things to note, a very large value in either direction of the number line is represented as `-inf` and `inf`. There is also `NaN` which stands for Not a Number meaning whatever operation you did to get to this value is invalid and it's output is just, not a number.

You can skip over this next part if you wish to, this is an explanation of how floating point numbers are stored internally.
### The internal representation of a floating point number
A quick example of scientific notation to jog your memory, say, you have $0.012785$, in scientific notation, it would be $1.2785 * 10^{-2}$ .

Converting this idea to binary, say we have a number $0.01100110$ in the equivalent binary scientific notation, it would be $1.100110 * 2^{-2}$.

A float can be split into three chunks
- A sign bit
- The exponent
- The fractional part

What about the  whole part, you ask? Well, we can get a little clever here, and apply a trick. We know binary only has two possible digits, 1 or 0. we can say $0.0$ is represented by all zeroes and skip storing the whole number part, because if the value is not $0.0$, we know the whole number part is 100% going to be a one. we just store the fractional ($100110$) part and the power of 2 it needs to be multiplied by $-2$ and then account for the 1 we didn't store when we're working out it's value.

```c
float temperature = 98.6;        // Standard decimal number
float pi = 3.14159f;             // Float with 'f' suffix
double precisePI = 3.141592653589793; // Double precision
```

## The character datatype
In C, characters are represented using the `char` data type. A `char` is essentially a single byte (8 bits) of storage, which can hold a single character from the ASCII character set.

**ASCII Character Set**
The [ASCII character set](https://en.wikipedia.org/wiki/ASCII) is a standard set of characters that includes letters (both uppercase and lowercase), digits, punctuation marks, and control characters (special characters that perform a specific function). Each character in the ASCII set is assigned a unique code, which is a number between 0 and 127. For example, the character 'A' has an ASCII code of 65, while the character 'a' has an ASCII code of 97. The ASCII code for a character is used to store the character in memory.

**Using char as a 1-byte Integer**
Remember how I said everything is just a bunch of bits wearing a trench coat pretending to be something else? well, we get to take advantage of that fact using things like this.

The `char` data type can also be used as a 1-byte integer. This is because a `char` is essentially a single byte of storage.

`char` and `unsigned char`
There are two variants of the `char` data type: `char` and `unsigned char`. The `char` data type is the default, and it can hold values between -128 and 127.

The `unsigned char` data type, on the other hand, can hold values between 0 and 255. This makes it useful for storing small non-negative integer values.

```c
char grade = 'A';                // Single character
char symbol = '$';               // Punctuation character
unsigned char byteValue = 255;   // Extended character range
```

## The Meaning of Void
The term "void" literally means "empty" or "without value". In the context of C programming, `void` is used to indicate that a function or expression does not produce a value. For now, that much information will suffice about void, though we have a couple extra places where void comes into play.

## Typecasting
Typecasting is the process by which you convert (or "cast") one type into another, depending on the types involved C handles this in different ways. In some cases it'll just read in the binary representation of one thing and read it in a different manner (namely in the form of the type you're converting it to), in others it'll actually convert the representation to the type it's being cast to.

as an example, `float` -> `int`  (and vice versa) casts actually change the representation
e.g if 7.5 is cast to an `int`, it becomes 7 or if 7 is cast to a `float`, it becomes 7.0.

Whereas, say if you cast a `float` or an `int` to a char, the first byte stored in the `int`/`float` gets read in and is interpreted as a character.

#### Syntax:
```c
(<type to convert to>) value
```

In general, these are the rules of typecasting
- **Integer typecasting**: When casting an integer value to another integer type, the value is truncated or padded with zeros to fit the new type.
- **Floating-point typecasting**: When casting a floating-point value to another floating-point type, the value is converted to the new type using the rules of floating-point arithmetic.
Just keep the next two rules in the back of your mind, you'll understand what it means when learning about pointers/structs respectively
- **Pointer typecasting**: When casting a pointer to one type to a pointer to another type, the pointer is simply reinterpreted as a pointer to the new type.
- **Structure typecasting**: When casting a structure to another structure type, the structure is reinterpreted as the new type.
## Type Modifiers

**Note:** these categories are not from anywhere, I just split them in this way because it made sense for me to do so.
### Memory modifiers
Before you come here, read [[Types of (primary) memory|this tangent on the types of memory]].

`auto`
it is used to declare a variable that is automatically allocated and deallocated by the compiler. It is not commonly used in modern C programming as it is the default behaviour now.

 `volatile`
 it is used to explicitly say that this variable should only be kept in the RAM whenever it is not needed, this helps avoids bugs introduced by compiler optimizations.

`register`
it is used to explicitly say that this variable should be kept in the register, which helps in having fast access to it.

You probably want to just the compiler figure out if something should be in the memory or in the 
register.

### Scope modifiers
Before you come here, read up on [[Scopes & Lifetimes|scopes]].
`extern`
it is used to declare a variable or function that is defined in another scope. It is not a type modifier in the classical sense, but rather a way of telling the compiler to look for the definition of a variable or function in another file/scope.
##### Multiple Files Example
**file1.c**
```c
// Global variable defined
int global_counter = 0;

// Function defined in this file
void increment() {
    global_counter++;
}
```

**file2.c**
```c
// Declare global variable from another file
extern int global_counter;

void print_counter() {
    printf("Current counter: %d\n", global_counter);
}
```
Here, file2 can access the value of global_counter from file1 (*assuming that they are both compiled into the same executable).

##### Local Scope Global Declaration
```c
void function() {
    extern int global_variable;  // Declares global variable within local scope
    
    // Can now use global_variable even if not previously mentioned in this function
    global_variable = 100;
}

// Global variable definition elsewhere in the program
int global_variable = 0;
```
drags in variable from surrounding (global) scope into the local scope.
### Misc modifiers
`const`
it is used to declare a variable or a return type of a function as a constant i.e it cannot be modified, once initialized it's value is a constant and cannot be changed at all.
e.g
```c
const int MAX_PLAYERS = 4;       // Unchangeable integer
const float TAX_RATE = 0.08;     // Constant decimal
const char NEWLINE = '\n';       // Constant character
````

`static` 
it is used to declare a variable whose value persists across multiple calls of a function. and whose value can only be initialized once, any further initialization statements are ignored.
e.g
```c
// The following function will print out the number of times it has been called
void countCalls() {
    static int callCount = 0;    // Retains value between function calls - Initialiazed only once
    callCount++;
    printf("Function called %d times", callCount);
}
```

it can also be used to declare functions which can only be used from within the file the function is defined in. (If you didn't know, you can compile more than 1 file into a single executable, because having 1 single file that does _everything_ is just a pain in the ass to maintain)

`restrict`
it is a hint to the compiler that a pointer is the only pointer to a particular object. This can improve performance by allowing the compiler to do some black magic that I do not understand. You probably won't use this for the code you write for this course.

`inline`
it tells the compiler to inline the function into assembly, making it faster than calling a function and returning values or whatever. You probably don't need to use this, The compiler is smart enough to figure out where in-lining would improve performance and do it depending on the optimization level.


## Types of Declaration

### Basic Declaration
```c
int age;
float temperature;
char initial;
```
### Declaration with Initialization
```c
int counter = 0;
float pi = 3.14159;
char grade = 'A';
```
## Multiple Variable Declaration
```c
int x, y, z;
float a = 1.0, b = 2.0, c = 3.0;
```
## Constants
**Note:** conventionally variables follow snake case for names which_uses_underscores_instead_of_spaces_with_all_small_letters. For constants, the convention is to use screaming snake case, WHICH_IS_THE_SAME_AS_SNAKE_CASE_BUT_WITH_ALL_CAPS.
```c
const int MAX_SIZE = 100;
const float GRAVITY = 9.81;
```
## Static Variables
```c
static int count = 0;
```

## Valid Naming Rules
Here are the rules C uses for determining if a variable name is valid or not,
- First character must be a letter (a-z, A-Z) or underscore (\_)
- Subsequent characters can be letters, digits (0-9), or underscores
- Case-sensitive (age, Age, AGE are different variables)
- No spaces or special characters allowed
- Cannot use reserved keywords (int, char, return, etc.)

## Uninitialized Variable Warnings
**Potential Issues**
- Contains random/garbage memory values
- Unpredictable program behavior
- Can lead to subtle, hard-to-debug errors
**Compiler Warnings**
```c
int dangerous_var;      // Compiler may warn: "variable might be used uninitialized"
printf("%d", dangerous_var);  // Undefined behavior
```

```c
int x;                  // Uninitialized
if(x == 0) {           // Dangerous! Value is unpredictable
    // Produces unexpected results
}
```

**Why Initialize?**
- Predictable program behavior
- Prevent memory-related bugs
- Improve code reliability
- Make debugging easier
**Best Practices**
- Always initialize variables before use
- Use meaningful initial values
- Use static analyzers for additional checks
[[Operators 1 - Arithmetic and Bitwise operators|Next]]