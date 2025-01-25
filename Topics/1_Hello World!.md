## An Introduction

So, you have decided you want to actually learn and understand C and not just get marks. Welcome! or rather, Hello, ~~World~~ Batch of '29 👋.

Let's get this out of the way, this is in no way a comprehensive guide to C. I am not even close enough to being well versed enough in C to create such a thing. What this will do is cover (almost) all the topics you are going to have in your syllabus, and then maybe go a bit deeper.

However, we are not looking to just say this is `x`, use it. If this guide achieves what I want it to, by the end of each topic. You will know
1. What `x` does.
2. Why/How so?
3. If it is contrary to the logical explanation, why does it do it this way?

This guide does take some liberties and assumptions and I suggest you look up anything you do not understand, however whatever I feel needs to be explained in depth is done in a complete (I atleast hope that it does) manner.

## The Beginning
^388301

So, without further ado! Let us begin!

The first bit of code we're going to look at is obviously going to be a Hello world program.

```c
#include <stdio.h>

int main(void) {
	puts("Hello World!");
	return 0;
}
```

***Assumption: You have a c compiler and an editor installed and know your way around the terminal, if you don't, here are my recommendations***
1. mac - gcc
2. windows - preferably try gcc under wsl, if you cannot figure it out, feel free to reach out to me (though exhausting your other options before you do so will be appreciated), if wsl is not an option, fall back to mingw64 - the gcc port for windows
3. linux - install gcc but, how are you on linux and not be atleast a little bit familiar with the terminal my guy?
4.  \*bsd - just. why?
5. android - you're a CSE student. **GET. A. LAPTOP.** but until then, use termux. (with gcc)
6. ios - don't even bother
7. you cannot reasonably be on any other platform
In short, use gcc, as for the editor, vscode is good for getting started on (**Visual Studio Code** and not **Visual Studio**, yes, ik, blame microsoft), but use whatever your heart desires (as long it isn't emacs)

## Compiling
Compiling, in general is a thing used to describe collecting data and presenting it in a different manner, usually one that is easier to comprehend to the one being presented with said "compiled" data. In the context of compiled programming languages, a compiler "compiles" the source code to machine code, which the machine understands.

there are a crapload of options in the gcc compiler, however we will only be looking at the following
`gcc /path/to/src/file -o /path/to/compiled/program`
breaking this command down, we are calling gcc with the following parameters.
1. `/path/to/src/file` - what file(s) to compile
2. `-o` - Flag to set output executable path
3. `/path/to/compiled/program` - path to output executable, which is the argument to the `-o` flag.
To get a grasp on paths, read [[Paths|this tangent on it]].

running the compiled program is as easy as typing the (relative or absolute) path of the compiled binary into your shell.

Back to hello world,
if you compile this code and run it,
you (ought to) get the following output

```bash
engliz@lattitude5491 ~ $ /tmp/hello_world 
Hello World!
engliz@lattitude5491 ~ $ 
```

We have "put" a string, onto the terminal. puts will be covered in a [[9_IO 1 - Terminal based IO|later]] topic

[[2_Why Main?|Next]]