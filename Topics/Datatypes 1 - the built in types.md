### Note
Before we start, I am assuming a 64 bit system when discussing the sizes of the the datatypes, it might differ on 32 bit or lower systems. you can look up the differences if you so desire.

# What are datatypes?
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

## The Meaning of Void
The term "void" literally means "empty" or "without value". In the context of C programming, `void` is used to indicate that a function or expression does not produce a value. For now, that much information will suffice about void, though we have a couple extra places where void comes into play.

## Typecasting

## Type Modifiers

[[Operators 1 - Arithmetic and Bitwise operators|Next]]