---
layout: post
title: Technical Specification. WTF?!
author: Iurii Ivanov
tags: [specification, spec, requirements, ticket, task, JIRA, process, agile]
---

How to deal with shitty specification? What if there is no tickets/tasks or they poorly specified?

NOTE: this article is not finished

"Knowing something incomplete is dangerous than not knowing it at all" (c)

At first, what is a specification?

In my opinion there are two types of specifications:
- a functional, which describes what the product should do, its features. There is no details "how" it should work.    
- a technical specification describes the "how" of the product, its data structures, DB schema, endpoints, payloads, blueprints, namespaces and so on.
Tickets or tasks for developers are based exactly on tech spec.

Soooo, I am more interested in tech specification, because, suddenly, I am a developer...

Why it matters? Because it relates to the code that’s going to be written, to decisions that have to be made. 
It is simple, if decisions are not made, you can’t write the code. 
The specification has to document any decision in details (trust me, it will save your life one day).
Plus detailed specification means detailed tasks. Which is REALLY good thing in a software developer's life.

Some developers may think, they are cool if they can work without specification or a ticket. Unfortunately, they are not. 
They are unproductive and incompetent. They write bad code.
You may ask, why? Well, it is all about communications. With a good specification you save time. 
Everybody on the team can just read the spec or a well detailed ticket. 
You, as a developer, do not have to explain people in the team another 1000 time how the programm works and waste time.
QA can read it, so they know what to expect and how to test. 

When you don’t have a spec, communications still happen, because it has to (unless you can read people's minds), but it happens ad hoc, irrational, with lost of time. 
You have to interrupt PM and ask another stupid question, 
eventually they will think that you are not good enough to work here, or you are a Junior developer, because you ask so many stupid questions...
You will not get a raise, or bonus, and you little chia-hua will suffer without a new sweater in a cold winter.

---

So, check this out, here some thoughts about (sorry for chaos, future me):

0. Imagine building a house without a blueprint. Or with unclear blueprint. Crazy, right? 
If you just a builder, should you create a blueprint on your own? I think the answer is obvious. 
This goes the same with a software development. How to start? What to implement? What to expect? 
The same thing with shitty requirements or cpecification.
1. Most of the time working on something big you can not assume what has to be done, because you do not see a big picture. 
Assumption can be incorrect (and actually allways is contr-prodactive) and then the whole thing you are working on will be done incorrectly. 
Therefore everything should be documented well (tickets or in a technical specification). 
Note, also, those artefacts should be up to date. Ask your manager aka Team Lead or Product Team about it.
2. If specification is shitty and there is not enough information in the ticket (or there are no tickets at all),
you will have to spend time for specifying requirements and things, which can be not so important in current iteration.
3. Of course, if you are a trusted senior developer or an engineering manager in a small company, it is kind of your responsibility too,
at least to help Product Team, manage the work or put some tech notes. But if not ...
4. ... it is not your responsibility to define what should be built or what requires.
Product Manager (or Owner) or Lead knows better, he/she gets money for this job. You are payed for writing code and solving problems based on a specification they provide.
Their job it is to make clear requirements. They have to tell you the “what to build”, plus some additional details, 
like required endpoints, POST/PATCH/PUT/GET payloads, etc. You will have to figure out "how". 
5. If requirements are still bad, your team can go for Agile with sprints/iterations. 
Every new sprint there will be planning, where you can ask your questions and therefore specify and clear all the requirements. 
And after the sprint is done, you get MVP, the piece of completed work with a feedback from customer (or external users).
6. Plus, it is important that every ticket/task or story should have Acceptance Criteria with a binary answer (True or False). 
It there is not enough details, then this is the fail of a team (or who was involved) during planning. 
Tickets which are not ready for development (unclear or do not have all details) should not be taken for work.

---

So, what if there is no specification or other required artefacts, like tickets in JIRA, for example? 
Or how to behave if nobody gives a shit?

If this situation happened to you, you have two ways, either you create tech specs and tickets on your own and then ask approve of your manager and PM,
or you stay cool and calm, but keep asking/pushing required docs and do not start working until everything is clarified and clear. And only then start working. 

You have to understand one thing, buddy, messages in Slack are not documentation.
Channel can be archived, data can be lost, messages can be edited, so the perspective will be changed, and also the whole meaning.
And you, my friend, will be the only one who fucked up. Not your manager, not PM, you. 
It is sad, but the truth is simple, you always have to have the documents with history of all the changes to save your ass in any possible cases and situations. 
And in this case a specification (approved specification) is a kind of self-defense document, which will save you a lot of nerves. 

