# Conditional Statements
### if-else / ternary
In programming, you often need to make a decision based on one or more factors, say the age old example of checking if an integer is even or not.
Here's how you would do it,
take some integer x, see if it is divisible by 2, _if_ it is you say that it is and _else_ you say it isn't. and if else statements in C (and most other programming languages) follow the same easy to follow structure.
The syntax for writing an if-else is as follows
```c
if (<condition>) {
	<thing to do>
} else {
	<thing to do if condition is not met>
}
```
**Note:** the else part of an if-else statement is completely optional

You can also check for different sets of conditions, say you have 3 conditions to check, you can chain together those conditions in the following manner

```c
if (<condition>) {
	<thing to do>
} else if (<different condition>) {
	<different thing to do>
} else if...
...
...
else {
	<thing to do if none of those conditions are met>
}
```

Now, the aforementioned even/odd example can be written as follows,
```c
// Assume x is some integer defined before here
if (x % 2 == 0) {
	puts("x is divisible by 2");
} else {
	puts("x is not divisible by 2");
}
```

as an example of an else-if chain, let's take fizzbuzz:
Take a number x,
- if x is divisible by 3, you print out `fizz`
- if x is divisible by 5, you print out `buzz`
- if x is divisible by both 3 & 5, you print out `fizzbuzz`
- if x is divisible by neither 3 nor 5, you print out x
```c
if (x % 3 == 0 && x % 5 == 0) {
	puts("fizzbuzz");
} else if (x % 3 == 0) {
	puts("fizz");
} else if (x % 5 == 0) {
	puts("buzz");
} else {
	printf("%d\n", x);
}
```

notice how we're calculating  `x % 3` and `x % 5` twice in two scenarios? (the ones where x is not divisible by 3, but is divisible by 5 and the case where it isn't divisible by either)

We can avoid that by using nested if statements (if statements within other if statements).

```c
if (x %3 == 0) {
	if (x % 5 == 0) {
		puts("fizzbuzz");
	} else {
		puts("fizz");
	}
} else if (x % 5 == 0) {
	puts("buzz");
} else {
	printf("%d", x);
}
```

Upon analyzing all possible scenarios, you'll see that the divisibility checks for 3 and 5 are each performed only once.

But it is to be noted that there a balance that needs to be struck between nesting and writing clean code.

Here are some tips to help you strike this balance:
1. **Don't overdo it**: Try to limit your nesting to 2-3 levels deep. If you find yourself nesting more than that, it might be a sign that your code needs to be refactored.
2. **Consider alternative approaches**: Sometimes, there are alternative ways to write your code that don't involve nesting. For example, you could use a switch statement or a lookup table instead of nested if statements.

Speaking of, let's move to the switch statement
### switch
Say you have a single variable that can be one of a few pre-defined values, like a grade
```c
char grade = ...; // One of 'O', 'A+', 'A', 'B+', 'B', 'P', 'RA'
switch (grade) {
case 'O':
	puts("91+");
	break;
case 'A+':
	puts("81-90");
	break;
case 'A':
	puts("71-80");
	break;
case 'B+':
	puts("61-70");
	break;
case 'B':
	puts("51-60");
	break;
case 'P':
	puts("41-50");
	break;
case 'RA':
	puts("Reappear");
	break;
default:
	puts("Invalid grade");
}
```

Here, break just tells your code to exit out of the switch statement when it is hit, break will be discussed a bit more [[6_Statements - if,while,for... etc.#break/continue|later in this topic]]. You might ask why not just do that by default? like why would you need to not break out of the switch statement after one of the conditions has been met, well it allows for a clever trick where you can use this to group together multiple cases with the same ouput.

```c
char grade = ...; // One of 'O', 'A+', 'A', 'B+', 'B', 'P', 'RA'
switch (grade) {
case 'o':
case 'O':
	puts("91+");
	break;
case 'a+':
case 'A+':
	puts("81-90");
	break;
case 'a':
case 'A':
	puts("71-80");
	break;
case 'b+':
case 'B+':
	puts("61-70");
	break;
case 'b':
case 'B':
	puts("51-60");
	break;
case 'p':
case 'P':
	puts("41-50");
	break;
case 'rA':
case 'RA':
case 'Ra':
case 'ra':
	puts("Reappear");
	break;
default:
	puts("Invalid grade");
}
```
Now we can match the grades being in any case, if the lower case 'b' matches it just "falls though" to the capital B case. You might ask but the grade isn't a capital 'B' how would that execute. you are entirely justified in that, but switch works a little bit differently to how you think, it doesn't check each case and then find the matching one and execute it. It just jumps to the matching case directly by doing [some big brain stuff](). and so it does only one jump to the matching case and executes everything else up until the first break statement it hits.
#TODO link a proper switch statement working explanation video
# Looping Statements
### while / do while### switch
Say you have a single variable that can be one of a few pre-defined values, like a grade
```c
char grade = ...; // One of 'O', 'A+', 'A', 'B+', 'B', 'P', 'RA'
switch (grade) {
​￼case 'O':
	puts("91+");
	break;
​￼case 'A+':
	puts("81-90");
	break;
​￼case 'A':
	puts("71-80");
	break;
​￼case 'B+':
	puts("61-70");
	break;
​￼case 'B':
	puts("51-60");
	break;
​￼case 'P':
	puts("41-50");
	break;
​￼case 'RA':
	puts("Reappear");
	break;
​￼default:
	puts("Invalid grade");
}
```

Here, break just tells your code to exit out of the switch statement when it is hit, break will be discussed a bit more [[6_Statements - if,while,for... etc.#break/continue|later in this topic]]. You might ask why not just do that by default? like why would you need to not break out of the switch statement after one of the conditions has been met, well it allows for a clever trick where you can use this to group together multiple cases with the same ouput.
#TODO link a proper switch statement working explanation video
### for

# Jump Statements
### break/continue
### return
### goto
[[7_Operators 3 - Relational operators|Next]]