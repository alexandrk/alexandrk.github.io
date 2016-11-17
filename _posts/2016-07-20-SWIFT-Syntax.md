---
layout: post
title: "SWIFT Basics"
tags:
  - swift
  - ios
  - basics
published: true
---

## Variables

* type is optional

		var x: Int = 42		//same as below
		var x = 42			//int is infered 

* constants are defined with **let** keyword

		let pi = 3.14

## Types

### Strings

You can type special characters directly into a string, since strings are Unicode.

`ctr+ cmd + space` - ***emoji keyboard***

**String interpolation**

`\([value here])` - used for interpolation

`doggyDiet = "\(dogName) eats 25lbs of dog food per month"`

**String can be treated as an array of characters or as an NSString.**


Swift automatically bridges between String Struct (Swift) and NSString class (Objective-C), giving access to all the NSString methods.

## Optionals

**Regular Swift variables CANNOT store `nil` values!**

*Optional is like a box:*

- it can be empty
- or it can have values, of type that we have to specify
- any existing type can be used in the type optional

		var z: Int?				// Int Optional
		var string = "123"
		z = string.toInt()

You cannot use optionals without unwrapping them.

		z + 3			// ERROR
		z! + 3			// Casts z to int and adds 3, note z HAS TO be and int

*Note: unwrapping with '!' is implicit. If the value is nil, an ERROR will be thrown*

Safe unwrapping with `if let`
		
		if let z = z {
			z * 2
		} else {
			"Not a Number"
		}

We can also declare variables with an '!'. Those are called Implicitly unwrapped. They can store both type value and nil, but are immediatly unwrapped when used in the expressions.

## Arrays

Ways to initialize arrays:

- Verbose: `var numbers = Array<Double>()`
- More often: `var moreNumbers = [Double]()`
- Array literal: `var otherArray = [2, 6, 5]`

*Note: Arrays can hold values of different types, as long as the type WAS NOT specified on initialization*

### Some Array methods:
	 var mixValues = [1, "text", 2, "yada"]
	 mixValues.append("ta-ta-ta")	//equivalent to mixValues += ["ta-ta-ta"]
	 mixValues.insert(5, atIndex: 2)
	 mixValues.removeAtIndex(2)		//returns the removed item
	 mixValues.count

	// Using subscript to change multiple values of an array at a time
	mixValues[0...3] = ["la-la-la"]	//mixvalues => ["la-la-la", "ta-ta-ta"]
	
	// To avoid quering for size use this instead of 
	// mixValues.removeAtIndex(mixvalue.count - 1)
	mixValues.removeLast()	
	
*Note: you can set a default size and value for an array at the time of the initialization:*
	
	var here10Ints = [Int](count: 10, repeatedValue: 0)
	
###Iterating over an Array of items with for-in loop:
	
    //NOTE: using .enumerate() to get the tuple (index, value) back (Swift 2.2)
     
	words = ["phooey", "darn", "drat", "blurgh", "jupiters", "argh", "fudge"]
	for (index, word) in words.enumerate() {
			//CODE
        }
    }
	 
## Dictionaries

Initialization:

- `var movies = Dictionary<keyType, valueType>()`
- `var grpipsDict = [String:String]()`
- `var animalGroupsDict = ["whales": "pod", "geese": "flock", "lions": "pride"]`

### Some dictionary methods:
		animalGroupsDict["crows"] = "murder"	//adding new elements to dict
		animalGroupsDict["whales"] = nil		//removing an element
		animalGroupsDict.count					//count
		
		// returns optional: old value or nil, if no match found
		animalGroupsDict.updateValue("SBlOOlBS", forKey: "whales")
		
## Sets

Sets are unordered collections of unique values

Initialization:

	// Initializer syntax
	var utensils = Set<String>()
	var trees = Set<Character>()
	
	// Literal syntax
	var cutlery:Set = ["fork", "knife", "spoon", "spoon"]  //{"fork", "knife", "spoon"}
	var flowers:Set<Character>
	
### Methods are simular to arrays and dictionaries:
	.insert("smth")
	.remove("smth")
	.count()
	
## Functions

Two types:

* global (floating in thin air; e.g. `print`)
* local (methods) - local to a class (`e.g. Arithmetic.sumOfStrings()`)
* nested functions

		func functionName (externalParamName localParamName: paramType)
		-> returnType {
			code to execute
			retutn objectOfReturnType
		}

*NO LONGER ALLOWED Note: if external and local parameter name are the same, you can use a shorthand definition:*

		func functionName (#paramName: paramType)
		-> returnType {
			code to execute
			retutn objectOfReturnType
		}

> **Note**: By default function parameters are immutable (as if defined as constants with the `let` keyword)._
> 
> Use `func functionName(var exernalParamName paramName: paramType)` to turn them into mutable ones, but that is **depricated and will be removed as of Swift 3.**

## Classes

### Properties:

variables and constants associated with a particular class are known as **properties**

> In Swift there is a strong emphasys on immutability. So you will see a lot more properties initialized as constants

####Three Types of properties:

* **Stored Properties**
	* must be set when the instance of the class is initialized (with the **class init method**)
* **Type Properties** aka **class properties** aka **static properties**
	* prefixed with `static` keywork `static let ratings = ["G", "PG"]'`
* **Computed Properties**
	* computed based on existing data in the class
	* have **custom getters and optional setters**

#### Init method

*Note: `init` method neither has a `func` prefix nor a `return type`, which are inferred.*

	class Animal {
	    var species: String = ""
	    let tail: Tail
	    
	    init(species: String) {
	        self.species = species
	    }
	}

##Enums and Structs

> More poverful than in other languages, since they are able to have their own methods and can conform to protocols.

Basic:

	enum PrimaryColor {
	    case Red
	    case Blue
	    case Yellow
	}

Shorthand Definition:
	
	enum Aunties {
	    case Aime, Billie, Diane, Gail, Janie, Pam
	}

Can be given value of ANY type, not just integer:
	
	enum AmericanLeagueWest: String {
	    case As = "Oakland"
	    case Astros = "Houston"
	    case Angels = "Los Angeles"
	    case Mariners = "Seattle"
	    case Rangers = "Arlington"    
	}

Access those values through a built-in property `rawValue`:

	var message = "I hope the A's stay in \(AmericanLeagueWest.As.rawValue)"


> Strucs and Enums are **value types** and classes are **reference types**. This is the major difference!

	struct PictureFrame {
	    var width = 5
	    var height = 7
	    var thickness: Double = 1.5
	
	    var area: Int {
	        get {
	            return (width * height)/2
	        }
	    }
	}

_**Note**: Structs get memberwise initializers automatically_

	var familyReunionFrame = PictureFrame(width: 10, height: 8, thickness: 1.5)
	familyReunionFrame.area

> ONLY Structs can have inheretence!

##Protocols and Extensions

> Both used to package modules of functionality that expand upon classes, enums and structs

* Protocols can be shared among classes
	* Much like an interface (Java) is a list of related method signatures
	* Adopting a protocol is like signing a contract to impliment EVERY method of set protocol.

E.g.:

	protocol Souschef {
	    func chop(vegetable: String) -> String
	    func rinse(vegetable: String) -> String
	}
	
	//Our class ADOPTS two protocols (one custom and one provided by Apple)
	class Roommate: Souschef, Equatable {
	    var hungry = true
	    var name: String
	    
	    init(hungry: Bool, name: String) {
	        self.hungry = hungry
	        self.name = name
	    }
	
	    func chop(vegetable: String) -> String {
	        return "She's choppin' \(vegetable)!"
	    }
	
	    func rinse(vegetable: String) -> String {
	        return "The \(vegetable) is so fresh and so clean"
	    }
	}
	//'Equatable' Protocol Implementation
	func ==(lhs: Roommate, rhs: Roommate) -> Bool {
	    return lhs.name == rhs.name && lhs.hungry == rhs.hungry
	}

> _**NOTE:** we impliment the protocol required function OUTSIDE of class definition. This is because operators are GLOBAL functions._

* Protocols are also TYPES. You can use them any place, you normally use a TYPE. E.g.:
	* To describe variables, constants
	* Set parameter or return types of methods and functions
	* Indicate item types in the collection

E.g.: 

	class DinnerCrew {
	    var members: [Souschef]
	
	    init(members: [Souschef]) {
	        self.members = members
	    }
	}

All members of the array need to impliment Souschef protocol, but otherwise can be of ANY class, enum or struct

* Extensions used to extend existing classes
	* Extensions are anologues to C# extensions and Objective-C `Catalogs`

E.g.:

	// Extending UIColor
	extension UIColor
	{
	    convenience init(redValue: Int, greenValue: Int, blueValue: Int)
	    {
	        let newRed   = CGFloat(Double(redValue) / 255.0)
	        let newGreen = CGFloat(Double(greenValue) / 255.0)
	        let newBlue  = CGFloat(Double(blueValue) / 255.0)
	        
	        self.init(red: newRed, green: newGreen, blue: newBlue, alpha: CGFloat(1.0))
	    }
	    
	    static func pistachio() -> UIColor {
	        return UIColor.init(redValue: 147, greenValue: 197, blueValue: 144)
	    }
	}
	
	UIColor.pistachio()

Using Extensions to allow classes to conform to protocols:

	protocol DirtyDeeds {
	    func cheat()
	    func steal()
	}
	
	class Minion {
	    var name: String
	    
	    init(name:String) {
	        self.name =  name
	    }
	}
	
	extension Minion: DirtyDeeds {
	    func cheat(){}
	    func steal(){}
	}

## Closures

> Closure Expression - unnamed, self-contained block of code that can be passed as an argument to a function

Good for:

* easy to specify a block of code to be executed sometime in the future

Closure expression typical form:

	{(parameters) -> returnType in
		//statements to execure
	}

	var birthYears = [2004, 2011, 1984, 2005, 1980, 2002]
	var reverseChronologicalOrder = birthYears.sort({
		(year1: Int, year2: Int) -> Bool in
			return year1 > year2
	})
	
Closure shorthand tricks:

	//: ### Tricks to make your closures more concise: filter
	// REGULAR
	var examGrades = [81, 99, 54, 84, 98]
	var passingGrades = examGrades.filter({(grade: Int) -> Bool in
	    return grade > 70
	})
	passingGrades
	
	//1
	//: Inferring closure expression type
	var grades = [81, 99, 54, 84, 98]
	var failingGrades = examGrades.filter({grade in
	    return grade < 70
	})
	failingGrades
	
	//2
	//: Implicit returns
	var moreGrades = [81, 99, 54, 84, 98]
	var morePassingGrades = examGrades.filter({grade in
	    grade > 70
	})
	morePassingGrades
	
	//3
	//: Shorthand argument names: $0, $1, $2 ...
	var myGrades = [81, 99, 54, 84, 98]
	var myFailingGrades = examGrades.filter({
	    $0 < 70
	})
	
## Branch Statements ([more info](https://developer.apple.com/library/content/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html))

>Branch statements allow the program to execute certain parts of code depending on the value of one or more conditions.

- **if-else-if-else**
	- The value of any condition in an if statement must be of type Bool or a type bridged to Bool. The condition can also be an optional binding declaration
- **guard**
	- A `guard` statement is used to transfer program control out of a scope if one or more conditions aren’t met.
	- Any constants or variables assigned a value from an optional binding declaration in a `guard` statement condition can be used for the rest of the `guard` statement’s enclosing scope **(guard's parent score, outside of guard itself)**.
	- The `else` clause of a `guard` statement is required, and must either call a function with the `Never` return type or transfer program control outside the guard statement’s enclosing scope using one of the following statements:
		- `return`
		- `break`
		- `continue`
		- `throw`
- **switch** ([more info](https://developer.apple.com/library/content/documentation/Swift/Conceptual/Swift_Programming_Language/ControlFlow.html#//apple_ref/doc/uid/TP40014097-CH9-ID129))
	- Switch Statements **Must Be Exhaustive**, you can include a default case to satisfy the requirement.
	- Program execution **does not continue** or “fall through” to the next case or default case. That said, if you want execution to continue from one case to the next, **explicitly include** a `fallthrough` statement.
	- A `switch` case can bind the value or values it matches to temporary constants or variables, for use in the body of the case. Known as `value binding` 
	- A `switch` case can use a `where` clause to check for additional conditions.

	E.g.:
	
		let yetAnotherPoint = (1, -1)
		switch yetAnotherPoint {
		
		case (let x, 0):		                                 //Value binding
		    print("on the x-axis with an x value of \(x)")
		case (0, let y):
		    print("on the y-axis with a y value of \(y)")
		case let (x, y) where x == y:	                        //Where clause
		    print("(\(x), \(y)) is on the line x == y")
		case let (x, y) where x == -y:
		    print("(\(x), \(y)) is on the line x == -y")
		case let (x, y):
		    print("(\(x), \(y)) is just some arbitrary point")
		}
		// Prints "(1, -1) is on the line x == -y"
