# Table of Contents

- [Table of Contents](#table-of-contents)
  - [1. What are the advantages of using MongoDB over a relational database? When would you prefer MongoDB?](#1-what-are-the-advantages-of-using-mongodb-over-a-relational-database-when-would-you-prefer-mongodb)
  - [2. Explain the difference between find() and aggregate() in MongoDB. When should you use aggregation?](#2-explain-the-difference-between-find-and-aggregate-in-mongodb-when-should-you-use-aggregation)
  - [3. How does indexing work in MongoDB? What types of indexes are available and when would you use each?](#3-how-does-indexing-work-in-mongodb-what-types-of-indexes-are-available-and-when-would-you-use-each)
  - [4. How does MongoDB handle transactions? Are they similar to SQL transactions? When should you use multi-document transactions?](#4-how-does-mongodb-handle-transactions-are-they-similar-to-sql-transactions-when-should-you-use-multi-document-transactions)
  - [5. Explain the concept of schema design in MongoDB. How do you decide between embedding and referencing?](#5-explain-the-concept-of-schema-design-in-mongodb-how-do-you-decide-between-embedding-and-referencing)
  - [6. Write a query to find all documents in a users collection where the age is between 25 and 35 and the user has at least one hobby of 'reading'.](#6-write-a-query-to-find-all-documents-in-a-users-collection-where-the-age-is-between-25-and-35-and-the-user-has-at-least-one-hobby-of-reading)
  - [7. What is the difference between $match and $project stages in the aggregation pipeline?Use replaceOne() when you want to overwrite the entire document.](#7-what-is-the-difference-between-match-and-project-stages-in-the-aggregation-pipelineuse-replaceone-when-you-want-to-overwrite-the-entire-document)
  - [8. How do you perform a left outer join in MongoDB?1. Query Behavior and Index Use](#8-how-do-you-perform-a-left-outer-join-in-mongodb1-query-behavior-and-index-use)
  - [9. Explain the difference between updateOne(), updateMany(), and replaceOne() methods. when conditions must apply to the same array element to avoid false matches.](#9-explain-the-difference-between-updateone-updatemany-and-replaceone-methods-when-conditions-must-apply-to-the-same-array-element-to-avoid-false-matches)
  - [is applied to all documents before filtering.](#is-applied-to-all-documents-before-filtering)
  - [10. What are some common performance pitfalls in MongoDB queries, and how do you diagnose and fix them?](#10-what-are-some-common-performance-pitfalls-in-mongodb-queries-and-how-do-you-diagnose-and-fix-them)
  - [1. Query Behavior and Index Use      from: "customers",](#1-query-behavior-and-index-use------from-customers)
  - [3. Aggregation Pipeline with $match and $project update fields safely without removing others, use update operators:](#3-aggregation-pipeline-with-match-and-project-update-fields-safely-without-removing-others-use-update-operators)
  - [nt transactions ensure all-or-nothing behavior, preserving data integrity.](#nt-transactions-ensure-all-or-nothing-behavior-preserving-data-integrity)
  - [4. $lookup Join Results](#4-lookup-join-results)
  - [{ category: "electronics" },](#-category-electronics-)
  - [5. Update vs Replace](#5-update-vs-replace)
  - [9. findOne() vs find().limit(1)](#9-findone-vs-findlimit1)
  - [urns a single document directly and is optimized for that purpose, making it slightly more efficient and convenient. find().limit(1) returns a cursor with one document, which you then need to iterate or extract. Use findOne() when you want exactly one document quickly; use find() when you plan to work with multiple documents or want to chain more cursor operations.”](#urns-a-single-document-directly-and-is-optimized-for-that-purpose-making-it-slightly-more-efficient-and-convenient-findlimit1-returns-a-cursor-with-one-document-which-you-then-need-to-iterate-or-extract-use-findone-when-you-want-exactly-one-document-quickly-use-find-when-you-plan-to-work-with-multiple-documents-or-want-to-chain-more-cursor-operations)
  - [10. Impact of Large Documents](#10-impact-of-large-documents)
  - [1. Query Behavior](#1-query-behavior)
  - [2. Array Query Ma](#2-array-query-ma)
  - [3. Aggregation Pi](#3-aggregation-pi)
  - [4. $lookup Join R](#4-lookup-join-r)
  - [5. Update vs Repl](#5-update-vs-repl)
  - [6. Transactions a](#6-transactions-a)
  - [7. Schema Design:](#7-schema-design)
  - [8. Query Using $i](#8-query-using-i)
  - [9. findOne() vs f](#9-findone-vs-f)
  - [10. Impact of Lar](#10-impact-of-lar)

---

## 1. What are the advantages of using MongoDB over a relational database? When would you prefer MongoDB?
**Explanation:**  
This tests conceptual understanding and use cases.

**Answer:**

MongoDB stores data as JSON-like documents (BSON), which allows flexible schema and hierarchical data representation.

It scales horizontally using sharding easily, better for large-scale distributed systems.

Good for agile development where schema evolves rapidly.

Prefer MongoDB when you have semi-structured data, require fast iterative development, or need to store nested objects/arrays naturally.

Not ideal for complex multi-table joins or strict ACID compliance requirements.

---

## 2. Explain the difference between find() and aggregate() in MongoDB. When should you use aggregation?
**Explanation:**  
Tests query building skills and when to use advanced querying.

**Answer:**

find() is for simple queries to retrieve documents based on criteria.

aggregate() allows complex data processing pipelines like grouping, sorting, filtering, projecting, joining ($lookup), and computing new fields.

Use aggregation when you need to perform transformations, compute aggregates (sum, avg), or do multi-stage filtering and grouping in a single query.

For example, to calculate total sales by category, you use aggregation.

---

## 3. How does indexing work in MongoDB? What types of indexes are available and when would you use each?
**Explanation:**  
Tests performance optimization knowledge.

**Answer:**

Indexes improve query performance by creating data structures that allow quick lookup.

Types: Single field, compound indexes, multikey (for arrays), text indexes (for text search), hashed indexes (for sharding).

Use single field for simple equality queries, compound indexes for queries on multiple fields with sort, multikey for array fields.

Text indexes for full-text search.

Hashed indexes to distribute data evenly across shards.

Proper indexing can drastically reduce query times, but too many indexes slow writes.

---

## 4. How does MongoDB handle transactions? Are they similar to SQL transactions? When should you use multi-document transactions?
**Explanation:**  
Tests understanding of ACID properties in MongoDB.

**Answer:**


js
Copy
Edit
db.users.find({
  age: { $gte: 25, $lte: 35 },
  hobbies: 'reading'
});
age uses range query with $gte and $lte.

hobbies is an array; matching a single value like 'reading' checks if the array contains it.

7. What is the difference between $match and $project stages in the aggregation pipeline?
Explanation:
Tests understanding of aggregation stages.
MongoDB supports multi-document ACID transactions since version 4.0.
swer:
Transactions ensure atomicity, consistency, isolation, durability across multiple documents and collections.
ch filters documents, similar to find() conditions, early in the pipeline to reduce data volume.
However, they have performance overhead and are less common in MongoDB compared to relational DBs.
 including/excluding fields or creating computed fields.
Use multi-document transactions when you need strong consistency for complex operations spanning multiple documents or collections (e.g., financial transfers).
tch is usually placed early to improve performance by filtering data, $project changes document shape often later in pipeline.
For simple operations on a single document, rely on atomic operations.
8. How do you perform a left outer join in MongoDB?
---
Tests knowledge of MongoDB’s join capabilities.
## 5. Explain the concept of schema design in MongoDB. How do you decide between embedding and referencing?
**Explanation:**  
Tests design strategy for data modeling.
Use the $lookup stage in aggregation pipeline.
**Answer:**
Example joining orders with customers:
MongoDB is schema-less but designing how data relates is critical for performance and ease of use.
js
Embed related data when you have 1-to-few or 1-to-many relationships and want to retrieve everything in one query (denormalization).
Edit
Reference (store ObjectIDs) when data is large, shared, or grows unbounded (normalization).
Embedding reduces the need for joins ($lookup), improves read performance.
 {
Referencing is better when the embedded data changes frequently or is used independently.
      localField: "customerId",
---oreignField: "_id",
      as: "customerInfo"
## 6. Write a query to find all documents in a users collection where the age is between 25 and 35 and the user has at least one hobby of 'reading'.
Tests basic querying syntax and understanding of operators.
]);
**Answer:**is includes customer data into each order as an array customerInfo.

```jsxplain the difference between updateOne(), updateMany(), and replaceOne() methods.
db.users.find({
    age: { $gte: 25, $lte: 35 },ts update semantics.
    hobbies: 'reading'
});
```
age uses range query with $gte and $lte.rst document matching the filter partially (using update operators like $set).

hobbies is an array; matching a single value like 'reading' checks if the array contains it.eMany() updates all documents matching the filter partially.

---laceOne() completely replaces the matched document with a new document (no update operators).

## 7. What is the difference between $match and $project stages in the aggregation pipeline?Use replaceOne() when you want to overwrite the entire document.
**Explanation:**  
Tests understanding of aggregation stages. some common performance pitfalls in MongoDB queries, and how do you diagnose and fix them?

**Answer:**Tests real-world troubleshooting skills.

$match filters documents, similar to find() conditions, early in the pipeline to reduce data volume.Answer:

$project reshapes documents by including/excluding fields or creating computed fields.Common pitfalls: Missing indexes, large documents, excessive document growth, inefficient queries (scanning entire collection), overuse of $lookup.

$match is usually placed early to improve performance by filtering data, $project changes document shape often later in pipeline.Diagnose using explain() to check query plans and execution stats.

---Fix by creating appropriate indexes, limiting fields with projection, optimizing schema design, reducing document size, and caching.

## 8. How do you perform a left outer join in MongoDB?1. Query Behavior and Index Use
**Explanation:**  
Tests knowledge of MongoDB’s join capabilities.

**Answer:**db.products.find({ price: { $gt: 100 }, category: "electronics" });
tion:
Use the $lookup stage in aggregation pipeline.
er by category at the same time, so it still needs to scan those price-matched documents to check category.
Example joining orders with customers:
 efficiently filter first by category then by price because the index is ordered by category then price. This can dramatically reduce the documents scanned, improving performance.
```js
db.orders.aggregate([), then range (price).
    {
            localField: "customerId",    $lookup: {
            foreignField: "_id",        from: "customers",
            as: "customerInfo"
        }
    }db.users.find({ hobbies: { $elemMatch: { type: "sport", frequency: { $gte: 3 } } } });
]);
```
This includes customer data into each order as an array customerInfo.

---ort" and also any element with frequency >= 3, not necessarily the same element.

## 9. Explain the difference between updateOne(), updateMany(), and replaceOne() methods. when conditions must apply to the same array element to avoid false matches.
**Explanation:**  
Tests update semantics.ggregation Pipeline with $match and $project

**Answer:**
updateOne() updates the first document matching the filter partially (using update operators like $set).

updateMany() updates all documents matching the filter partially.  { $project: { orderId: 1, total: 1 } },

replaceOne() completely replaces the matched document with a new document (no update operators).]);

Use replaceOne() when you want to overwrite the entire document.
is applied to all documents before filtering.
---
ch filters documents, ideally as early as possible to reduce the dataset.
## 10. What are some common performance pitfalls in MongoDB queries, and how do you diagnose and fix them?
**Explanation:**  s first, the pipeline processes every document projecting fields before filtering. This is inefficient.
Tests real-world troubleshooting skills.
ters documents first, reducing the workload of $project downstream. This reduces processing and improves performance.
**Answer:**

Diagnose using explain() to check query plans and execution stats.Common pitfalls: Missing indexes, large documents, excessive document growth, inefficient queries (scanning entire collection), overuse of $lookup.js

Fix by creating appropriate indexes, limiting fields with projection, optimizing schema design, reducing document size, and caching.Edit

---  {

## 1. Query Behavior and Index Use      from: "customers",
omerId",
```js    foreignField: "_id",
db.products.find({ price: { $gt: 100 }, category: "electronics" });  as: "customer"
```}
**Explanation:**
If there is only an index on price, MongoDB can use this index to quickly find documents with price > 100. However, it cannot use the index to filter by category at the same time, so it still needs to scan those price-matched documents to check category.

If the index is compound on { category: 1, price: 1 }, MongoDB can efficiently filter first by category then by price because the index is ordered by category then price. This can dramatically reduce the documents scanned, improving performance.
ter join: for each order, it looks up matching customer documents by matching customerId with _id.
Index order matters: if the query filters on both fields, the index should start with the most selective or equality field (category), then range (price).
ere is no matching customer, the customer field will be an empty array [] (not null).
---
s means all orders appear in the output; unmatched joins do not filter out documents but show empty join results.
## 2. Array Query Matching
5. Update vs Replace
```js
db.users.find({ hobbies: { $elemMatch: { type: "sport", frequency: { $gte: 3 } } } });Copy
```
**Explanation:**db.users.updateOne(

$elemMatch matches documents where at least one array element satisfies all the conditions inside. Here, it finds users who have at least one hobby object with type: "sport" and frequency >= 3.  { name: "Alice", age: 30 }

Without $elemMatch, querying { hobbies: { type: "sport", frequency: { $gte: 3 } } } looks for documents where the array contains an element with type: "sport" and also any element with frequency >= 3, not necessarily the same element.planation:

$elemMatch is important when conditions must apply to the same array element to avoid false matches. operation will replace the entire document with { name: "Alice", age: 30 }, removing all other fields!

---rs like $set are missing, so MongoDB treats it as a replacement document.

## 3. Aggregation Pipeline with $match and $project update fields safely without removing others, use update operators:

```jsjs
    { $project: { orderId: 1, total: 1 } },db.orders.aggregate([
    { $match: { total: { $gte: 100 } } }
]);db.users.updateOne(
```
**Explanation:**  { $set: { name: "Alice", age: 30 } }

$project changes the shape of the documents and is applied to all documents before filtering.ransactions and Atomicity
anation:
$match filters documents, ideally as early as possible to reduce the dataset.
 at the single-document level by default.
Because $project comes first, the pipeline processes every document projecting fields before filtering. This is inefficient.
ducting money from one account and adding to another involves multi-document updates. Without transactions, if the process crashes halfway, one update might succeed and the other fail, causing inconsistency.
Reversing the order ($match first) filters documents first, reducing the workload of $project downstream. This reduces processing and improves performance.
nt transactions ensure all-or-nothing behavior, preserving data integrity.
---
c updates (embedding), or implementing compensating actions and retries in your application logic, but these are more complex and error-prone.
## 4. $lookup Join Results

```jsExplanation:
db.orders.aggregate([
    {Embedding comments inside the blog post is fine if the number of comments is small and bounded, as it allows fetching a post and comments in a single query.
        $lookup: {
            from: "customers",If each post can have thousands of comments, embedding would lead to very large documents, which hurts performance and exceeds MongoDB’s document size limit (16MB).
            localField: "customerId",
        }onal queries or $lookup for retrieval.
    }            as: "customer"
]);
```
**Explanation:**
js
$lookup performs a left outer join: for each order, it looks up matching customer documents by matching customerId with _id.
Edit
If there is no matching customer, the customer field will be an empty array [] (not null).nics", "books", "clothing"] } });
.products.find({
This means all orders appear in the output; unmatched joins do not filter out documents but show empty join results.r: [
{ category: "electronics" },
---
lothing" }
## 5. Update vs Replace

```js
    { name: "Alice", age: 30 }users.updateOne(
);bjectId("abc123") },h queries are logically equivalent: find documents where category matches any of the values.
```
**Explanation:**

This operation will replace the entire document with { name: "Alice", age: 30 }, removing all other fields!harder to read.

This is because update operators like $set are missing, so MongoDB treats it as a replacement document.

To update fields safely without removing others, use update operators:
Explanation:
```js
db.users.updateOne(turns a single document, stopping the query after finding the first match. It’s optimized for this use case.
    { _id: ObjectId("abc123") },
    { $set: { name: "Alice", age: 30 } }
);
```ecially when you want just one result.

---

## 6. Transactions and Atomicity
Explanation:
**Explanation:**
MongoDB atomicity applies only at the single-document level by default.nts can slow queries, especially if many fields are returned, because MongoDB reads and transfers the entire document.

Deducting money from one account and adding to another involves multi-document updates. Without transactions, if the process crashes halfway, one update might succeed and the other fail, causing inconsistency.Updates to large documents are more expensive since they may require moving the document on disk if it grows beyond allocated space (causing fragmentation).

Multi-document transactions ensure all-or-nothing behavior, preserving data integrity.MongoDB has a 16MB document size limit; large embedded arrays risk hitting this.

Alternatives include designing your schema to use single-document atomic updates (embedding), or implementing compensating actions and retries in your application logic, but these are more complex and error-prone.To mitigate:

---Use referencing for large or unbounded arrays.

## 7. Schema Design: Embedding vs ReferencingProject only necessary fields in queries to reduce network overhead.

**Explanation:**Use schema design to keep documents compact.

Embedding comments inside the blog post is fine if the number of comments is small and bounded, as it allows fetching a post and comments in a single query.Consider MongoDB’s bucket pattern for very large datasets.
If each post can have thousands of comments, embedding would lead to very large documents, which hurts performance and exceeds MongoDB’s document size limit (16MB).

Referencing comments in a separate collection scales better, supports pagination, and avoids document bloat. However, it requires additional queries or $lookup for retrieval.

The choice balances read performance vs. document size and update complexity.

---

## 8. Query Using $in vs Multiple $or Conditions

db.products.find({ category: { $in: ["electronics", "books", "clothing"] } });
db.products.find({“Applying $project before $match forces MongoDB to process every document to reshape it before filtering. This wastes resources if many documents get filtered out later. By putting $match first, we reduce the data early, so $project only processes the filtered subset, improving efficiency by minimizing workload and memory usage.”
    $or: [
        { category: "electronics" },n Results
        { category: "books" },
        { category: "clothing" }“The $lookup stage performs a left outer join, adding an array field with matching documents from the foreign collection. If no matching customer is found for an order, the customer field will be an empty array. This ensures all orders are preserved in the output, and you can detect missing related documents by checking if the array is empty.”
    ]
});eplace
```
**Explanation:**“The query will replace the entire document with { name: 'Alice', age: 30 }, removing all other fields, which is usually unsafe unless that is intended. To update just the name and age fields without losing other data, we should use the $set operator like this:

js
Copy
Edit
Both queries are logically equivalent: find documents where category matches any of the values.sers.updateOne(
_id: ObjectId("abc123") },
$in is more concise and often optimized internally.Alice", age: 30 } }

$or with many conditions can be less efficient and harder to read.ps the rest intact.”

$in is preferred for matching multiple values on the same field.
Sample Answer:
---operations are atomic, but multi-document operations like transferring funds between accounts need multi-document transactions to maintain consistency. Without transactions, one update could succeed while the other fails, causing inconsistent state. Using a transaction groups the operations so either both succeed or both fail. If you want to avoid transactions, you can design your data model to keep related data in a single document for atomic updates, or implement compensation logic in the application, but that adds complexity and risk.”

## 9. findOne() vs find().limit(1)
Sample Answer:
**Explanation:**nt is fine when the number of comments is small and bounded because it allows efficient retrieval of a post and its comments in one query. But if the comments grow large (thousands), the document can become very large, hitting MongoDB’s 16MB limit and causing performance degradation on reads and writes. Referencing comments in a separate collection is better for scalability, supports pagination, and reduces document size, but requires extra queries or $lookup to fetch comments.”
findOne() returns a single document, stopping the query after finding the first match. It’s optimized for this use case.
8. Query Using $in vs Multiple $or Conditions
find().limit(1) returns a cursor with one document, which you then need to iterate or extract.
es are logically equivalent and will return the same results. However, $in is more concise and generally more efficient because it is optimized internally by MongoDB to handle multiple values in a single field. Using $or with many conditions can be more verbose and slightly slower, especially with large lists. I’d prefer $in for readability and performance.”
findOne() is more convenient and slightly more efficient for retrieving a single document, especially when you want just one result.
9. findOne() vs find().limit(1)
Use find() when you want a cursor to iterate over results; use findOne() for single document fetch.
urns a single document directly and is optimized for that purpose, making it slightly more efficient and convenient. find().limit(1) returns a cursor with one document, which you then need to iterate or extract. Use findOne() when you want exactly one document quickly; use find() when you plan to work with multiple documents or want to chain more cursor operations.”
---
10. Impact of Large Documents
## 10. Impact of Large Documents

Large documents can slow queries, especially if many fields are returned, because MongoDB reads and transfers the entire document.

Updates to large documents are more expensive since they may require moving the document on disk if it grows beyond allocated space (causing fragmentation).

MongoDB has a 16MB document size limit; large embedded arrays risk hitting this.

To mitigate:

- Use referencing for large or unbounded arrays.
- Project only necessary fields in queries to reduce network overhead.
- Use schema design to keep documents compact.
- Consider MongoDB’s bucket pattern for very large datasets.

---

## 1. Query Behavior
“With an index only on price, MongoDB will efficiently filter documents by price but will still scan all documents with price > 100 to check the category. This means the query is only partially covered by the index and can be inefficient if many documents match the price condition. However, if we use a compound index { category: 1, price: 1 }, MongoDB can use the index to filter first by category and then by price, significantly reducing scanned documents because the index entries are sorted first by category. This compound index improves query selectivity and performance, especially when category is more selective or frequently filtered.”

---

## 2. Array Query Ma
“The $elemMatch operator ensures that all the conditions apply to the same array element. So here, we’re looking for users who have a hobby where type is 'sport' and frequency is at least 3 in the same array element. Without $elemMatch, MongoDB checks if any array element matches type: 'sport' and any element matches frequency >= 3, but those could be different elements, potentially returning false positives. $elemMatch is essential for accurate matching when multiple conditions must apply within the same nested document in an array.”

---

## 3. Aggregation Pi
“Applying $project before $match forces MongoDB to process every document to reshape it before filtering. This wastes resources if many documents get filtered out later. By putting $match first, we reduce the data early, so $project only processes the filtered subset, improving efficiency by minimizing workload and memory usage.”

---

## 4. $lookup Join R
“The $lookup stage performs a left outer join, adding an array field with matching documents from the foreign collection. If no matching customer is found for an order, the customer field will be an empty array. This ensures all orders are preserved in the output, and you can detect missing related documents by checking if the array is empty.”

---

## 5. Update vs Repl
“The query will replace the entire document with { name: 'Alice', age: 30 }, removing all other fields, which is usually unsafe unless that is intended. To update just the name and age fields without losing other data, we should use the $set operator like this:

```js
db.users.updateOne(
    { _id: ObjectId("abc123") },
    { $set: { name: "Alice", age: 30 } }
);
```
This updates only those fields and keeps the rest intact.”

---

## 6. Transactions a
“In MongoDB, single-document operations are atomic, but multi-document operations like transferring funds between accounts need multi-document transactions to maintain consistency. Without transactions, one update could succeed while the other fails, causing inconsistent state. Using a transaction groups the operations so either both succeed or both fail. If you want to avoid transactions, you can design your data model to keep related data in a single document for atomic updates, or implement compensation logic in the application, but that adds complexity and risk.”

---

## 7. Schema Design:
“Embedding comments inside the post document is fine when the number of comments is small and bounded because it allows efficient retrieval of a post and its comments in one query. But if the comments grow large (thousands), the document can become very large, hitting MongoDB’s 16MB limit and causing performance degradation on reads and writes. Referencing comments in a separate collection is better for scalability, supports pagination, and reduces document size, but requires extra queries or $lookup to fetch comments.”

---

## 8. Query Using $i
“The two queries are logically equivalent and will return the same results. However, $in is more concise and generally more efficient because it is optimized internally by MongoDB to handle multiple values in a single field. Using $or with many conditions can be more verbose and slightly slower, especially with large lists. I’d prefer $in for readability and performance.”

---

## 9. findOne() vs f
“findOne() returns a single document directly and is optimized for that purpose, making it slightly more efficient and convenient. find().limit(1) returns a cursor with one document, which you then need to iterate or extract. Use findOne() when you want exactly one document quickly; use find() when you plan to work with multiple documents or want to chain more cursor operations.”

---

## 10. Impact of Lar
“Large documents increase query and update costs because MongoDB reads and writes the entire document, leading to higher IO and network usage. If a document grows beyond its allocated space, it may need to be moved on disk, causing fragmentation and slowing operations. To mitigate, design your schema to avoid embedding large arrays or deeply nested data. Use referencing for large or unbounded data and project only required fields during queries to reduce payload size.”
ge Documents  
**Sample Answer:**  ind().limit(1)  
**Sample Answer:**  n vs Multiple $or Conditions  
**Sample Answer:**   Embedding vs Referencing  
**Sample Answer:**  nd Atomicity  
**Sample Answer:**  ace  
**Sample Answer:**  esults  
**Sample Answer:**  peline with $match and $project  
**Sample Answer:**  tching  
**Sample Answer:**   and Index Use  
**Sample Answer:**  ts increase query and update costs because MongoDB reads and writes the entire document, leading to higher IO and network usage. If a document grows beyond its allocated space, it may need to be moved on disk, causing fragmentation and slowing operations. To mitigate, design your schema to avoid embedding large arrays or deeply nested data. Use referencing for large or unbounded data and project only required fields during queries to reduce payload size.”**Explanation:**
