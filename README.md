# go-mongo-db

## Installation

```
npm i github:MidSpike/go-mongo-db
```

## Usage

```js
/* Importing GoMongoDB */
const GoMongoDB = require('go-mongo-db');

async function main() {
    /* Creating a GoMongoDB instance */
    // process.env.MONGO_CONNECTION_URL = 'mongodb://username:password@hostname:port/'
    const connection_url = process.env.MONGO_CONNECTION_URL;
    const go_mongo_db = new GoMongoDB(connection_url);

    /* Finding document(s) in a database collection */
    const database_name = process.env.MONGO_DATABASE_NAME;
    const collection_name = process.env.MONGO_USERS_COLLECTION_NAME;
    const find_query_filter = {
        'gender': 'male',
        'age': 35,
    };
    const all_matching_documents = await go_mongo_db.find(database_name, collection_name, find_query_filter);
    const [ first_matching_document ] = await go_mongo_db.find(database_name, collection_name, find_query_filter);

    /* Adding document(s) to a database collection */
    const documents_to_add = [
        {
            'id': '34565232141264',
            'name': 'John Doe',
            'gender': 'male',
            'age': 26,
        }, {
            'id': '34561234213412'
            'name': 'Jane Doe',
            'gender': 'female',
            'age': 43,
        },
    ];
    const all_matching_documents = await go_mongo_db.add(database_name, collection_name, documents_to_add);

    /* Updating document(s) in a database collection */
    const update_filter = [
        {
            'id': '34565232141264',
        },
    ];
    const update_operations = {
        $set: {
            'age': 27,
        },
    };
    const update_options = {
        upsert: true, // used to make a new document if it doesn't exist already
    };
    await go_mongo_db.add(database_name, collection_name, update_filter, update_operations, update_options);

    /* Removing document(s) from a database collection */
    const remove_filter = [
        {
            'id': '34561234213412',
        },
    ];
    await go_mongo_db.remove(database_name, collection_name, remove_filter);
}
main();
```
