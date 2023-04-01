# HW-NoSQL-MongoDB

## Part 1

You're creating a database to contain a set of sensor measurements from a two-dimensional grid.
Each measurement is a time-sequence of readings, and each reading contains ten labeled values.
Should you use the relational model or MongoDB? Please justify your answer
#### <ins>Answer</ins>
  I will use MongoDB because sensor data may evolve over time, with new types of readings or additional values being introduced, and MongoDB's schema-less nature allows for greater flexibility in integrating new data structures. Each measurement is a time-sequence of readings, and each reading contains ten labeled values. This kind of data structure can be better represented and stored in MongoDB using its native JSON/BSON format. MongoDB provides native support for time-series data, which is a common type of data generated by sensors.

## Part 2

For each of the following applications
a. IoT
b. E-commerce
c. Gaming
d. Finance
Propose an appropriate Relational Model or MongoDB database schema. For each application,
clearly justify your choice of database.
#### <ins>Answer</ins>

#### IoT

  For IoT applications, I will use MongoDB because IoT devices generate large amounts of time-series data and may have varying schemas. MongoDB's flexible schema and horizontal scalability can handle these requirements better than relational databases.

#### E-commerce

  For e-commerce applications, I will use the relational model because there is typically a lot of structured data involved, with various entities like products, customers, and orders all interconnected. Relational databases are well-suited for managing structured data, ensuring data consistency and supporting transactions.

#### Gaming

  For gaming applications, I will use MongoDB because gaming apps need to process data quickly and have complex structures. MongoDB's flexible schema and high-performing capabilities are well-suited for these requirements.

#### Finance

  For financial applications, I will use the relational model because financial applications usually involve structured data with strict consistency requirements and transactions. Relational databases provide ACID properties, ensuring data consistency and reliability.
    
## Part 3

#### Create a database named studentsDB  
```use studentsDB```
 
#### Insert some information  
```
db.students.insertMany([  
  {"name":"Ramesh","subject":"maths","marks":87},  {"name":"Ramesh","subject":"english","marks":59},  
  {"name":"Ramesh","subject":"science","marks":77},  {"name":"Rav","subject":"maths","marks":62},  
  {"name":"Rav","subject":"english","marks":83},  {"name":"Rav","subject":"science","marks":71},  
  {"name":"Alison","subject":"maths","marks":84},  {"name":"Alison","subject":"english","marks":82},  
  {"name":"Alison","subject":"science","marks":86},  {"name":"Steve","subject":"maths","marks":81},  
  {"name":"Steve","subject":"english","marks":89},  {"name":"Steve","subject":"science","marks":77},  
  {"name":"Jan","subject":"english","marks":0,"reason":"absent"}
])
```
### Give MongoDB statements (with results) for the following queries
#### Find the total marks for each student across all subjects.
MongoDB statements:
```SQL
db.students.aggregate([{$group: {_id: '$name', total_marks: {$sum: '$marks'}}}])
```
output:
```SQL
[
  { _id: 'Rav', total_marks: 216 },
  { _id: 'Alison', total_marks: 252 },
  { _id: 'Ramesh', total_marks: 223 },
  { _id: 'Steve', total_marks: 247 },
  { _id: 'Jan', total_marks: 0 }
]
```
#### Find the maximum marks scored in each subject.
MongoDB statements:
```SQL
db.students.aggregate([{$group: {_id: '$subject', maximum_marks: {$max: '$marks'}}}])
```
output:
```SQL
[
  { _id: 'english', maximum_marks: 89 },
  { _id: 'science', maximum_marks: 86 },
  { _id: 'maths', maximum_marks: 87 }
]
```
#### Find the minimum marks scored by each student.
MongoDB statements:
```SQL
db.students.aggregate([{$group: {_id: '$name', minimum_marks: {$min: '$marks'}}}])
```
output:
```SQL
[
  { _id: 'Rav', minimum_marks: 62 },
  { _id: 'Alison', minimum_marks: 82 },
  { _id: 'Ramesh', minimum_marks: 59 },
  { _id: 'Steve', minimum_marks: 77 },
  { _id: 'Jan', minimum_marks: 0 }
]
```
#### Find the top two subjects based on average marks.
MongoDB statements:
```SQL
db.students.aggregate([{$group: {_id: '$subject', average_marks: {$avg: '$marks'}}}, {'$sort': {average_marks: -1}}, {'$limit': 2}])
```
output:
```SQL
[
  { _id: 'maths', average_marks: 78.5 },
  { _id: 'science', average_marks: 77.75 }
]
```
