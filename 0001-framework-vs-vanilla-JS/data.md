# Frameworks vs Vanilla JS

## Table of Contents

1. [Introduction](#introduction)
2. [Vanilla JS](#vanilla-js)
3. [JavaScript Frameworks](#javascript-frameworks)
4. [Comparison](#comparison-between-vanilla-js-and-frameworks)
   - Vanilla JS
     - [Advantages](#advantages-of-vanilla-js)
     - [Disadvantages](#disadvantages-of-vanilla-js)
   - Frameworks
     - [Advantages](#advantages-of-frameworks)
     - [Disadvantages](#disadvantages-of-frameworks)
5. [Conclusion](#conclusion)

## Introduction

JavaScript is one of the most popular programming languages in the world and is used in virtually every area of software development. When it comes to developing web applications, there are two main approaches that developers can use: Vanilla JavaScript and JavaScript frameworks, such as React, Vue, and Angular.

In this article, we will compare the advantages and disadvantages of both approaches, examining code examples for each of them.

## Vanilla JS

The term "vanilla" is used to describe "pure" JavaScript, without the use of additional libraries or frameworks. Vanilla JavaScript is the oldest method of developing web applications, but it is still widely used today.

Here is an example of vanilla JavaScript code that creates a button and adds a click event using `addEventListener`:

```javascript
const myButton = document.createElement("button");
myButton.textContent = "Click me";

myButton.addEventListener("click", () => {
  console.log("Button clicked");
});

document.body.appendChild(myButton);
```

## JavaScript Frameworks

JavaScript frameworks, on the other hand, are libraries of pre-written code that help developers to create web applications more quickly and efficiently. They typically come with a set of pre-built components and a defined architecture, making it easier to build complex applications.

Here is an example of creating a button component in React:

```javascript
import React from "react";

function MyButtonComponent() {
  const handleClick = () => {
    console.log("Button clicked");
  };

  return <button onClick={handleClick}>Click me</button>;
}

export default MyButtonComponent;
```

And here is an example of creating the same button component in Angular:

```javascript
import { Component } from "@angular/core";

@Component({
  selector: "app-my-button",
  template: '<button (click)="handleClick()">Click me</button>',
})
export class MyButtonComponent {
  handleClick() {
    console.log("Button clicked");
  }
}
```

In both examples, the button component is created using a specific framework's syntax. In React, the component is created using a function and JSX syntax, while in Angular, the component is created using a template and a `(click)` event. The `MyButtonComponent` component is created using a TypeScript class decorated with a `@Component` decorator.

## Comparison between Vanilla JS and Frameworks

Now that we've looked at code examples for both approaches, let's compare their advantages and disadvantages.

### Advantages of Vanilla JS:

- Total control over the code and application functionality.
- No dependency on external libraries or frameworks, making the application lighter.
- Lower learning curve, as only basic JavaScript knowledge is needed.

### Disadvantages of Vanilla JS:

- More time and effort to create more complex functionality.
- Possibility of duplicated or inconsistent code, since everything needs to be built from scratch.
- Can be difficult to maintain the application as it grows, especially without a defined architecture pattern.

### Advantages of Frameworks:

- Pre-built tools and resources to simplify development.
- Defined architecture patterns, making maintenance easier.
- Faster development of more complex functionality.

### Disadvantages of Frameworks:

- Dependency on external libraries, making the application heavier.
- Higher learning curve, especially for beginners to programming.
- Limitations in customization, as frameworks have their own rules and patterns that need to be followed.

## Conclusion

Ultimately, the decision to use Vanilla JavaScript or a JavaScript framework will depend on the needs and goals of the application. Both approaches have their advantages and disadvantages, and it is up to developers to decide which one is most suitable for the project at hand.
