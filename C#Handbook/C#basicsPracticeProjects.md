Practice Projects

Averager

Repeatedly prompt the user for numbers. Add all of the numbers together. When the user types in “done”, print the average of all of the numbers by dividing the total by the number of numbers entered.

treehouse:~/workspace$ mcs Program.cs && mono Program.exe
Enter a number or type "done" to see the average: 5.5
Enter a number or type "done" to see the average: bogus
That is not valid input.
Enter a number or type "done" to see the average: 4.2
Enter a number or type "done" to see the average: 99
Enter a number or type "done" to see the average: done
Average: 36.2333333333333
treehouse:~/workspace 


Interactive Quiz

Write an interactive quiz. It should ask the user three multiple-choice or true/false questions about something. It must keep track of how many they get wrong, and print out a "score" at the end. 


Arithmetic Calculator

Create a calculator that does one arithmetic operation at a time and prints the result to the screen. 


Prompt the user for a number.
Prompt the user for an operation (+ - / *).
Prompt the user for another number.
Perform the operation.
Print the result to the screen.
Repeat until the user types in “quit” at any of the prompts.
Extra Credit: Add the power operator using the ^ symbol. You can calculate a number raised to a power using the Math.Pow method. 


Math Function Calculator

Prompt the user for a math function such as sine, cosine, tangent, square root, logarithm, etc. Then prompt the user for the function's parameter. Perform the function and print the result back to the screen.

Use .NET’s Math class to do perform the math for you.