---
category: Book-Summary
date: 2020-12-31
layout: post
title: Book-Summary - Debugging - The 9 Indispensable Rules for Finding Even the Most
  Elusive Software and Hardware Problems
updated: 2024-04-17
---

- Author: **David J. Agans**
- GoodReads: [Debugging - The 9 Indispensable Rules for Finding Even the Most Elusive Software and Hardware Problems](https://www.goodreads.com/book/show/3938178-debugging)


- First step of debugging is "UNDERSTAND THE SYSTEM". Understanding does not mean just knowing the different terms of systems and different components of a system, but rather knowing the working knowledge of the system. One should be able to answer the following questions -
	- What is the work of the system? What is it supposed to to do?
	- What is the environment of the system? How does the system interact with the environment?
	- What are the different components of the system? What are the critical components?
	- What is the work of each component in the system?
	- How does each component do its work?
	- How does the system as a whole work?
	- How does one know things are working as it should be?
	- How does the external components affect the internal components? Or how does the input affect the output?
	- If component x fails, how does it affect the whole system and output?
- For "Understanding the system", one needs to do following things -
	- read the code of the application
	- read the design documents
	- read the code reviews
	- read the manuals
	- ask questions to the person who knows about it
	- explain what has been understood
	- know the fundamentals that was used by this system.
	- Treat the system as a black-box and pull the leavers and see what happens.
- When something happens, look it up and understand why that happened. Do not guess.
- When a failure happens, try to repeat the events to reproduce the failure. During this process, log every event or steps or any observation you are seeing. Some failures are intermittent. So some execution will not result in failure and some will. By documenting, we can compare the notes with non failure runs and the failure runs. If the logs or notes are detailed enough, we can see the in logs of the failure run that there will be some missing or extra steps or observations. This would help in further investigation.
- When we say document everything. Question is "what is everything?".  To know what is everything - we need to know the system and its environment , i.e we need to "UNDERSTAND THE SYSTEM".  To understand a software system, we need to read the code and infer the design from it. The other way is to run the system and observe, based on this run make assumptions of how system works.
- Running the steps again and again manually will be painful, so better to automate this step. It might fail intermittently but that would save a lot of time during debugging too.
- Sometimes the failure will not happen from the steps we followed, so we may have to change the steps. Be cautious not to change too many things. Its always better to do a single change at a time.
- Any system that is running, has two parts - system itself and the environment in which the system is running. So any mistake that led to the error/failure will have 3 possible cases - 
	- Something wrong in the system (Coding mistake led to an exception due to which website is not loading) 
	- Something wrong done by the environment (there is no internet connection so website is not loading). 
	- combination of both (Website was overrun by the resources due to too many connections - may be intentional/may be not).
- Any failure of a system has a reason. It may be covered in the randomness of the environment and the system but there is something which broke which resulted in that failure.
- During debugging, we need to try to find the cause (x). We know the effect (y) - failure/error (website is not loading). Based on the observation and understanding of the system, we will come up with N different causes. Then we start reasoning out why X1(it did not had internet connection failure as other websites was reachable) is not the cause or why X2 (its not connection overrun as at the time it had only say 45 open requests whereas it has limit of 100) is not the cause. If some causes look plausible, we should read about it and go deep in them. We might also add more possible causes as we understand more about the system and environment.
- One cannot say "I ran the system x times and failure did not happen even once so it is fixed". This is using statistics as a reason for the fix. Always remember "if one does not know what is x and y in the relation x(cause) led to y (failure)", the system is not fixed yet.
- This is an interesting problem - "A family complained their car fails to start based on the flavour of ice-cream they bought from the store". The first thought that comes to our mind is - this is ridiculous -  there is no relation between flavour of ice cream and working of a car.  Now lets hear the problem in more detail -  "On some evenings, family in their car - a model x, go to a near by local ice cream shop. The shop has Vanilla, Chocolate and Meeta Paan flavors.  Car does not give any problem on the days family choose Vanilla or Chocolate, but on the days they picked Meeta Paan flavor, car won't start. It needs lot of trials before it finally starts and even after starting it does make a noise while driving". Now immediately, our thought is what is the relation between Vanilla, Chocolate , Meeta paan with the starting of Car? Is the meeta paan too cold, which is making the car temperature too less due to which AC is consumed more and that is affecting the engine? Is the smell of the meeta paan doing something with the car engine? Or are they taking different route when they go for picking the meeta pan, or is the day they picked meeta pan is different from the day they picked other flavours?  If you observe, our attention is fixed on finding the cause in Ice cream flavours. So, we are trying hard to find the relation between ice cream flavour and the car engine where the failure happened.  Rather one should go in reverse direction - Why the car needed so many tries to start? Why was their noise when driving it? What all the possible ways that can cause it - example petrol is low or it is cold or car engine is heated up.  Now try to connect these with the ice cream flavours. On the day they pick meeta paan, is the petrol low - do they go a different route, do they have some other work added due to which they have to take a different route; Or is it cold  - do they pick meeta paan on the cold days?; Or is it hot - that is day is is hot on the days they pick meeta paan.  So the questioning should start from the failure and the system that failed not the environment.  The real reason was - "They go to icecream store on the days it is warmer. Both vanilla and chocolate are prepacked in the shop so it is quick, where as meeta paan had to be packaged after order is given. That usually takes some time. As it is a warm day, during the wait time of packaging, coolant gets evaporated in the engine. So when they finally try to start the car it wont." So moral is - "Start from the failure (car not starting) and the system (car), environment is just aiding the system for failure. So, find why the system as such failed then find the relation between environment and the failed use case."
- One of the best way to learn about a failure is by looking at how it failed. Sometimes it is too costly to repeat the failure.In such cases Logs and Metrics will help you understand how was the system during the event. First thing after the event is to collect the logs and metrics.
- Use divide and conquer approach.  In the system, identify a range where the bug might be. The point where it crashed is the starting point, from there till the beginning of the system is the end point of investigation.  Choose a half way and see if things look good. If things look good go towards crash. If things look bad go further away, that is next half. Do this until you find the exact issue point. Also during this search, we might find some small bugs. Fix them and restart the search, but do not get carried away and start fixing design and best practice issues.
- During debugging, we are in the race to find the bug. So during that time, we either try to fail the system from good state to reproduce the issue or correct the system from failed state to find a fix. To do that, we modify the system by overwriting the variables, adding extra logic, updating inputs, etc. All these things should be done in isolation and tested to see its affect. If the change is not giving any result, then it needs to be reverted back. Do single change at a time and revert it if it is having no affect.
- Keep an audit trail detailing everything - time of events, steps of the event, components in the event, how each of the components interact, what was changed and what was observed. This would help in reproducing the error, analyze the failure and find the solutions for it.
- During debugging, we make lot of assumptions. These assumptions should be documented. Always keep in mind, from time to time, these assumptions should be questioned - do they still hold. Otherwise there is a chance that it might lead to wrong results/conclusions.
- Apart from assumptions, there are basic fundamentals which we usually assume to be true. Again verify those basic fundamentals.
- It is never fixed until you know the root cause and prove it by removing the fix to reproduce it.
- When we get stuck, not knowing what is going on, it is important to get a fresh view. We can choose one of these or a combination of them - 
	1. Talk to Krishna about my thoughts on the issue (Rubber Duck) 
	2. Talk to experienced person who knows about the environment or used the product a lot. 
	3. Talk to an expert who knows about the subject.