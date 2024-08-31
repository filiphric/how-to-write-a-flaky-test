---
layout: default
---

# Test automation scaling

<div v-click.hide=3>
<img src="/images/axes_1.png" class="w-90 left-35% fixed" v-click.show=1 />
<img src="/images/axes_2.png" class="w-90 left-35% fixed" v-click.show=2 />
</div>
<img src="/images/axes_3.png" class="w-90 left-35% fixed" v-click.show=3 />


<ul class="fixed right-30 bottom-10" v-click.show=4>
<li>DOM flakiness</li>
<li>network flakiness</li>
</ul>

<ul class="fixed left-30 bottom-55"  v-click.show=5>
<li>isolation issues</li>
<li>infrastructure issues</li>
</ul>

<ul class="fixed right-60 top-70" v-click.show=6>
<li>DRY principle</li>
<li>test idling</li>
</ul>

<!-- 
- generally as your project scales, there are three axes on which the project grows
- [click] test coverage - number of tests
- [click] test execution - a way of how you execute your test, usually this means dealing with stuff such as parallelism, pipelines etc
- [click] test performance - pretty much just means the speed of how individual test execute
- flakiness can occur in any one of these axes
- [click] on the x axis, as the project grows, we deal with randomly occurring issues connected to DOM re-rendering and network related issues
- [click] on the y axis, as we run our tests in parallel, flakiness can come from stuff like bad test isolation or simply the infrastructure that we are testing on
- [click] and on the z-axis we mostly deal with performance issues and flakiness connected to how tests execute
- so let’s break down how a flaky test happens on each of these axes, and how to fix and prevent it from happening
-->

---
layout: default
---

<img src="/images/axes_1.png" class="w-180 relative bottom-90 left-15" />

<!--
- do let’s talk about the first axis and the flakiness issues that arise as the test suite grows in number of tests
-->