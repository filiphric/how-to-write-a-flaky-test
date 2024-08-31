---
layout: default
---

<img src="/images/axes_2.png" class="w-150 relative bottom-20 left-40" />

<!--
- let’s talk about the second axis of scaling and the flakiness issues that arise from the way test is being executed
-->

---
layout: default
---

# Test isolation issues

❌ don’t do this
```js
describe('item workflow', () => {

  it('creates an item', () => {
    
  })
  
  it('edits an item', () => {

  })
  
  it('deletes an item', () => {

  })
})
```

<!--
- you probably know that when writing test, they should not have side effects in other tests
- cypress does a good job isolating tests. every it() blocks has its own cookies, local storage, even an empty page is opened briefly in between tests to avoid any side effects
- in my experience as consultant I still see people trying to create tests that depend on each other
- this is flaky by design, because you are creating a situation where a test fails or is not ever ran, because of some outside factor
- normally I’d recommend splitting these tests into different specs
-->

---
layout: default
---

# Test isolation issues

<img src="/images/parallel_1.png" class="w-100 top-30 left-70 absolute" v-click.show='[0, 1]'/>
<img src="/images/parallel_2.png" class="w-100 top-30 left-70 absolute" v-click.show='[1, 2]'/>
<img src="/images/parallel_3.png" class="w-100 top-30 left-70 absolute" v-click.show='[2, 3]'/>
<img src="/images/parallel_4.png" class="w-100 top-30 left-70 absolute" v-click.show=3 />


<div class="bottom-10 left-105 absolute text-color-#ff657a" v-click.show='[1, 3]'>1 failed test</div>
<div class="bottom-10 left-103 absolute text-color-#ff657a" v-click.show=3>2 failed tests</div>

<!-- 
- but you’d be right to point out that splitting these test into their own spec files might also create problems once you decide to run your tests in parallel
- problem can arise when tests on different machines start affecting each other
- let’s say you have a testing account that you run your tests with
- while you are running your tests one by one, nothing serious would happen
- but as your test suite grows, you realize you should probably run your tests in parallel, and that’s where trouble happens
- you may have a test that creates a resource on one machine, a test that edits resource on second machine and then a test that deletes a resource on third machine
- depending on how these tests run, you may encounter flakiness
- [click] either we delete item before editing it
- [click] try to delete a non-existing item
- [click] or create an item way too late
- in any case, good luck debugging that
- my #1 advice would be that even if you don’t run your tests in parallel today, you should start designing the test isolation 
- to do that, you can think about the common denominator for your test and make sure that it is separated on separate machines
- so for example, if you are testing an ecommerce site, you should make sure that parallel processes don’t share the same customer account
-->
