Warning: Each character in MongoDB is case sensitive
Database ==🡺 Collections ==🡺 Documents ==🡺
Database - local
Collection - player
Document (Record) - 
      {  
         "position":"Right Wing",
         "id":8465166,
         "weight":200,
         "height":"6' 0\"",
         "imageUrl":"http://1.cdn.nhle.com/photos/mugs/8465166.jpg",
         "birthplace":"Seria, BRN",
         "age":37,
         "name":"Craig Adams",
         "birthdate":"April 26, 1977",
         "number":27
      }

db.collection.insert () - for one document

for eg.
db.players.insert(
     {
     “name”:”Ram”,
    “DOB” : “20-02-2015”
     }
)

db.collection.insert ( [ ] ) - for multiple documents

db.collection.find( )  - to find in records
db.collection.find( ).pretty() – to display in JSON format
db.collection.findOne( ) -  to display first record entered in Collection.
db.collection.remove ( { } )  -  to remove document from collection
eg.
db.players.update (
  {"_id" : ObjectId("55cf7a33cf899002fbed9892")} ,
 // my updated matter will be in this block
  {  
         "position":"Left Wing",
         "id":8475761,
         "weight":195,
         "height":"6' 2\"",
         "imageUrl":"http://1.cdn.nhle.com/photos/mugs/8475761.jpg",
         "birthplace":"Gardena, CA, USA",
         "age":24,
         "name":"Beau Bennett",
         "birthdate":"November 27, 1991",
         "number":19    }
)
db.players.find(
                 {"position" : "Right Wing", "id" : 8475761}
).pretty()
============================================================
db.players.find (
    {"age":{ $gt : 30 } }     
)
$ gt = greater than
$ lt = less than
$ gte/lte = greater than equal to/less than equal to
$ ne = not equal
If we want to deactivate any field, use as follows:
db.players.find(
   {"position":"Right Wing"},
   {"name":1,_id:0}
)

> db.players.find(
   {"position":"Right Wing"},
   {"name":1,_id:0}
)
{ "name" : "Beau Bennett" }
{ "name" : "Steve Downie" }
{ "name" : "Pascal Dupuis" }
{ "name" : "Patric Hornqvist" }

> db.players.find(
   {"position":"Right Wing"},
   {"name":1,_id:0}
).limit(3)
{ "name" : "Beau Bennett" }
{ "name" : "Steve Downie" }
{ "name" : "Pascal Dupuis" }

> db.players.find(
   {"position":"Right Wing"},
   {"name":1,_id:0}
).skip(1)
{ "name" : "Steve Downie" }
{ "name" : "Pascal Dupuis" }
{ "name" : "Patric Hornqvist" }

To know about particular status of MongoDB documents, you can enter these parameters:

> db.bank.find(
     {"age":{$lt:23}}
).explain("executionStats")

{
	"queryPlanner" : {
		"plannerVersion" : 1,
		"namespace" : "bank.bank",
		"indexFilterSet" : false,
		"parsedQuery" : {
			"age" : {
				"$lt" : 23
			}
		},
		"winningPlan" : {
			"stage" : "COLLSCAN",
			"filter" : {
				"age" : {
					"$lt" : 23
				}
			},
			"direction" : "forward"
		},
		"rejectedPlans" : [ ]
	},
	"executionStats" : {
		"executionSuccess" : true,
		"nReturned" : 2,
		"executionTimeMillis" : 33,
		"totalKeysExamined" : 0,
		"totalDocsExamined" : 35,
		"executionStages" : {
			"stage" : "COLLSCAN",
			"filter" : {
				"age" : {
					"$lt" : 23
				}
			},
			"nReturned" : 2,
			"executionTimeMillisEstimate" : 0,
			"works" : 37,
			"advanced" : 2,
			"needTime" : 34,
			"needFetch" : 0,
			"saveState" : 0,
			"restoreState" : 0,
			"isEOF" : 1,
			"invalidates" : 0,
			"direction" : "forward",
			"docsExamined" : 35
		}
	},
	"serverInfo" : {
		"host" : "mayur-PC",
		"port" : 27017,
		"version" : "3.0.5",
		"gitVersion" : "8bc4ae20708dbb493cb09338d9e7be6698e4a3a3"
	},
	"ok" : 1
}

If want to make indexing, we can give this command:

db.bank.ensureIndex({“age”:1})

where 1 stands for True

To get total count for numbers,

db.bank.getIndexes()

[
	{
		"v" : 1,
		"key" : {
			"_id" : 1
		},
		"name" : "_id_",
		"ns" : "bank.bank"
	},
	{
		"v" : 1,
		"key" : {
			"age" : 1
		},
		"name" : "age_1",
		"ns" : "bank.bank"
	}
]

db.bank.dropIndex( { “age” : 1 } )










Aggregation

> db.bank.aggregate({
   $group : {
       _id :"$eyeColor",
       total : {$sum : 1}
   }
})
This query stands for creating group with some category, here say, $eyeColor and after getting eyecolors I want to get total of all eyecolors separately which is represented by total : {$sum : 1} where 1 is having status “True”.

{ "_id" : "green", "total" : 14 }
{ "_id" : "brown", "total" : 12 }
{ "_id" : "blue", "total" : 9 }

To get average age,

db.bank.aggregate ({
        $group: {
          _id : “$gender”,
          averageAge : {$avg : “$age”}
       }
})

To get maximum balance based on gender,

> db.bank.aggregate ({
        $group: {
          _id : "$gender",
          averageAge : {$max : "$balance"}
       }
})
{ "_id" : "male", "maxBal" : "$3,818.97" }
{ "_id" : "female", "maxBal" : "$3,960.64" }
