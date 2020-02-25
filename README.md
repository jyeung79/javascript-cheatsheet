# Javascript-cheatsheet
Cheatsheet on Javascript language, programming paradigms, tips&tricks, etc.

## OOP vs Functional programming
Object Oriented Programming - programming paradigm that focuses on three aspects
<ol>
  <li> Encapsulation - Hiding implementation details from outside to prevent improper changes to private data. ex) Black box with known inputs and outputs
  <li> Inheritance - Child classes derives attributes and methods from parent classes. Child classes may have uniqure attributes apart from parent class. This is the same as JS Object Prototypes. All JS objects inherit properties and methods from a prototype. ex) I inherit my big butt genes from my parents
   <li> Polymorphism - Objects can take on multiple forms. Methods that might belong to one class might be overridden with a diffrent implementation. This includes function/operator overloading and overriding. ex) A man can be a father, a husband, an employee and NBA basketball player
</ol>
<a href="https://medium.com/javascript-scene/master-the-javascript-interview-what-is-functional-programming-7f218c68b3a0">Functional Programming</a> - a programming paradigm that focuses on pure functions
<ol>
  <li> Pure functions - functions where return values are only determined by input values without observable side effects
  <li> Function composition
  <li> No shared state
  <li> No side-effects
  <li> Immutable data
</ol>

### Promises vs Async/Await
Promise is an object that is a placeholder for the resulting value of an asynchronous operation. A promise is in one of these states:
<ul>
  <li> pending: initial state neither fulfilled or rejected
  <li> fulfilled: operation completed successfully
  <li> rejected: meaning that the operation failed
</ul>
To understand Async/Await better you must understand <a href="https://medium.com/@bluepnume/learn-about-promises-before-you-start-using-async-await-eb148164a9c8"> promises.</a>
The reason you want to want to use Async/Await instead of Promises is to avoid
<a href="https://getstream.io/blog/javascript-promises-and-why-async-await-wins-the-battle/#callback-hell">Callback-hell.</a>

```javascript
function getUsers(userId) {
	axios
		.get(`/users/userId=${users[0]}`)
		.then(res => {
			// save the response for user 1
			response.push(res);

			axios
				.get(`/users/userId=${users[1]}`)
				.then(res => {
					// save the response for user 2
					response.push(res);

					axios
						.get(`/users/userId=${users[2]}`)
						.then(res => {
							// save the response for user 3
							response.push(2);

							axios
								.get(`/users/userId=${users[3]}`)
								.then(res => {
									// save the response for user 4
									response.push(res);
								})
								.catch(err => {
									// handle error
									console.log(err);
								});
						})
						.catch(err => {
							// handle error
							console.log(err);
						});
				})
				.catch(err => {
					// handle error
					console.log(err);
				});
		})
		.catch(err => {
			// handle error
			console.log(err);
		});
}
```
Instead you can use 
<a href='https://blog.logrocket.com/promise-chaining-is-dead-long-live-async-await-445897870abc/'>Async/Await</a>.
 Code is simplified and reduced significantly. Also there is no need to chain promises to make infinite callback loops.
```javascript
async function getUsers(users) {
	try {
		response[0] = await axios.get(`/users/userId=${users[0]}`);
		response[1] = await axios.get(`/users/userId=${users[1]}`);
		response[2] = await axios.get(`/users/userId=${users[2]}`);
		response[3] = await axios.get(`/users/userId=${users[3]}`);
	} catch (err) {
		console.log(err);
	}
}
```
Await must be used within functions that are declared with async in front. ie)
```javascript
async function makeCoffee() {
    try {
    	let cupOfMojo = await promiseToMakeCoffee;
    } catch(err) {
    	console.log('Let me sleep more Zzzzz');
    }
  }
  
  let result = await promiseToMakeCoffee;
  console.log(result);
}
```
<ol>
  <li> Async/Await reduces the amount of code and cleans it up without complicated, nested promises
  <li> Can use error handling with try/catch instead of in each promise
  <li> Error stacks shows exact place instead of ambiguous errors in Promises loops
  <li> Avoid Callback-hell (Not fun :sob: )
</ol>

