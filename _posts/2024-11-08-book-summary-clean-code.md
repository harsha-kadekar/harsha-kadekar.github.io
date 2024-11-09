---
category: Book-Summary
date: 2024-11-08
layout: post
title: Book-Summary - Clean Code
updated: 2024-11-08
---

- Author: **Robert C. Martin**
- GoodReads: [Clean Code - A handbook of agile software craftsmanship](https://www.goodreads.com/book/show/3735293-clean-code)

[Clean Code](https://www.goodreads.com/book/show/3735293-clean-code) provides an opinionated view of some of the best practices to be followed in Java programming. Many of them can be applied to any of the languages. Here are some of the important points, I liked about
- Make the variable names searchable across the project
- Do not add type information to the variable name, function name or class name
- If a function needs more than 2 parameters think of creating an object and passing it around.
- Try to have shorter function. It is doing one thing at a time. Have the top down function expansion.
- A function needs to do only one thing at a time. Everything it is doing should be conveyed by the function name  
- Leave comment to explain a decision. Leave comment to emphasize of something that looks simple or normal  but has big effect.
- Mandating comment on every function, variables, return variable, function arguments, classes is waste. Write code which are self explanatory  
- Law of Demeter - Do not call functions of the object  returned by one of your allowed function call  
	- Do not return null
	- Do not pass null  
- Test code is just as important as the production code. Do not treat your unit, integ and canary tests as second class citizens  
- Test only one concept in single test function   
- Testing should follow FIRST principle 
	- It should be fast
	- It should be Isolated/Independent
	- It should be repeatable
	- It should be self - validating
	- It should be thorough
- Simple design has 4 rules
	- Runs all the tests  
	- Contains no duplication  
	- Expresses the intent of the programmer   
	- Minimizes the number of classes and methods 
- In a multi threaded application, spurious test case failures needs to be investigated and should not just treat it as one off failures
- Run with more threads than the processor core to understand the issues with respect to task swapping  
- First implement the functionality. It might be not return clean but make sure to have tests covering it. Then start cleaning that code, refactoring it with small changes until desired cleanliness is achieved.