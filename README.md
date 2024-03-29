# Tyler's Notes
## Summary
This repository contains all of the notes taken by [Tyler](https://github.com/tylercaceres) for the [Lighthouse Labs](https://www.lighthouselabs.ca/) Web Development Bootcamp.
## Table of Contents
* [Week 1](/Week_1)
  * [Day 1](/Week_1/Day_1)
  
  * Unit Testing
   * mocha and chai packages
   
 Mocha gives us the describe and it functions. Each it is a test, and each test should have at least one assertion.
 Chai is an assertion library. It gives us assertion functions so that we no longer have to use our assertEqual and other assertion functions that we implemented previously. Chai assertion functions are deliberately designed to play nice with testing frameworks like Mocha.


var obj = {something: 123, newthing: 321} ---> delete obj.newthing --> obj = {something: 123}

When data is sent across the web using HTTP request/responses, the Media Type for JSON data is application/json (compared to text/html for HTML). It is set via the Content-Type HTTP response header.

app.get('/', (request, response) => {
  response.status() // to set the status of the response
  response.set() // to set outgoing headers of the response
  response.json() // to send an object as JSON in the response-body
});

app.get('/', (request, response) => {
  response.get() // to see what headers we've already set
});

app.get('/', (request, response) => {
  response.locals;
  response.headersSent;
});

Summary of OOP features that we covered:
We learned the following features about Classical OOP:

A class is a blueprint from which instances of objects can be created (i.e. newTask vs a task)
Classes have data in the form of value properties and behaviour in the form of methods
Classes can inherit behaviour from other classes using the extends keyword
Subclasses can override methods that are inherited in their superclass
JavaScript also gives us get and set keywords to more cleverly define methods that are data getters and setters

#Promises
## 4 states
- fulfilled (resolved) :it worked
- rejected: it didn't work
- pending: still waiting...
- settled: something happened! (either resolved or rejected)

# good coding practises
https://github.com/airbnb/javascript

# DNS RECORD TYPES
Although there are many available DNS Record Types, there is a small subset that cover most use cases.

A: most common; map a hostnames to IP address (IPv4, 32-bit address)
NS: Name Server that is responsible for a DNS zone
MX: Mail Exchange record specifies where email gets sent to
CNAME: Canonical Name, an alias for another hostname
AAAA: similar to A, but uses IPv6, 128-bit address

Web Server: Node.js
Middleware: Express
Template Engine: EJS

# EJS partials
* use _ when naming partial for convention 
** Create a new file called _header.ejs inside the new partials directory.
Notice that the name of this file starts with an underscore (_). This is to signify that it's a partial, in this case, a header partial.

# CRUD
Action	Description
Create	Add a new record
Read	Retrieve the value of a record
Update	Update a record's value
Delete	Delete a record

Operation	SQL	HTTP	RESTful WS	DDS
Create	INSERT	PUT / POST	POST	write
Read (Retrieve)	SELECT	GET	GET	read / take
Update (Modify)	UPDATE	PUT / POST / PATCH	PUT	write
Delete (Destroy)	DELETE	DELETE	DELETE	dispose


HTTP method	RFC	Request has Body	Response has Body	Safe	Idempotent	Cacheable
GET	RFC 7231	Optional	Yes	Yes	Yes	Yes
HEAD	RFC 7231	Optional	No	Yes	Yes	Yes
POST	RFC 7231	Yes	Yes	No	No	Yes
PUT	RFC 7231	Yes	Yes	No	Yes	No
DELETE	RFC 7231	Optional	Yes	No	Yes	No
CONNECT	RFC 7231	Optional	Yes	No	No	No
OPTIONS	RFC 7231	Optional	Yes	Yes	Yes	No
TRACE	RFC 7231	No	Yes	Yes	Yes	No
PATCH	RFC 5789	Yes	Yes	No	No	No

The order of route definitions matters! The GET /urls/new route needs to be defined before the GET /urls/:id route. Routes defined earlier will take precedence, so if we place this route after the /urls/:id definition, any calls to /urls/new will be handled by app.get("/urls/:id", ...) because Express will think that new is a route parameter. A good rule of thumb to follow is that routes should be ordered from most specific to least specific.

Method 2: Use an escape function
Alternatively, you could use a function to escape some text, and then use it inside .html() or $(). Here is such a function (it also makes use of .createTextNode()):

const escape =  function(str) {
  let div = document.createElement('div');
  div.appendChild(document.createTextNode(str));
  return div.innerHTML;
}


******conversion

let result = 0;

for (let i = 0; i < array.length; i++) {
  let number = array[i];
  result += number;
}

console.log(result);
**********

let result = 0; // 1

for (
  let i = 0; // 1
  i < array.length; // n + 1
  i++ // n
) {
  let number = array[i]; // n
  result += number; // n
}

console.log(result); // 1

*****

guessing game algorithm pseudocode:
Here's a step-by-step description of using binary search to play the guessing game:
Let min = 1 min=1m, i, n, equals, 1 and max = nmax=nm, a, x, equals, n.
Guess the average of maxmaxm, a, x and minminm, i, n, rounded down so that it is an integer.
If you guessed the number, stop. You found it!
If the guess was too low, set minminm, i, n to be one larger than the guess.
If the guess was too high, set maxmaxm, a, x to be one smaller than the guess.
Go back to step two.



Big O notation, written as O(), describes how the number of steps in an algorithm scales relative to it's input. As we increase the amount of data, does the algorithm grow linearly, exponentially, or logarithmically?

When we evaluate an algorithm using Big O notation, there are three main things to remember:

We only care about arbitrarily large input.
What does the run time of binary search look like when we give it an array of one million items?
We drop the non-dominant terms.
When our algorithm had a running time of (n^2+n)/2, it was the n^2 that was hurting us. So we'll just forget about everything else.
We drop constant terms.
If you graph (n^3)/2 or (n^3)*2, it has pretty much the same curve as n^3, so let's just get rid of the constant 2.


Logarithmic O(log n)
If the number of operations that an algorithm has to do is directly proportional to the logarithm of the size of the input, then that algorithm runs in logarithmic time.

## Databases
Edgar F. Codd, the computer scientist who layed down the theoretical basis of relational databases, called this step of removing repetitive data across columns the first normal form (1NF).
-->normalization


## POSTGRES SQL

for loop? 

SELECT continent, name, area
FROM world x
WHERE area >= ALL
(
SELECT area
FROM world y
where x.continent = y.continent and y.area > 0
)

Find the largest country (by area) in each continent, show the continent, the name and the area:

SELECT name, continent, population
FROM  world x
WHERE 25000000 > ALL (
SELECT population
FROM world y
WHERE x.continent = y.continent)

Find the continents where all countries have a population <= 25000000. Then find the names of the countries associated with these continents. Show name, continent and population.


SELECT name, continent
FROM world x
WHERE population >= (
SELECT population*3
FROM world y
WHERE y.continent = x.continent and y.name != x.name
ORDER BY population DESC
LIMIT 1
)

Some countries have populations more than three times that of any of their neighbours (in the same continent). Give the countries and continents.

*****
Give a distinct list of the stops which may be reached from 'Craiglockhart' by taking one bus, including 'Craiglockhart' itself, offered by the LRT company. Include the company and bus no. of the relevant services.

SELECT DISTINCT bstop.name, a.company, a.num
FROM route a
JOIN route b ON (a.company = b.company AND a.num = b.num)
JOIN stops astop ON (a.stop = astop.id)
JOIN stops bstop ON (b.stop = bstop.id)
WHERE astop.name = 'Craiglockhart'


Quick Reference
Primary key column:
Use the name id and then SERIAL PRIMARY KEY.
Foreign key columns:
Add _id to the singular name of the column you are referencing.
If the primary key is SERIAL, then the foreign key should be INTEGER.
You also should create the foreign key with REFERENCES table_name(id) ON DELETE CASCADE.
Names, emails, usernames and passwords can all be stored as VARCHAR(255). Students to cohorts would be cohort_id. The type would be INTEGER .
Dates would use the DATE type. If we needed date and time, use TIMESTAMP.
Numbers:
We will use INTEGER to represent most numbers. There are other sizes of integers as well.
SMALLINT -32,768 to 32,767 (thirty-two thousand)
INTEGER -2,147,483,648 to 2,147,483,647 (two billion)
BIGINT -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 (nine quintillion)
SERIAL 1 to 2,147,483,647 (auto incrementing)
Dates, Phone Numbers & Currency
Become familiar with the ISO 8601 date formatting standard. The string '2018-02-12' uses this format to represent 'February 12th, 2018'. Year, month and then day. Dates should be stored consistently. Apply timezones and formatting when displayed to the user.
Store phone numbers as VARCHAR, there are so many possible formats. The number 214 748 3647 hits our INTEGER limit.
Store currency as an integer representing cents. Use a BIGINT if you need values over $21 million dollars.

