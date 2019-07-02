# Redux Usage

Any react project with more than a basic state should be using [Redux](https://redux.js.org/) as an application state management utility.

## General

> Redux is a predictable state container for JavaScript apps.

Redux maintains the entire application state in a singular store.

## Redux Modules

Once our singular store model exceeds basic complexity, we need to split code into different speciality areas called "modules".

When designing a module, there should be mindfulness of the total usage of data since the Redux store is kept in users' browser memory. Individual redux modules should be thought of as a tables in a relational database, normalizing data so that it isn't repeated thoughout multiple modules.

A redux module contains actions, reducers and, optionally, selectors. Some stores are simple enough that they can be contained in one `index.js` file. Once complexity has risen, the following file formats should happen:

```sh
my-redux-module/
  actions.js
  index.js
  reducer.js
  selectors.js
  [constants.js]
  [helpers.js]
```

## Actions

Actions are plain objects describing what happened in the app, and serve as the sole way to describe an intention to mutate the data.

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

### Async Middleware (Thunks)

> Thunks are the recommended middleware for basic Redux side effects logic, including complex synchronous logic that needs access to the store, and simple async logic like AJAX requests. [ref](https://github.com/reduxjs/redux-thunk#why-do-i-need-this)

When an action is expected to reach out to a service to fetch data or use values from the existing store, we use a middleware called [Redux Thunks](https://github.com/reduxjs/redux-thunk).

### Action Creators

> Redux Thunk middleware allows you to write action creators that return a function instead of an action. The thunk can be used to delay the dispatch of an action, or to dispatch only if a certain condition is met. The inner function receives the store methods dispatch and getState as parameters.

A complex example of getting an avatar either by existing store or fetching it new:

```js
function fetchAvatar({space, userId}, spark) {
  return (dispatch, getState) => {
    const {avatar} = getState();
    const avatarId = space ? space.id : userId;
    const hasFetched = avatar.hasIn(['items', avatarId]);
    const isFetching = avatar.hasIn(['avatarsInFlight', avatarId]);

    if (hasFetched) {
      return Promise.resolve(avatar.getIn(['items', avatarId]));
    }

    if (isFetching) {
      return Promise.resolve();
    }

    if (space) {
      return dispatch(fetchSpaceAvatar(space, spark, userId));
    }

    return dispatch(fetchUserAvatar(userId, spark));
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

## References

- [Speeding up Product Development with Redux Modules](https://www.smartly.io/blog/speeding-up-product-development-with-redux-modules)
- [Thunks in Redux](https://medium.com/fullstack-academy/thunks-in-redux-the-basics-85e538a3fe60)
