# Metab Language
## Simplifying your code, speeding your development!

Metab is a clear language to work with javascript. Everything you write in Metab language compile to standard javascript to run in many places, from a common browser to a IoT device with node.js

## In Metab language, you write this:

```CoffeeScript
class File
	enum TYPES FILE, FOLDER, LINK	# enumerates
	static Type = TYPES.FILE		# statics vars
	Name	
	
	ReadAll ->
		<- 'Data'					# simply returns
	
class Folder : File					# short inheritance
	static Type = TYPE.FOLDER
	
	GetFiles ->
		<- ['file1','file2']
	
```

## to run this:

```JavaScript
class File{
	constructor(...args) {
		this.Name = null;
		if(!(this.constructor.prototype instanceof File) && this.init)return this.init(...args);
	}
	ReadAll() 	{
		return 'Data';
	}

}
File.TYPES = {
	"FILE" : 0,
	"FOLDER" : 1,
	"LINK" : 2
};
File.Type = File.TYPES.FILE;

class Folder extends File{
	constructor(...args) {
		super(...args);
		if(!(this.constructor.prototype instanceof Folder) && this.init)return this.init(...args);
	}
	GetFiles() 	{
		return ['file1', 'file2'];
	}

}
Folder.Type = TYPE.FOLDER;



```

# Index
- [Install](#install)
- [Use](#use)
  - [Command Line](#use-from-command-line)
  - [Javascript](#use-from-javascript)
- [Language](#language)
  - [Introduction](#introduction)
  - [Basic concepts](#basic-concepts)
  - [Comments](#comments)
  - [Classes](#classes)
    - [Variables](#variables)
    - [Functions](#functions)
    - [Enums](#enums)
    - [Getters / Setters](#getters--setters)
  - [Import / Export modules](#import--export-modules)
  - [Conditionals](#conditionals)
    - [If / Else](#if--else)
    - [Switch](#switch)
  - [Loops](#loops)
    - [For](#for)
    - [Do](#do)
    - [While](#while)
  - [Try / Catch / Finally](#try--catch--finally)
  - [Array / Object](#array--object)
  - [This / New / Super](#this--new--super)
  - [Increment / Decrement](#increment--decrement)
  - [Operators](#operators)
    - [Unary](#unary)
    - [Arithmetic](#arithmetic)
    - [Relational](#relational)
    - [Equality](#equality)
    - [Bitwise shift](#bitwise-shift)
    - [Binary bitwise](#binary-bitwise)
    - [Binary logical](#binary-logical)
    - [Conditional](#conditional)
    - [Assignment](#assignment)
  - [Break / Continue](#break--continue)
  - [Throw](#throw)
  - [Debugger](#debugger)
- [License](#license)


## Install
```
npm install -g metab
```

## Use
### Use from command line
```
metab test.metab
```

### Use from Javascript 
```JavaScript
require('metab');

Metab.Import('./test',()=>{
	//test imported
},(err)=>{
	console.error err
});
```

## Language

### Introduction
Metab language was born to write minimum code and do the maximum work possible. Once the code is minimalized it becomes clearer and you can work faster.

### Basic concepts
The first rule to write less, like Python and Coffescript languages, is that Metab use tabulated code to remove braces and save hundreds of lines.
To use class members, you do not need to write 'this' all the time :)
With Metab language, you can call asynchronous functions like synchronous and your code become more linear. Thanks to this, you can import asynchronous modules like synchronous.
Metab uses '.metab' extension for metab code and '.mson' for json files in metab language style

### Comments
```CoffeeScript
#this is a single line comment
###
	this is a multiline comment
###
```

### Classes
```CoffeeScript
class Animal
	Name	#variable
	Height
	
	Run ->	#method of Animal class
		speed = 2	#local variable
		
class Dog : Animal #inherit from Animal class
	Height = 20
	
	init ->		#constructor
		super	#call to Animal constructor
		Name = 'Max'	#the use of class members, do not need 'this' keyword :)
		
```
#### Variables
The variables are defined in the scope where they are initialized, this is, in a class or in a function scope.
```CoffeeScript
class Animal
	Name	#this is a class variable
	
	Run ->
		speed = 2		#this is a function variable
		if speed > 1
			isRunning = yes	#this is also a function variable
			
```
#### Functions
There are three types of functions:
```CoffeeScript
normalFunction = ->
	a = 1
	
	
#asynchronous functions, define the local variables 'cb' and 'ce', to return a Promise when it is resolved (cb) or rejected (ce)	
asynChronous = --> #note the double dash
	a = 1
	if a > 1
		cb(a)	#return the result a
	else
		ce('error')	#return the error
	
		
#in this function, @ convert it in asyncrhonous function, do asynchronous work and return when everything is done		
automaticAsynchronous = ->
	a = 1
	@ doAsyncWork()	#use @ to call asyncrhonous functions like syncrhonous


#you can call functions with or without parenthesis
a(1,2)
a 1, 2

a(1,b(2,3))
a 1, b 2, 3

#and return values like in javascript
return a

#or more simply
<- a
```

#### Enums
```CoffeeScript
#In a class, you can define enums
class Animal
	enum COLORS BROWN,RED,GREY
	enum TYPES DOMESTIC=1,WILD	#you can initialize enum values
	
	Color = COLORS.BROWN
```
#### Getters / Setters
```CoffeeScript
#like in modern Javascript, you can define getters / setters in classes
class Animal
	_Speed = 1
	
	get Speed ->
		<- _Speed
		
	set Speed (val) ->
		_Speed= val
		
```

### Import / Export modules
You can use import / export keywords to load asynchronous modules
```CoffeeScript
import 'Animal'	#define de Animal variable with default export of module
import Bird as Fly 'Bird'	#define Fly variable with Bird export of module

export class Dog : Animal
```

### Conditionals

#### If / Else
```CoffeeScript
if a > 1	#you not need to use parenthesis
	b()
else
	c()
	
if a > 1
	b()
else a < 1	#equivalent to 'else if', but more simple :)
	c()
else
	d()
	
unless a > 1	#equivalent to 'if not'
	c()

#also you can write it in one line
c()	unless a > 1	#like in Coffeescript
```	
#### Switch
```CoffeeScript
switch a
	case 1
		b1()
	case 2
		b2()
	case 2
		b3()
	default
		b()
		
#and more simple
switch a
	1
		b1()
	2
		b2()
	3
		b3()
	else
		b()
```
### Loops

#### For
```CoffeeScript
for val in values	#loop in a collection, val is the item of collection
	b(val)
	
for val, key in values	#now, you also have the key (or position in arrays)
	b(val)
	
for val, key, count in values	#and now, you also have a counter of loop executions ( 0, 1, 2, ...)
	b(val)
	
for i in 1..10		#loop from i=1 to i=10
	b(i)

for i in 1..<10		#now, loop from i=1 to i=9
	b(i)
	
```
#### Do
```CoffeeScript
do
	a()
	b++
while b > 2
```
#### While
```CoffeeScript
while b > 2
	a()
	b++
```
### Try / Catch / Finally
```CoffeeScript
try
	a()
catch err
	console.error err
	
try
	a()
catch err
	console.error err
finally
	b()
```
### Array / Objects
```CoffeeScript
#you can define objects and arrays like in Javascript
obj = {a:'b',c:'d'}

#and more simple
obj =	#no more braces
	a: 'b'	#no more commas
	c: 'd'
arr = [1,2,3,4]

arr = [
	1,2
	3,4
]

mix = 
	a: [1,2]
	b: 
		c: 3
		d: [
			4
			5
		]

```
### This / New / Super
```CoffeeScript
#like in javascript

this.Size = 10	#but you can use class members without 'this'

a = new Animal

#and you can use super with or without parameters
class Dog : Animal
	Run (quantity) ->
		super	#equivalent to 'super(quantity)'
```
### Increment / Decrement
```CoffeeScript
#like in javascript
a++
b--
++c
--d
```

### Operators

#### Unary
```CoffeeScript
#like in javascript
delete a
void 0
~ bitwise

#and not operator
a = not a
```

#### Arithmetic
```CoffeeScript
#Like in javascript
a = a + 1 #Addition operator
a = a - 1 #Subtraction operator
a = a / 2 #Division operator
a = a * 2 #Multiplication operator
a = a % 2 #Remainder operator
a = a ** 2 #Exponentiation operator
```

#### Relational
```CoffeeScript
#Like in javascript
a = b instanceof Animal
a = c < d
a = c > d
a = c <= d
a = c >= d

#and you can test elements in array
a = 'Max' in ['Tom','Paula','Max','Laura']
```

#### Equality
```CoffeeScript
# like in javascript
if b == c
	d()
if b != c
	d()
if b === c
	d()
if b !== c
	d()

#or more simple
if b is c	# similar as '===' operator
	d()
if b isnt c	# similar as '!==' operator
	d()
```

#### Bitwise shift
```CoffeeScript
# like in javascript
a = b << c
a = b >> c
a = b >>> c

```
#### Binary bitwise
```CoffeeScript
# like in javascript
a = b & c
a = b | c
a = b ^ c
```

#### Binary logical
```CoffeeScript
# like in javascript
if a is 1 && c is 2
	d()
if a is 1 || c is 2
	d()	

# more clear
if a is 1 and c is 2
	d()
if a is 1 or c is 2
	d()
```

#### Conditional
```CoffeeScript
# like in javascript
a = b? c : d
```

#### Assignment
```CoffeeScript
# like in javascript
a = b	# Assignment operator.
a = *= b	# Multiplication assignment.
a = /= b	# Division assignment.
a = %= b	# Remainder assignment.
a = += b	# Addition assignment.
a = -= b	# Subtraction assignment
a = <<= b	# Left shift assignment.
a = >>= b	# Right shift assignment.
a = >>>= b	# Unsigned right shift assignment.
a = &= b	# Bitwise AND assignment.
a = ^= b	# Bitwise XOR assignment.
a = |= b	# Bitwise OR assignment.

#create variables from array
[a,b] = [1,2]    # a=1 and b=2

{a,b} = {a:1,b:2}    # a=1, b=2
{a:c,b} = {a:1,b:2}    # c=1, b=2

```

### Break / Continue
```CoffeeScript
# like in javascript
for val in values
	if val is null
		break
	if val < 0
		continue
```

### Throw
```CoffeeScript
# like in javascript
throw 'error ...'
```

### Debugger
```CoffeeScript
# like in javascript
#stop here
debugger
```




## License
Copyright 2016 Amefy

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
