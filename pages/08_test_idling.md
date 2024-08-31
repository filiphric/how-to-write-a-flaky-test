---
layout: two-cols
---

# Test idling

❌ incorrect way, don’t use
```js {*|2|none}{at: 1}
cy.visit('/')
cy.wait(10000)
cy.get('button') 
  .should('be.visible')
```

```js {none|*|none}{at:2}
// cypress.config.js
import { defineConfig } from 'cypress'

export default defineConfig({
  e2e: {
    defaultCommandTimeout: 60000
  },
})
```

::right::

✅ much better
```js {*|2|none}{at: 1}
cy.visit('/')
cy.get('button', { timeout: 10000 })
  .should('be.visible')
                                                                      // need this for better alignement
```

```js {none|*}{at:3}
// legacy part of the app that takes too long to load
it('test', { defaultCommandTimeout: 60000 }, () => {

})
```

<!-- 
- finally, we get to test idling - this refers to any time a test is waiting
- you probably know that you should avoid hard waiting as much as possible, but as we know there are many instances where it seems like the waiting is inevitable
- [click] in any case, avoiding explicit waiting should be used whenever possible, and instead timeouts should be used
- you can think of timeouts as the upper limits for a test failure, compared to explicit wait, that just waits for set amount of seconds
- [click] that being said, you should avoid setting the limits too high, because that can make your whole test execution very slow, especially if you have multiple tests that have failed
- [click] instead, you should make sure you set a granular timeout for a single test
-->

---
layout: two-cols
---

# Test idling

waiting for DOM elements
```js
it('testing todos', () => {
  cy.visit('/')
  // page loading, wait for loader to disappear
  cy.get('.loader')
    .should('not.exist')

  // continue with our test
})
```

::right::


waiting for network calls
````md magic-move
```js
it('testing todos', () => {
  cy.intercept('/todos').as('todos')
  cy.visit('/')
  cy.wait('@todos')
  // page is loaded, continue with the test
})
```

```js
it('testing todos', () => {
  cy.intercept('/todos').as('todos')
  cy.intercept('/profile').as('profile')
  cy.visit('/')
  cy.wait(['@todos', '@profile'])
  // page is loaded, continue with the test
})
```

```js
it('testing todos', () => {
  cy.intercept('**').as('requests')
  cy.visit('/')
  cy.get('@requests.all')
    .should('have.length', 10)
  // all 10 requests have been sent
})
```

```js
it('testing todos', () => {
  cy.intercept('**').as('requests')
  cy.visit('/')
  // set longer timeout
  cy.get('@requests.all', { timeout: 30000 })
    .should('have.length', 10)
  // all 10 requests have been sent})
```
````

<!-- 
- one of the most common areas that causes test to be idle is the first page load - once a page is loaded, most applications operate relatively smoothly, but the beginnings can be messy, which can result in more test flakiness
- the easiest way to make sure the page is loaded is by checking the DOM and as the example on the left shows, wait for the loader element to disappear
- a slightly more thorough way is to wait for the network calls
- as the example on the right shows, you can use intercept to make sure that a certain API call happened, and that you can proceed with your test
- [click] there are also multiple ways of how it can be taken further, as this update example now shows, you can wait for a whole array of API calls
- [click] of course, you may not want to name all the API calls one by one, especially if there are many of them, so you can choose an approach that is slightly more loose and wait for all the requests
- [click] there’s just one small caveat, and it is that the should command in the example will will usually need to be set up for a longer timeout
-->