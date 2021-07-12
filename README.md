# es6-features
Core fatures in ES6(ECMAScript2015)


<b> How to do ES5 to ES6 Migration ? </b>

<ul>
	<li> Migrting from ES5 to ES6 there is nothing to do.
	<li> ECMAScript 6 is a superset of ECMAScript 5. 
	<li>Therefore, all of your ES5 code is automatically ES6 code. 
	<li>That helps tremendously with ncrementally adopting this new version. 
	<li> ES6 has the backward compatablity 
	</ul>
	
# Call, Apply and Bind

- <b>this</b> keyword behaves differently in JavaScript than in other object-oriented languages. 
- The call, bind and apply methods can be used to set the <b>this</b> keyword independent of how a function is called.
- The <b>bind</b> method creates a copy of the function and sets the <b>this</b> keyword,while the <b>call</b> and <b>apply</b> methods sets the <b>this</b> keyword and calls the function <b>immediately</b>.

<b>bind : </b>
```sh
function greeting(lang) {
  console.log(`${lang}: I am ${this.name}`);
}
const alex = {
  name: 'alex'
};
const john = {
  name: 'john'
};
const greetingAlex = greeting.bind(alex, 'en'); // binding the object to this context with extra parameter
greetingAlex(); // function will invoke here
const greetingJane = greeting.bind(jogn, 'es');
greetingJohn();

```
<b>Call : </b>
```sh
function greeting() {
  console.log(`Hi, I am ${this.name} and I am ${this.age} years old`);
}
const john = {
  name: 'John',
  age: 24,
};
const jane = {
  name: 'Jane',
  age: 22,
};
// Hi, I am John and I am 24 years old
greeting.call(john);
// Hi, I am Jane and I am 22 years old
greeting.call(jane);
```
<b>apply : </b>
```sh
function greet(greeting, lang) {
  console.log(lang);
  console.log(`${greeting}, I am ${this.name} and I am ${this.age} years old`);
}
const john = {
  name: 'John',
  age: 24,
};
const jane = {
  name: 'Jane',
  age: 22,
};
// Hi, I am John and I am 24 years old
greet.apply(john, ['Hi', 'en']);
// Hi, I am Jane and I am 22 years old
greet.apply(jane, ['Hola', 'es']);
```

## closure 
- A closure is a function having access to the parent scope, even after the parent function has closed.
- A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment). In other words, a closure gives you access to an outer function's scope from an inner function.
```sh
var add = (function () {
  var counter = 0;
  return function () {counter += 1; return counter}
})();

add();
add();
add();

// the counter is now 3
```
```javascript
console.clear();
function add(a){
  return function(b){
      return a+b;
    }
}
 console.log(add(2)(36)); // 38

function forLoop(){
  for(let i=0;i<3;i++){
    setTimeout(()=>{
      console.log(i);
      },i*1000)
  }
};
console.log(forLoop()); // 0,1,2 with timeout of 1000 ms

function forLoop(){
  for(var i=0;i<3;i++){
    setTimeout(()=>{
      console.log(i);
      },i*1000)
  }
};
console.log(forLoop()); // 4,4,4 with timeout of 1000 ms

function forLoop(){
  for(var i=0;i<3;i++){
    // setTimeout(()=>{
      console.log(i);
   //    },i*1000)
  }
};
console.log(forLoop()); // 0,1,2 with timeout of 1000 ms
```


### Promise
A Promise is a proxy for a value not necessarily known when the promise is created. It allows you to associate handlers with an asynchronous action's eventual success value or failure reason. This lets asynchronous methods return values like synchronous methods: instead of immediately returning the final value, the asynchronous method returns a promise to supply the value at some point in the future.

**A Promise is in one of these states:**

1. **pending**: initial state, neither fulfilled nor rejected.
2. **fulfilled**: meaning that the operation was completed successfully.
3. **rejected**: meaning that the operation failed.

```javascript
const promise = New Promise((resolve,reject)=>{
 setTimeout(()=>{
  resolve("Succeffully return New Promose Object after 100ms ");
},100)
});
```

```javascript
promise.all([pr1,pr2,pr3]); // if any one is rejected it throws the errors return a single Promise Object
promise.race([pr1,pr2,pr3]); // if any one Rejected or Resolved
promise.allSetted([pr1,pr2,pr3]);  // it will wait untill all of them get resloved/rejected
promise.any([p1,p2,p3]) // any one is get resolved
```
### Rxjs Subject
RxJS provides an implementation of the Observable type, which is needed until the type becomes part of the language and until browsers support it. The library also provides utility functions for creating and working with observables. These utility functions can be used for:

Converting existing code for async operations into observables
- Iterating through the values in a stream
- Mapping values to different types
- Filtering streams
- Composing multiple streams

```javascript
import { BehaviorSubject, Subject, ReplaySubject,AsyncSubject } from "rxjs";

const behaviourSubject = new BehaviorSubject(123);
const subject = new Subject();
const replaySubject = new ReplaySubject();
const asyncSubject = new AsyncSubject();
console.log('***************** Subject *********************')
/**
 *  Subject no need of intial value
 * ony current value will return for the all the subscribers
 *  output 456,789
 *  */  
subject.subscribe(console.log);
subject.next(456); 
subject.next(789);
subject.subscribe(console.log); // No value for this subsciber
subject.subscribe(console.log); // No value for this subscriber

console.log('*************** BehaviorSubject *****************')
/**
 * Bahaviour Subject need intial value
 * otherwise the subscriber will get undefined
 * Next subscriber will get the current value i.e 789
 *  output 123,456,789,789,789 
 * Requires an initial value and emits the current value to new subscribers
 *  */  

behaviourSubject.subscribe(console.log);
behaviourSubject.next(456); 
behaviourSubject.next(789);
behaviourSubject.subscribe(console.log);// here next subscriber get the current value i.e 789
behaviourSubject.subscribe(console.log); // here next subscriber get the current value i.e 789
console.log('************* ReplaySubject *********************')
/**
 * Replay Subject emits old values to New subscribers
 * Relay subject takes intput for the number previous values to emit
 * if input 0 or 1 current value will be return
 * output 456,789,789,222,222,222
 * 
 * * if input empty current value will be return
 * output  will as shown below
 *  */  

replaySubject.subscribe(console.log);
replaySubject.next(456); // 456
replaySubject.next(789); // 789
replaySubject.subscribe(console.log);// 456,789
replaySubject.next(222); // 222,222
replaySubject.subscribe(console.log); // 456,789,222

console.log('************* AsynchSubject *********************')
/**
 * Asynch Subject emits only latest value to all subscribers
 * only after it's complete
 *  */  

asyncSubject.subscribe(console.log); //222
asyncSubject.next(456); 
asyncSubject.next(789); 
asyncSubject.subscribe(console.log);// 222
asyncSubject.next(222); 
asyncSubject.subscribe(console.log); // 222
asyncSubject.complete();
```

####  RxJS Operators

##### forkJoin
This operator is best used when you have a group of observables and only care about the final emitted value of each. **One common use case for this is if you wish to issue multiple requests on page load (or some other event) and only want to take action when a response has been received for all**. In this way it is similar to how you might use **Promise.all.**

------------
 ##### combineAll
**combineAll** takes an Observable of Observables, and collects all Observables from it. Once the outer Observable completes, it subscribes to all collected Observables and combines their values using the combineLatest strategy, such that:
-  Every time an inner Observable emits, the output Observable emits
-  When the returned observable emits, it emits all of the latest values

------------
 ##### combineLatest
 When any observable emits a value, emit the last emitted value from each.**combineLatest** will not emit an initial value until each observable emits at least one value. This is the same behavior as withLatestFrom and can be a gotcha as there will be no output and no error but one (or more) of your inner observables is likely not functioning as intended, or a subscription is late.

####  **Spiral of n-dimentional matrix**


    const mat =  [[1,2,3,4,5],
           		      [6,7,8,9,10],
           			  [11,12,13,14,15],
           			  [16,17,18,19,20]];
					  
    const spiral =(matr)=>{
       if(matr.length && matr[0].length) {
     	   matr[0].forEach(item=>{
       	   console.log(item);
        });
        matr.shift();
        matr.forEach(item=>{
        	  console.log(item.pop());
        });
        spiral(revserse(matr));
      }
    }
      const revserse =(matr)=>{
      	   matr.forEach(item=>{
        		  item.reverse();
        });
        matr.reverse();
        return matr;
      }
    console.log(spiral(mat));
    output:	1 2 3 4 5 10 15 20 19 18 17 16 11 6 7 8 9 14 13 12
    
> ***ECMAScript 6(2015)***
> 
##### **1. UNICODE STANDARD VERSION 8 SUPPORT**
it will allows the use of the unicode characters as variable

	    let unicode_1 ='\u{102C0}';
	    console.log(unicode_1);
	                
	    var unicode_2 = '\uD83D\uDC04';
	    console.log(unicode_2)
	    
	    Output: -   "𐋀"
			    -   "🐄"
##### **2.**  **BINARY, HEX AND OCTAL NUMBER SUPPORT**
-   hex — base 16 — starts with  `0x`
-   Oct — base 8 — starts with  `0o`
-   Binary — base 2 — starts with  `0b`

```java
	var decimalLit = 15;
	var hexadecimalLit = 0xF;
	var octalLit = 0o17;
	var binaryLit = 0b1111;
	console.log(decimalLit,hexadecimalLit,octalLit,binaryLit); // 15 15 15 15
	console.log(decimalLit == hexadecimalLit); // true
	console.log(decimalLit == octalLit); // true
	console.log(decimalLit == binaryLit); //true
```
##### **3.**  **STRING TEMPLATE (BACKTICK Strings)**

concatenating string using  `+`, can now be done using`` ` ``

##### OLDER VERSION:

```java
	let user ={firstName:'fname',lastName:'lName'};
	var message = "The user "+ user.firstName + "" + user.lastName ;
```

##### NEWER VERSION:

```java
	let user ={firstName:'fname',lastName:'lName'};
	var message = `The user ${user.firstName} ${user.lastName}`;
```
##### **4. DESTRUCTURING ASSIGNMENT**

It breaks an array into its elements, keeping the original array unchanges. This process assignes the variables with items in the corresponding positions.

```java
	let names = ["Ted", "Jenni", "Athen"];
	let [ted, jenni, athen] = names;
	console.log(ted, jenni, athen); //  "Ted Jenni Athen"
```
```java
	let numbers= ["One", "" ,"Three", "Four"];
	let [One, Two, Three] = numbers;
	console.log(One, Two, Three); //  "One", "" ,"Three",
```
		
##### **5.DESTRUCTURING IN OBJECTS**

```java
	let url = "https://jsbin.com/?js,console";
	let parsedURL = /^(?:https?:\/\/)?(?:[^@\/\n]+@)?(?:www\.)?([^:\/?\n]+)/igm.exec(url);
	let [ fullhost,protocol] = parsedURL;
	console.log(parsedURL); // ["https://jsbin.com", "jsbin.com"]
    console.log(fullhost);  // "https://jsbin.com"
    console.log(protocol);  // "jsbin.com"
```

```java
	let point = { x:2, y: 5 };
	let {x, y} = point;
	console.log(x, y); // prints 2, 5
```

```java
	let point = { x:2, y: 5 };
	let {y, x} = point;
	console.log(x, y); // prints 2, 5
```

```java
	let point = { x:2, y: 5 };
	let {y: pty, x: ptx} = point;
	console.log(ptx, pty); // prints 2, 5
```
##### **6.DESTRUCTURING OBJECT PRAMETERS IN A METHOD CALL**

```java
let person = {
    firstName: "Ted",
    lastName: "Neward",
    age: 45,
    favoriteLanguages: ["ECMAScript", "Java", "C#", "Scala", "F#"]
}
```

```java
function displayDetails({firstName, age}) {
    console.log(`${firstName} is ${age} years old`); // "Ted is 45 years old"
}
```

```java
displayDetails(person);
```
##### **7.DEFAULT PARAMETER**

Now we can provide the default values of the function variables 
```java
let sayHello = function(message = "Hello world!") {
    console.log(message);
}
```

```java
sayHello(); // "Hello world!"
```

```java
sayHello("Howdy!"); // "Howdy!"
```
##### **8.SPREAD PARAMETERS: OPPOSITE TO REST PARAMETERS**

This destructurs an array into individual parts and simplest use case is to concatanate arrays.

```java
let arr1 = [0, 1, 2];
let arr2 = [...arr1, 3, 4, 5];
console.log(arr2); // 0,1,2,3,4,5
```

```java
//IMPORTANT USECASE:
function printPerson(first, last, age) {
    console.log(first, last, age); // "Ted" "Neward" 45
}
```

```java
let args = ["Ted", "Neward", 45];
```

```java
printPerson(...args);
```
##### **9.KEYS AND VALUES OF ARRAY**

Get values(for of) and keys(for in) from the array by Iterating 

```java
let arr1 = ['Zero', 'One', 'Two'];
const arrayInerate = (arr1) =>{
 for(value of arr1){
   console.log(value ) // 'Zero', 'One', 'Two'
 }
}
arrayInerate(arr1);

```
```java
let arr1 = ['Zero', 'One', 'Two'];
const arrayInerate = (arr1) =>{
 for(key of arr1){
   console.log(key ) // 0,1,2
   console.log(arr1[key] ) // 'Zero', 'One', 'Two'
 }
}
arrayInerate(arr1);
```
##### 10. **IF `this` IS REFERENCED FROM THE GLOBAL SCOPE THEN IT REFERS TO THE GLOBAL VARIABLES, FUNCTIONS, AND OBJECTS.**

`this` Refers to the parent  global object


```java
let displayThis = function() {
    for (let m in this) {
        console.log(m); // global object values
    }
};
displayThis(); // this == global object
```
`this` Refers to the object of the function which is called
```java
let displayThis = function() {
    for (let m in this) {
        console.log(m); // "firstName"  "lastName" "displayMe"
    }
};
let bob = {
    firstName: "Bob",
    lastName: "Robertson",
    displayMe: displayThis
};
bob.displayMe(); // this == bob
```

##### **11. IN NODE JS `require(‘events’)` IS A PUB-SUB MODULE- EVENT LISTENERS**

```java
// let EventEmitter = require('events');
let ee = new EventEmitter(); // Default JS feature no need to import 
```
```java
ee.on('event', function() {
    console.log("function event fired", this); // Event Subscriber
});
```
```java
ee.emit('event'); // Event Emitter
```
##### **12. GENERATOR FUNCTION: SIMILAR TO STREAMS IN REACTIVE PROGRAMMING**

Infinte stream is implemented using GENERATOR in ES6.


```java
function* getName() {
   yield "One";
   yield "Two";
   yield "Three";
  yield "Four";
}
```

```java
let names = getName();
```

```java
console.log(names.next().value); // "One"
console.log(names.next().value); // "Two"
console.log(names.next().value); //"Three"
console.log(names.next().value); //"Four"
console.log(names.next().value); // undefined
```

The function will print each name in order. When it runs out of names it will print  `undefined`.

##### **13. CONSTRUCTOR OF A CLASS**

```java
class Person{
    constructor(firstName, lastName, age){
        this.firstName = firstName;
        this.lastName = lastName;
        this.age = age;
        this.fullName = this.firstName +' '+ this.lastName;
    }
}
```

```java
let ted = new Person("Ted", "Neward", 45);
console.log(ted.firstName); // "Ted"
console.log(ted.age); // 45
console.log(ted.fullName); // "Ted Neward"
```
