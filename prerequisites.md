
# Prerequisites

## Node

You'll need to have Node.js 6+ (and npm 5.2+) installed on your development machine in order to support the tooling that's typically used for React, Angular, and Vue development.

You can use a package manager (like [Chocolately](https://chocolatey.org/) on Windows or [Homebrew](https://brew.sh/) on macOS) to install Node.js, or you can use the official installer available at [https://nodejs.org/en/](https://nodejs.org/en/).

## Angular and Vue CLIs

In this workshop, we'll be using [Create React App](https://github.com/facebook/create-react-app), the [Angular CLI](https://cli.angular.io/), and the [Vue CLI](https://cli.vuejs.org/). Create React App doesn't require any installation, but both the Angular and Vue CLIs need to be installed globally by running the following commands:

```
npm install -g @angular/cli
npm install -g @vue/cli
```

## Caching NPM Packages

This step is optional, but if you have the time ahead of attending the workshop, you can run the following CLI commands to create your first React, Angular, and Vue projects.

```
npx create-react-app my-react-app
ng new my-angular-app
vue create my-vue-app
```

Doing this will build up your local cache of the necessary npm packages (~/.npm on Linux/OS X and %AppData%/npm-cache on Windows), which will speed up the project creation process (packages can be loaded locally from your cache instead of having to be downloaded).

## Browser DevTools

Each of the frameworks has a browser extension available that extends the browser's built-in devtools.

* [react-devtools](https://github.com/facebook/react-devtools)
* [Angular Augury](https://augury.angular.io/)
* [vue-devtools](https://github.com/vuejs/vue-devtools)

## Editor

I'll be using [Visual Studio Code](https://code.visualstudio.com/), but you're welcome to use any code editor or IDE that suits your needs.

If you're using Visual Studio Code, you can optionally install these extensions:

* [Vetur](https://marketplace.visualstudio.com/items?itemName=octref.vetur)
* [Angular Language Service](https://marketplace.visualstudio.com/items?itemName=Angular.ng-template)
* [VS Live Share](https://marketplace.visualstudio.com/items?itemName=MS-vsliveshare.vsliveshare)

## Git Tooling (Optional)

Having access to Git tooling isn't required in this workshop, but you might find it helpful (just in case you need to quickly catch up with the group).

I'll be using Git from the command line, but you're welcome to also use an application like [GitHub Desktop](https://desktop.github.com/) or Visual Studio.
