# *Creating a timetabling database using Neo4J*

# Introduction
This repository will contain documentation and work for my third year graph theory project in the course Computing and Software Development. The lecturer for this module is Ian Mcloughlin. I am required to design and prototype a Neo4j database for use in a timetabling system for a third level institute like GMIT which I am currently attending. The database should store information about student groups, classrooms, lecturers and class hours. 

# What is Neo4J?
Neo4j is the world's leading graph database. It is an open source NoSQL graph database implemented in java, hence the name Neo4java. It is described by its developers as an ACID (Atomicity, Consistency, Isolation, Durability) compliant transactional database with native graph storage and processing.

## what is a Graph Database?
A graph database is a database that uses graph structures for semantic queries with nodes, edges and properties to represent and store data. It is essentially a collection of nodes and edges. The key concept of the system is the graph (edge or relationship), which directly relates data items in the store. Each node represents an entity e.g. a person or business, and each edge represents a connection or relationship between two nodes. Every node in a graph database is defined by a unique identifier, a set of outgoing/incoming edges and a set of properties expressed as key/value pairs. Vice Versa with edges. 
### Benefits of a graph database
Graph databases are well suited for analysing interconnections, which is why there is been a lot of interest in using graph databases to mine data from social media websites. Graph databases are also useful for working with data in business disciplines that involve complex relationships and dynamic schema.

# Cypher
Cypher is a declarative graph query language that allows for expressive and efficient querying and updating of the graph store. It is similar in a way to MySQL with its structure i.e. queries are built up using various clauses. Very complicated database queries can easily expressed through Cypher. Cypher was originally created by Neo Technology for its graph database Neo4j. Now it is adopted by other graph database vendors such as SAP and HANA.

# Design
A graph database contains nodes, relationships, relationship types, labels and properties.
## *Node*
A node is a seperate entity e.g. a Person is a node
Here are each module node with name properties:
![](https://cloud.githubusercontent.com/assets/22341150/25282596/e04b88ac-26a8-11e7-95cd-7157b80a2967.PNG)

## *Label*
A label is a grouping facility for node where all nodes having a label are part of the same group. Labels on nodes are optional and any node can have a number of labels attached to it.
Here are two labels for modules in semester 5 and semester 6:
![](https://cloud.githubusercontent.com/assets/22341150/25281769/417cb4fa-26a6-11e7-9df1-906a5f759d75.PNG)

## *Relationship*
A node can have a relationship with another node. Relationships between nodes are the key feature of graph databases, as they allow for finding related data. A relationship connects two nodes. Relationships organise nodes into arbitrary structures allowing a graph to resemble a list, a tree or a map. 
Here is a relationship 'courseYear' between course and the years:
![](https://cloud.githubusercontent.com/assets/22341150/25282510/9711f0ea-26a8-11e7-84e0-12de81b6a06d.PNG)


The first thing I had to do was to come up with a design of the database. What would be nodes, what would be labels, which nodes had relationships and what would be properties. The database will be designed using the timetable of my current year as creating a timetabling database for all courses in the college would be quite difficult. I drew out my design of the graph database on a page. It took a few pages to finally get it right. The biggest obstacle was the time slots and its relationship with modules, rooms, groups and lecturers. I decided to make each day of the week a node and each hour a node instead of having a day node with each hour as properties. It would be easier to query. Although trying to create a relationship between them all takes a lot of time and queries.



## Nodes/Labels/Properties
| Nodes | Label | Properties |
| ------ | ------ | ------ |
| Course | Courses | courseId: Software Development |
| Module | Modules/Semester5/Semester6 | name: Graph Theory |
|  Year | Years | year: 3 |
|  Room | Rooms | room: G0994 |
| Lecturer | Lecturers | lecturer: Dr Ian Mcloughlin |
| Group | Groups | group: A |
| Day | Days/Week | day: Monday |
| Hour | Hours | hour: 2pm |

## Relationships
| Node | Relationship | node(s) |
| ------ | ------ | ------ |
| module | classOn | Monday/Tuesaday/Wednesday/Thursday/Friday |
| Course | courseYear | 1/2/3/4 |
|  Lecturer | lectures | graph theory |
| Year | modulesInYr3 | graph theory |
| Year | studentGroups | group A/B/C |
| Day | times | 8am/9am/10am/11am/12pm/1pm/.. |




### Load CSV
In order to get data such as rooms, modules, groups and lectures to use for the graph database, I first had to extract the data from GMIT's website by opening up the websites source code and taking out html tags containing the relevent data. I pasted the data into Notepad++ where I could use regular expression techniques to remove the html tags and clean up the data. The best way to import data into neo4j is by using CSV (Comma Seperated Values) files. To do this, I put the cleaned up data into microsoft excel and saved it as a CSV file. 

How to import data from a CSV file into neo4j:
```sh
LOAD CSV FROM 'file:///c:/rooms.csv' AS LINE CREATE (:Rooms {room: line.room})
```
or with headers
```sh
LOAD CSV WITH HEADERS FROM 'file:///c:/rooms.csv' AS LINE CREATE (:Rooms {room: line.room})
```
