#ES 6 - New Features

##Let Definitions
	
__Lets you define a variable within a lexical scope:__

	if (true){
	  let a = 5;
	  console.log(a);  //5
	}
	console.log(a);	//Error: variable undefined

####Errors:####
	
	let a = 3;
	let a = 2; //Syntax Error: variable already exists

Same thing, if you declared a variable with var and then try to redeclare it with let.

	var b = 5;
	let b = 123;	//Syntax Error: variable already exists
	
__Temporal Dead Zone__
	- the variable is defined, but is in a 'temporal dead zone', where it can't be used until it is set.

	function doSomething(){
	  console.log(a);		//Should throw a ReferenceError (per specs)
	  let a = 1;
	  console.log(a);
	}
	doSomething();

##Const

	const a = 5;
	a = 10;		//Error: a is read-only
	
## Scope operator
	
	{
		let a = 30;
		console.log(a);	//30
	}
	console.log(a);		//ReferenceError
	
## Rest Parameter (splat operator) and Spread operator

	function lotsOfArgs(first, second, ...other){
		console.log(`First: ${first}`);	                     //"First: me1"
		console.log(`Second: ${second}`);	                 //"Second: me2"
		console.log(`All the rest: ${other.join(' ')}`);     //"All the rest: me3 me4 me5 me6"
	}
	lotsOfArgs('me1', 'me2', 'me3', 'me4', 'me5', 'me6');

__Spread Operator:__

	let nums = [1, 2, 3];
	let abcs = ['a', 'b', 'c'];
	
	let alphanum = [...nums, ...abcs];	//[1, 2, 3, 'a', 'b', 'c']

## Destructuring Objects

_**Destructuring** allows you to bind a set of variables to a corresponding set of values anywhere that you can normally bind a value to a single variable._

	var person = {name: 'Aaron', age: 35};
	
	function getData(person){
	  let {name, age, address} = person;  //address = undefined
	  
	  // forgives the whole pattern (if they are not present in the object)
	  let {name, age, address = '111 second st'} = person;  //address = 'default value'
	}
	
__Patterns with Default Values__

	let {a: x = 1} = undefined;	//x = 1
	let {a: x} = undefined;			//x = undefined
	
## Arrow Function

_**Real Benifit**: lexical binding of 'this'_

	(param) => {return ...}
	() - 	are optional, if there is only one argument
			required, if no arguments
	{return} - 	is optional for one liner finctions
					e.g.: let squareArg = arg => arg * arg;

## Default Parameters

_**Note**: **Undefined** triggers a default parameter (even the one purposefully passed as an argument). **Empty String** - DOESN'T_!

	function say(name = 'World'){
		console.log(`Hello ${name}!`);
	}
	
	say('Boo');			//Hello Boo!
	say('');				//Hello !
	say();					//Hello World!
	say(undefined);		//Hello World!

### Default parameter can be set with a function call
_Notice that the function is called everytime the dafault value is needed_

	let getCount = () => {
	  let i = 0;
      return () => i++;
    }();

	function logMe( count = getCount()){
		console.log(count);
	}

	logMe();		//0
	logMe(5)		//5
	logMe();		//1
	logMe(12);		//12
	logMe();		//2
	
### Default parameters don't appear in 'arguments' array###

	function tes(a = 1, b = 2, c = 3){
	  console.log(arguments.length);
	}
	
	tes();					//0
	tes(1);					//1
	tes(1, 2, 3, 4, 5);		//5