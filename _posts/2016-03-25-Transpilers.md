**Note:** _From Frontend Masters Angular 2 course_

You can use Transpiler option with Angular 2 or not.

## Transpiler - Convers source code from one language to another
* ES5 -> ES6
* TypeScript -> Javascript
* etc...

### Build-Time Transpiler

	Dev
		ES6+
		|
		Transpiler
		|
		ES5

Then sent to the server and run by the browsers (ES5+)

### Run-Time Transpiler
_for less stranious code (side projects), since the load of conversion from ES6+ to ES5 is on the browser_

### Transpiler Options

* Traceur (_built by Google_)
	* Build Time
	* Run Time
* Babel (_aka 6to5_)
	* Works with ES7 features
* TypeScript