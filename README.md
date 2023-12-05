# TestCase
Restful Api with Junit test

Run Application Locally 

To run our application, all we need to do is to run the SpringrestApplication class that contains the main()method that starts Spring Boot. Eclipse automatically detects that we have a class with a main() method and allows us run it.
To start our application, we have to follow the below steps: 
•	Click Run Application (the "play" icon) in the toolbar.
•	Select Run › Run As in the menu → Java Application.
•	Press Ctrl+F11.
•	Select the SpringrestApplication.java in the Project Explorer, right-click, and select "Run As → Java Application".
The first time we start a Springrest application, it downloads frontend dependencies and builds a JavaScript bundle. This can take several minutes, depending on our computer and internet speed.
We’ll know that our application has started when we see the following output in the console:
Tomcat initialized with port(s): 8080 (http)
Started SpringrestApplication in 4.05 seconds (JVM running for 4.721)
We can now open the Postman App.
Create and test requests in Postman
To add a new book (POST).

Change the HTTP method to POST.

 

In the Enter Request URL field, enter “http://localhost:8080/books/”.

 
The endpoint /books, is preceded by the server and port where the application is running. If our application is running in a different port, replace the 8080 in the URL.
To send request body to this request URL endpoint, navigate to the Body tab, choose the raw checkbox with JSON as the request body format.
 

Enter the below data in the provided textbox:
 

   These are the book details that will be added to the database. Click on Save then Send. 

   Below is the response you get in Postman:
 

Notice the 200 OK response status and that the response body is a JSON containing the employee record details that were saved in the database.

Go to MySQL Workbench and verify that a new row gets created with the above book details with id=1 by executing the query:

SELECT * FROM hibernatebookdb.book;

 


Similarly, you’ll create and run requests to GET, DELETE, and UPDATE books.

To retrieve a list of all books (GET), enter “http://localhost:8080/books/” in the Enter Request URL field. Leave the Body empty and click Send.

 

To retrieve a single book by ID (GET), enter “http://localhost:8080/books/1” in the Enter Request URL field. Leave the Body empty and click Send.

 
To update an existing book (UPDATE) the book with a specific ID, create a PUT request. Enter “http://localhost:8080/books/” in the Enter Request URL field. Enter the following 	details in the raw JSON body and click Send:
      
       	
To delete a book by ID (DELETE) a book record, create a DELETE request. Enter “http://localhost:8080/books/1” in the Enter Request URL field. Leave the Body empty and click Send.
 


REST Specific HTTP Status Codes
200(OK): It indicates that the REST API successfully carried out whatever action the client requested. A 200 response should include a response body.
•	GET an entity corresponding to the requested resource is sent in the response;
•	POST an entity describing or containing the result of the action;
201(Created): A REST API responds with the 201 status code whenever a resource is created inside a collection. There may also be times when a new resource is created as a result of some controller action, in which case 201 would also be an appropriate response.
401(Unauthorized): A 401 error response indicates that the client tried to operate on a protected resource without providing the proper authorization. It may have provided the wrong credentials or none at all.
404 (Not Found): The 404 error status code indicates that the REST API can’t map the client’s URI to a resource but may be available in the future.
500 (Internal Server Error): 500 is the generic REST API error response. Most web frameworks automatically respond with this response status code whenever they execute some request handler code that raises an exception.
A 500 error is never the client’s fault, and therefore, it is reasonable for the client to retry the same request that triggered this response and hope to get a different response.
The API response is the generic error message, given when an unexpected condition was encountered and no more specific message is suitable.






Configuring MySQL Database
Since we’re using MySQL as our database, we need to configure the URL, username, and password. So, that our spring boot can establish a connection with the database on startup. Open the src/main/resources/application.properties file and add the following properties to it:
spring.datasource.url=jdbc:jdbc\:mysql\://localhost\:3306/hibernatebookdb
spring.datasource.username=root
spring.datasource.password=root

spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL8Dialect
spring.jpa.hibernate.ddl-auto=update

Also, Create a database named hibernatebookdb in MySQL.
You don’t need to create any tables. The tables will automatically be created by Hibernate from the bookentity. This is made possible by the property spring.jpa.hibernate.ddl-auto = update.



