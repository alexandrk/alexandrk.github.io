# ES6 - Classes

Classes so far are just a sintaxical sugar on top of what we already have

	function Foo(){
		//....
	}

Equivalent to:

	class Foo{
		
	}

### Constructor and private properties and subclassing:

	(function(){
		var fooHealth = Symbol();
		class Foo{
		
			//Constructor function
			constructor(name, health){
				this.name = name;
				this[fooHealth] = health;	//'private' property
			}
			
			//Getter / Setter (ES5)
			get health(){
				return this[fooHealth];
			}
			set health(){
				this[fooHealth] = health;
			}
		
		}
		
		//Subclassing with extends
		class Bar extends Foo {
			constructor(){
				super('Yada', 10000);
			}
		}
		window.Foo = Foo;
		window.Bar = Bar;
	
	})();

### Endless loop with setters

	//having the same name for a setter as
	//for a property creates an endless loop
	class Foo{
		constructor(bar){
			this.bar = bar;			//this.bar is a call to the setter
		}
		
		set bar(blah){
			this.bar = blah;		//this.bar is STILL a call to the setter
		}
	}


## Collections


