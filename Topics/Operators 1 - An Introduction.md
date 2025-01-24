### Let's Make the Computer Do the Heavy Lifting
Okay, now that we have an idea of the various types of data that we can store/represent in C, how do we do operations on it? Well, we have a variety of operators at our disposal, let's have a look.
Refer to [this](https://man7.org/linux/man-pages/man7/precedence.7.html) page for a list of all operators with their associativity and precedence.

### List of operators
Here's what they do, just look up their functionality because this is just going to be a 1 sentence description of their working. (In the order of the manpage)
`[]` - indexing operator
`()` - various places, mostly to mark explicit precedence of operations especially when deviating from the standard precedence

`.` - structure member access
`->` - structure member access via pointer, (say you have a pointer to a struct and you want to access it, you'd use this). 
- `(*<struct pointer>).<member>` => `<struct pointer>->member`

`++`, `--` - postfix increment and decrement, uses the variable in the current statement, and then increments/decrements it by 1.
`++`, `--` - prefix increment and decrement, increments/decrements the variable by 1, and then uses it's value in the current statement.

`&`, `*` - `&` takes in an identifier and returns a pointer to the identifier, `*` takes in a pointer and returns the value stored at the corresponding memory address.

`+`, `-` - Unary plus and minus operators denote the sign of a number.

`~` - Bitwise not, flips all the bits of a member i.e 0s become 1s and vice-versa
`!` - Logical not, flips a true value to false and vice-versa.
- **Note:** C doesn't have boolean values out of the box, so 0 is false and anything else is true, you can access boolean types by including the `stdbool.h` header.

`sizeof` - takes in a datatype/variable and returns the amount of memory it takes up in bytes
- **Note:** This is a compile time operator, i.e the size of the argument is calculated when you compile the program and is substituted in.

`(<type>)` - type casting operator, already discussed.

`*`, `/`, `%` - Arithmetic multiplication, division and modulo
`+`, `-` - Arithmetic addition and subtraction
`<<`,`>>` - Bit shift operators, shifts the bits of a variable in the direction specified, by the amount specified.
`<`, `<=`,`>`,`>=` - Relational operators, less than, less than or equals etc.
`==`,`!=` - Equality/Inequality operator, checks if two things are the same (or) not same
- `!=` => `!(<a> == b)`

`&`,`^`, `|`, - Bitwise AND, XOR and OR operator, does the specified bitwise operation on each bit of the two operands and returns the result.

`&&`,`||` - Logical AND and OR operator, follows boolean logic.

`?:` - Ternary operator, `<condition> ? <expression 1> : <expression 2>`
- boils down to the following
```c
if (<condition>) {
	<expression 1>;
} else {
	<expression 2>;
}```

`=` - assignment operator, assigns a value to a variable.
- **Note:** can be chained like `a = b = c = 3;`

`*=`,`/=`,`%=`,`+=`,`-=`,`<<=`,`>>=`,`&=`,`^=`, `|=` - augmented assignment operators,
- `a <operator>= b;` => `a = a <operator> b`

`,` - used to separate in specific places.

[[Operators 2- Arithmetic and Bitwise Operators|Next]]