Parse4J - Java Library for parse.com
====================================

The non-official java library for parse.com

Summary
-------


Getting Started
---------------

### Maven ###

```XML
	<project ...>
	    ...
	    <dependencies>
	        <dependency>
	            <groupId>org.parse4j</groupId>
	            <artifactId>parse4j</artifactId>
	            <version>1.0</version>
	        </dependency>
	    </dependencies>
	    ...
	</project>
```


Objects
-------

Storing data on Parse is built around the ParseObject. Each ParseObject contains key-value pairs of JSON-compatible data. This data is schemaless, which means that you don't need to specify ahead of time what keys exist on each ParseObject. You simply set whatever key-value pairs you want, and our backend will store it.

For example, let's say you're tracking high scores for a game. A single ParseObject could contain:

```Java
	score: 1337, playerName: "Sean Plott", cheatMode: false 
```

Keys must be alphanumeric strings. Values can be strings, numbers, booleans, or even arrays and objects - anything that can be JSON-encoded.

Each ParseObject has a class name that you can use to distinguish different sorts of data. For example, we could call the high score object a GameScore. Parse recommend that you NameYourClassesLikeThis and nameYourKeysLikeThis, just to keep your code looking pretty.

#### Saving Objects

```Java
	ParseObject gameScore = new ParseObject("GameScore");
	gameScore.put("score", 1337);
	gameScore.put("playerName", "Sean Plott");
	gameScore.put("cheatMode", false);
	gameScore.save();
```

Use saveInBackground() if you want to delegate the operation to a background thread

```Java
	gameScore.saveInBackground();  
```

#### Retrieving Objects

```Java
	ParseQuery<ParseObject> query = ParseQuery.getQuery("GameScore");
	query.getInBackground("xWMyZ4YEGZ", new GetCallback<ParseObject>() {
	  public void done(ParseObject object, ParseException e) {
	    if (e == null) {
	      // object will be your game score
	    } else {
	      // something went wrong
	    }
	  }
	}); 
```


To get the values out of the ParseObject, there's a getX method for each data type:

```Java
	int score = gameScore.getInt("score");
	String playerName = gameScore.getString("playerName");
	boolean cheatMode = gameScore.getBoolean("cheatMode");
```

If you don't know what type of data you're getting out, you can call get(key), but then you probably have to cast it right away anyways. In most situations you should use the typed accessors like getString.

The three special values have their own accessors:

```Java
	String objectId = gameScore.getObjectId();
	Date updatedAt = gameScore.getUpdatedAt();
	Date createdAt = gameScore.getCreatedAt();
```

#### Callback functions

You can also add a callback function to the save operation

```Java
	final ParseObject gameScore = new ParseObject("GameScore");
	gameScore.put("score", 1337);
	gameScore.put("playerName", "Sean Plott");
	gameScore.put("cheatMode", false);
	gameScore.saveInBackground(new SaveCallback() {			
			@Override
			public void done(ParseException parseException) {
				System.out.println("saveInBackground(): objectId: " + parseObject.getObjectId());
				System.out.println("saveInBackground(): createdAt: " + parseObject.getCreatedAt());
				System.out.println("saveInBackground(): updatedAt: " + parseObject.getUpdatedAt());
			}
		});
```

#### Delete

To delete an object, just call the method delete().

```Java
	gameScore.delete();
```
You can also attach a callback function on the delete/deleteInBackground methods.

```Java
	gameScore.deleteInBackground(new DeleteCallback() {
			@Override
			public void done(ParseException parseException) {
				//do something
			}
		});
```

#### Counters

You can also increment and decrement values from Number (int, long, double...) attributes.

```Java
	gameScore.increment("score");
	gameScore.decrement("score");
	gameScore.saveInBackground();
```
You can also increment by any amount using increment(key, amount) or decrement by any amount using decrement(key, amount).

#### Arrays

```Java
gameScore.addAllUnique("skills", Arrays.asList("flying", "kungfu"));
gameScore.saveInBackground();
```

Queries
-------

Pending...

Users
-----

In development...

Roles
-----

Pending...


Files
-----

```JAVA
	byte[] data = "Working at Parse is great!".getBytes();
	ParseFile file = new ParseFile("resume.txt", data);
	file.save();
```


```JAVA
	byte[] data = getBytes("song.mp3");
	ParseFile file = new ParseFile("song.mp3", data);
	file.save(new ProgressCallback() {
		
		@Override
		public void done(Integer percentDone) {
			System.out.println("uploadPdf(): progress " + percentDone + "%");
		}
	});
```


```JAVA
	byte[] data = getBytes("song.mp3");
	ParseFile file = new ParseFile("song.mp3", data);
	file.save(new SaveCallback() {
		
		@Override
		public void done(ParseException parseException) {
			System.out.println(parseException);
		}
	});
```


Analytics
---------

Pending ...

Cloud Functions
---------------

In development...

GeoPoints
---------



Notes
-----

### License


TODO
-----

### Pending Functionalities

 * Queries
 * Analytics
 * Push Notifications
 * Cloud Functions
 * Instalations
 
### Implemented Functionalities

 * Objects
 * Files
 * Geopoints
  
 
 