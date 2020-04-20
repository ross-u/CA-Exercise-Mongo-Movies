# Exercise - MongoDB Movies

 

<br>



## Intro

![img](https://i.imgur.com/NzalR30.png)

When working with any Database, there are a few operations that we will always need to use. These operations are so popular that we have an acronym for it: CRUD stands for create, read, update and delete:

![img](https://i.imgur.com/CRowB2i.png)

## Getting Started

<br>



### Fork and Clone the repo

```bash
git clone https://github.com/ross-u/CA-Exercise-Mongo-Movies.git

cd CA-Exercise-Mongo-Movies
```

<br>


### Start the MongoDB

If you already have your MongoDB running, you can skip this step.

Additionaly, **remember to check if your MongoDB is running every time you restart your machine and start it if needed running the below commands.**



### Linux

```bash
# Run mongod
sudo service mongod start

# Check if mongod process is running
ps -e | grep 'mongod'
```



### Mac

```bash
# Run mongodb
brew services start mongodb-community

# Check if mongod process is running
ps -e | grep 'mongod'
```





<br>



### Import the data via `mongoimport`

Using the terminal navigate to the directory of the cloned repo on your system. Then using `mongoimport`, import the JSON data to the database `video`. Import the data from the `movies.json` file into the collection `movies`.

```bash
# Import the data from `movies.json` to the `video` database, collection `movies`
mongoimport --db=video --collection=movies --file=movies.json --jsonArray
```



<br>



### Open the `mongo` shell

```bash
# Run mongo shell
mongo
```



#### In the `mongo` shell:

```js
// List databases
show dbs

// Switch to database `video`
use video

// Show collections
show collections

// List all the documents in the `movies` collection
db.movies.find().pretty()
```

<br>

## Reference

You may use the following Lecture Notes as your reference:

### [MongoDB - Lecture Notes](https://gist.github.com/ross-u/cf1f144c7706610e9f70c2700f8b391d)

<br>

## Tasks

### 1. Retrieve all the documents  from the `movies` collection:

**<u>Your query</u>**:

```js
db.movies.find()
```

  

<br>



### 2. Retrieve all the documents  from the  `movies` collection and prettify the result:

**<u>Your query</u>**:

```js
db.movies.find().pretty()
```

  

<br>



### 3. Retrieve all the documents  from the  `movies` collection where the field `year` is  2000:

**<u>Your query</u>**:

```js
db.movies.find( {year: 2000  } )
```

  

<br>



### 4. Retrieve all the documents from the `movies`  collection where the field `rate` is "8.8"

**<u>Your query</u>**:

```js
db.movies.find( {rate: "8.8"})
```

 

<br>



#### 5. Retrieve the movie with the field `_id` `"5cbf03ca570ffc7ef7ac4861"`

To specify an **`ObjectId`** type, use the format **`ObjectId(’id’)`**, 

**<u>Your query</u>**:

```js
db.movies.find( {_id: ObjectId( "5e9d9ac1b156e84cbfe66b80")})
```

  

<br>



### 6.  Retrieve all documents in our collection where the field `year` equals `2000` **AND** the `rate` equals `'8.5'`.

**<u>Your query</u>**:

```js
db.movies.find(  {$and:[{rate:"8.5"},{year:2000}  ]   }
```

  

<br>



### 7. Retrieve all documents from the `movies` collection where the field `year` equals `2000` **OR** the `year` equals `2005`.

**<u>Your query</u>**:

```js
db.movies.find({$or:[{year:2000},{year:2005}]})
```

  

<br>



### 8. Retrieve all documents from the `movies` collection that do not have a rate of “9.0” and limit the result to 10 documents.

**<u>Your query</u>**:

```js
db.movies.find({rate:{$ne: 9}}).limit(10)
```

 

<br>

 

### 9. Retrieve all documents from the `movies` collection where field `director` is `not` "Steven Spielberg" `or` "Quentin Tarantino".  

### Display only `title` and `director` fields for each document.

**<u>Your query</u>**:

```js
db.movies.find(  {$nor:[{director: "Steven Spielberg"},{director:"Quentin Tarantino"}]}, {title:1, director:1, _id:0})
```

  

<br>



### 10. Retrieve all documents from the `movies` collection, using the projection return only the fields `title`, `year`, `genre` and exclude field `_id`.

**<u>Your query</u>**:

```js
db.movies.find( {}, {title:1, genre: 1, year: 1, _id: 0}  )
```

  

<br>



### 11. Retrieve all documents from the `movies` collection including only the field `title` using projection and sorting them by `name`.

**<u>Your query</u>**:

```js
db.movies.find({},{title:1, _id:0}).sort({name: 1})
```

  

<br>



### 12. Retrieve all documents from the `movies` collection including only `title`  and `director` fields ,  sort them by `name` , skipping first 5 documents

**<u>Your query</u>**:

```js
db.movies.find({},{title:1, director:1, _id: 0}).skip(5)
```

  

<br>



### 13. Retrieve all documents from the `movies` collection where `director` field `equals`  "Robert Zemeckis"

**<u>Your query</u>**:

```js
db.movies.find({director:"Robert Zemeckis"})
```

  

<br>



### 14. Retrieve all documents from the `movies` collection where the `rate` field is different than "8.5". Using projection include only `title` and `rate` field, excluding `_id`

**<u>Your query</u>**:

```js
db.movies.find({rate:{$ne:8.5}} , {title: 1, rate: 1, _id: 0})
```

  

<br>



### 15. Retrieve all documents from the `movies` collection where the `year` field is greater than or equal 2015. Using projection include only `title` , `year`and `director` fields.

**<u>Your query</u>**:

```js
db.movies.find({year: {$gte: 2015}   }  ,{title:1, year:1, director:1, _id:0})
```

  

<br>



### 16. Retrieve all documents from the `movies` collection where the `year` field is less than 2000. Using projection include only `title` , `year`and `director` fields.

**<u>Your query</u>**:

```js
db.movies.find({year: {$lt: 2000}   }  ,{title:1, year:1, director:1, _id:0})
```

  

<br>



### 17. Retrieve all documents from the `movies` collection created in the years 2000, 2005 and 2010. Sort the result by `year` in ascending order.

**<u>Your query</u>**:

```js
db.movies.find(  {$or:[{year:2000},{year:2005},{year:2010}]  }  ).sort({year:1})
```

  

<br>



### 18. Retrieve all documents from the `movies` collection created in the years 1999 and 2010 and excluding the movie with `title` "Inception"

```js
db.movies.find({ $and:[ { $or: [{year: 1999}, {year: 2010}] }, { name: {$ne: "Inception"} },],})
```

 

<br>



### 19. Delete documents from the `movies` collection created in the year 1999. 

**<u>Your query</u>**:

```js
db.movies.deleteMany({year: 1999})
```



<br>



### 20. Delete document from the `movies` collection with the `_id`  "5cbf03ca570ffc7ef7ac4869".

 **<u>Your query</u>**:

```js
db.movies.deleteOne({_id: ObjectId("5e9d9ac1b156e84cbfe66b89")})
```

 

<br>



### 21. Update all documents from the `movies` collection created in the `year` 2017 and add an additional field named `rating`: 

```js
var ratingObj = {
  rating: "TV-G",
  "violence": false,
  "drug_use": false,
  "strong_language": false
}
```

###  

**<u>Your query</u>**:

```js
db.movies.updateMany(  {year:2017   }  ,{$set: ratingObj})
```

 

 

<br>



### 22. Update the document from the `movies` collection with  `title` "Dunkirk" and set `rating`  to "PG-13" and fields  `violence` and `strong_language` to `true`  : 



**<u>Your query</u>**:

```js
db.movies.updateOne({title:"Dunkirk"},{$set:{rating:"PG-13",violence:true,strong_language:true}})
```

 

 

<br>





### 23. Delete documents from the `movies` collection using the titles provided in the array:

```js
let moviesToDelete = ["12 Angry Men", "Se7en", "Cidade de Deus", "Braveheart"]
```

###  

**<u>Your query</u>**:

```js
db.movies.deleteMany( { title: { $in: moviesToDelete } } )
```





 

<br>

