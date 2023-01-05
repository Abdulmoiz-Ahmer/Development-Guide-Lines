# Development-Guide-Lines


**JavaScript**

**Line Length**

Lines shouldn’t be longer than 100 characters, and mustn’t be longer than 120 characters. Comments mustn’t be longer than 80 characters.

**Quotes**

Use single quotes if possible. If you need multiline strings or interpolation, use template strings.

```
// Good
const company = 'YardCrm';

// Bad, single quotes can be used here.
const company = "YardCrm";

// Good
function greet(name) {
  return 'Hello ${name}!';
}

// Bad, template strings are preferred.
function greet(name) {
  return 'Hello ' + name + '!';
}
```

Also, when writing HTML templates, start multiline templates on a new line if possible.

```
function createLabel(text){
  return `
    <div class="label">
      ${text}
    </div>
  `;
}
```

**Semicolons**

```
Always.
```

**Variable Assignment**

Prefer const over let. Only use let to indicate that a variable will be reassigned. 

```
// Good
const person = { name: 'Sebastian' };
person.name = 'Seb';

//Bad, the variable was never reassigned
let person = { name: 'Sebastian' };
person.name = 'Seb';
```


Use var where it makes sense to for instance:
```
// Good
var assignment;
try{
	assignment = //...
}catch(error){
	//...
}

//Bad
try{
	let assignment = //...
}catch(error){
	//...
}


```



**Variable Names**

Variable names generally shouldn’t be abbreviated, should always be singular and use camel casing.

```
// Good
function saveUser(user){
 localStorage.set('user', user);
}

// Bad, it's hard to reason about abbreviations in blocks as they grow.
function saveUser(u){
 localStorage.set('user', u);
}
```

**Comparisons**

Always use a triple equal to do variable comparisons. If you’re unsure of the type, cast it first.

```
// Good
const one = 1;
const another = "1";

if(one === parseInt(another)){
  // ...
}

// Bad
const one = 1;
const another = "1";

if(one == another){
  // ...
}
```

**Function Keyword vs. Arrow Functions**

Function declarations should use the function keyword.

```
// Good
function scrollTo(offset){
  // ...
}

// Using an arrow function doesn't provide any benefits here, while the
// `function` keyword immediately makes it clear that this is a function.
const scrollTo = (offset) => {
  // ...
};
```
Avoid anonymous functions expressions or arrow functions as much as possible since they are harder for debugging.
Anonymous functions should use arrow functions, unless they need to access `this`.

```
['a', 'b'].map(a => a.toUpperCase());

$('a').on('click', function (){
  window.location = $(this).attr('href');
});
```

To learn more about the this keyword in JavaScript, refer to:

[this on Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)

[Gentle Explanation of "this" in JavaScript by Dmitri Pavlutin](https://dmitripavlutin.com/gentle-explanation-of-this-in-javascript/)

Object methods must use the shorthand method syntax.

```
// Good
export default {
    methods: {
        handleClick(event) {
            event.preventDefault();
        },
    },
};

// Bad, the `function` keyword serves no purpose.
export default {
    methods: {
        handleClick: function (event) {
            event.preventDefault();
        },
    },
};
```

**Object and Array Destructuring**

Destructuring is preferred over assigning variables to the corresponding keys.

```
// Good

const [hours, minutes] = '12:00'.split(':');

// Bad, unnecessarily verbose, and requires an extra assignment in
// this case.
const time = '12:00'.split(':');
const hours = time[0];
const minutes = time[1];
```

Destructuring is very valuable **for** passing around configuration-like objects.

```
function uploader({
    element,
    url,
    multiple = false,
    beforeUpload = noop,
    afterUpload = noop,
}) {
    // ...
}
```


**Classes**

Classes must be defined using a **class declaration** and not via **class expression** or **function-based syntax**. Class names must use pascal case.

```
// Good
class Agent{
  constructor(name, email){
    this.name = name;
    this.email = email;
  }
    
  getContacts(){
    // ...
  }
}

// Bad
const Agent = class{
  constructor(name, email){
    this.name = name;
    this.email = email;
  }
    
  getContacts(){
    // ...
  }
}

// Bad
function Agent(name, email) {
  this.name = name;
  this.email = email;
}

Agent.prototype.getContacts = function() {
  // ...
}
```

**
Maps vs. Objects**

For storing keyed values—such as a collection of Agents or locations by ID or slug—maps must be used instead of objects. Maps offer several advantages over objects for storing data, mainly that maps are iteratable, preserve key order, does not contain any default keys (only what is explicitly put in it), and it’s size can be determined via its size property.

```
// Good
const addressList = new Map([
	[
		'611ee42cd999d422f22d1b16',
		{
			street_address_1: '543 Red Mangrove Lane',
			street_address_2: '',
			city: 'Apollo Beach',
			state: 'FL',
			postal_code: '33572',
			country: 'US'
		}
	],
	[
		'611ee42cd999d422f22d1b17',
		{
			street_address_1: '9306 Tepee Trl',
			street_address_2: '',
			city: 'Houston',
			state: 'TX',
			postal_code: '77064',
			country: 'US'
		}
	],
	[
		'611ee42cd999d422f22d1b18',
		{
			street_address_1: '2014 Austin Park Cir',
			street_address_2: '',
			city: 'Decatur',
			state: 'GA',
			postal_code: '30032',
			country: 'US'
		}
	]
]);

// Bad
const addressList = {
	'611ee42cd999d422f22d1b16': {
		street_address_1: '543 Red Mangrove Lane',
		street_address_2: '',
		city: 'Apollo Beach',
		state: 'FL',
		postal_code: '33572',
		country: 'US'
	},
	'611ee42cd999d422f22d1b17': {
		street_address_1: '9306 Tepee Trl',
		street_address_2: '',
		city: 'Houston',
		state: 'TX',
		postal_code: '77064',
		country: 'US'
	},
	'611ee42cd999d422f22d1b18': {
		street_address_1: '2014 Austin Park Cir',
		street_address_2: '',
		city: 'Decatur',
		state: 'GA',
		postal_code: '30032',
		country: 'US'
	}
};
```
For more information on Maps refer to the documentation on [Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map).


