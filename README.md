# cypress-ui-automation
Automate UI testing Cypress

## Cypress compared to Selenium

Cypress is a compelte framework, whereas Selenium is a library. Cypress being JS based, runs directly in the browser and does not require web drivers, hence it is very fast. On the cons side, Cypress code works in async mode (more on that later), hence code needs to be written tht way. It does not support multiple domains/tabs, and not good with iFrames. 

## Project setup

```
npm install
npm start # start the app

```

## If setting up a project from scratch, you would do following
```
npm install cypress --save-dev
npx cypress open # opens cypress and gives you config for cypress.config.ts (already added in this project)
``