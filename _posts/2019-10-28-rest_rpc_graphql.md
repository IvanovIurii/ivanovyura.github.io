---
layout: post
title: REST vs RPC vs GrapQL
author: Iurii Ivanov
tags: [postgres, lock]
---

Notes about REST(ful), (g)RPC and GrapQL.

The first thing, REST should be stateless (the opposite is stateful).
If you have a session, the service can not be considered as RESTful.

Stateless - this means *no client session on the server*. So for the service it does not matter, who sends requests. And the service does not save any state about client.
This means that service can serve a client any time and each HTTP request is done in an isolation. And the server never assumes anything from previous requests.
And if we need to save the state we save them on the client as COOKIES files. All the information which needed to communicate with the server is fulfilled during the request.
Between the requests the server even does not know that user exists.

If you look to the REST abbreviation, ST there is for State Transfer, so instead of saving the session, you just transfer the state. In other words, if client makes request, he SHOULD include all state that server may need to process the request.

But what the is REST itself?

What is RESTful?

But if you have an action, a verb in your URL - it is some kind of indication about RPC. It looks like a function call with parameters, but from URL. 
Plus the codes you return are custom codes, not HTTP ones.

In REST every action is represented by HTTP verbs: POST to create, PUT/PATCH to update, GET to fetch data.

Plus the URLs are different. If for REST it is a resource, for RPC you have a function name.

For example, create a resource:

RPC: `POST /resources/createResource`
REST: `POST /resources`

Look at REST POST, to fetch resources the URL will be the same.

But for getting resource REST URL is the same as for creation one, but for RPC it is different:

RPC: `GET /resources/getResources`
REST: `GET /resources`

*TBD:* Python gRPC, GraphQL and REST example/comparison



