---
layout: default
---

# What is flakiness?

<img src="/images/app_tests.png" class="w-140 m-auto" />

<!--
- simply put, test flakiness happens when a test gives you inconsistent results
- if you run a test 100 times, it should give you the same result
- if it doesn’t and there is no known reason for a different result (test change, app change), then it’s flaky
- so why does flakiness happen? well because things are complicated
- essentially, when writing e2e tests, we attempt to write a program that automates another program
- you can imagine it as a integrating two systems - one system being your app and one system being your test
- a good test fits the app like two cog wheels fitting together
- when things start to grind - that’s when flakiness happens
-->

---
layout: default
---

# Harm caused by flakiness

- loss of confidence
  
- more manual work
- delivery slow down
- lost test coverage
- execution slow-down
- added debugging time
- lost trust in QA process


<style>
  li {
    font-size: 22px;
  }
</style>

<!-- 
- and this is why we need to think about test flakiness. it’s not only about the fact we need to fix some code
- test flakiness has a ripple effect on the whole organization. it may result in:
- loss of confidence in test automation 
- more manual work (need to check flows manually)
- delivery slow down (rerun a pipeline, devs waiting)
- lost test coverage (maybe you choose to ignore a test now)
- execution slow-down (retrying)
- added debugging time (CI related issues)
- lost trust in QA process
- something testers might fear right now, as the rise of AI and ever present demand on cost-cutting is higher than ever
 -->


---
layout: default
---

# Flaky test "fixing" strategies
![](/images/strategies.png){class="h-80"}

<!--
- I’ve consulted and colaborated with many companies varying from ecommerce, through fintech to saas
- and I have seen these so-called strategies helping us live with the fact that our tests are flaky
- muting a test
- quarantining a test
- retrying a test
- adding a longer timeout
- reproducing a test locally
- deleting a test
-->

---
layout: default
---
# Flaky test "fixing" strategies

![](/images/stages_of_grief.png){class="h-80.5"}

<!-- 
- or as I like to call them:
- shock
- denial 
- anger
- bargaining 
- depression
- acceptance
- but there is one that is actually the only one that works
-->

---
layout: cover
---

# Fixing the damn problem!
or you know... not creating the problem in the first place

<!--
- fix the damn problem
- or don’t create it
- of course, this is easier said than done
- as the test automation grows, the problems with flaky tests grow with it
- so how do you fix it?
-->
