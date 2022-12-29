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

## If setting up a project from scratch, configure Cypress on your app
```
npm install cypress --save-dev
npx cypress open 
```
Above command opens cypress and creates config files in the project like cypress.config.ts, a cypress folder with e2e.ts, commands.ts and example.json. Replace cypress.config.ts with js file as mentioned in this url: https://docs.cypress.io/guides/references/configuration. Other two ts files are also renamed to js.

## Cypress folder structure and important files

cypress/support/e2e.js is the first file that gets executed by Cypress. Here you import and invoke command.ts/js, download custom packages etc.

cypress/support/command.js is where you keep custom or common commands that you want to share with multiple test files. eg. login command. In our project, we have a command to open the hope page ('/'). 

cypress/fixtures/ folder is used to keep json files with mock responses in case you want to intercept backend calls and mock their responses.

cypress/e2e/: This is the folder where we create our own tests.

cypress.config.js: present at root, this file has the main configuration for Cypress framework like the url of the application to open, spec files to run, which ones to exclude, etc.

## Writing test cases

See firstTest.spec.js on how to access various DOM elements by id, tag, class, class and value, attribute name, attribute name and value, etc. See various comments in the file to explain what we are trying to achieve.  

Cypress works in **async** mode. See the test case 'then and wrap methods'. If you are to capture some dom elemnts to further perform actions on it, or assert values etc, you cannot simply assign the values you would with Selenium (as shown in commented code). Once the elements are captured as shown in the code, they behave like jQuery elements. Hence use Chai framework way to assert values on them. You can use cy.wrap() function to convert those back into Cypress elements.
