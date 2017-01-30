REPL: Read Evaluate Print Loop
	-launch using the mono interpreter and run: csharp
	-think of it as the V8 console within chrome
	
You can't expect integers and doubles (decimal numbers) to play nice with each other
	int x = 9/6 will compile successfully
	int x = 9/6.0 will not however, the reason being that the process of (9/6.0) will return a double, and you are trying to store x as an integer. That being said it is possible if you call the 'cast' method. Example: int x = 9/(cast)6.0 would compile correctly since it forces the double into an integer.
	
Compile time inference: basically some methods don't need a declaration of what type of input they'll receive.
	ex1: instead of:
		string entry = Console.ReadLine();
	it would be:
		var entry = Console.ReadLine();
	var isn't a keyword but Console.ReadLine() can only accept a string as an input and therefore this is valid.
	ex2: instead of:
		double runningTotal = 0;
	try:
		var runningTotal = 0.0;
	the runningTotal method knows that the input must be a number however in this case it's important to note that we want a double and therefore must set the method equal to '0.0' instead of '0'. This is because runningTotal doesn't explicitly accept a double and will by default only accept an integer if '0' was declared. By declaring that the method is equal to a double it will use such input as it's guideline for future input.
Effecting a variable to itself is very simple in C# and while it can be redundant there is a simple shortcut:
	bank = bank + money; -> bank += money;
	bank -= money;
	bank *= money;
	bank /= money;
	bank %= money;
