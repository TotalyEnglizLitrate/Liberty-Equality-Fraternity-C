
The previously discussed [[1_Hello World!#^388301|Hello World]] has a lot of stuff that you have to just accept as is, practically the entire program. Though I will get to explaining all the bits eventually, it's going to stay that way for a while. We are just going to talk about this piece of code here (and it's variations).

```c
int main(void) {
	return 0;
}
```


Before we start, let's skip ahead a bit and read up on [[16_Functions 1 - an introduction#^14c3c5|what a "function" is]].
Done? Alright, let's continue.

Now that we know what a function is, we can break this down.
`main` - this is the alpha of our C program (and most compiled programs) hell, even python has `if __name__=="__main__":...`. 
`main` is where it all starts i.e where your code's starting point is, and as such it is called the 
**entry point** of our program.

So, why main? well, the answer is, just coz 🤷
In all seriousness, "just coz" actually means convention here. convention being something that is agreed (or convened) upon by everyone (or atleast a significant portion of everyone).

You can [[2_Why Main#^edf75b|skip over]] the next bit if you want to, isn't strictly relevant
## A history of main

The concept of main being a starting point probably stemmed from the idea of a main "routine" in IBM PC's in the days before C, or UNIX for that matter. When UNIX was being created, it would just look at a program and executing it from the very start, this had some technical limitations and so the idea of a custom starting point was introduced, and it was called main borrowing the name from the IBM PC's main coroutine.

`main`'s role as the entry point of a program was later set in stone when the creators of C (who were also responsible for UNIX) decided to set main as the entry point, and pretty much all other languages that came later followed this convention.
## Variations of main
^edf75b

 There are a few variations of main that are valid in modern C standards.
 **Note:** C is still evolving as a language, just like any other piece of software like whatsapp, or youtube receive updates, so do programming languages.
 The currently widespread C standard is C17/C23 which were published in 2018 and 2024 respectively
 
back to the different forms of main

A little bit of setup - We know main is the entry point, `{}` denotes the "body" of the function i.e the actual code it executes. `()` encloses the arguments that are passed to the function, `return` returns some value (or maybe no value at all) from the function. it is the "result" of the function, so to speak. `int`/`void`/`char` are data types in C, i.e they denote what is the "type" of value they are storing, `int` is an integer, `void` is nothing (empty, void), `char` is a character.

```c
int main(void) { // same as int main()
	return 0;
}
```

Here the `int` denotes the return type of the function, i.e the function returns a value that is an integer.

As for the arguments, `()` and `(void)` are equivalent, they both denote that the function does not take any arguments at all.

Now, the return value, we know it returns an integer, and we're returning 0 by default in pretty much all programs, but where is this returning to? and why are we defaulting to 0? can we return something else?

Again, this concept is more convention than a rule, but the idea of status/exit codes come into play here.

Basically your program cannot just run just like that, in one way or another, it has to be "invoked" by someone/thing else in order to start and then do it's thing. Now after the program is done, it returns this value from the main function to whatever called the program. Let's say you compile and run the following piece of code in your terminal

```c
int main(void) {
	return 1;
}
```

You can get the return value of this program from your terminal
If you're on bash, you can use the `?` variable that stores the exit code of whatever program that was previously run.

```sh
engliz@lattitude5491 ~ $ /tmp/ret_0
engliz@lattitude5491 ~ $ echo $?
0
engliz@lattitude5491 ~ $ 
```

If you change the code to return some other integer, say 1, or whatever your heart desires
(\*not exactly, integers do have some limitations, which will be discussed in [[3_Datatypes 1 - the built in types|Datatypes 1]])

```sh
engliz@lattitude5491 ~ $ /tmp/ret_1
engliz@lattitude5491 ~ $ echo $?
1
engliz@lattitude5491 ~ $
```

On non bash shells, consult the documentation on how to get the status codes, here are some common ones

| shell       | variable       | accessing variables | echoing              |
| ----------- | -------------- | ------------------- | -------------------- |
| bash/zsh/sh | `?`            | `$variable`         | `echo $?`            |
| fish        | `status`       | `$variable`         | `echo $status`       |
| powershell  | `LastExitCode` | `$variable`         | `echo $LastExitCode` |
| cmd         | `ERRORLEVEL`   | `%variable%`        | `echo %ERRORLEVEL%`  |
Now that we know where the return value of main goes to, how about what it means, and why (or why not) 0?

These exit codes represent if the program ran as intended, or ran into some error/problem etc.
`0` - Conventionally means everything went smooth, no errors or issues.
Anything else indicates an error, it is upto the program to define the number -> specific error relationship, though there are some standardized error code lists out there.
So our return value goes back to whoever called the program, and indicates if the program ran fine, and if it didn't, it can possibly indicate as to what exactly went wrong.

Another variation is,
```c
void main(void) { // same as void main()
	return;
}
```

Here, everything is the same as before, except we return `void` i.e nothing, here the status code is not a predictable value, and will vary depending on your compiler and/or OS and/or shell. It is not documented, and should be treated as undefined behaviour i.e it cannot be predicted and it's functionality should not be relied upon as it is not deterministic (i.e it's output is not predetermined under a given set of circumstances) or in simple terms, it is not consistent.

As mentioned above, it is convention to have a exit codes indicating success/failure, using void main is not recommended as it essentially throws out the concept of exit codes out the window due to the unpredictable default and lack of ability return different values for indicating failure.

A couple other variations are,

```c
int main(int argc, char *argv[]) { // same as int main(int argc, char **argv)
	return 0;
}
```

```c
void main(int argc, char *argv[]) { // same as void main(int argc, char **argv)
	return;
}
```

In short, this allows you to access what are known as command line arguments, as an example let's look at the cp command

```sh
engliz@lattitude5491 ~ $ cp path/to/source_file path/to/destination_file
```

here, `path/to/source_file` & `path/to/destination_file` are "command line arguments",
they are essentially passed to main using the two variables `argc` & `argv`. Where `argc` is the number of arguments passed in and `argv` is a list of the arguments (**Note:** it includes the programs name as well). So in the above example, `argc` would be 3 and`argv` would be `[cp, path/to/source_file, path_to_destination_file]`.  We will look at the reasoning behind the type of `argc` and `argv` at a later point, along with the internal representation of `argv`. #TODO link to the later points after it's done

void is discouraged in this form as well due to the same reasons.

[[3_Datatypes 1 - the built in types|Next]]