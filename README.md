# Modules

## Overview

In this lesson we're going to go into modules and how to create and load our own. You'll recognise the syntax from our previous module!

## Objectives

- Describe the setter/getter syntax
- Create a module using a setter
- Fetch the module using a getter
- Import a submodule

## What is a module?

Think of a module as a container for specific parts of your application. Each module should provide a set of functionality (for instance you might have a "login" module that handles everything to do with user authentication and logging the user in). Modules can contain views, components, routes, etc, but that's not important right now (you'll learn all about these very shortly).
 
It's important that we have at least one module - otherwise we couldn't do anything!

Why do we split our application into modules? Modules allow us to separate our application into logical chunks (much like MVC/MVVM that we touched on earlier) that can be reused. It's recommended that you create modules for 

- Each feature in your application
- Each reusable component in your application
- An application module that our application uses as a base

Angular comes with a lot of plugins available on the web. Each one of these will be it's own module - meaning that you can just slot it into your application and not have to worry about it interfering with any other aspects of your app!

## Setter/getter syntax

### Modules

Angular is magical, but it isn't *that* magical. We need to tell Angular about all of our modules, controllers, etc, when we create them - otherwise, it would have absolutely no idea what is used for what.

The way we tell Angular about our modules is:

```js
angular
  .module('exampleModule', [])
```

The `angular` object we're using there is the Angular core. This is the core API - this allows us to create and load modules (using `angular.module`).

You might be wondering why we have a second parameter with an empty array in it. This is very important - it tells Angular that we need to *create* a new module. If we omit the second parameter, it would tell Angular that we'd like to *retrieve* a module with the name `exampleModule`.

The empty array is very important for our module too. This is an array of modules that our module depends on. If you were to download a plugin online, you can't just drop the code in and expect Angular to know that it needs to be a part of your application. This is where this array comes in - you can tell Angular that your module depends on the plugin's module that you just downloaded, and it will include it into your application and allow you to use it - amazing!

The number of parameters is true for everything we set/get in Angular. If we only have one parameter, we are telling Angular to `get`. If we have two parameters, we are telling Angular to `set`.


If we were to be doing routing in our app, we'd include Angular's `ngRoute` module. First of all, we'd download the files from the web and make sure we include them via script tags in our HTML file. Then, we'd tell Angular that our module relies on `ngRoute` - otherwise Angular wouldn't know that we actually would like to use the module, even though it exists:

```js
angular
  .module('exampleModule', ['ngRoute'])
```

Simple! That is the `setter` syntax for modules.

### Controllers, directives and everything else
 
Now, we can't just call `angular.controller` for our controllers. Controllers, directives, services, etc, must be attached to our modules. This is done as so:

```js
function ExampleController() {
}

// We assume that the module "exampleModule" has already been created
angular
  .module('exampleModule') // fetch the module
  .controller('ExampleController', ExampleController); // create the controller
  
// both of these do exactly the same thing
  
var module = angular.module('exampleModule'); // fetch the module
module.controller('ExampleController', ExampleController); // create the controller
```

This is similar to our module setter/getter. Much like `angular` having `angular.module`, all of our modules have the method `.controller`, allowing us to get (or set) the controller.

Why are we fetching the module? Well, we could possibly be in a completely different file. How would Angular know what module our controller belongs to unless we tell it?

We can then retrieve the controller we've created by omitting the second paramater.

```js
// We assume that the module "exampleModule" has already been created
angular
  .module('exampleModule') // fetch the module
  .controller('ExampleController'); // fetch the controller
  
// both of these do exactly the same thing
  
var module = angular.module('exampleModule'); // fetch the module
module.controller('ExampleController'); // fetch the controller
```

## Using our module in our application

Now we've got Angular aware of our module, we need to tell it where our module actually needs to be used.

### ng-app

We can do this via the `ng-app` HTML attribute Angular makes available for us. All we need to do is find the HTML element where we want Angular to start rendering, and add `ng-app="exampleModule`.

```html
<div class="app" ng-app="exampleModule">
</div>
```

## Resources

- [Todd Motto's guide for Angular Modules, Setters & Getters](https://toddmotto.com/angular-modules-setters-getters/)
- [Angular Documentation for Modules](https://docs.angularjs.org/guide/module)