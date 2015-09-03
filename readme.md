class: center, middle, title
# Tests & Copilote

[jop@infologic.fr](mailto:jop@infologic.fr)<br>2015

---
layout: true
.left-column[
1. [Disclaimer](#disclaimer)
1. [Readability](#readability)
1. [Benefits](#benefits)
1. [Example](#example)
1. [Bring code under test](#undertest)
1. [Integration tests](#integration)
1. [Maintenance](#maint)
]
---

name: disclaimer
# !!! Disclaimer !!!
## I will not try to convince anybody to write tests.
## We need internally valued reasons to do something.
## However, in the long run, I believe that
# tests minimise maintenance effort!
## So, in my view, in tests, one of the most important things is...
---

name: readability
# Readability
## Test goal's should be obvious from the first look
## Why? Two years after writing the program,
# I don't want to have to sort through layers of irrelevant stuff in order to discover what bug my test just caught.
## And all of it, because I'm <b><u>LAZY</u></b> now!
---

name: benefits
# Think about your future self
## Tests serve against regressions
## Tests serve as executable documentation
.spacer[]
# And think about yourself, now
## Tests give insights about code design
## Tests help us learn new things
.spacer[]
# But, it's not easy to write good tests...
---
name: example
.center[
<br><br><br><br><br><br><br><br>
# OK, now show me some code!
]
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
