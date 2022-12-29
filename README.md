# cypress-ui-automation
Automate UI testing Cypress

## Cypress compared to Selenium

Cypress is a compelte framework, whereas Selenium is a library. Cypress being JS based, runs directly in the browser and does not require web drivers, hence it is very fast. On the cons side, Cypress code works in async mode (more on that later), hence code needs to be written tht way. It does not support multiple domains/tabs, and not good with iFrames. 

## Project setup

```
npm install
npm start # start the web app to be tested
npm install cypress --save-dev # one time Cypress install
npx cypress open # opens console where you can select e2e and browser to run suite
```

Above command opens opens cypress console, and if when run for the first time on a project, creates config files in the project like cypress.config.ts, a cypress folder with e2e.ts, commands.ts and example.json. Replace cypress.config.ts with js file as mentioned in this url: https://docs.cypress.io/guides/references/configuration. Other two ts files are also renamed to js.

## Cypress folder structure and important files

cypress/support/e2e.js is the first file that gets executed by Cypress. Here you import and invoke command.ts/js, download custom packages etc.

cypress/support/command.js is where you keep custom or common commands that you want to share with multiple test files. eg. login command. In our project, we have a command to open the hope page ('/'). 

cypress/fixtures/ folder is used to keep json files with mock responses in case you want to intercept backend calls and mock their responses.

cypress/e2e/: This is the folder where we create our own tests.

cypress.config.js: present at root, this file has the main configuration for Cypress framework like the url of the application to open, spec files to run, which ones to exclude, etc.

## Writing test cases

See **firstTest.spec.js** on how to access various DOM elements by id, tag, class, class and value, attribute name, attribute name and value, etc. See various comments in the file to explain what we are trying to achieve.  

Cypress works in **async** mode. See the test case 'then and wrap methods'. If you are to capture some dom elemnts to further perform actions on it, or assert values etc, you cannot simply assign the values you would with Selenium (as shown in commented code). Once the elements are captured as shown in the code, they behave like jQuery elements. Hence use Chai framework way to assert values on them. You can use cy.wrap() function to convert those back into Cypress elements.

'invoke' command test case shows how to use 'invoke' command. It is a very usefull command which can be used for fetching values for given attributes, which can then be asserted.

'dilog box' test case shows how to deal with dialoge boxes like alerts. These are not part of DOM, and are part of window object instead, hence cypress provides a way to access them through windows object as shown in the test case.

Next, see testWithPageObjects.spec.js on how we can organise our test cases in a more readable way using 'Page Object' design pattern. This allows you write code in reusable manner. See how reusable functions are created under the support folder, and then used in the test case. Also see how cy.openHomePage() method is called as defined in cypress/support/command.js (command file explained above)

## Working with APIs

Not covered in this POC project, but using Cypress, you can interact with backend APIs as well. You can invoke the backend apis directly (using **cy.request()**) and inspect the response. 

You can also intercept backend calls with UI automation tests. Call **cy.intercept()** before performing operation (like button click) which makes backend call. With this intercept, you can verify the backend response, or even change the request and response from the API.

## Some more features

### npm scripts and cypress cli

Instead of npx cypress open, you can do **npx cypress run** to run all test cases headlessly. This is the command that you would also configure in your CI testing pipleines.This also creates a video folder with video recording of all UI actions performed. If you dont want these recordings to be created, you can switch the feature off in main cypress config file.

To run the test cases against a browser, you may do as 'npx cypress run --browser chrome'.

To run a specific test file, do as 'npx cypress run --spec "<test-file.js>"

You may configure npx cypress commands as npm script by adding them under scripts section of package.json

### env properties

You can give env variables in Cypress.config.js but its not a good place for passwords. You can refer to these passwords in spec.js code as Cypress.env("<envVarName>")

You can also specify your env variables (esp passwords) in a cypress.env.json file, which can then be added to gitignore and not checked into code repo.

You can also pass env properties from command line using --env. eg 'npx cypress run --env dbPassword=value'.

### test reports

You can generate test reports by using 'Mochawesome reporters'.

https://docs.cypress.io/guides/tooling/reporters#Examples

