#Four Fundamental Operations
	There are many different types of collections within the .NET framework. To choose which one to use consider which of these Operations you are most concerned with.
	Other things to consider:
		Size of the collection and the data within.
		The importance of the order of the items within the collections.
		How quickly items within the collections can be copied from one to another.
Insert

Access / Find

Update

Delete

csharp>REPL
	class Cell
		{
			public string Contents {get; set; }
		}

#Arrays
	An indexed/numbered list of items. When creating an array you must tell it what the maximum number of items within the array will be.
When creating an array you can use the statements below:

int[] arrayName = new int[3];
	This will initialize a new array that will contain integers and contains 3 items. Since no values have been provided for the items within this array their default value will be [0, 0, 0]. If this were any other kind of array their default values would've been 'null'.
int[] arrayName = new int[] {2, 4, 6};
	This array doesn't need to be told how many different items it'll contain because you've defined it's contents when you initialized it.
	Additionally this new array can also be created like this
		int[] arrayName = {2, 4, 6};
	since it was declared that this array would contain integers it doesn't need to be defined once more, and since you are adding in the values as soon as you initialize this array the 'new[]' becomes uneeded as well.
	
#LOOK UP THE DIFFERENCES BETWEEN JAGGED AND MULTIDEMENSIONAL ARRAY#

---Arrays are useful when constructing a fixed matrix of items and/or variables however they aren't that useful when it comes to flexible situations in which you would need to add items into the array w/o already having accounted for that extra information in the first place.
	---Ex: int arr = new int[3];
		This array cant have another item added to it, [4] instead of [3], to do so you would need to create a new array -> copy older contents into it -> then overwrite the previouse array with the new one. On top of that you would have to go back and update every instance in which the array and its items within it would've been called within your application.
		
#LISTS
	A special type of class called a 'generic' this allows the list class to be a collection of any type of objects. Using the List class you don't need to specify the total number of items within the collection. Another benefit of a list is that you can itterate through them using any kind of loop that you like.
	
How to make a list:
	List<'type of object'> listName = new List<'type of object'>();
		Ex:	List<string> students = new List<string>();
		
	To add items to the end of a list:
		listName.Add('item');
		
	To insert an item into the list:
		listName.Insert(index, 'item');
		This inserts the desired item at the specified index and moves everything after it down one.
		
	To remove an item w/o knowing the index:
		listName.Remove('item');
		This will search through the list, and call RemoveAt on the index of the first item within the list that matches the item-name that you passed through the argument.
		
	To sort a list:
		listName.Sort();
		This method will automatically choose the best method to sort the items w/n a consistant list, all numbers, all strings, all doubles, etc...
		
	