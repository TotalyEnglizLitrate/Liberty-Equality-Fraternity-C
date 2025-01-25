# Arithmetic operators
Arithmetic operators are used to perform mathematical operations on variables and constants. The following are the arithmetic operators available in C:
- `+` (Addition)
- `-` (Subtraction)
- `*` (Multiplication)
- `/` (Division)
- `%` (Modulus)
```c
int a = 10;
int b = 3;

int sum = a + b;  // sum = 13

int difference = a - b;  // difference = 7

int product = a * b;  // product = 30

int quotient = a / b;  // quotient = 3

int remainder = a % b;  // remainder = 1
```

# Bitwise Operators
Bitwise operators are used to perform operations on the individual bits of a variable. The following are the bitwise operators available in C:
- `&` (Bitwise AND)
- `|` (Bitwise OR)
- `^` (Bitwise XOR)
- `~` (Bitwise NOT)
- `<<` (Left Shift)
- `>>` (Right Shift)

```c
unsigned int a = 5;   // 00000101
unsigned int b = 3;   // 00000011

unsigned int and_result = a & b;  // and_result = 00000001 (1)

unsigned int or_result = a | b;  // or_result = 00000111 (7)

unsigned int xor_result = a ^ b;  // xor_result = 00000110 (6)

unsigned int not_result = ~a;  // not_result = 11111111 11111111 11111111 11111010 (4294967290)

unsigned int left_shift_result = a << 1;  // left_shift_result = 00001010 (10)

unsigned int right_shift_result = a >> 1;  // right_shift_result = 00000010 (2)
```


# Augmented assignment of Arithmetic and Bitwise operators
Augmented assignment operators are a shorthand way to perform an operation on a variable and assign the result back to the same variable. They are used to simplify code and improve readability. All the aforementioned operators (i.e arithmetic and bitwise operators) have augmented counterparts except bitwise NOT as it is a unary operator
```c
int a = 10;

a += 5;  // equivalent to a = a + 5; a = 15

a -= 3;  // equivalent to a = a - 3; a = 12

a *= 2;  // equivalent to a = a * 2; a = 24

a /= 4;  // equivalent to a = a / 4; a = 6

a %= 3;  // equivalent to a = a % 3; a = 0

a <<= 2;  // equivalent to a = a << 2; a = 0 (since a was 0)

a >>= 1;  // equivalent to a = a >> 1; a = 0

a &= 5;  // equivalent to a = a & 5; a = 0

a ^= 3;  // equivalent to a = a ^ 3; a = 3

a |= 2;  // equivalent to a = a | 2; a = 3
```

### Chaining Augmented Assignment Operators
Augmented assignment operators can be chained together to perform multiple operations in a single statement.
```c
int a = 10;

a += 5 *= 2;  // equivalent to a = (a + (5 * 2)); a = 20
```
**Note:** the order of operations is still followed when chaining augmented assignment operators. In the above example, the multiplication is performed first, and then the addition.

Augmented assignment operators serve as short hand, that is also more readable than the conventional way of doing an operation on a variable and then storing it in the same variable.

[[6_Statements - if,while,for... etc.|Next]]