Learning SQL
	Popular SQL systems
		MySQL
		Microsoft SQL Server
		Oracle
		PostgreSQL
		SQLite
		
	Best practices:
		While not required, its most common in the industry to capitalize the key words used within the SQL code.
		
		
Writing in SQL:
	#Syntax rules:
		text - requires ""
		date - requires ""
		numeric - no "" or spaces
		
	#Simple query string:
		SELECT * FROM books;
		-SELECT = get info from
		-* = all available info from all the columns within the table
		-FROM = signifies which specific table
		-books = name of the table
		
		SELECT column FROM table;
		-Use the above for specific info
		
		SELECT column, column FROM table;
		-To retrieve multiple specific columns from a table.
		
		SELECT columnName AS newName FROM table;
		-This will give the columns new alias names but will not alter any info within the tables.
		
		SELECT column FROM table WHERE column = or != value;
		-Use this to filter through the columns within a table by the type of values within one of the columns.
		
		SELECT column FROM table WHERE condition OR/AND condition;
		-This is how you can string multiple conditions into the same query string.
		
		SELECT column FROM table WHERE column IN (value1, value2...);
		SELECT column FROM table WHERE column NOT IN (value1, value2...);
		-Use either of these to evaluate multiple values against a condition.
		
		SELECT column FROM table WHERE column BETWEEN value1 AND value2;
		-Use this method example to set a range to retrieve data from within.
		
		SELECT column FROM table WHERE column LIKE "value%";
		-Use this method to query relative matches, you MUST add the '%' at the end however as a place holder or 'Wild Card' so that the computer understands that any additional unknown value may go there.
		-For relative matches you don't have to be case sensitive or remember all the workds needed. Just place a % in the direction of the missing words:
			"The Crazy%" => "The Crazy Farmer"
			"%Crazy Farmer" => "The Crazy Farmer"
			"%Crazy%" => "The Crazy Farmer"
		
		SELECT column FROM table WHERE column IS/IS NOT NULL;
		-Use this method to query results that are representitive of:
			for IS = void of information
			for IS NOT = contain some kind of info
		
		SELECT column FROM table1, table2
			WHERE table1.column = table2.column;
		-Use this method to return a set of data from 2 tables that have corrosponding column info; like book id's, similar pricing across departments, etc...
		
		INSERT INTO table VALUES (value1, value2, value3...);
		-Use this to add info to a table, with this setup you must have the correct corrosponding values to match up with each column that they'll be populating.
		-It may be possible to utilize NULL to enter a 'void of info' value to a specific column, however this is not always applicable.
		-Also in specific situations NULL may also be used to auto populate an entry within the table; Ex: using NULL wher an 'id' integer is called for, if the creator ot the table set up an auto property within this column then it would be possible to use a NULL value here and it would automatically populate the next entry with the included information. This is especially useful when you have multiple entries coming in at once and not necessarily from the same source.
		
		INSERT INTO table (column1, column2, column3...)
			VALUES (value1, value2, value3...);
		-Use this method logic to specify where different info may be added within the table schema. So long as you match up the correct column to its corrosponding value you will not run into issues:
			O (column1, column3, column2) (value1, value3, value2)
			X (column1, column3, column2) (value3, value1, value2)
		-Additionally you may use this logic to omit info instead of using the NULL keyword:
			(columnId, column1, column2) (NULL, value1, value2)
			(column1, column2) (value1, value2)
		
		INSERT INTO table (column1, column2, column3...)
			VALUES
				(value1, value2, value3...),
				(value1, value2, value3...),
				(value1, value2, value3...);
		-Use this to add multiple sets of data into the table schema.