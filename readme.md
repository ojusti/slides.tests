class: center, middle, title
# Tests & Copilote

[jop@infologic.fr](mailto:jop@infologic.fr)<br>2015

---
layout: true
.left-column[
1. [Excuses](#excuses)
1. [Difficulties](#difficulties)
1. [Readability](#readability)
1. [Risk-based testing](#risk)
1. [Bring code under test](#undertest)
1. [Integration tests](#integration)
1. [Maintenance](#maint)
]

---
name: excuses
# Frequent excuses to not write tests
<br>
### I don't have time to write tests. I could be coding new features instead
## But, how much time do you spend chasing bugs?
### Manual testing is good enough
## But, do you really test everything everytime?

---
template: excuses
# Tests **minimise maintenance** in the long run

---
name: difficulties
# It's not easy to write good tests
#### How many tests should you write for this method?
```
public int compute(int number)
```

---
template: difficulties
```
{
  return number;
}
```

---
template: difficulties
#### For this one?
```
public int compute(int a, int b)
```

---
layout: true
class: center, middle, title

---
# To be contd

---
# Questions ?
