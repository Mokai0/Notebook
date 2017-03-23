ActionResult -> Most common type of return type for action methods, since all the MVC action result types share the ActionResult base class.

ViewBag -> Is an object provided by MVC that allows you to pass data from a controller to a view. This means that you'll be passing data in the form of a property on the ViewBag object and therefore by convention you should capitalize the name of each property that you pass through.
	This is one of the few true dynamic controllers used by C#.
	Be very careful when using ViewBag because if you have a typo there won't be an error, things just won't appear.
	
Look up Elmah.MVC in the NuGet Package Manager