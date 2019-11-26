---
layout: post
title: Test Coverage
author: Iurii Ivanov
tags: [coverage, tdd, tests]
---

Does a test coverage really matters? What is the best number of coverage?

Recently in the interview I was asked the question, if this is really important to reach 100% coverage.

Well ...

I think it is an open discussion, but here are my notes about what I think about this topic.

- You can write shitty code with 100 coverage, and it will tell you nothing, if code smells or bad.
- The coverage does not say anything, and it depends on many factors, which only the developer of tested code can know.
- Of course it is better have unit-tests than not to.
- But anyway metrics do not make the code good. It is easy to reach high coverage with low quality tests, so its is better to write good tests, instead of thinking about metrics.
- We still can cover each path, but if the code itself does not do what it should do, it is useless.
- TDD can help, but it is not a silver bullet.
- We always should focus more on things if we write tests right, if the coverage is high, but there are bugs in production, your tests are shit.
- If small changes in the code make you to do excessive changes in tests, you do something wrong.
- And the last one, test coverage is a guideline, not the rule, it just helps us to find untested code.
