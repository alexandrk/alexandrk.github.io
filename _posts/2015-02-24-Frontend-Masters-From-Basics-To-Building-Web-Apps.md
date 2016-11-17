---
layout: post
title: "Frontend Masters From Basics To Building Web Apps"
tags:
  - javascript
  - jquery
  - tips-and-tricks
published: true
---

Using 'rel' attribute as a hook for javascript jQuery lookups.
  $("[rel='js-controls'] > [rel*='js-register']") // gets a child element of js-controls with js-register in it's 'rel' attr

Use word 'debugger' in the javascript code to insert a breakpoint from within the text editor (works in chrome)
  function showName(name){
    debugger; //will pause execution when the interpreter hits this line
    console.log(name)
  }
  showName('Bob');

ES6: Object.is()
