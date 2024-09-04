---
layout: two-cols
---

# DOM flakiness

<div class="h-full relative">
<div class='absolute top-35 w-full'>
```js {*|3-4|*}
it('finds the word "bugs" on a card item', () => {
  cy,visit('/board/1')
  cy.get('[data-cy=card]')
    .eq(0)
    .should('contain.text', 'bugs')
})
```
</div>
</div>

::right::
<div v-click.hide=2>
  <img src="/images/selecting_elements.png" class="absolute w-107"/>
</div>
<img src="/images/selecting_elements_2.png" class="absolute w-107" v-click.show=2 />
<!-- 
- let’s talk about DOM flakiness first
- consider the following scenario. You want to select a card (the white element on the page) and assert its text
- Notice how both of these elements contain the word "bugs" inside. Can you tell which card are we going to select when using this code?
- You might be guessing the first one, with the text "triage found bugs"
- [click] the reasoning might be, because we select the card element and filter the first one. While that may be a good answer it’s not the most precise one. 
- Correctly it is - whichever card will load first
- [click] consider if at time of the execution of these commands, our app would look like this
- we’d still select card elements, we’d still filter the first one and make our assertion
 -->

---
layout: default
---

# DOM flakiness

<img src="/images/app_tests.png" class="w-140 m-auto" />

<!-- 
- if we ignore what the app is doing, there’s a high chance our test not doing what we expect, and therefore leading to flaky results
- this ties to the graphic I showed before, where these two cog wheels start to grind, or not even move properly
-->

---
layout: two-cols
---

# DOM flakiness

<div class="h-full relative">
  <div class='absolute top-35 w-full'>
````md magic-move
```js
it('finds the word "bugs" on a card item', () => {
  cy,visit('/board/1')
  cy.get('[data-cy=card]')
    .eq(0)
    .should('contain.text', 'bugs')
})
```
```js
it('finds the word "bugs" on a card item', () => {
  cy.visit('/board/1')
  cy.get('[data-cy=card]')
    .should('have.length', 2)
    .eq(0)
    .should('contain.text', 'bugs')
})
```
````
  </div>
</div>

::right::
<img src="/images/selecting_elements.png" class="absolute w-107"/>

<!-- 
- so what is the solution?
- there’s no one size fits all, but my recommendation would be to add a level of determinism to your test
- [click] one solution would be to add assertions to your tests that will serve as checkpoints - places where your app and test are in complete sync
- these will pretty much make sure that the test is not moving faster than the app or vice versa
- the example checks number of elements, but this could be assertion on loaders no longer existing, API request responding, element appearing and so on
-->