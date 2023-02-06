# REST APIs project

## Description:
This is a project made in relation with udemy course: REST APIs with Flask and Python in 2023.

## Endpoints
### Item
- endpoint: `/item`
- methods: `GET`, `POST`
- parameters: `ITEM_DATA`
- returns: all items if get request, new item with post request.

### Item by id
- endpoint: `/item<int:item_id>`
- methods: `GET`, `PUT`, `DELETE`
- parameters: `ITEM_ID` `ITEM_DATA` 
- returns: updated item, deleted item, item by id.

### Store
- endpoint: `/store`
- methods: `GET`, `POST`
- parameters: `store_data`
- returns: all stores if get request, new store with post request.

### Store by id
- endpoint: `/item/<int:store_id>`
- methods: `GET`, `DELETE`
- parameters: `store_id`
- returns: store by id, deleted store

## Resources
I created a folder `resources` to improve the structure by splitting items and stores into their own files.
Then creating a `blueprint` for each related group of resources.
Followed by adding `MethodView` Class where each method maps to the endpoint the method is associated with.
Then importing the `blueprints`, configurating `Flask-Smorest` and register the blueprints in app.py with `Flask-Smorest`.

## Schemas
For validation purposes I have used `marshmallow` and its property; `fields` to validate incoming data wether its `required`, `string`, `dump_only` etc. 
Furthermore, I have used `@blp.arguments()` and `@blp.response()` to decorate certain requests under their respective endpoints, where we once again can use `schemas` as argument/response to format what data the function takes and outputs.

## Data storage 
Implemented a relational database: `SQLite3`, and in order to interact with that database we will use `SQLAlchemy`

### Models
Created models for resources and each model has a few properties that let us interact with the database through the model.

### One-to-many relationships
With `models` we can now create relationships between these models.
For an example can `class StoreModel` have a relationship with items, where `db.relationship` will connect these two tables together. The models having relationship makes so we can modify the mashmallow schemas so they will return some or all of the information about the related models. This is done with the `Nested` mashmallow field.

### Many-to-many relationships

Unlike One-to-many relationships, many-to-many requires a secondary table to link between a specific tag and a specific item, that way we can tag the same item with multiple different tags. 

 ### JSON Web Token

With JWTs we can now apply authentication on certain endpoints, that the user is in fact logged in and the details are matched with the user in database. The JWT is generated upon login between the client and database, and can be cached so the user doesnt have to keep authenticating upon requests.

## Database migrations

Along the project we have used different databases in the form a python dictionary and now SQLite, with changes in the models it will eventually be out of sync and causing problems with SQLAlchemy, therefore with migrations its possible to modify existing models and Alembic will detect these changes to models and upgrade the database to meet the modifications.
