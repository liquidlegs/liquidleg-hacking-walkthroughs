# Lab walkthroughs

##### SQL injection vulnerability in WHERE clause allowing retrieval of hidden data
[lab 1](/PortSwigger_Web_Security_Academy/SQL_Injection/lab1/lab1.md)

##### SQL injection vulnerability allowing login bypass
[lab 2](/PortSwigger_Web_Security_Academy/SQL_Injection/lab2/lab2.md)

##### SQL injection UNION attack, determining the number of columns returned by the query
[lab 3](/PortSwigger_Web_Security_Academy/SQL_Injection/lab3/lab3.md)

##### SQL injection UNION attack, finding a column containing text
[lab 4](/PortSwigger_Web_Security_Academy/SQL_Injection/lab4/lab4.md)

##### SQL injection UNION attack, retrieving data from other tables
[lab 5](/PortSwigger_Web_Security_Academy/SQL_Injection/lab5/lab5.md)

##### SQL injection UNION attack, retrieving multiple values in a single column
[lab 6](/PortSwigger_Web_Security_Academy/SQL_Injection/lab6/lab6.md)

##### SQL injection attack, querying the database type and version on Oracle
[lab 7](/PortSwigger_Web_Security_Academy/SQL_Injection/lab7/lab7.md)

##### SQL injection attack, querying the database type and version on MySQL and Microsoft
[lab 8](/PortSwigger_Web_Security_Academy/SQL_Injection/lab8/lab8.md)

##### SQL injection attack, listing the database contents on non-Oracle databases
[lab 9](/PortSwigger_Web_Security_Academy/SQL_Injection/lab9/lab9.md)

##### SQL injection attack, listing the database contents on Oracle
[lab 10](/PortSwigger_Web_Security_Academy/SQL_Injection/lab10/lab10.md)

##### Blind SQL injection with conditional responses
[lab 11 (TODO)]()

##### Blind SQL injection with conditional errors
[lab 12 (TODO)]()

##### Visible error-based SQL injection
[lab 13 (TODO)]()

##### Blind SQL injection with time delays
[lab 14 (TODO)]()

##### Blind SQL injection with time delays and information retrieval
[lab 15 (TODO)]()

##### Blind SQL injection with out-of-band interaction
[lab 16 (TODO)]()

##### Blind SQL injection with out-of-band data exfiltration
[lab 17 (TODO)]()

##### SQL injection with filter bypass via XML encoding
[lab 18 (TODO)]()

# SQL injection
SQL injection (SQLi) is a web application security vulnerability that allows an attacker to interfere with queries to a database. This commonly appears through user-controlled HTTP request parameters and form fields. SQLi generally allows an attacker to access data that they should never have access to. Data includes user credentials, personal information, internal server files, web application source code, etc. Given the severity of the SQLi vulnerability and the privileges of the user, an attack may be able to drop files on the server, delete files, exfiltrate data from the server, modify data, and make persistent changes to the web application's contents or behaviour.

In some situations, an attacker might find another vulnerability through SQLi that they can leverage to escalate privileges and compromise the backend system beyond the database.

## Types of SQLi
### Classic SQLi
Classic SQLi is the easiest to exploit because it allows an attacker to gather results and launch an attacker through one communication channel.

### Error-based SQLi
In Error-based SQLi an attacker relies on the error/exception messages thrown by the database in order to gether information about the target. As a best practice, error messages and stack traces should be disabled before pushing the application into a production environment.

### Union-based SQLi
This attack relies on the UNION SQL operator in order to combine the results from multiple SELECT queries together. By leveraging the UNION operator, an attacker can access and dump information from other tables within the database and even access adjacent databases in search of sensitive information.

### Blind SQLi
Unlike classic SQLi or Error-based / Union-based SQLi techniques, Blind SQLi does not return and display any information from the database. Instead, other techniques must be utilized to determine if the web application is vulnerable. A common testing technique is to cause the connection to sleep for a certain number of seconds and if the database takes about that long to respond, it is likely vulnerable. Blind SQLi is quite considerably harder to exploit than other SQLi attacks and requires the attacker to create injection payloads based on the application responses.

There are two sub-types of Blind SQLi, which are Time-based Blind SQLi and Boolean-based Blind SQLi

### Time-based Blind SQLi
This kind of Blind SQLi works by sending a payload to the application and causing its response time to be delayed by however many seconds. If the application takes the specified number of seconds to respond, then the query is equal to True, else, it is False.

As this kind of SQLi relies on the time it takes for the application to respond and for the query to return True or False, this means that if the attacker wants to enumerate the database, this will need to be done character by character.

### Boolean-based Blind SQLi
This kind of SQLi attacker is similar to Time-based Blind SQLi in that when the server responds, it will return either True/False or 1/0. In this kind of SQLi, the HTTP response is what determines whether the query is True or False.

Boolean-based Blind SQLi will be a bit faster than Time-based Blind SQLi, in that the attacker does not have to wait for an extra delayed response, however, the attacker will still need to enumerate the database one character at a time.

## Preventing SQLi
A mass majority of SQLi vulnerabilities can be solved by creating a prepared statement instead of string concatenation within a query.

The code block below shows an SQLi vulnerability that can easily be exploited by an attacker by inserting quotation marks and other characters to break out of the string concatenated query.

```Java
String query = "SELECT * FROM products WHERE category = '"+ input + "'";
Statement statement = connection.createStatement();
ResultSet resultSet = statement.executeQuery(query);
```

If an attacker inserted the following payload `'+union+select+table_name,null,null,null+from+products+where+table_schema+=+"public"`, the code block above would become the query below.

```Java
"SELECT * FROM products WHERE category = '' union select table_name,null,null,null from products where table_name = \"public\""
```

The payload above shows how attackers can easily exploit SQLi and leverage the vulnerability to access adjacent tables that contain sensitive information.

The same query can easily be rewritten to perform the same functionality without allowing an attacker to interfere with the structure of the query.

```Java
PreparedStatement statement = connection.prepareStatement("SELECT * FROM products WHERE category = ?");
statement.setString(1, input);
ResultSet resultSet = statement.executeQuery();
```

Using a prepared statement can prevent an attacker from inserting malicious queries with the `where` clause, and the `insert` and `update` statements. For queries that require user input to be submitted as column names or utilized by the `order by` statement, these will require a different approach such as whitelisting or rewriting the query in a different way that provides the same functionality.