_Okay, where do we start then? I thought best place to start learning Redux would be the docs._

# Part 1

[Redux Essentials: Redux Overview and Concepts](https://redux.js.org/tutorials/essentials/part-1-overview-concepts)

### What is Redux, anyway?

> Redux is a pattern and library for managing and updating application state, using events called "actions".

It helps us to manage the state of our app or website.

### Why Should I Use Redux?

Redux helps to manage the global state = state that is needed across many parts of your application.

The patterns and tools provided by Redux make it easieri to understand when, where, why and how the state in your application is being updated, and how your application login will behave when those changes occur.

Predictable and Testable

## Redux Terms and Concepts

### State Management

- The **state**, the source of truth that drives our app;
- The **view**, a declarative description of the UI based on the current state
- The **actions**, the events that occur in the app based on user input, and trigger updates in the state

![One-way data flow: ](./assets/redux_state.png)

### Immutability

"Mutable" means "changeable". If something is immutable it can never be changed.

**In order to update values immutably, your code must make copies of existing objects/arrays, and then modify the copies.**

**Redux expects that all state updates are done immutably.**

## Terminology

### Actions

An action is plain JavaScript object that has a type field. **You can think of an action as an event that describes something that happened in the application.**

An example of a typical action object:

```javascript
const addTodoAction = {
  type: "todos/todoAdded",
  payload: "Buy milk",
};
```

### Action Creators

An actions creator is function that creates and returns an action object. We typically use these so we don't have to write the action object by hand every time.

```javascript
const addTodo = (text) => {
  return {
    type: "todos/todoAdded",
    payload: text,
  };
};
```

### Reducers

A **reducer** is function that receives the current `state` and an `action` object, decides how to update the state if neccessary, and returns the new state: `(state, action) => newState`. **You can think of a reducer as an event listener which handles events based on the received action (event) type.**

#### Reducers must _always_ follow below rules:

- They should only calculate the new state value based on the `state` and `action` arguments;
- They are not allowed to modify the existing `state`. Instead, they must make _immutable updates_, by copying the existing `state` and making changes to the copied values.
- They must not do any asynchronous logic, calculate random values, or cause other "side effects"

#### The logic inside reducer functions typically follow the same series of steps:

- Check to see if the reducer cares about this action

* if so, make a copy of the state, update the copy with new values, and return it

- Otherwise, return the existing state unchanged;

#### An example of how reducers should look like:

```javascript
const initialState = { value: 0 };

function counterReducer(state = initialState, action) {
  // check to if the reducer cares about this action
  if (action.type === "counter/increment") {
    // if so, make a copy of  `state`
    return {
      ...state,
      // and update the copy with the new value
      value: state.value + 1,
    };
  }

  // otherwise, return the existing state unchanged
  return state;
}
```

> Reducers can use any kind of logic inside to decide what the new state should be: `if/else`, `switch`, loops, and so on.

[Why Are They Called `Reducers` in depth explanation link](https://stackoverflow.com/questions/40599496/why-is-a-redux-reducer-called-a-reducer)
