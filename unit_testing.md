# Unit testing
- great for refactoring
- makes you think about architecture

## Automated tests
- Can be divided into unit tests, integration tests, and end-to-end tests
- Improve code reliability, but reduce development speed in the short term

## Unit test
A single function performs as expected, i.e. given an input we expect a specific output. Great for checking edge cases.
These work independently of each other - check functions in insolation

## Integration test
Tests that functions work all together. Good for testing APIs before it goes to production. 
Testing that everything works together as intended.

## End to end testing
Simulate entire interaction from user perspective.
run by bots to simulate human interaction
It is not good to just have end to end test as we would not be able to quickly pinpoint where exactly the problem is. 

### Mix of different types of tests:
- 70 % Unit
- 20 % Integration
- 10 % E2E


## Pros and Cons
Pro:
- reliability
- running production app without test is a nightmare

Cons:
- development speed in short term
- bunch of unit test during prototyping phase is gonna be annoying

## What should you test for?
- check if you can even call the function
- input types - handle the ones that you want gracefully and catch all the edge cases
- check 


## Testing frameworks
- Assertion styles (assert, expect, should)
[Jest](https://jestjs.io/docs/setup-teardown)
- beforeEach and afterEach for setting up the tests
- describe to group test
- assertion libraries - check documentation for each framework

[Mocha](https://mochajs.org/)
- requires external assertion libraries, `assert` comes with node. Chai is a popular one to be used with Mocha.


## TDD test driven development and BDD behaviour driven development
code coverage - number of lines covered by tests
### TDD
- In TDD you always start by implementing a test that fails, and then write the code to fix it, proceeding one test at a time

- first all test should be written
- check that all tests are failing
- write code and try to pass all tests
- refactor

forces you to think about all the edge cases

### BDD
- in BDD you test a list of expected inputs / outputs based on common use cases
- test some specific example behaviour
- test can come before or after writing

### Tradeoff between reliability and development speed
- Few tests are better than no test
- How solid does your implementation needs to be? 
- If too much time spent debugging - write more tests!
