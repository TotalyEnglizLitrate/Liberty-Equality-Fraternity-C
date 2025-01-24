# Relational operators
Relational operators are used to compare two values and determine their relationship. They are used to control the flow of a program by making decisions based on the relationships between values.
The following are the relational operators available in C:
- `==` (Equal To)
- `!=` (Not Equal To)
- `>` (Greater Than)
- `<` (Less Than)
- `>=` (Greater Than or Equal To)
- `<=` (Less Than or Equal To)
```c
int a = 10;
int b = 5;

if (a == b) {
    printf("a is equal to b\n");
} else {
    printf("a is not equal to b\n");
}

if (a != b) {
    printf("a is not equal to b\n");
} else {
    printf("a is equal to b\n");
}

if (a > b) {
    printf("a is greater than b\n");
} else {
    printf("a is not greater than b\n");
}

if (a < b) {
    printf("a is less than b\n");
} else {
    printf("a is not less than b\n");
}

if (a >= b) {
    printf("a is greater than or equal to b\n");
} else {
    printf("a is not greater than or equal to b\n");
}

if (a <= b) {
    printf("a is less than or equal to b\n");
} else {
    printf("a is not less than or equal to b\n");
}
```

# Logical operators
Relational operators can be chained together using logical operators to create more complex conditions, because, most things in our world are not decided by one single factor, logical operators offer a way to mix and match between many factors or conditions.
The following are the logical operators available in C:
- `&&` (Logical AND)
- `||` (Logical OR)
- `!` (Logical NOT)

```c
int a = 10;
int b = 5;
int c = 15;

if (a > b && a < c) {
    printf("a is greater than b and a is less than c\n");
} else {
    printf("a is either not greater than b or is not greater than c (or both)\n");
}

if (a > b || a < c) {
    printf("a is greater than b or a is less than c\n");
} else {
    printf("a is neither greater than b nor less than c\n");
}

if (!(a > b)) {
    printf("a is not greater than b\n");
} else {
    printf("a is greater than b\n");
}
```


[[8_Operators 4 - Misc Operators|Next]]