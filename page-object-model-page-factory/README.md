#Page Factory

This is a sample Java UI test framework implementing Page Factory Model which can be used as a template for any Java UI test automation framework using BDD.

The design pattern of this framework wraps HTML pages with application-specific interfaces allowing your tests to interact with the page elements
without the tests themselves needing knowledge of the underlying HTML. This means any changes to the application HTML are
limited to your page classes - the test code doesn't need to change.


## Application under test
The website I have used for this demo project is a 3rd-party website called ["the-internet"](https://the-internet.herokuapp.com/), 
which is one I came across when I first started learning to develop automated tests. It is divided into a number of 
sub-pages, each demonstrating a different type of HTML element (e.g. checkboxes, dropdowns, inputs etc) and common challenges
you might face when automating a website (e.g. uploading files, infinite scrolls, nested frames etc).

I have chosen to write tests for a subset of these pages, namely:
* Home i.e. the main page
* Checkboxes
* Dropdown
* Dynamic Controls
* Form Authentication

## Project structure
Each page tested has a corresponding feature file, step file and a page class - implementing the Page Factory Model

### Page Factory
My Page Factory classes have two sections:
1. WebElement variable definitions - this combines the selector and getter from the Page Object Model into a single variable
   declaration decorated with the `@FindBy` annotation, which takes in the selector type and value as a parameter, e.g. 
   `@FindBy(id = "checkboxes")`. Page Factory variables are declared as either `WebElement` or `List<WebElement>` depending
   on whether you expect a single control or multiple controls to be returned i.e. replacing calls to `findElement` and 
   `findElements` respectively.
2. public interaction methods - these are the same methods as the Page Object Model but where those methods used the 
   getter methods to obtain the WebElements, here we use the above variables directly.
   
## Running the tests
As the project uses Maven for dependency management the tests can be run using the Maven SureFire plugin:
`mvn clean test`

This can be modified to use a different browser, and to change whether the browser is run in headless mode, e.g.
`mvn clean test -Dbrowser=firefox -Dheadless=false`
will run the tests in non-headless Firefox.