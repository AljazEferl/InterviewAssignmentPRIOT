# InterviewAssignmentPRIOT

# Answers 
1. How could we adjust the API to show user's personal results?

   First of all we should use some authentication like QR code (different for every user), this will provide us UserID for every measurement that will save to database, with all elements other elements. 
   I would add UserId to Measurement class. Then I would need to change GetFastestLaps method, it will need to accept UserId so that I can get the fastest lap of each person. So before calling fastest lap
   method, I would need to retrive user informations based on UserID and then pass the retrieved measurements as the argument in the GetFastestLaps method.

2. What's the time complexity of finding fastest laps? Could it be improved?
  
   Now the complexity of finding fastest lap is next. First I group measurement by rfid then sort by date in ascednig order and calculating the duration between measurements. i have seen that the time complexity
   can be improved with min-heap to find minimum duration faster. 

3. Is the project code appropriate for use with a database (instead of in-memory saving)? If not, what would we have to
   change to allow calculations saving and querying on database level? (imagine we have 1M entries in the database, what would be your approach?)
   
   The project code is not appropriate for use with database, we would need to make some changes. If we would have a lot of users I would use NoSql database like MongoDB, because from my past MySql has a lot of
   limits. But for project like this with small amount of users this can work with MySql database. For big project we need to go step by step, we need to create ER model with tables, columns and foreign keys, then we set up
   environment. We need to save UserID, rfid, date. Method GetFastestLap would work on a data from database not on memory saving. If we have a lot of data I wuold use chunks this will provide us faster working algorithm. 
   I would delete not used data from database.
   
   For connection I would use this: 
   ```using System.Data.SqlClient; 
      public DatabaseConnector(string connectionString)
        {
            this.connectionString = connectionString;
        }
        // Open the database connection
        connection.Open();
        
        // Perform database operations
        string query = "SELECT * FROM YourTable";
        SqlCommand command = new SqlCommand(query, connection);
        SqlDataReader reader = command.ExecuteReader();

         // Process the query results
         while (reader.Read())
         
4. Suggest possible upgrades and changes to improve the project (both content and technical).  
   I think very good practice will be integration with database, I maybe then show this data on simple website, but overall I really liked this exercise. 
