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
if (x % 3 == 0) {
	if (x % 5 == 0) {
		puts("fizzbuzz");
	} else {
		puts("fizz");
	}
} else if (x % 5 == 0) {
	puts("buzz");
} else {
	printf("%d\n", x);
}
```

Upon analyzing all possible scenarios, you'll see that the divisibility checks for 3 and 5 are each performed only once.

But it is to be noted that there a balance that needs to be struck between nesting and writing clean code.

Here are some tips to help you strike this balance:
1. **Don't overdo it**: Try to limit your nesting to 2-3 levels deep. If you find yourself nesting more than that, it might be a sign that your code needs to be refactored.
2. **Consider alternative approaches**: Sometimes, there are alternative ways to write your code that don't involve nesting. For example, you could use a switch statement or a lookup table instead of nested if statements.

Speaking of, let's move to the switch statement
### switch
Say you have a single variable that can be one of a few pre-defined values, like a grade,
here's how you would use a switch statement to print out the corresponding marks
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
Now we can match the grades being in any case, if the lower case 'b' matches it just "falls though" to the capital B case. You might ask but the grade isn't a capital 'B' how would that execute. you are entirely justified in that, but switch works a little bit differently to how you think, C takes care of the shared execution when you have "fall through" cases such as this one. Moreover, it can do some black magic to jump directly to the desired case without any comparisons at all in some cases (if the compiler can figure out a way to do that, do note that this is highly dependent on your code).
# Looping Statements
### while / do while
In many places, you have to not just check and do something based on a condition, but you have to repeat it again and again as long as the condition is true.
Take a lays factory for example, at the final packaging stage, the production line keeps running as long as there is
- chips to go in packets
- packaging material to be shaped into the packets
The production keeps chugging on. Similarly, there are a lot of places in code where you want to do something repeatedly for as long as a condition is true. 
for example, take calculating the number of digits in a given number.
**Note:** integer division truncates (or floors)
```c
int x = ...; // some integer
int digits = 0
while (x != 0) { // As long as x is not 0, divide it by 10
	x /= 10;
	digits++; // increase the digit count everytime you divide it by 10
}

/*
  When x becomes zero a total of n division operations will have occured,
  where n is the number of digits, and since the digits variable
  has been incremented once per divison, it contains the number of digits as well.
*/
```

there are also do-while statements that are for the same purpose except the very first time the loop executes without checking the condition and only checks the condition from the second iteration.

```c
int num;
do {
	printf("Input a number between 1 and 10: ");
	scanf("%d", &num); // just reads in input to num.
} while !(num < 1 || num > 10);
```

In the above example,
- The variable `num` is not initialized before the loop, so it doesn't have a valid value.
- If this were a while loop, the condition `num < 1 || num > 10` would be checked before the code inside the loop is executed. Since `num` is not initialized, this condition would be undefined behavior.
- By using a do-while loop, the code inside the loop is executed at least once, which allows the user to input a value for `num`.
- After the first iteration, the condition `num < 1 || num > 10` is checked, and if it's false, the loop continues. If it's true, the loop exits. (because of the `!` negation)
### for
You can also have to do a task repeatedly, but for a defined number of times, say printing out all the even numbers between 0 and 100 (inclusive), you can use a for loop to do so.

```c
for (unsigned int i = 0; i <= 100; i = i + 2) {
	printf("%u", i);
}
```
here the for loop has three things separated by a `;`
- The first bit is the initialization statement, it is executed once at the very start of the for loop - can be any valid assignment statement.
- The second one is a check, executed every single time and the for loop ends when the condition is no longer met - can be anything (since C can interpret anything as true or false).
- The third bit is the modification statement - can be any valid assignment statement.
All three statements are completely optional.

You can even have multiple variables since any valid assignment statement is allowed
```c
for (int i = 0, j = 10; i < 10; i++, j--) {
	printf("i = %d, j = %d\n", i, j);
}
```

And yes, any for loop of the form
```c
for (<initialization>;<condition>;<modification>) {
	...
}
```
can be modified into a while with the following structure
```c
<initalization>
while (<condition>) {
	...
	<modification>
}
```
# Jump Statements
### break/continue
### return
### goto
[[7_Operators 3 - Relational operators|Next]]