mongoose-diff-history
=============

Store all the differences any collection goes through it's lifecycle.

## Installation
---------------
###npm
``` sh
npm install mongoose-diff-history
```

## Operation
---------------
Each update will create a history record with [jsonDiff](https://github.com/benjamine/jsondiffpatch) of the change. This helps in tracking all the changes happened to an object from the beginning.

Following will be the structure of the diff history being saved:


diff Collection schema:

```
 _id : mongo id of the diff object
 collectionName: Name of the collection for which diff is saved
 collectionId : Mongo Id of the collection being modified
 diff: diff object
 user: User who modified
 reason: Why the collection is modified
 createdAt: When the collection is modified
 _v: version
```

## Usage
---------------
Use as you would any Mongoose plugin:

``` js
    var mongoose = require('mongoose'),
        diffHistory = require('mongoose-diff-history/diffHistory'),
        schema = new mongoose.Schema({ ... });
        schema.plugin(diffHistory.plugin);
```


## Helper Methods
---------------
You can get all the histories created for an object using following method:

``` js
  diffHistory.getHistories(modelName, ObjectId, <expandable fields>, function (err, histories) {

  }
```

## Example
---------------
I have created an example express service, demonstrating this plugin via an simple employee schema, checkout `example` folder.

## TODO
---------------
- Store a version along with the diff, this feature will be configurable.
- instance methods to fetch an older version of object