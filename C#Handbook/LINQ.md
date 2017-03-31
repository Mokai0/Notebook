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
		
#####Elements Operators
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
		
#####Partioning Operators
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
		
#####Joins
	Join - allows you to process multiple conditions in conjuction with one another:
				[Example in query syntax]
		var colors = new List<string> { "Red", "Blue", "Purple" };
		var favoriteBirds = from b in birds
			join c in colors on b.Color equals c
			select b;
				[Example in method syntax]
		var favoriteBirds = birds.Join(colors,
			b => b.Color,
			c => c,
			(bird, color) => bird);
						
	GroupJoin - Don't really understand why diff from Join
			[Example]
		var groupBirds = colors.GroupJoin(birds,
		c => c, b=> b.Color,
		(color, bird) => new { Color = color, Birds = bird });
		
	SelectMany - presents flattened data - like a reverse group - and allows it's catagories to be more appropriately searched:
			[Example]
		groupBirds.SelectMany (g => g.Birds);
	
	GroupBy - 
			[Example in query syntax]
		from b in birds
		group b by b.Color;
			[Example in method syntax]
		birds.GroupBy(b => b.Color);
			
#####Aggregate Operators
	Count - definitely useful:
			[Example]
		birds.GroupBy(b => b.Color).Select( g => new {Color = g.Key, Count = g.Count() });
		
	Sum Average Min Max - they're exactly as they sound:
			[Example]
		birds.Sum(b => b.Sightings);
			[Example2]
		birds.GroupBy(b => b.Color)
		.Select(g => new { Color = g.Key, 
		Sightings = g.Sum(b => b.Sightings)});
		
#####Set Operations
	Distinct - examining a single sequence and returns unique elements:
		[Example]
	birds.Select(b => b.Color);
	-result-{"Red", "White", "Red", "Blue",
			"Yellow", "Black", "White}
	birds.Select(b => b.Color).Distinct();
	-result-{ "Red", "White", "Blue", "Yellow", "Black" }
	
	Except() - returns the difference that lives in the first of the 2 paramaters passed through the operator:
			[Example]
		var colors = new List<string> {"Pink", "Blue", "Teal"};
		colors.Except(birds.Select(b => b.Color)
			  .Distinct());
		-result-{ "Pink", "Teal" }
		
	Intersect() - returns all shared items between the paramaters:
			[Example]
		colors.Intersect(birds.Select(b => b.Color)
			  .Distinct());
		-result-{ "Blue" }
		
	Union() - returns all the items in question, preserving unique items only:
			[Example]
		colors.Union(birds.Select(b => b.Color));
		-result-{ "Pink", "Blue", "Teal", "Red", "White", "Yellow", "Black" }
	
	Concat() - returns everything, concatination is the name of the game:
			[Example]
		colors.Concat(birds.Select(b => b.Color));
		-result-{ "Pink", "Blue", "Teal", "Red", "White", "Red", "Blue", "Yellow", "Black", "White" }
		
#####Generation Operators
	Range(starting#, #ofLoops) - think 'for loops'; 
		ONLY works with integers:
		var numbers = new List<int>();
			[Example of 'for loop']
		for(int i = 0; i < 10; i++)
			{numbers.Add(i);}
			[Example of Range]
		var numbers = Enumerable.Range(0, 10);
		
	Repeat(itemToRepeat, #ofTimes) - will repeat declared item declared number of times:
			[Example]
		Enumerable.Repeat("LINQ is awesome!", 10);
		
	Empty<type>(); - will generate an empty enumerable
			[Example]
		var emptyBirds = Enumerable.Empty<Bird>();
		
	DefaultIfEmpty() - creates an empty enumerable w/o the need for a type. This will also return the elements of the specified sequence or the type parameter's default value in a singleton collection if the sequence is empty:
			[Example]
		var numbers = Enumerable.Empty<int>();
		-result-{ }
		numbers.DefaultIfEmpty();
		-result-{0}
	
#####Conversion Operators
	ToList();
	ToArray();