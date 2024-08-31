---
layout: default
---

<img src="/images/axes_3.png" class="w-120 relative bottom-10 left-50" />

<!--
- the final axis is the individual test performance, and as you scale up, the flakiness can become more prominent
-->

---
layout: default
---

# DRY principle

<img src="/images/tweet_david.png" class="w-150 m-auto top-25 relative" v-click />

<!-- 
- one very popular way of optimization is using the DRY principle
- I’m actually not a fan of DRY
- [click] my friend David actually might have said it the best - DRY does not belong into tests
- I could probably do a talk and a half on why I think you should probably use less abstractions than you already do in your test code, but I’ll just say that overusing abstractions in your test code leads to harder debugging and maintenance
- test code should describe the app behavior, and I’ve seen way too many instances of code being optimized for abstraction over being optimized to be maintainable

- but I still think there’s a grain of truth in the DRY principle
- if you want to avoid writing flaky tests, you should not be repeating yourself in test execution
-->

---
layout: two-cols
---

# DRY principle

```js
Cypress.Commands.add('login', () => {

  cy.visit('/')
  cy.get('#email').type('user@example.com')
  cy.get('#password').type('abcd1234')
  cy.get('#submit').click()
  cy.location('pathname').should('eq', '/home')

})
```

::right::

```js
it('test #2', () => { 

  cy.login() // go through UI

})

it('test #2', () => { 

  cy.login() // go through UI

})

it('test #3', () => { 

  cy.login() // go through UI

})
```

<!-- 
- for years I’ve been saying that page object model is not an ideal pattern, mostly because it encourages people to overdo it with abstractions, overuse UI and repeat the same set of actions over and over
- for example, if your app uses a login, there’s a good chance most of your tests require you to log in
- usually, the login object is the first page object you create
- in my example here I’m using a custom command, bit the idea is pretty much the same - on the right side you can see the abstraction being used
- as we use it, we are repeatedly performing a login
- while we our code is written with the DRY principle in mind, the execution is repetitive and slow
- and there’s a danger of flakiness, especially if the application that you test has protection against login attacks, such as CAPTCHA

-->

---
layout: two-cols
---

# DRY principle
```js {3,9}
Cypress.Commands.add('login', () => {

  cy.session('user #1', () => {
    cy.visit('/')
    cy.get('#email').type('user@example.com')
    cy.get('#password').type('abcd1234')
    cy.get('#submit').click()
    cy.location('pathname').should('eq', '/home')
  })

})
```

::right::

```js
it('test #2', () => { 

  cy.login() // go through UI

})

it('test #2', () => { 

  cy.login() // restore from cache

})

it('test #3', () => { 

  cy.login() // restore from cache

})
```
<!-- 
- the way to solve this, which I still see not being that popular is by caching the browser state
- many testing tools already have this
- in Cypress you can do a snapshot of your browser after you have successfully logged in
- and then load that snapshot, so as you can see in the test on the right, the UI login will only happen in the first test, and the rest of your tests will instantly load the cached browser data and have you logged in
- this is THE best way to work with login in your test that will reduce execution time and will reduce the flakiness
-->