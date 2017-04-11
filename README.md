# Creating a timetabling database using Neo4J

# Introduction
This repository will contain documentation and work for my third year graph theory project in the course Computing and Software Development. The lecturer for this module is Ian Mcloughlin. I am required to design and prototype a Neo4j database for use in a timetabling system for a third level institute like GMIT which I am currently attending. The database should store information about student groups, classrooms, lecturers and class hours. 

# What is Neo4J?
Neo4j is the world's leading graph database. It is an open source NoSQL graph database implemented in java, hence the name Neo4java. It is described by its developers as an ACID (Atomicity, Consistency, Isolation, Durability) compliant transactional database with native graph storage and processing.

## Graph Database
A graph database is a database that uses graph structures for semantic queries with nodes, edges and properties to represent and store data. It is essentially a collection of nodes and edges. The key concept of the system is the graph (edge or relationship), which directly relates data items in the store. Each node represents an entity e.g. a person or business, and each edge represents a connection or relationship between two nodes. Every node in a graph database is defined by a unique identifier, a set of outgoing/incoming edges and a set of properties expressed as key/value pairs. Vice Versa with edges. 
### Benefits
Graph databases are well suited for analysing interconnections, which is why there is been a lot of interest in using graph databases to mine data from social media websites. Graph databases are also useful for working with data in business disciplines that involve complex relationships and dynamic schema.

# A timetabling System
