---
theme: excali-slide
highlighter: shiki
info: |
  ## How to write a flaky test
title: How to write a flaky test
mdc: true
layout: intro
themeConfig:
  primary-highlight: "#ff657a"
  secondary-highlight: "#ffd76d"
---
# How to write a flaky test

<!--
- flake is the real dirty word
- this presentation is all about how to get rid of it, because it makes testing painful and less enjoyable
- you might remember that feeling when you wrote your first UI test which it opened the page, clicked through, until it turned all green
- the thing you had to do manually before is now automated
- I remember a time when I was just starting test automation and I would race my colleague to see if she can go through the critical scenarios manually, or whether the test automation wins
- over time we built up confidence in test automation so that we no longer needed to do manual checks
- we added more and more tests, but something started brewing in the background
- something that started to break our confidence and slowly built up an anxiety about our test automation
- we would start trusting our tests less and started relying on manual checks again
- it almost felt like checking stuff manually was - in a way - faster
- and this was all caused by a single problem
- test flakiness
-->

---
src: './pages/01_flakiness.md'
---

---
src: './pages/02_scaling.md'
---

---
src: './pages/03_dom_flakiness.md'
---

---
src: './pages/04_network_flakiness.md'
---

---
src: './pages/05_isolation_issues.md'
---

---
src: './pages/06_infrastructure.md'
---

---
src: './pages/07_dry_principle.md'
---

---
src: './pages/08_test_idling.md'
---

---
src: './pages/09_ending.md'
---
