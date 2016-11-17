# Learning Firebase with Udemy Course

### Create basic file structure

	mkdir 	livelinks
	cd 		livelinks
	touch 	index.html app.js

### Basic Scaffolding

	<html>
		<head>
			<script src="path-to-cdn-firebase"></script>
			<script src="path-to-cdn-jquery"></script>
			<script src="app.js"></script>
		</head>
		<body>
			<h1>Live Links</h1>
		</body>
	</html>

*Ensure the firebase and jQuery are included correctly using the chrome dev tool to check the existance of their global variables.*

__Create a global consturctor for the app code:__

	function app(fbname){
	  var firebase = new Firebase('http://' + fbname + '.firebaseio.com')
	  return {
	    firebase: firebase
	  };
	}

__Now you can connect to your firebase app in from chrome dev tools:__
	
	//'livelinks' is a name of the app inside the Firebase service
	ll = app('livelinks');
	
### Ways to interact with the database
	
	//add a key/value pair to the database
	ll.firebase.push({key: value});
	
	//replaces all values in the database with the values provided
	ll.firebase.set({key: 'value', key2: 'value2'})
	
## Retrieve data from DB
	
#### 5 events:
1. 	__value__: *fired initially to retrieve data and everytime a value changes with in the object, including it's nested values (use with caution)*

		ll.firebase.on('value', function(ss){
			console.log(ss.val());
		})

2. __child_changed__: *only fired when data changes and retrieves ONLY the changed node*
		
		ll.firebase.on('child_changed', function(ss){
			console.log(ss.key() +': '+ ss.val())
		})

3. __child_removed__: *fired when a node has been removed. Returns the node data, which can be used to update DOM*

4. __child_added__: *[reference docs](https://www.firebase.com/docs/web/api/query/on.html)*

5. __child_moved__: *[reference docs](https://www.firebase.com/docs/web/api/query/on.html)*

## Updating and Deleting Data

