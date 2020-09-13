# Testing Redux Store

Testing Redux store using Cypress as described in [this blog post](https://www.cypress.io/blog/2018/11/14/testing-redux-store/).

## Commands to run example (SiecleGitHub)

mkdir cypress\
cd cypress\
git clone https://github.com/SiecleGitHub/cypress-example-recipes.git \
cd cypress-example-recipes\
code .\
npm install\
cd examples\
cd blogs__testing-redux-store\
npm start &\
npm run cypress:run -- --browser chrome

## Shows how to

- control application via DOM and check that Redux store has been properly updated
- drive application by dispatching Redux actions
- use Redux actions directly from tests
- load initial Redux state from a fixture file
- use automatic user function retries with [cypress-pipe](https://github.com/NicholasBoll/cypress-pipe#readme)
- use snapshot testing via [meinaart/cypress-plugin-snapshots](https://github.com/meinaart/cypress-plugin-snapshots) plugin

## Application

The example TodoMVC application in this folder was copied from [https://github.com/reduxjs/redux/tree/master/examples/todomvc](https://github.com/reduxjs/redux/tree/master/examples/todomvc) on November 2018.

The application exposes the reference to to the store while running inside Cypress-controlled browsers like this

```js
const store = createStore(reducer);

render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
);

// expose store when run in Cypress
if (window.Cypress) {
  window.store = store;
}
```

And the tests can access the store using

```js
it('has expected state on load', () => {
  cy.visit('/');
  cy.window()
    .its('store')
    .then((store) => {
      // manipulate the store reference
    });
});
```
