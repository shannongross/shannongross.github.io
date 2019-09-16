---
published: true

layout: post
title: "SQL Indexing"
date: 2018-04-04
description: Introduction to SQL indexing and clustering # Add post description (optional)
img: dbi.jpg  # Add image post (optional)
---
# Indexing
* An index is an example of an access path that allows direct access to data using an index term or a keyword. It is similar to the index at the end of this book, except that it may be organized in a linear, hierarchical (tree-structured), or some other fashion.
* PostgreSQL allows the use of multiple indexes in a single query. Of course, this makes sense if many columns are queried at the same time. However, that's not always the case. It can also happen that a single index is used multiple times to process the very same column.
* Once a data table exceeds a few thousand rows, you may want to build an index to speed up searches of the data (unless all your searches are based on attributes, in which case you’ll want to build a normal index on the attribute fields).
* Indexes are what make using a database for large data sets possible. Without indexing, any search for a feature would require a "sequential scan" of every record in the database. Indexing speeds up searching by organizing the data into a search tree which can be quickly traversed to find a particular record.
* If you see 'primary key' in sql statement, it automatically creates an index (an extra index)
* Primary key helps for sorting
* If a certain column is not sorted however, you have to search through entire column. Unless you create an index. So a secondary index helps if you wish to search for something else (besides the primary key)

{% highlight ruby %}
Create index students_name
On students*name);
{% endhighlight %}


# Clustering
* Allows the reordering of a table on disk based on an index
* The table is essentially completely rewritten from an initial unordered state into an ordered state. This ensures that records with similar attributes have a high likelihood of being found in the same page, reducing the number of pages that must be read into memory for some types of queries. This is harder to visualize for spatial data since the index doesn’t have a simple linear ordering, but the effect is the same. Geometries that are near each other in space are near each other on disk.

{% highlight ruby %}
CLUSTER jacksonco_streets USING jacksonco_streets_gix;
ANALYZE jacksonco_streets;
{% endhighlight %}

## What is the advantage of clustered tables?
* Consider you want to read a whole area of data. This might be a certain time range, some block, IDs, or so.
* The runtime of such queries will vary depending on the amount of data and the physical arrangement of data on the disk. So, even if you are running queries that return the same number of rows, two systems might not provide the answer within the same time span, as the physical disk layout might make a difference.
* In PostgreSQL, there is a command called CLUSTER that allows us to rewrite a table in the desired order. It is possible to point to an index and store data in the same order as the index
* Data can only be organized according to one index. You cannot order a table by postal code, name, ID, birthday, and so on, at the same time. It means that CLUSTER will make sense if there is a search criteria, which is used most of the time



## Spatial Indexing
* What do we mean by Spatial Access Methods?
* Spatial access = spatial index (knowing where to get things) + spatial clustering
* Two aspects of Spatial Access Methods
  -	Indexing: knowing the storage location fast (computer/disk/memory) when searching for certain objects. Index is an additional structure to help point in the right direction
  -	Clustering: storing objects close together, which are also often selected together (e.g. because they are nearby in space)

## What do we mean by Spatial Indexing?
1.	Spatial Indexing
a.	Indexing of administrative data is typically based on sorting (ie organize alphabetically, then create a B-tree)
b.	However, multidimensional data cannot be sorted this way
i.	If you sort on longitude, latitudes may still be very far away so its not convenient
* We can speed up determining the relationship between two geometries by first determining the relationship between the bounding boxes of the geometries. Index the bounding boxes of the geometry rather than the geometry itself.
* GIST is lossy (inexact) while the default btree must index the entire geometry which can be very large
* By storing these bounding boxes in an R-Tree index, the boxes can be quickly located and compared and the number of full geometry comparisons reduced before the geometry is ever read from disk.





<br>

# Reference
* Database Systems (Elmasri and Navathe)
