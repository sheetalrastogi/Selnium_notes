# BDD Learning Resources and Topics Covered

| # | Website | URL | Main BDD Topics Covered |
|---|---------|-----|-------------------------|
| 1 | Behavior-Driven Development - Cucumber | https://cucumber.io/docs/bdd/ | What is BDD, Discovery, Formulation, Automation, Living Documentation, Agile + BDD, Executable Specifications |
| 2 | Behavior Driven Development Tutorial - TutorialsPoint | https://www.tutorialspoint.com/behavior_driven_development/index.htm | BDD Introduction, BDD vs TDD, Specification by Example, Cucumber, Gherkin, SpecFlow, BDD Tools |
| 3 | Behavior-Driven Development (BDD) Tutorial - ZetCode | https://zetcode.com/terms-testing/bdd/ | Core Principles, Ubiquitous Language, Collaboration, Executable Specifications, Outside-In Development, Gherkin |
| 4 | BDD (Behavior Driven Development) Framework: A Complete Tutorial - SoftwareTestingHelp | https://www.softwaretestinghelp.com/bdd-framework/ | BDD Framework, Cucumber, Given-When-Then, Feature Files, Step Definitions, BDD vs TDD, Automation Examples |
| 5 | What is Behavior-Driven Development (BDD)? - GeeksforGeeks | https://www.geeksforgeeks.org/software-engineering/behavioral-driven-development-bdd-in-software-engineering/ | Discovery Phase, Formulation Phase, Automation Phase, Collaboration, Gherkin Examples, Acceptance Criteria |
| 6 | Dan North | https://dannorth.net | Original BDD Concepts, Introducing BDD, Outside-In Development, Specification by Example |
| 7 | Cucumber School | https://school.cucumber.io | Example Mapping, Three Amigos, Writing Better Scenarios, Living Documentation |
| 8 | Martin Fowler | https://martinfowler.com | Acceptance Testing, BDD Concepts, Specification by Example, Agile Analysis |
| 9 | ToolsQA Selenium Cucumber Framework | https://www.toolsqa.com/selenium-cucumber-framework/ | Selenium + Cucumber Framework, POM, Page Factory, Dependency Injection, Reporting |
| 10 | Semaphore CI Blog | https://semaphoreci.com/blog | BDD in CI/CD, Test Automation, Continuous Testing, Best Practices |

## Key BDD Topics Across All Resources

- Introduction to BDD
- BDD vs TDD
- Specification by Example
- Discovery Workshops
- Three Amigos Collaboration
- Example Mapping
- Ubiquitous Language
- Gherkin Syntax
- Given-When-Then Format
- Feature Files
- Step Definitions
- Acceptance Criteria
- Living Documentation
- Outside-In Development
- Executable Specifications
- Selenium + Cucumber Framework Design
- Page Object Model (POM)
- Dependency Injection
- Reporting and Test Automation
- BDD in CI/CD Pipelines
- Continuous Testing Best Practices
---

### B. Cucumber Automation Framework Tutorial

## B.1 Cucumber Automation Framework
https://www.toolsqa.com/selenium-cucumber-framework/cucumber-automation-framework/

## B.2. End to End Selenium Test
https://www.toolsqa.com/selenium-cucumber-framework/selenium-end-to-end-automation-test/

## B.3. Convert Selenium Test to Cucumber BDD Style
https://www.toolsqa.com/selenium-cucumber-framework/convert-selenium-test-to-cucumber/

## B.4. Gherkin Keywords
https://www.toolsqa.com/cucumber/gherkin-keywords/

## B.5. Feature Files
https://www.toolsqa.com/cucumber/cucumber-jvm-feature-file/

## B.6. Step Definitions
https://www.toolsqa.com/cucumber/step-definition/

## B.7. Test Runner
https://www.toolsqa.com/cucumber/junit-test-runner-class/

## B.8. Page Object Model using Page Factory
https://www.toolsqa.com/selenium-cucumber-framework/page-object-design-pattern-with-selenium-pagefactory-in-cucumber/

## B.9. Page Object Manager
https://www.toolsqa.com/selenium-cucumber-framework/page-object-manager/

## B.10. Config File Reader
https://www.toolsqa.com/selenium-cucumber-framework/read-configurations-from-property-file/

## B.11. File Reader Manager
https://www.toolsqa.com/selenium-cucumber-framework/file-reader-manager-singleton-design-pattern/

## B.12. WebDriver Manager
https://www.toolsqa.com/selenium-cucumber-framework/design-webdriver-manager/

## B.13. Sharing Test Context with PicoContainer
https://www.toolsqa.com/selenium-cucumber-framework/sharing-test-context-between-cucumber-step-definitions/

## B.14. Hooks (@Before/@After)
https://www.toolsqa.com/selenium-cucumber-framework/how-to-use-hooks-in-selenium-cucumber-framework/

## B.15. Data Driven Testing using JSON
https://www.toolsqa.com/selenium-cucumber-framework/data-driven-testing-using-json-with-cucumber/

## B.16. Wait Utility for Ajax Wait
https://www.toolsqa.com/selenium-cucumber-framework/handle-ajax-call-using-javascriptexecutor-in-selenium/

## B.17. Sharing Scenario Context
https://www.toolsqa.com/selenium-cucumber-framework/share-data-between-steps-in-cucumber-using-scenario-context/

## B.18. Cucumber Reports
https://www.toolsqa.com/selenium-cucumber-framework/cucumber-reports/

## B.19. Extent Reports with Cucumber
https://www.toolsqa.com/selenium-cucumber-framework/cucumber-extent-report/

## B.20. Run Cucumber Tests from Command Line
https://www.toolsqa.com/selenium-cucumber-framework/run-cucumber-test-from-command-line-terminal/


### Core BDD Concepts
01. Gherkin Language:	Given, When, Then, And, But, Scenario, Scenario Outline
02. Feature files
03. Step Definitions
04. Test Runner
05. Cucumber Options
06. Hooks
07. Scenario Contexts
08. Dependency Injection
09. Reporting
10. Data-Driven BDD


### Selenium Framework Design Topics

Design Patterns

| Pattern / Design Approach | Usage |
|---------------------------|-------|
| Page Object Model (POM) | Encapsulate page actions and locators |
| Page Factory | Element initialization using annotations |
| Singleton | File Reader Manager (single configuration instance) |
| Manager Pattern | Page Object Manager for centralized page object creation |
| Dependency Injection (DI) | PicoContainer for object sharing and lifecycle management |
| Context Pattern | Scenario Context for sharing test data between steps |
| Factory / Driver Management | WebDriver Manager for browser driver creation and management |


### Framework Utilities

| Utility Area              | Purpose                          |
|---------------------------|----------------------------------|
| Configuration Management  | Property Files                   |
| Test Data Management      | JSON Reader                      |
| Driver Management         | WebDriver Manager                |
| Synchronization           | Ajax Wait Utility                |
| Reporting                 | Cucumber + Extent Reports        |
| Context Sharing           | Scenario Context                 |
| Setup/Teardown            | Hooks                            |
| Execution Management      | Command Line Execution           |



### BDD Framework Components

```text
Feature Files
     ↓
Step Definitions
     ↓
Test Runner
     ↓
PicoContainer DI
     ↓
Scenario Context
     ↓
Page Object Model
     ↓
Page Object Manager
     ↓
WebDriver Manager
     ↓
Config Reader
     ↓
JSON Test Data
     ↓
Hooks
     ↓
Wait Utilities
     ↓
Reports
     ↓
CLI / CI Execution
```







