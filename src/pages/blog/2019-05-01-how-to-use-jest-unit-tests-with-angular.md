---
templateKey: blog-post
title: How to use Jest unit tests with Angular
date: 2018-04-18T17:41:24.441Z
description: >-
  The Jest unit test framework is a relatively new unit testing tool built by
  Facebook, it is widely used for testing ReactJS projects. Studies shows that
  Jest is much faster than other unit test frameworks for JavaScript, since it’s
  using a custom built JavaScript engine instead of running the tests in a full
  blown browser.
featuredpost: true
featuredimage: /img/b3a4e-18iiqp3olqundv92tekcmaw2x.jpeg
tags:
  - Angular
  - JavaScript
  - Jest
  - Typescript
  - Unit Testing
---
The question is can it also be used for unit tests in an Angular project? \
The answer is **yes**!

## Setup the Angular project

So let’s get started, first you need an Angular project that you want to create and run the unit tests for. In this guide we will create the Jest unit tests for the [Angular’s Tutorial: Tour of Heroes](https://angular.io/tutorial).

If you want to follow along this guide interactively, you can download the starting point from here: <https://angular.io/generated/zips/toh-pt6/toh-pt6.zip>

Unzip it in some folder and run npm install in the folder to get all npm dependencies that you need.

## Running the tests with Karma

The project is already shipped with unit tests using [Karma](https://karma-runner.github.io/). Let’s see if they are working before we convert the project to Jest.

So I started up the tests with command, 

```
npm run test
```

and noticed that 7 of 8 tests failed. So I had to fix them first before I could even start doing the examples for this story.

[You can click here if you are interested in what I fixed in the Karma tests.](https://github.com/nerdic-coder/jest-angular-demo/commit/19589b43272b0013db49bcf66d5e4496120bfcd7?diff=unified)

## Convert the unit test framework to Jest

Now when that is out of the way, we can start the conversion to Jest, start by installing the Jest development dependencies with the command,

```
npm install --save-dev jest jest-preset-angular
```

In src directory create '_setupJest.ts'_ file with following contents,

```
import 'jest-preset-angular';import './jestGlobalMocks'; // browser mocks globally available for every test
```

also create a file '_jestGlobalMocks.ts'_ in the '_src'_ folder with the following content

<https://gist.github.com/nerdic-coder/ab1738348f762fd8e2bb263f5fdd4ce2>

and include this in your '_package.json',_

```
"jest": {  "preset": "jest-preset-angular",  "setupTestFrameworkScriptFile": "<rootDir>/src/setupJest.ts"}
```

You also need to update the scripts part of the '_package.json'_ replacing the old test script with the following,

```
"test": "jest","test:watch": "jest --watch"
```

Let’s run the tests now again with Jest in place with command, 

```
npm run test
```

and for me it all turned green on the first try, very surprising but great!

[Click here to see the commit changes I made to configure Jest for Angular.](https://github.com/nerdic-coder/jest-angular-demo/commit/650219083cd62c3fc91b00f78c0ce275409863f4)

Check the whole demo project here on GitHub: <https://github.com/nerdic-coder/jest-angular-demo>

## Sources

Here is a few places where I found the information about using Jest with Angular.

Jest website: <https://facebook.github.io/jest/>

Xfive: <https://www.xfive.co/blog/testing-angular-faster-jest/>

Jest-preset-angular on npm: <https://www.npmjs.com/package/jest-preset-angular>
