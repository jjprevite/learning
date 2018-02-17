# JavaScript and React Study guide 
This is a study guide for understanding topics related to JavaScript and React. 

## JavaScript Questions

### What's the difference between statements and expressions in JavaScript?
We'll say almost anything is an expression. It's basically anything that can go in between the `=` and the semicolon. Here are some examples:

```javascript
var dog = 'Foxy';
var bark = function() { return: 'Bark bark bark!' };
var addTwo = x + 2;
```
So if you remove the assignment operator (`=`) and everything before it + the semicolon, you get:
```
'Foxy'
function() { return: 'Bark bark bark!' }
x + 2
```
These are considered expressions in JavaScript.

Statements usually perform actions. Loops and 'if statements' are statements.

```javascript
//first we define an expression.
const numbers = [0,1,2,3,4];

//then we define a statement which is the loop and then the action of console.log
for(let i = 0; i < numbers.length; i++){
  console.log(numbers[i]);
}
```

This article explains it really well: (Expressions versus statements in JavaScript)[http://2ality.com/2012/09/expressions-vs-statements.html]



### What is a class in ES6?
If we take a look at the (definition by MDN)[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes], it's basically a "special function". Similar to functions in that there are two "components" - class expressions and class declarations. Here's a simple example of a class declaration:

```javascript
class Dog {
  constructor(name, age, breed) {
    this.name = name;
    this.age = age;
    this.breed = breed;
  }
}
```
When we actually use this class, we "construct" it so-to-speak, which is why we use the `constructor` function which defines the parameters for the class, which we will then use when creating an instance of that class.

*Note* - unlike function declarations, class declarations are **not** hoisted. So you need to define the class before you access it.

Class expressions and similar to function expressions. Here's an example:

```javascript
// named
var Rectangle = class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
};
```

### What is a constructor? 
In order to undrestand this, we must first answer the question "What is a class in ES6?" 

A constructor is basically the function which executes when an instance of a class is created.

### When to use () with the arrow function?
The other day, I was doing a tutorial in Gatsby.js and confused by one arrow function has () after the => and one another one didn't. I finally found the answer in this article ("ES6 Arrow Functions: The New Fat & Concise Syntax in JavaScript
Related Topics")[https://www.sitepoint.com/es6-arrow-functions-new-fat-concise-syntax-javascript/].

So if you are using an arrow function to return an expression, then the () are optional. 


## React

### When we're creating a constructor, why do we call super()?
When you extend a class (as we often do in React), we need to call super() to access the methods of the parent. Otherwise, we won't have access to them. For instance, here's an example from the Gatsby.js tutorial:

```javascript
class Counter extends React.Component {
    constructor() {
        super()
        this.state = { count: 0 }
    }
    render() {
        return (
            <div>
                <h1>Counter</h1>
                <p>current count: { this.state.count }</p>
                <button onClick={() => this.setState({ count: this.state.count + 1 })}>plus</button>
                <button onClick={() => this.setState({ count: this.state.count - 1 })}>minus</button>
            </div>
        )
    }
}
```

**Notice** - here, we are creating a class component called "Counter", which extends the Component class from the React library. As a result, when we "construct" this new class, we want it to have all the methods that the parent class has, so we call super(). That gives us access to those methods such as setState which we use for the buttons.


### How does the spread syntax work in JSX?
Originally, I thought my confusion was using the spread syntax in regular JavaScript. However, I first saw it used while working on a React project - in JSX. In this scenario, we're referring to "spread attributes". What is that exactly? It's where you 'spread' your attributes on a Component instead of add them all. Here's an example:

```javascript
  var kobeBryant = {};
  props.name = 'Kobe Bryant';
  props.number = 24;
  props.team = 'Lakers';
  var component = <Card {...kobeBryant} />;
```

Think about how much time this saves! This use of spread attributes in JSX prevents us from having to do this:

```javascript
  var kobeBryant = {};
  props.name = 'Kobe Bryant';
  props.number = 24;
  props.team = 'Lakers';
  var component = <Card name={kobeBryant.name} number={kobeBryant.number} team={kobeBryant.team}  />;
```

### What's the difference between functional components and class components?
According to the (official React docs)[https://reactjs.org/docs/components-and-props.html#es6-classes], the simplest way to create a component is by writing a JavaScript function, which then returns JSX. It is called a functional component because it is a literal function. Here's an example:

```javascript
function Image(props) {
  return <img src={props.src} alt={props.alt} />;
}
```

### What's the difference between uncontrolled and controlled components?
Helpful links for when I decide to answer this...
- (Uncontrolled components)[https://reactjs.org/docs/uncontrolled-components.html]
- (Controlled components)[https://reactjs.org/docs/forms.html#controlled-components]

A controlled input for example needs two things:
 1. A value which is stored somewhere in the state
 2. an `onChange` prop which updates the value in the state when you interact with the input.

### What is the `ref` prop used for in React specifically?
- (Ref prop)[https://reactjs.org/docs/refs-and-the-dom.html]
