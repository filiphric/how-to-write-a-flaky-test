---
layout: default
---

# Infrastructure issues

<div v-click.show='[0,1]'>
  <img src="/images/monitor.png" class="w-200 absolute"/>
</div>

<div v-click.show=1>
  <div class="pb-6">
    <img src="/images/monitor.png" class="w-54 relative inline-block"/>
    <img src="/images/monitor.png" class="w-54 relative inline-block"/>
    <img src="/images/monitor.png" class="w-54 relative inline-block"/>
    <img src="/images/monitor.png" class="w-54 relative inline-block"/>
  </div>
  <div class="pb-6">
    <img src="/images/monitor.png" class="w-54 relative inline-block"/>
    <img src="/images/monitor.png" class="w-54 relative inline-block"/>
    <img src="/images/monitor.png" class="w-54 relative inline-block"/>
    <img src="/images/monitor.png" class="w-54 relative inline-block"/>
  </div>
  <div class="pb-6">
    <img src="/images/monitor.png" class="w-54 relative inline-block"/>
    <img src="/images/monitor.png" class="w-54 relative inline-block"/>
    <img src="/images/monitor.png" class="w-54 relative inline-block"/>
    <img src="/images/monitor.png" class="w-54 relative inline-block"/>
  </div>
</div>

<!--
- another common problem when it comes to flakiness are infrastructure issues
- it’s not uncommon that running test automation happens on a staging server and performance of that server is way too low
- the funny thing is, that even without parallelism your test automation can become a load test
- at one of the companies I have worked with, we were using a testing account that would have thousands of resources on it
- all these API endpoints would contain way too much data and would strain database
- [click] so simply opening an application and make frontend fetch those resources was something that made the backend work extra hard
- since our tests were nice and granular (which is essentially a good thing), we would end up opening the application pretty often
- but we were pretty much DDoSing our staging server by opening that huge testing account tens or hundreds times a minute
-->

---
layout: default
---

# Infrastructure issues

```js
beforeEach(() => {

  if (Cypress.currentRetry === 1) {
    Cypress.config('defaultCommandTimeout', 8000)
  }

  if (Cypress.currentRetry === 2) {
    Cypress.config('defaultCommandTimeout', 12000)
  }

})
```

<!--
- one of the quickfix solutions I have used in the past as many tests started failing was to increase default command timeout when a test failed
- this was based on the assumption that maybe the API responses got slower and the whole application needed more time for elements to render and so on
- I wouldn’t call this an ideal solution, but maybe you could call it pragmatic
- either way, the problem at hand - the huge testing account needed to be solved - ideally by cleaning up the data
-->

---
layout: cover
---

## Which is better?
&nbsp;
```js
beforeEach(() => {}) 
before(() => {}) 
```

vs.

```js
afterEach(() => {}) 
after(() => {}) 
```

&nbsp;
<v-click>opinion: cleanup should happen outside test suite</v-click>

<!--
- when designing a test suite, there’s often a debate on whether you should clean up your data after the test, or before the test
- while I generally lean to cleaning up before the test, if you really want to avoid flakiness
- [click] I’m pretty sure it should happen outside of testing 
- set up a cron job that will clean up data created by tests
- seed your database before e.g. if you are docker
- make sure you have monitoring set up for your testing environment as well to keep it healthy
-->
