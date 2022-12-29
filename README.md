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

## If setting up a project from scratch, you would do following
```
npm install cypress --save-dev
npx cypress open 
```
Above command opens cypress and help create config files in the project like cypress.config.ts, e2e.ts, commands.ts and example.json. Replace cypress.config.ts with js file as mentioned in this url: https://docs.cypress.io/guides/references/configuration. Other two ts files are also renamed to js.