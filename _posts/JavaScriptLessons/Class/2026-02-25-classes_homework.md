---
layout: post
codemirror: true
microblog: true
title: Classes Homework
description: Practice using JavaScript classes by creating a class with two methods.
permalink: /js/classes/homework
author: Aashi
---

## Class Practice Challenge

Create a simple JavaScript class that has **two different methods**. Instantiate the class and call both methods so you can see them run in the console.

{% capture challenge0 %}
Define a class with at least two methods and use them from an instance.
{% endcapture %}

{% capture code0 %}
// start your class definition and method calls here
class MyClass {
    constructor(name) {
        this.name = name;
    }

    greet() {
        console.log(`Hello, my name is ${this.name}`);
    }

    farewell() {
        console.log(`Goodbye from ${this.name}`);
    }
}

const obj = new MyClass("Test");
obj.greet();
obj.farewell();
{% endcapture %}

{% capture source0 %}
```javascript
%%js
// CODE_RUNNER: Homework challenge – create a class and add two methods, then invoke them.

class MyClass {
    constructor(name) {
        this.name = name;
    }

    greet() {
        console.log(`Hello, my name is ${this.name}`);
    }

    farewell() {
        console.log(`Goodbye from ${this.name}`);
    }
}

const obj = new MyClass("Test");
obj.greet();
obj.farewell();
```
{% endcapture %}

{% include code-runner.html
   runner_id="js-classes-0"
   language="javascript"
   challenge=challenge0
   code=code0
   source=source0
%}
