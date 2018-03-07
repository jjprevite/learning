# Redux Study guide 
This is a study guide for understanding topics related to Redux. 

## Questions

### What are the two fundamental pieces of Redux?
Actions and reducers. Actions do the thing and reducers handle the actions.

### What exactly is an 'action'?
In a React application, anytime you want to change the state, you should dispatch an action. They don't actually change the state, they let the reducer do that. However, they are the ones who handle changes.

Here's a simple example:
```javascript
export const action = {
    type: 'ADD_CARD',
    text: 'The content of the card',
    listIndex: 4
}
```

Notice a few things here:
- `type`: all actions have a type property with a string value. The string describes the action itself. 
- the additional properties are called the 'payload'. So in this case, we would say the payload consists of the card's text and it's index within the list. So in the case: the card will have two properties: the text which will probably be displayed on the card and the index within the list.

Another way to create an action is with an 'action creator function`. Here, we use a factory function to create our action.
```javascript
export const ADD_CARD = 'ADD_CARD';
//*Why do we create this variable instead of adding it within the factory function?
export const addCard = (text, listIndex) => ({
    type: ADD_CARD,
    text,
    listIndex
    //notice that we initialize the variables but don't declare them as anything.
});

// Use the action creator to create an action
const action = addCard('The content of the card', 4);
//now when we're ready to create the action, we use a function expression by calling the factory function and passing in two arguments respectively for the `text` and `listIndex`.
```

### What is a 'reducer'?
A reducer is simply a function that accepts two arguments: the current state and the action to modify the state.

When you create a reducer, inside the function, you create an object, which will be the new state and then you return it.

The reducer will run every time a new action is dispatched.

Here's an example in it's simplest form:
```javascript
const initialState = {};

export const reducer = (state=initialState, action) => {
    return state;
};
```

Notice how we use one of the new ES6 features- default parameter. So if there is no state passed to the reducer, we use the default which is an empty object containing the initial state.

The structure of reducers is made up several if/else statements which handle different types of actions. Then if we don't modify the state (becauase the actions don't match any actions defined in the if/else statement), we return it just how it is.

Here's an example:
```javascript
export const trelloReducer = (state=initialState, action) => {
    if (action.type === actions.ADD_LIST) {
        // ... do something to generate new state
        return newState;
    }
    else if (action.type === actions.ADD_CARD) {
        // ... do something to generate new state
        return newState;
    }
    return state;
};
```

The second part is this:
```javascript
    if (action.type === actions.ADD_LIST) {
        // ... here, Object.assign generates
        // a new state object by merging an object
        // representing the new state of the lists
        // to the existing state, and in turn, that resulting 
        // object into an empty object, which ensures
        // that we're not mutating the original state object,
        // which is a big no-no
        return Object.assign({}, state, {
            lists: [...state.lists, {
                title: action.title,
                cards: []
            }]
        });
    }
```

Here, we use the syntax `Object.assign({}, state, newState)`.
Three arguments mean this:
- first, we create an empty object.
- then we merge the existing `state` into that object.
- then we add in the newState, which will override any of the state properties that match. This will prevent us from modifying the state directly.

#### What's happening here?
```javascript
[
    ...state.lists,
    {
        title: action.title,
        cards: []
    }
]
```
So we're copying the pre-existing lists, then we create the NEW list, which remember, lists is an array of objects which each represent a single list. In each list, we have an object, which has a title and cards. So in the array, we copy the lists then create this new list which has no cards when we create it which is why it's an empty array.

The spread operator ... allows us to 'spread' the previous lists without have to write them out.

### What is the 'store'?
This is the place that keeps the state and allows you to dispatch actions to modify the state.

Here's a simple example of using the store, actions and reducers together:
```javascript
import * as actions from './actions';
import store from './store';

// Add a third list to the state
store.dispatch(actions.addList('Example list 3'));
// Add a card to the third list
store.dispatch(actions.addCard('Example card 1', 2));
// Logs out the state, with the list and the card added
console.log(store.getState());

### Summary:
Using Redux, he's the basic flow:
- create an action
- handle the action using the reducer
- trigger it using the store.dispatch method
```
