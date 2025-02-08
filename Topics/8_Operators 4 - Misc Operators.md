# Unary operators
Unary operators are the operators that operate on only one operand.
- `&` (address-of operator)
	- It operates on a variable and returns in address (location) in memory
```c
int a = 1002; // say this is stored in memory address 0x1000
printf("%p\n", &a); // outputs 0x1000
```
- `*` (dereference operator)
	- It operates on a memory address and returns (or) fetches the value stored at that memory address
```c
int a = 1002; // same assumption of address = 0x1000
int *a_address = &a; // value = 0x1000
printf("%d\n", *a_address); // outputs 1002 
```
- `~` (bitwise NOT operator)
	- The bitwise not operator operates on numerical values and and flips all the bits present in a number, i.e 0's become 1's and vice-versa
```c
unsigned short a = 1231; // 0000010011001111
printf("%hu", ~a); // outputs 64304 - 1111101100110000
```
- `!` (logical NOT operator) is also a unary operator, but has been covered already
- `sizeof` (sizeof operator)
	- The sizeof operator takes in a datatype or variable and returns the amount of memory it takes up in bytes
	- **Note:** This is a compile time operator, i.e the size of the argument is calculated when you compile the program and is substituted in as an integer. This is because looking up the size of a variable/datatype at runtime would be inefficient.
- `+`/`-` (Unary +/- operator)
	- These are used to denote the sign of a signed integer/float, I presume you do not require examples for this.
- '++'/'--' (Prefix/Postfix increment/decrement operator) already covered under arithmetic operators, they are not strictly classified as unary under C. but they do fit the definition of a unary operator, so I have included them in this list.
- `(type)` (Type casting operator) has been covered before

## Other misc operators
### Comma Operator

The comma operator is used to separate expressions in a single statement. It has the lowest precedence of all operators in C, meaning that it is evaluated last.

```c
// expression1, expression2, ...;
int x = 10, y = 20;
```
The comma operator is often used to separate expressions in a single statement, such as initialising multiple variables or calling multiple functions.
### Member Access Operators
The member access operators are used to access members of a structure or union.
#### Dot Operator
The dot operator is used to access members of a structure or union directly.
```c
// structure_name.member_name
// Structs are going to be visited at a later part but I believe for explaining member access this would suffice
struct Person {
	int age;
	char name[20];
};
...
...
...
struct Person person;

person.age = 30;
```
#### Arrow Operator

The arrow operator is used to access members of a structure or union through a pointer.

```c
// pointer_name->member_name
struct Person {
	int age;
	char name[20];
};
...
...
...
struct Person *person;
person->age = 30;
```

### Indexing Operator

The indexing operator is used to access elements of an array.

```c
// array_name[index]

int arr[10];
arr[0] = 10;
```
[[9_IO 1 - Terminal based IO|Next]]