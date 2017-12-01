# Redux Usage

Any react project with more than a basic state should be using [Redux](https://redux.js.org/) as an application state management utility.

## General

> Redux is a predictable state container for JavaScript apps.

Redux maintains the entire application state in the forms of different data stores. Since Redux stores are kept in users' browser memory, there should be mindfulness of the total usage of data. Individual data stores should be thought of as a tables in a relational database, normalizing data so that it isn't repeated thoughout multiple stores.

A redux store (or module) contains actions, reducers and, optionally, selectors. Some stores are simple enough that they can be contained in one `index.js` file. Once complexity has risen, the following file formats should happen:

```sh
my-redux-module/
  actions.js
  index.js
  reducer.js
  selectors.js
```

## Actions

### Action Names

- Your action should describe a change that has happened in your system in the format `VERB_NOUN`

- All action names should be exported constants so that other modules can listen for them as well:

  ```js
  export const ADD_USER = `ADD_USER`;
  export const REMOVE_USER = `REMOVE_USER`;
  ```

- For grouped actions, the beginning should match:

  ```js
  export const FETCH_USER_BEGIN = `FETCH_USER_BEGIN`;
  export const FETCH_USER_ERROR = `FETCH_USER_ERROR`;
  export const FETCH_USER_SUCCESS = `FETCH_USER_SUCCESS`;
  ```

- In an application that has multiple redux modules, action names should be preceeded by the module name

  ```js
  export const ADD_USER = `users/ADD_USER`;
  ```

### Action Functions

Action functions that directly effect the store should match their names: `ADD_USER` === `function addUser(user)`.

The shape of the object returned from the function should be the same for all actions, "type" and "payload". This makes the reducers cross compatible and easier to develop.

  ```js
  function addUser(user) {
    return {
      type: ADD_USER,
      payload: {
        user
      }
    };
  }
  ```

## Reducers

### Initial State

Reducers should have an exported initial state. This makes testing much easier.

  ```js
  export const initialState = {
    users: []
  }
  ```

### Reducer

The main reducer function should be the default exported item of the redux module.

  ```js
  export default function reducer(state = initialState, action) {
    switch (action.type) {
    case ADD_USER:
  ```

## Debugger

A very powerful utility to assist your redux debugging is the [Devtools for Redux, https://github.com/gaearon/redux-devtools](https://github.com/gaearon/redux-devtools)

## Inspiration

A huge inspiration for this style was from the ["Ducks: Redux Reducer Bundles"](https://github.com/erikras/ducks-modular-redux) project!
