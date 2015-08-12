# ngDatabase
ngDatabase is a lite, very easy to use and powerful local storage solution for your Ionic apps.
You don't need to have a back-end or SQL background to understand this service.

With ngDatabase you can store any data as you want (text, number, date, object, ...) thanks to human-friendly methods names.
Work perfectly on desktop and mobile devices powered by Ionic Framwork (http://ionicframework.com/).

## Installation
### ngCordova and cordovaSQLite
First, install ndCordova to your project (http://ngcordova.com/docs/install/) :
```shell
bower install ngCordova
```
Don't forget to include the ng-cordova.js file and add ngCordova in your app dependencies :
```html
<script src="lib/ngCordova/dist/ng-cordova.js"></script>
```
```javascript
angular.module('myApp', ['ngCordova'])
```

Then, add the cordovaSQLite plugin :
```shell
cordova plugin add https://github.com/litehelpers/Cordova-sqlite-storage.git
```
### ngDatabase
* __Bower__ : bower install ng-database
* __NPM__ : npm install ng-database

Include the ng-database js file in your ptoject :
```html
<script src="path/to/your/lib/ng-database/src/ng-database.min.js"></script>
```
Then include ngDatabase dependency :
```javascript
angular.module('myApp', ['ngDatabase'])
```

## Usage

##### Important note : all of ngDatabase method must be used when the _deviceready_ event fired.

### Initialize ngDatabase
##### Prototype
```javascript
void init (object NGDB_SCHEMA)
```
##### Description
ngDatabase _init()_ setup the local database configuration thanks to the NGDB_SCHEMA object (see below).
##### Exemple
Don't forget to include _ngdb_ dependency in the angular _run()_ method (or where you want) :
```javascript
app.run(function($ionicPlatform, ngdb) {
  var NGDB_SCHEMA = {
    //...
  };

  $ionicPlatform.ready(function(){
    ngdb.init(NGDB_SCHEMA);
  });

});
```

### Create repositories
##### Prototype
```javascript
object NGDB_SCHEMA
```
Repositories are the equivalent of tables in SQL. In other words, it's where and how your data are stored.
##### Exemple
For exemple, if you have an user management in your app, your repositories looks like that :
```javascript
var NGDB_SCHEMA = {
  users: {
    id:         'ID',
    pictures_id:'NUMBER'
    name:       'STRING',
    born:       'DATE'
  },
  pictures: {
    id:         'ID',
    pictures:   'OBJECT'
  }
};
```
##### Typing
ngDatabase has a human friendly typing syntax. ngDatabase just make a conversion in correct SQLite types.

__Note that these types are important for the internal working.__
* __ID__        : set an _integer primary key_
* __STRING__    : set a _text_
* __NUMBER__    : set an _integer_
* __BOOLEAN__   : set a _boolean_
* __OBJECT__    : set a _text_
* __ARRAY__     : set a _text_
* __DATE__      : set a _datetime_

### Get repositories
##### Prototype
```javascript
resource getRepository(string repositoryName)
```
