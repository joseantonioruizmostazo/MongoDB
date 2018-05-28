# MongoDB - Práctica de Bases de Datos

<h1>1. Crear una base de datos</h1>

```console
> use clubes
switched to db clubes
```
Comprobamos en qué base de datos nos encontramos
```console
> db
clubes
```

<h1>2.Tener una colección</h1>

```console
> MongoDB Enterprise > db.createCollection('jugadores')
{ "ok" : 1 }
```

<h1>3.Insertar,modificar y borrar documentos en la colección</h1>
<h2>3.1 Insertar</h2>

```console
> MongoDB Enterprise > db.jugadores.insert({nombre: "Cristiano Ronaldo", edad: 31, equipo: "Real Madrid"})
WriteResult({ "nInserted" : 1 })
> MongoDB Enterprise > db.jugadores.insert({nombre: "Messi", edad: 30, equipo: "FC Barcelona"})
WriteResult({ "nInserted" : 1 })
> MongoDB Enterprise > db.jugadores.insert({nombre: "Sergio Ramos", edad: 32, equipo: "Real Madrid"})
WriteResult({ "nInserted" : 1 })
> MongoDB Enterprise > db.jugadores.insert({nombre: "Griezman", edad: 25, equipo: "Atl Madrid"})
WriteResult({ "nInserted" : 1 })
> MongoDB Enterprise > db.jugadores.insert({nombre: "Isco", edad: 24, equipo: "Real Madrid"})
WriteResult({ "nInserted" : 1 })
> MongoDB Enterprise > db.jugadores.insert({nombre: "Iniesta", edad: 33, equipo: "FC Barcelona"})
WriteResult({ "nInserted" : 1 })
```
<img src=./capturas/insertar.png width=600px>

<h2>3.2 Modificar</h2>
```console
MongoDB Enterprise > e = db.jugadores.findOne({nombre: "Isco"})
{
        "_id" : ObjectId("5b0c26458fabcc31ed191c53"),
        "nombre" : "Isco",
        "edad" : 24,
        "equipo" : "Real Madrid"
}
MongoDB Enterprise > e.edad = 26
26
MongoDB Enterprise > db.jugadores.update({nombre: "Isco"}, e)
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })
MongoDB Enterprise > db.jugadores.find({nombre: "Isco"})
{ "_id" : ObjectId("5b0c26458fabcc31ed191c53"), "nombre" : "Isco", "edad" : 26, "equipo" : "Real Madrid" }
```
<img src=./capturas/modificar.png width=600px>

<h2>3.3 Eliminar</h2>

```console
> MongoDB Enterprise > db.jugadores.remove({nombre: "Iniesta"})
WriteResult({ "nRemoved" : 1 })
```
<img src=./capturas/eliminar.png width=600px>

<h1>4 Crear un índice sobre un campo de la colección</h1>

```console
> MongoDB Enterprise > db.jugadores.createIndex({clubes: 1})
{
        "createdCollectionAutomatically" : false,
        "numIndexesBefore" : 1,
        "numIndexesAfter" : 2,
        "ok" : 1
}
```
<img src=./capturas/crearindice.png width=600px>

<h1>5. Realizar consultas en las que utilices mayor que, igual que, menor que.</h1>
<h2>5.1 Muéstrame aquellos jugadores cuya edad sea mayor que 28</h2>
```console
> MongoDB Enterprise > db.jugadores.find({"edad" : {$gt:28} })
{ "_id" : ObjectId("5b0c26198fabcc31ed191c50"), "nombre" : "Messi", "edad" : 30, "equipo" : "FC Barcelona" }
{ "_id" : ObjectId("5b0c26308fabcc31ed191c51"), "nombre" : "Sergio Ramos", "edad" : 32, "equipo" : "Real Madrid" }
{ "_id" : ObjectId("5b0c2b878fabcc31ed191c55"), "nombre" : "Cristiano Ronaldo", "edad" : 31, "equipo" : "Real Madrid" }
```

<img src=./capturas/mayorque.png width=600px>
<br/>
<h2>5.2 Muéstrame aquellos jugadores cuya edad sea menor que 30</h2>
```console
> MongoDB Enterprise > db.jugadores.find({"edad" : {$lt:28} })
{ "_id" : ObjectId("5b0c263b8fabcc31ed191c52"), "nombre" : "Griezman", "edad" : 25, "equipo" : "Atl Madrid" }
{ "_id" : ObjectId("5b0c26458fabcc31ed191c53"), "nombre" : "Isco", "edad" : 26, "equipo" : "Real Madrid" }
```
<img src=./capturas/menorque.png width=600px>
<br/>
<h2>5.3 Muéstrame aquellos jugadores cuya edad sea igual que 25</h2>
```console
> MongoDB Enterprise > db.jugadores.find({"edad" : 25 })
{ "_id" : ObjectId("5b0c263b8fabcc31ed191c52"), "nombre" : "Griezman", "edad" : 25, "equipo" : "Atl Madrid" }
```
<img src=./capturas/igualque.png width=600px>
<br/>
<h1>6. Realizar una consulta en la que los documentos se muestren ordenados y se limite el número de mostrados.</h1>
```console
> MongoDB Enterprise > db.jugadores.find().sort( {nombre: +1}).limit(2)
{ "_id" : ObjectId("5b0c2b878fabcc31ed191c55"), "nombre" : "Cristiano Ronaldo", "edad" : 31, "equipo" : "Real Madrid" }
{ "_id" : ObjectId("5b0c263b8fabcc31ed191c52"), "nombre" : "Griezman", "edad" : 25, "equipo" : "Atl Madrid" }
```
<img src=./capturas/ordenado.png width=600px>
<br/>
<h1>7.Realizar una consulta con agrupamiento y una función para mostrar la media, o suma, o la que tú decidas.</h1>
```console
> MongoDB Enterprise > db.jugadores.aggregate( [ {$group: {_id: "$equipo", repetidos: {$sum: 1}, "edad media": {$avg: "$edad"}}} ] )
{ "_id" : "FC Barcelona", "repetidos" : 1, "edad media" : 30 }
{ "_id" : "Atl Madrid", "repetidos" : 1, "edad media" : 25 }
{ "_id" : "Real Madrid", "repetidos" : 3, "edad media" : 29 }
```
<img src=./capturas/edadmedia.png width=600px>

