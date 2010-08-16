# CouchDB Demo
Given on August 16th, 2010, at the ChicagoDB user's group

## Setup
1. [Get CouchDB](http://www.couch.io/get)
2. Install and start CouchDB
3. Navigate to http://localhost:5984/_utils
4. Create yourself an admin account, with a username of 'admin' and a password of 'admin'

## CRUD on the Couch
#### Create database
    curl -X PUT http://admin:admin@localhost:5984/employees/

#### Get some information about that database
    curl http://localhost:5984/employees

#### Create a new document
PUT or POST can be used.  POST will use a server generated DocID.  Use PUT if you want to specify the DocID.  PUT is recommended, because some network intermediaries will resend POST requests, resulting in duplicate documents.

    curl -X PUT http://localhost:5984/employees/1234 -d @first_doc.json

#### Fetch a document
    curl http://localhost:5984/employees/1234

#### Update a document
First, make a change to the first_doc.json file.  For example, change the last name from "Woo" to "Wood".  In addition, be sure to include the "_rev" property that was returned when you fetched the document in the previous command.  CouchDB will reject document updates with a conflict error if they don't include the revision number of the current document.

    curl -X PUT http://localhost:5984/employees/1234 -d @first_doc.json

#### Delete a document
    curl -X DELETE http://localhost:5984/employees/1234?rev=xxxx


## Create some documents for the view demo
    curl -X PUT http://localhost:5984/employees/1 -d @john.json
    curl -X PUT http://localhost:5984/employees/2 -d @ryan.json
    curl -X PUT http://localhost:5984/employees/3 -d @ethan.json
    curl -X PUT http://localhost:5984/employees/4 -d @bob.json


## Create a design document with the views, for the view demo
    curl -X PUT http://admin:admin@localhost:5984/employees/_design/stats -d @stats_design_doc.json


## Execute the views
#### How many employees does our company have?
    curl 'http://localhost:5984/employees/_design/stats/_view/total_employees'

#### See all employees sorted by last name
    curl 'http://localhost:5984/employees/_design/stats/_view/by_lastname'
    curl 'http://localhost:5984/employees/_design/stats/_view/by_lastname?include_docs=true'

#### See all employees whose last names are between A-G
    curl 'http://localhost:5984/employees/_design/stats/_view/by_lastname?startkey="A"&endkey="H"&include_docs=true'

#### Find all employees with a last name of "Wood"
    curl 'http://localhost:5984/employees/_design/stats/_view/by_lastname?key="Wood"&include_docs=true'

#### See all dependents
    curl 'http://localhost:5984/employees/_design/stats/_view/dependents?reduce=false'

#### See all of John's dependents
    curl 'http://localhost:5984/employees/_design/stats/_view/dependents?key="1"&reduce=false'

#### Count how many dependents John Wood has
    curl 'http://localhost:5984/employees/_design/stats/_view/dependents?startkey="1"&endkey="1"'

#### What is the total payroll?
    curl 'http://localhost:5984/employees/_design/stats/_view/total_payroll'

#### Which employees started after March 10th, 2010?
    curl 'http://localhost:5984/employees/_design/stats/_view/by_date_hired?startkey=\[2010,3,10\]'
    curl 'http://localhost:5984/employees/_design/stats/_view/by_date_hired?startkey=\[2010,3,10\]&include_docs=true'

#### Which employees started in 2010?
    curl 'http://localhost:5984/employees/_design/stats/_view/by_date_hired?startkey=\[2010,{}\]&include_docs=true'

