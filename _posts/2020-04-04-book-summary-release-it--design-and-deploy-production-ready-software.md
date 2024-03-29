---
category: Book-Summary
date: 2020-04-04
layout: post
title: Book-Summary - Release It! Design and Deploy Production-Ready Software
updated: 2024-02-04
---

- Author: **Michael T. Nygard**
- GoodReads Link: [Release It!](https://www.goodreads.com/book/show/1069827.Release_It_)

As the name of the book implies, the main topic of this book is about how you will design your applications and services such that it can be deployed and maintained in a production environment. There are multiple factors which help for a good design
{: style="text-align: justify;"}
* The stress, impulses or component failures will affect the integration points of the application. These integration points will fail and this failure will spread to other parts of the application.
* Whenever you are connecting to remote applications or databases via sockets or RMI or any means we need to protect these connections with timeouts. These remote calls are unpredictable - it can fail with an error, it can take a lot of time to return or it can fail silently. So, better to protect them with timeouts.
* Use circuit breakers to protect from the impulses, stress. Make sure there is a way to know whether circuit breaker is activated - some kind of metric or alarm is needed.
* In web applications, use sessions judiciously. Each session resides in the memory and it will reside for long time even if it is not used.
* If you are expecting high demand for certain resources or functionality then protect it such that those demands are diverted to a separate resource thus protecting the other functionality and components from getting affected due to resource crunch.
* Always use connection pool to connect to a resource whether it is multiple instances of services or database.
* Use ORM to connect and operate to the database. Never directly run a direct SQL query from your application.
* Before releasing to production do a load testing. And remember your development environment and QA environment will never be able to match the scale of production. Rather than trying to match the scale of production, design your application code such that even in the heightened requests or stress, application should be able to transact.
* Slow responses from your application will lead to other problems like more traffic and customers will keep retrying and more resources are utilised leading to cascading failures.
* Fail fast is better than slow responses.
* For slow responses, reason could be memory leaks or resource contentions like DB pool is filled up or thread pool is filled up.
* Do not blindly put an SLA to your services. Measure it. Understand the SLA of your dependent services. Based on that derive your SLA. You cannot give an SLA which is better than your dependent service.
* Use bulkheads in case of failures, so that even if some components fail your product is still running and insulated from the failed components.
* Caching has limits. It increases your services response to certain extent after that it will eat your memory and thus leading to decrease in response. So use it carefully.
* Make sure you clean up your old logs. Either move to a different location but do not allow it fill up space.
* Clean up your old data. Maintain data hygiene.
* All these disk cleanup and application data clean up has to happen automatically via your application rather than human intervention.
* When you test, do not just go by your requirements. Go out of requirements when testing negative failure scenario.
* Try to use intelligent load balancers that consistently does health checks of the underlying systems and based on bad health stops sending requests to those instances.
* Try to provide an administrative CLI tool for every service for ops work.
* Set up alarms and monitors like for system health, requests received, response time, max threads, max connections. There should be dashboard to monitor these metrics and alarms to give real time picture of what is happening to your service or application. Logs are a great way to learn about what is happening but metrics & alarms give you high level picture of what is going on. Also have tools which will read your logs and alarms based on specific stack trace occurrence such as exceptions or faults being reported in logs.
* Releases should be done often and all the release activity should be automated - aim for continuous deployment.