# MongoDB Library Database Project

## Introduction
This project demonstrates how to set up and interact with a MongoDB database for a library system. It includes creating a database, inserting book records, querying data, updating records, deleting data, using aggregation pipelines, indexing, and performing tests.

---

## 1. Setting Up MongoDB
### **Installation & Verification**
1. **Install MongoDB** (if not installed):  
   - [MongoDB Installation Guide](https://www.mongodb.com/docs/manual/installation/)
2. **Start the MongoDB server** (locally):
   ```sh
   mongod
   ```
3. **Check MongoDB version**:
   ```sh
   mongo --version
   ```
4. **Open MongoDB shell**:
   ```sh
   mongosh
   ```

---

## 2. Database & Collection Creation
### **Create the Database**
```js
use library  // Switch to or create the `library` database
```

### **Create the Books Collection**
```js
db.createCollection("books")
```

---

## 3. Inserting Data
Insert at least five book records into the `books` collection:
```js
db.books.insertMany([
    { title: "The Great Gatsby", author: "F. Scott Fitzgerald", publishedYear: 1925, genre: "Classic", ISBN: "9780743273565" },
    { title: "To Kill a Mockingbird", author: "Harper Lee", publishedYear: 1960, genre: "Fiction", ISBN: "9780061120084" },
    { title: "1984", author: "George Orwell", publishedYear: 1949, genre: "Dystopian", ISBN: "9780451524935" },
    { title: "The Catcher in the Rye", author: "J.D. Salinger", publishedYear: 1951, genre: "Classic", ISBN: "9780316769488" },
    { title: "The Road", author: "Cormac McCarthy", publishedYear: 2006, genre: "Post-Apocalyptic", ISBN: "9780307387899" }
])
```

---

## 4. Retrieving Data
Retrieve all books:
```js
db.books.find().pretty()
```
Retrieve books by a specific author:
```js
db.books.find({ author: "George Orwell" }).pretty()
```
Find books published after the year 2000:
```js
db.books.find({ publishedYear: { $gt: 2000 } }).pretty()
```

---

## 5. Updating Data
### **Update the publishedYear of a book**
```js
db.books.updateOne(
    { title: "1984" },
    { $set: { publishedYear: 1950 } }
)
```
### **Add a new field `rating` to all books**
```js
db.books.updateMany(
    {},
    { $set: { rating: 4.0 } }
)
```

---

## 6. Deleting Data
### **Delete a book by ISBN**
```js
db.books.deleteOne({ ISBN: "9780451524935" })
```
### **Remove all books of a particular genre**
```js
db.books.deleteMany({ genre: "Classic" })
```

---

## 7. Aggregation Pipeline
### **Find the total number of books per genre**
```js
db.books.aggregate([
    { $group: { _id: "$genre", totalBooks: { $sum: 1 } } }
])
```
### **Calculate the average published year of all books**
```js
db.books.aggregate([
    { $group: { _id: null, avgPublishedYear: { $avg: "$publishedYear" } } }
])
```
### **Identify the top-rated book**
```js
db.books.find().sort({ rating: -1 }).limit(1)
```

---

## 8. Indexing for Performance
### **Create an index on the `author` field**
```js
db.books.createIndex({ author: 1 })
```
### **Benefits of Indexing in MongoDB**
- **Faster Query Performance**: Improves the speed of search queries.
- **Optimized Sorting**: Sorting results becomes more efficient.
- **Efficient Read Operations**: Reduces the load on the database.
- **Better Query Execution Plans**: MongoDB uses indexes to fetch data efficiently.

---

## 9. Testing & Verification
### **Using MongoDB Shell**
```js
db.books.find().pretty()
```
### **Using MongoDB Compass**
1. Open MongoDB Compass.
2. Connect to your MongoDB server.
3. Navigate to the `library` database and `books` collection.
4. Run queries to verify data insertion and retrieval.

---


