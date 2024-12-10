# Ex 2-1

**Description**
```
Write a query to retrieve all Movie nodes that released in 2019.
```

**Our Query Answer**
``` Cypher
// Ex2-1
MATCH (m:Movie{released:2019})
RETURN m
```

# Ex 2-2

**Description**
```
Write a query to retrieve all Movie nodes that were released in 2020.
```

**Our Query Answer**
``` Cypher
// Ex2-2
MATCH (m:Movie{released:2020})
RETURN m
```

# Ex 2-3

**Description**
```
Write a query to retrieve all Movie released in 2003, returning their titles.
```

**Our Query Answer**
``` Cypher
// Ex2-3
MATCH (m:Movie{released:2003})
RETURN m.title
```

# Ex 2-4

**Description**
```
Write a query to retrieve all Movie nodes and display the title, released, and tagline values.
```

**Our Query Answer**
``` Cypher
// Ex2-4
MATCH (m:Movie)
RETURN m.title, m.released, m.tagline
```

# Ex 2-5

**Description**
```
WrModify Ex 2-4 query to rename the columns as ‘movie title’,
‘released year’, and ‘tagLine’
```

**Our Query Answer**
``` Cypher
// Ex2-5
MATCH (m:Movie)
RETURN m.title AS `movie title`, m.released AS `released year` , m.tagline AS `tagLine`
```

# Ex 3-1

**Description**
```
Write a query to retrieve all Person names who wrote the movie Top Gun.
```

**Our Query Answer**
``` Cypher
// Ex3-1
MATCH (p:Person)-[rel:WROTE]->(m:Movie{title:"Top Gun"})
RETURN p.name
```

# Ex 3-2

**Description**
```
Write a query to retrieve all movie titles connected with Tom Hanks.
Hint: Tom Hanks has multiple relationships with a movie (Actor and Director)
```

**Our Query Answer**
``` Cypher
// Ex3-2
MATCH (p:Person{name:"Tom Hanks"})-[rel]-(m:Movie)
RETURN m.title
```

# Ex 3-3

**Description**
```
Modify Ex 3-2 query to return the information as a table about the type of relationships between Tom Hanks and the movies.
```

**Our Query Answer**
``` Cypher
// Ex3-3
MATCH (p:Person{name:"Tom Hanks"})-[rel]-(m:Movie)
RETURN m.title, type(rel)
```

# Ex 3-4

**Description**
```
Retrieve information about the movies and roles that Tom Hanks acted in.
```

**Our Query Answer**
``` Cypher
// Ex3-4
MATCH (p:Person{name:"Tom Hanks"})-[rel:ACTED_IN]->(m:Movie)
RETURN m.title, rel.roles
```

# Ex 4-1

**Description**
```
Retrieve all movies that Tom Cruise acted in and return their titles (using WHERE clause).
```

**Our Query Answer**
``` Cypher
// Ex4-1
MATCH (p:Person)-[rel:ACTED_IN]->(m:Movie)
WHERE p.name = "Tom Cruise"
RETURN m.title
```

# Ex 4-2

**Description**
```
Retrieve all people that were born in the 70’s and return their names and year born.
```

**Our Query Answer**
``` Cypher
// Ex4-2
MATCH (p:Person)
WHERE 1970 <=  p.born < 1980
RETURN p.name, p.born
```

# Ex 4-3

**Description**
```
Retrieve the actors who acted in the movie The Matrix who were born after 1960, and return their names and year born

Constraints:
- using WHERE clause only
- Specifying a condition directly in a MATCH clause is not allowed.
```

**Our Query Answer**
``` Cypher
// Ex4-3
MATCH (p:Person) -[:ACTED_IN]-> (m:Movie)
WHERE p.born > 1960 AND m.title = "The Matrix"
RETURN p.name, p.born
```

# Ex 4-4

**Description**
```
Retrieve all people in the graph that do not have a born property, returning their names.
```

**Our Query Answer**
``` Cypher
// Ex4-4
MATCH (p:Person)
WHERE p.born IS NULL
RETURN p.name
```

# Ex 4-5

**Description**
```
Retrieve all people related to movies where the relationship has the rating property, then return their name, movie title, and the rating.
```

**Our Query Answer**
``` Cypher
// Ex4-5
MATCH (p:Person) -[rel]- (m:Movie)
WHERE rel.rating IS NOT NULL
RETURN p.name, m.title, rel.rating
```

# Ex 4-6

**Description**
```
Retrieve all REVIEWED relationships from the graph where the summary of the review contains the string ‘fun’, returning the movie title reviewed and the rating and summary of the relationship.
```

**Our Query Answer**
``` Cypher
// Ex4-6
MATCH (p:Person) -[rel:REVIEWED]- (m:Movie)
WHERE rel.summary CONTAINS 'fun'
RETURN m.title, rel.summary, rel.rating
```

# Ex 4-7

**Description**
```
Retrieve the movies and their actors where one of the actors also directed the movie, returning the actors names, the director’s name, and the movie title.

Constraint:
- The results should exclude a record that has the same actor’s name and director’s name.
```

**Our Query Answer**
``` Cypher
// Ex4-7
MATCH (d:Person)-[:ACTED_IN]->(m:Movie)<-[:DIRECTED]-(d)
MATCH (a:Person)-[:ACTED_IN]->(m)
WHERE a <> d
RETURN a.name, d.name, m.title
```

# Ex 4-8

**Description**
```
Retrieve the movies that have an actor’s role that is the name of the movie, return the movie title and the actor’s name.
```

**Our Query Answer**
``` Cypher
// Ex4-8
MATCH (a:Person)-[rel:ACTED_IN]->(m:Movie)
WHERE m.title IN rel.roles
RETURN m.title, a.name
```
