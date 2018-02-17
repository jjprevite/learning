# React Study guide 
This is a study guide for understanding topics related to React. 

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

A constructor is basically the function which execut s when an instance of a class is created.

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
