class: center, middle, title
# Tests@Copilote

[jop@infologic.fr](mailto:jop@infologic.fr)<br>2015
---

layout: true
.left-column[
1. [Disclaimer](#disclaimer)
1. [Readability](#readability)
1. [Example](#example)
1. [Unit testing](#pattern)
1. [Benefits & Costs](#costs)
1. [Practical stuff](#tools)
1. [Bring code under test](#undertest)
]
---

name: disclaimer
# !!! Disclaimer !!!
## I will not try to convince anybody to write tests
## We need internally valued reasons to do something
## However, in the long run, I believe that
# tests minimise maintenance effort!
## In my view, in tests, one of the most important things is...
---

name: readability
# Readability
## Test goal's should be `obvious` from the first look
## Why? Two years after writing the program,<br>.red[I don't want to have to sort through layers of irrelevant stuff in order to discover what `bug` my test just caught]
## And all of it, because I'm .red[too lazy] now
---

name: example
.center[
<br><br><br><br><br><br><br>
# OK, great! Now show me some `code`!
]
???
TestCaseBlocageUpdaterSansBlocage#testLotAvecDeuxCqTT + testLotAvecDeuxCqTF
TestCaseCapteursTempsMachineUpdater#testBuildCover
TestCaseCreateListProduitHelper#testCalcDateTheo
TestCaseListInvLocker#testVerrouillage (ok, but variables names)
TestCaseMvtWrapperServiceImpl#testAddAnnulation1 + testDoMvtManu2
JTestConversionMonnaie
---

name: pattern
# Unit test pattern
## Setup: `Given` a context
## Exercise: `When` an action is carried out
## Verify: `Then` some consequences should be observable
## Teardown
---

name: granularity
# What does `unit` means in unit testing?
## A method? A class? A cluster of classes?
## A feature? A bug? An idem?
## My code and the database?
## My code and your code?
## Whole system?
---

exclude: true
name: granularity2
# What does `unit` means in unit testing?
## A method? A class? A cluster of classes?
## .red[A feature, a bug, an idem]
## My code and the database?
## My code and your code?
## Whole system?
---

name: risk
# What to test? Risk based testing
## What is the feature that, if it doesn't work, we .red[loose money or clients]?
## What is the part of the code that, if it doesn't work, will .red[bring Copilote down]?
## What are the most .red[complex parts] of the software?
## What are the types of .red[mistakes] we are usually making when developing?
---

name: costs
# Costs
## For yourself, now
### Tests are hard to write
### Tests take time to write
### Tests force us to learn new things
## For your future self
### Bad tests are hard to debug and maintain
### Fine grained tests make production code hard to change
## Unit tests will not catch all bugs!
---

name: benefits
# Benefits
## For yourself, now
### Tests force us to think as consumers of our own code
### Tests make us to re-read our code
### Tests give us insights about design
### Tests help us learn new things
## For your future self
### Tests protect against regression
### Tests provide executable documentation
### Tests facilitate refactoring
---

name: tools
# Create database
```
generator = new TestDBGenerator().dropAll().selectAll(Monnaie.metaDataId)
                                           .select1stLevelDeep0(Societe.metaDataId)
                                           .select1stLevel(Dossier.metaDataId)
                                           .selectAllDeep(PosteStock.metaDataId)//996 tables
                                 .schema()
                                 .createPersistenceContext()
                                 .save(monnaie)
                                 .saveDeep(societe)
                                 .initServiceManager()
                                 .finishInitialisation();
```
# Replace services
```
generator.getServiceManager().injectServiceImpl(SiteService.ROLE, mySiteServiceImpl)
                             .replaceImplClass(StockADateService.ROLE, MyStockADate.class);
```
# Clean the mess
```
generator.tearDown();
```
###.right[see DEVFAQ-230]
---

name: problems
# Problems
## Database setup is hard and ugly
## `static`
* #### `static` state needs explicit teardown
* #### `static` creates globally accessible variables/methods .red[&#8658; hidden dependencies]
## Platform dependency (Linux vs Windows)
* #### file system
* #### line break
## Very well hidden dependencies (ventes vs superviseur)
* #### modules fonctionels
---

# Dependencies
* #### caches
* #### services (`public void service(ServiceManager manager) { ... }`)
* #### services (`ServiceFactory.getService(...)`)
* #### setter arguments
* #### constructor arguments
* #### constructor calls
* #### database
* #### log
* #### filesystem
* #### external library (Velocity, ...)
* #### graphical library (SWT, ...)
* #### browser
* #### time
# Explicit dependencies are better than hidden ones
---

name: blackbox
# Black box testing
#### How many tests should you write for this method?
```
public int compute(int number)
```
--

```
{
  return number;
}
```
---

name: blackbox2
template: blackbox
#### For this one?
```
public int compute(int number, boolean flag)
```
--

#### What about this one?
```
public List manageContQuals(int nomChaine, Produit produit, TypLot typLot,
      List cqComplementaires, List contQualVals, List extraContQualVals,
      VelocityContext ctx, VartampModel vartamp, LotContQualDebugger lotCQDebugger,
      Set<? extends IFonctionSaisieCQ> fonctionSaisieCQs, XmlDb xmlDbTactileParam)
```
### Value sampling
### Equivalence partitioning
---

# Code coverage
## Several types: statement vs branch vs expression vs ...
### Statement coverage is the most basic one
#### Red code is not covered
#### Yellow code is partially covered (conditions)
#### Green is covered but double check branches
![eclEmma screenshot](coverage3.png)
###.right[see [eclEmma](http://www.eclemma.org)]
---

name: undertest
# Bring code under test
## Reproduce bugs as unit tests
## Red: Test should fail
.right-column[![TDD loop](tddloop.jpg)]
## Fix the problem
## Green: Test should succeed
## Refactor: Improve the code
# Freebie: protection against regression
---

layout: true
class: center, middle, title
---

# Questions?
