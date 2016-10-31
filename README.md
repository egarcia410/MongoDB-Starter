# Getting Started with MongoDB
---

## Prerequisite:
1. Install [MongoDB](https://docs.mongodb.com/master/installation/)

## Creating Customer Database
1. Open a terminal window (or a command prompt for Windows) and run the mongo shell.

2. Once inside mongo shell, create a Customer database

        > use customers

3. Create an AdminUser.

        > db.createUser( { "user" : "Tammy",
                 "pwd": "1234",
                 "roles" : [ { role: "clusterAdmin", db: "admin" },
                             { role: "readAnyDatabase", db: "admin" },
                             "readWrite"
                             ] },
               { w: "majority" , wtimeout: 5000 } )

4. Create a Collections.

        > db.createCollection('customers')

5. Insert more customers into the `customers` collection.

        > db.customers.insert([
                {
                    first_name:"April", last_name:"Ludgate"
                },
                {
                    first_name:"Andy", last_name:"Dwyer"
                },
                {
                    first_name:"Leslie", last_name:"Knope"
                },
                {
                    first_name:"Ron", last_name:"Swanson"
                },
                {
                    first_name:"Jerry", last_name:"Gergich"
                }
            ])

6. Return all the customers in the `customers` collection in a pretty format.

        > db.customers.find().pretty()

7. Insert new customers with additional fields.

        > db.customers.insert({first_name:"Tom", last_name: "Haverford", gender:"male", age: 33, birthdate: new Date('Feb 23, 1983')})

        > db.customers.insert({first_name:"Ben", last_name: "Wyatt", gender:"male", age: 43, birthdate: new Date('Apr 3, 1973')})

8. Query customers who are male.

        > db.customers.find({gender:"male"})

9. Query customers who are male and display first name only.

        > db.customers.find({gender:"male"}, {first_name: 1})

10. Query one specific customer by first name.

        > db.customers.findOne({first_name:"Ron"})

11. Update a customers last name whose first name is April.

        > db.customers.update({first_name:"April"}, {$set: {last_name: "Dwyer"}})

12. Inserting a customer who doesn't exist with update, use `upsert` - Update/Insert.

        > db.customers.update({first_name: "Ann"}, {$set: {
                first_name: "Ann",
                last_name: "Perkins",
                age: "30"
            }}, {upsert: true})

13. Remove customer's age with the last name of Perkins.

        > db.customers.update({last_name: "Perkins"}, {$unset: {age: 1}})

14. Increment customer Tom's age by one.

        > db.customers.update({first_name: "Tom"}, {$inc: {age: 1}})

15. Remove a customer from the collection.

        > db.customers.remove({first_name: "Jerry"}, true)

    >Note: The second parameter `true` will only delete just one Jerry, if `false` it will delete all Jerrys. When deleting, it is safer to delete by unique ID, not by first name.

