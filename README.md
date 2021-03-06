Deferred-tools
==============

Deferred tools comprise a couple of lightweight wrappers around common asynchronous APIs. These wrappers adapt the APIs to use jQuery's Deferred object rather than argument based callbacks.

[Web Database API](http://www.w3.org/TR/webdatabase/#asynchronous-database-api)
----------------

Hey, its not much. But it can be helpful if you have already bought into using the jQuery Deferred object to handle asynchronous operations.

### Example

```javascript
var db = window.openDatabaseDeferred('example', 1, 'Example Database', function (tx) {
	tx.executeSql('CREATE TABLE IF NOT EXISTS Employee ( ID INTEGER PRIMARY KEY, Name VARCHAR )')
		.done(function () {
			console.log('Employee table created.');
		});
});

db.transaction(function (tx) {
	tx.executeSql('INSERT INTO Employee (ID, Name) VALUES (?, ?)', [1, 'John Smith']);
})
.done(function (result) {
	console.log(result.rowsAffected + ' record(s) updated.');
})
.then(function (result) {
	return db.transaction(function (tx) {
		tx.executeSql('SELECT * FROM Employee WHERE ID = ?', [result.insertId]);
	});
})
.then(function (result) {
	console.log(results.rows.item(i).Name + ' was added as an employee.');
})
.fail(function () {
	console.log('Something went wrong.');
})
```

### API

```javascript
window.openDatabaseDeferred( name, version, displayName, estimatedSize, creationCallback );
```

### SQL Database

```javascript
db.transaction( callback )
    .done(function ( ) {})
    .fail(function ( error ) {});
```

```javascript
db.readTransaction( callback )
    .done(function ( ) {})
    .fail(function ( error ) {});
```

```javascript
db.changeVersion( oldVersion, newVersion, callback )
    .done(function ( ) {})
    .fail(function ( error ) {});
```

### SQL Transaction

```javascript
transaction.executeSql( sqlStatement, sqlArguments, errorCallback )
    .done(function ( transaction, resultSet ) {})
    .fail(function ( transaction, error ) {});
```


[Filesystem API](http://www.w3.org/TR/file-system-api/#the-asynchronous-filesystem-interface)
--------------

Again, not much to see here beyond what you would expect. Fewer callbacks, more promises, if that is what you want.

### API

```javascript
window.requestFileSystemDeferred( type, size )
	.done(function ( filesystem ) {})
	.fail(function ( error ) {});
```

```javascript
window.resolveLocalFileSystemURLDeferred( type, size )
	.done(function ( entry ) {})
	.fail(function ( error ) {});
```

### File Entry

```javascript
fileEntry.getMetadata()
	.done(function ( metadata ) {})
	.fail(function ( error ) {});
```

```javascript
fileEntry.moveTo( parent, newName )
	.done(function ( entry ) {})
	.fail(function ( error ) {});
```

```javascript
fileEntry.copyTo( parent, newName )
	.done(function ( entry ) {})
	.fail(function ( error ) {});
```

```javascript
fileEntry.remove()
	.done(function () {})
	.fail(function ( error ) {});
```

```javascript
fileEntry.getParent()
	.done(function ( entry ) {})
	.fail(function ( error ) {});
```

```javascript
fileEntry.createWriter()
	.done(function ( fileWriter ) {})
	.fail(function ( error ) {});
```

```javascript
fileEntry.file()
	.done(function ( file ) {})
	.fail(function ( error ) {});
```
### Directory Entry

```javascript
directoryEntry.getMetadata()
	.done(function ( metadata ) {})
	.fail(function ( error ) {});
```

```javascript
directoryEntry.moveTo( parent, newName )
	.done(function ( entry ) {})
	.fail(function ( error ) {});
```

```javascript
directoryEntry.copyTo( parent, newName )
	.done(function ( entry ) {})
	.fail(function ( error ) {});
```

```javascript
directoryEntry.remove()
	.done(function () {})
	.fail(function ( error ) {});
```

```javascript
directoryEntry.getParent()
	.done(function ( entry ) {})
	.fail(function ( error ) {});
```

```javascript
directoryEntry.getFile( path, options )
	.done(function ( entry ) {})
	.fail(function ( error ) {});
```

```javascript
directoryEntry.getDirectory( path, options )
	.done(function ( entry ) {})
	.fail(function ( error ) {});
```

```javascript
directoryEntry.removeRecursively()
	.done(function () {})
	.fail(function ( error ) {});
```

### Directory Reader

```javascript
directoryReader.readEntries()
	.done(function ( entries ) {})
	.fail(function ( error ) {});
```