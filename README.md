# redux-basic-http-middleware

A super simple redux middleware for intercepting HTTP events.

## Install

```shell
$ npm install --save redux-basic-http-middleware
```

## Usage

```javascript
import { createStore, applyMiddleware } from 'redux';
import reduxBasicHttpMiddleware from 'redux-basic-http-middleware';
import thunkMiddleware from 'redux-thunk';
import rootReducer from './reducers';

//Basic configuration for the middleware
const config = {
  baseUrl: 'YOUR API ROUTE'
};

createStore(rootReducer, applyMiddleware(thunkMiddleware, reduxBasicHttpMiddleware(config)))
```

## API

#### Action Example

```javascript
const fetchUser = user => ({
  type: 'FETCH_USER',
  promise: {
    method: 'get',
    url: `users/${user}`
  }
});
```

#### Action With Options

```javascript
const saveUser = user => ({
  type: 'FETCH_USER',
  promise: {
    method: 'post',
    url: 'users',
    data: {
      user
    }
  }
});
```

#### Aync actions

`redux-basic-http-middleware` is built on the idea of async actions, and correlating action types are called for each action.

When an action is called, the acion type of `ACTION_TYPE_REQUEST` is called, where `ACTION_TYPE` is the name of your action.

If an action completes successfully, we call `ACTION_TYPE_SUCCESS` where `ACTION_TYPE` is the name of your action.

If an action fails, we call `ACTION_TYPE_FAILURE` where `ACTION_TYPE` is the name of your action.

**Quick example**

```javascript
const fetchUser = user => ({
  type: 'FETCH_USER',
  promise: {
    method: 'get',
    url: `users/${user}`
  }
});

//"FETCH_USER_REQUEST" is called immediately and can be used to show a loading state
//If the function succeeds, "FETCH_USER_SUCCESS" is called
//If the function fails, "FETCH_USER_FAILURE" is called
```

## Development

If you find an issue, feel free to [open an issue](https://github.com/hcjk/redux-basic-http-middleware/issues).

```shell
git clone git@github.com:hcjk/redux-basic-http-middleware.git
```

## License

Copyright (c) 2017 Henry Kaufman, licensed under the MIT license. See [LICENSE.md](https://github.com/hcjk/redux-basic-http-middleware/blob/master/LICENSE.md) for more information.
