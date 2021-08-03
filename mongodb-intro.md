#backend

# MongoDB & Mongoose

## Intro

## NoSQL

Para bases de datos no relacionales. Ventajas:

- Maneja Big Data
- Los modelos de datos no utilizan estructuras predefinidas
- NoSQL soporta dato no estructurada
- Más barato el soporte
- Muy escalable

## MongoDB

## Commont terms

- _id: como primary key
  ```
  objectID("548y484y48y484")
  {
    "_id": 3,
    "item": "xyz",
    "price": 5,
    "quantity": 18
  }
  ```
- Collection: Es un grupo de MongoDB documents
- Document: Es un conjunto de claves y valores, lo equivalente a una fila
- Cursor: El resultado que nos genera una query
- Fields: Son las columnas de la tabla

## Getting started

GUI: NoSQL Booster, para manejarlo graficamente

## Basic commands

- help: Sirve para mostrar ayuda
- show: Para enseñar cualquier cosa ("show dbs")
- mongoimport: Nos permite importar json file o csv a la base de datos
  
# Live coding

## Commands

- count()
  db.students.count()

- sort()
  db.students.find({}).sort({ age: 1 }).pretty()

- limit()
  db.students.find({}).sort({ age: 1 }).limit(2).pretty()

- Projection
  db.students.find({}, { name: 1 }).pretty()

- Excluding elements
  db.students.find({}, { grades: 0 }).pretty()

-------------------------------------------------

Operators

- $eq (igual a)
  db.movies.find({ name: "Homeland" }, { name: 1 }).pretty()
  db.movies.find({ name: { $eq: "Homeland" } }, { name: 1 }).pretty()

- $ne (diferente a)
  db.movies.find({ name: { $ne: "Homeland" } }, { name: 1 }).limit(5).pretty()

- $gt (mayor que)
  db.movies.find({ runtime: { $gt: 60 }}, { name: 1, runtime: 1 }).limit(5).pretty()

- $gte (mayor o igual que)
  db.movies.find({ runtime: { $gte: 60 }}, { name: 1, runtime: 1 }).limit(5).pretty()

- $lt (menor que)
  db.movies.find({ runtime: { $lt: 60 }}, { name: 1, runtime: 1 }).limit(5).pretty()

- $lte (menor o igual que)
  db.movies.find({ runtime: { $lte: 60 }}, { name: 1, runtime: 1 }).limit(5).pretty()

- $in (entre)
  db.movies.find({ runtime: { $in: [ 30, 120 ]}}, {runtime: 1}).pretty()

- $nin (fuera de)
  db.movies.find({ runtime: { $in: [ 30, 120 ]}}, {runtime: 1}).pretty()

----------------------------------------------

- Subdocuments: Dentro de cada document puede haber una subpropiedad, que también se puede acceder a ella
  db.movies.find({ "rating.average": 8 }, {"rating.average": 1}).limit(1).pretty()

-----------------------------------------------

- Array elements:
  db.movies.find({ genres: "Drama" }, {genres: 1}).limit(1).pretty()

- Array elements in subdocuments
  db.movies.find({ "schedule.days": "Sunday" }, {"schedule.days": 1}).limit(1).pretty()

------------------------------------------------

Logical operators

- $and, $not, $nor, $or
  db.movies.find({ $and: [{ language: "English" }, { "rating.average": 8 }] }, {language: 1, "rating.average": 1
}).limit(2).pretty()

-------------------------------------------------

Update Operators

-$inc Incrementa el valor
  db.movies.updateOne({ name: "Bitten" }, { $inc: { runtime: 1 }})
  // runtime de la película "Bitten" pasa de 60 a 61

- $min Setea un valor si el valor que le pasamos es menor que el actual
  db.movies.updateOne({ name: "Bitten" }, { $min: { runtime: 40 }})
  // runtime era 60, pero como 40 es menor, runtime pasa a ser 40

- $set Para setear nuevas propiedades
  db.movies.updateOne({ name: "Bitten" }, { $set: { myNewProp: 1000 }})
  // La pelicula "Bitten" pasa a tener una nueva propiedad llamada "myNewProp"

- $rename Para renombrar una propiedad
  db.movies.updateOne({ name: "Bitten" }, { $rename: {myNewProp: "myRenamedProp"}})
  // La propiedad myNewProp pasa a ser myRenamedProp

- $unset Para eliminar la propiedad de un documento
  db.movies.updateOne({ name: "Bitten"}, { $unset: { myRenamedProp: ""}})
  // La pelicula "Bitten" deja de tener la propiedad myRenamedProp

- $push Para añadir un elemento a un array
  db.movies.updateOne({ name: "Bitten" }, { $push: { genres: "Boring"}})
  // Añade en el array "genres" la opción de "Boring"
  "_id" : ObjectId("5fec9a7c6a8ea453c3d1b62c"),
        "genres" : [
                "Drama",
                "Horror",
                "Romance",
                "Boring"
        ]

- $each Para añadir un array de nuevos elementos a un array
  db.movies.updateOne({ name: "Bitten" }, { $push: { genres: { $each: ["a", "b", "c"] }}})
  // Añade al array "genres" los elementes a, b y c
  "_id" : ObjectId("5fec9a7c6a8ea453c3d1b62c"),
        "genres" : [
                "Drama",
                "Horror",
                "Romance",
                "Boring",
                "a",
                "b",
                "c"
        ]

- $pop Elimina el último elemento (1) o el primero (-1) de un array
  db.movies.updateOne({ name: "Bitten" }, { $pop: { genres: 1 }})
  //Elimina el último elemento de genres
  db.movies.updateOne({ name: "Bitten" }, { $pop: { genres: -1 }})
  //Elimina el primer elemento de genres

- $pull Elimina un conjunto de elementos que hace match en una query usando $in
  db.movies.updateOne({ name: "Bitten" }, { $pull: { genres: { $in: ["a", "b"] }}})
  // Elimina de genres los elementos a y b

---------------------------------------------------------------

Removing Documents from MongoDB

- deleteOne(): Eliminar un documento de una colección
  db.movies.deleteone({ name: "Bitten" })

- deleteMany(): Para eliminar varios documentos de una colección usando el $in para indicar varios valores
  db.movies.deleteMany({ name: { $in: ["Grimm", "Lost Girl", "The Strain"] }})
  

  
  






# Resources

https://github.com/assembler-school/mongodb-intro-workshop



