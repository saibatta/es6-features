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
