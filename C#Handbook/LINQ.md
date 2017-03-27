Learning LINQ

List<int> numbers = new List<int> {2,4,8,16,32,64};
=> {2,4,8,16,32,64}
from number in numbers where number > 10 select number;
=> {16,32,64}
Also possible:
from n in numbers where n > 10 select n;
=> {16,32,64}

#LINQ queries must be in IEnumerable<T>
	This will not run:
	List<int> numbersGreaterThan10 =
		from n in numbers where n > 10 select n;
	
	This however will run w/o issue:
	IEnumerable<int> numbersGreaterThan10 =
		from n in numbers where n > 10 select n;
		
	LINQ queries won't run w/o enumerating through the desired data.
	
#LINQ's brand of sugar is very useful:
	BEFORE
	from b in birds where b.Color == "Red" select b;
	
	AFTER
	birds.Where((b) => b.Color == "Red");
	
	AFTER STILL
	birds.Where(b => b.Color == "Red");
	//This last one is only allowed on the condition that we have 1 parameter to worry about.
	
#####Another Example:
	from b in birds orderby b.Color select b;
	
	birds.OrderBy(b => b.Color);
	//pay attention to how the sugar needs 'OrderBy' instead of 'orderby'.
	
	birds.OrderByDescending(b => b.Color);
	
#####LINQ syntactic sugar also allows for method chaining:
	birds.Where(b => b.Color == "Red")
		 .OrderBy(b => b.Name);
		 
#####To enumerate anon types:
	birds.Select(b => new { b.Name, b.Color });
	//For anon types it is imperitive that you use the 'Select' keyword.
	
#####Standard Query Operators
	Any - check if at least one objects match; can be used to check if object exists before continuing to process a function:
				   [relates to the delegate]
		if (!birds.Any(b => b.Name == "Crow"))
		{birds.Add(new Bird {Name = "Crow"});}
		//This method will stop at the first 'true' instance of the condition.
			[Example2:]
		var anyBlueBirds = false;
		if (birds.Any(b => b.Color == "Blue"))
			{ anyBlueBirds = true; }
	
	Contains - check if at least one objects match; this quantifier does not require a predicate delegate and instead passes an object to check against:
				   [relates to the object]
		if (!birds.Contains(sparrow))
		{birds.Add(new Bird {Name = "Sparrow", Color = "Brown"});}
		
	All - check if all objects match; has the ability to check that all the objects within a collection pass/have a test/condition:
				[relates to the delegate]
		birds.All(b => b.Name != "Sparrow");
		//Think of a reverse 'Any' statement
		//This method will stop at the first 'false' instance of the condition.
		
	Single - can be used to check simple inqueries and return a single result; very similar to the 'Where' method:
			[Example1]
		birds.Where(b => b.Name == "Crow").Single();
			[or]
		birds.Single.(b => b.Name == "Crow");
			[if defensively coding]
		birds.SingleOrDefault.(b => b.Name == "Falcon");
		//This will prevent an error from being thrown and will return a null value.
		
	First or Last - the name says it all:
			[Example1]
		birds.First();
			[Example2]
		birds.Last(b => b.Color == "Red");
			[Example3]
		birds.FirstOrDefault(b=>b.Color=="Gold");
		
	ElementAt - similar to calling the index of an item within an array however it will work when LINQ index inqueries won't such as the result of a LINQ query, which is a pure enumerable.
			[Example]
		var redBirds = birds.Where(b => b.Color == "Red");
			[This won't work]
	X	redBirds[0]; //The reason being is because it is a pure enumerable, think of it as an anon type.
			[Answer]
	O	redBirds.ElementAt(0);
		//This works -- just because. Remember 'OrDefault' will also work here.
		
	Take - selects a number of items from the beginning of the collection:
			[Example]
		birds.Take(3);
		
	Skip - skips a number of items from the beginnin of the collection, useful when omitting outliers before processing:
			[Example]
		birds.Skip(2).Take(3);
		
	TakeWhile and SkipWhile - requires a conditiont to test against and will stop as soon as it fails:
			[Example1]
		birds.OrderBy(b=>b.Name.Length).TakeWhile(b=>b.Name.Length<7);
			[Example2]
		birds.OrderBy(b=>b.Name.Length).SkipWhile(b=>b.Name.Length<7);
		
	