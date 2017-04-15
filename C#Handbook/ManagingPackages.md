Package Manager Console
	
#	enable-migrations

#	add-migration <name>
		Ex:		add-migration Initial
		-additionally you may use the '-force' flag to overwright/restart the migration. Ex:
				add-migration Initial -force
				
#	update-database
		-when doing so you must create a 'seed' to be planted whenever this code is ran. Ex:
		
		protected override void Seed(Context context)
		{
			context.Roles.AddOrUpdate(
				r => r.Name,
				new Role() {Name = "Script"},
				new Role() {Name = "Pencils"}
				);
		}

#	update-database -targetmigration <name>
		-this will revert the database to the time-stamped instance of the named migration. Ex:		update-database -targetmigration Initial
		-think of how git works
		
#	#if DEBUG (followed by) #else (ended with) #endif
		-this is what's known as a pre-processor directive. They basically variablize code to be used within certain contexts. This one specifically is used to differentiate code to only be active when the solution is in the DEBUG state, and will comment out the code when the solution exists in any other state (release, test, etc...). These commands do NOT require simicolons (;).

#	update-database -script
run that to open a dedicated window to see the migration script