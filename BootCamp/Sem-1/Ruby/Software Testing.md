# Software Testing

* Testing is an extremely important part of development
* Even with a QA team adequate testing coverage is integral for all developers
* There are many ways to test and they are done throughout the whole process

#### The goals of testing

* Functional - it meets the requirements
* Usability - Ease of use and interface intuitiveness
* Reliable - does not break with unexpected inputs
* Scalable - performs well under expected load
* Secure - Protects user data and companies from financial loss

---

## Functional testing

Functional testing verifies that the application functions as expected without errors. Here are some examples of functional testing:

* Unit testing
* Integration testing
* Smoke testing
* End-to-end testing
* Regression testing
* Acceptance testing

### Unit Testing

* Done from the very start of the development process
  * Often with Test Driven Development (TDD)
* Automated
* Tests the deterministic behaviour of individual functions
* Constantly updates for bug fixes, new features, and code refactoring
* For ruby, use Rspec, MiniTest, or TestUnit
* For Javascript, use Mocha or Jest

### Integration Testing

* Done from early in the development process
* Tests that units work together as expected
* Incorporate testing of environment, such as network, environment variables, and database
* If unit tests are sufficient, failures indicate issues in the environment or infrastructure (or how the application is using those resources)
* Can use same testing libraries used for unit test

###  End-to-end (system) testing

* Comprehensive integration tests for entire application processes
* Involves testing front and back-end code
* Tests that entire user scenarios can be performed as expected
* Common testing frameworks are Selenium and Cypress

### Acceptance Testing

* Final step of functional testing
* Verifies 'definition of done' criteria are met
  * All requirements agreed on by development and stakeholders are met
* Often performed by a QA team
* Combination of automated and manual testing

---

## Non Functional testing

Nonfunctional testing is used to verify other aspects of the application, such as usability, performance, and security. Some types of nonfunctional testing are:

* User Interface/User Experience (UI/UX) testing
* Accessibility testing
* Performance testing
* Internationalization testing
* Security testing
* Disaster recovery testing

### Usability Testing

* Tests the user experience of the application
* Can start as soon as UI prototype is available
* Happens at every part of the iterative development process
* Done by end user target audience
* Used to identify missing or inadequate UI/UX

---

## Manual testing Vs Automated Testing

* A combination of manual and automated testing is always used
  * Many but not all tests can be automated
* There is always a tradeoff between effort required to write and maintain automate tests and effort required for manual testing
* When either is used, documenting results is important
* A balance that provides adequate test coverage and on time application delivery is the goal

### Benefits of automated tests

* Manual testing takes too long and is not consistent or reliable enough for commercial products
* Well-written automated tests provide a faster and more reliable way to test application
* Automated tests can be used in continuous integration and continuous deployment(CI/CD)
* Automated tests increase developer confidence in making changes

### Challenges of automated testing

* Automated tests are code - so they increase the amount of code that has to be written and maintained for an application
* Writing effective tests is a skill and requires investment
* Dependence on automated tests can lead to false confidence when the tests are not well maintained

---

## Developer responsibilities

As developers we are expected to :

*  Identify testing requirements
* Write automated tests
* Write manual test cases
* Execute tests
* Document Results
* Review tests with code review
* Maintain tests

### Documenting test results

* Tests are not useful if results are not documented
  * May be required for International Standards Organization (ISO) compliance
* Automated tests should be self documenting
* Manual tests require rigid process to ensure results are consistently documented
  * Can use various tools for documentation (spreadsheets, wikis, Confluence)

### Reviewing tests is a part of code review

* When code changes are submitted, they should often include tests
  * When new features are added they need tests
  * When bugs found by someone outside of the development team are fixed, add tests to detect the bug
* It is common for test coverage to be a consideration for code review
  * If inadequate tests are provided with the code change, changes may be rejected
  * 'Adequate tests' is something that requires consideration as careful as other coding decisions

### Tests require constant maintenance

* As an application is updated, tests must be updated
* As new bugs are found, tests must be updated
* If tests are not maintained, they become useless and even dangerous for inspiring false confidence

