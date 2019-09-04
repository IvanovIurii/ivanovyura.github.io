---
layout: post
title: RabbitMQ and Kombu message lib
author: Iurii Ivanov
tags: [rabbitmq, kombu]
---

Here is RabbitMQ installation in Docker and simple use case with Kombu lib.

I dont like installing a lot of work related soft to my laptop, even in work laptop. I think its kind of messy, it is better to have everything in isolated environment. ANd containerization really helps in this. Thats why I most of the time use Docker for services like Postgres or Redis. It is eassy to brake something in my local, so containers help me to stay clean.

Yeah, and RabbitMQ is not an exception. Of course we need to tune some things in container after it is up and running, but it is only one time (if we use `Volume`, just should be `-v` command during its run, or smth).

So, I suppose, that docker is installed on your laptop, bro...

# STEPS

```bash
docker run -d -p 5672:5672 --name some-rabbit rabbitmq:3
```
It is detached and run on your 5672 port. `--name` allows to setup the name of a container and access it by its.

After that its can be available by standart port like 0.0.0.0:5672.
So, perform the command and make sure:
```bash
docker port some-rabbit

> 5672/tcp -> 0.0.0.0:5672
```

There is at least 2 ways to publish massage to the queue.

First one is to use manage-plugin: `rabbitmqadmin`. (NOTE: it is not the same as `rabbitmqctl`).
But first of all this plugin should be activated.

- you can use another Docker image from HUB, with pre-installed and enabled `rabbitmqadmin`: `rabbitmq:3-management`.

But I will just do it on my own.

For this we need to go inside the container.

```bash
docker exec -it some-rabbit bash
```

And after we need to enable the plugin.

```bash
rabbitmq-plugins enable rabbitmq_management
```

Probably you will need to go to the place where this plugin is located and tun it with python and arguments you need.
Oh, shit ... there is no Python in container. So lets install it.

```bash
apt-get update && upt-get install python3.6
```

And check that everything is ok:

```bash
find / -name rabbitmqadmin
> /var/lib/rabbitmq/mnesia/rabbit@my-rabbit-plugins-expand/rabbitmq_management-3.7.17/priv/www/cli

cd /var/lib/rabbitmq/mnesia/rabbit@my-rabbit-plugins-expand/rabbitmq_management-3.7.17/priv/www/cli

python3.6 rabbitmqadmin list exchanges

+----------------------------------+---------+
|               name               |  type   |
+----------------------------------+---------+
|                                  | direct  |
| amq.direct                       | direct  |
| amq.fanout                       | fanout  |
| amq.headers                      | headers |
| amq.match                        | headers |
| amq.rabbitmq.trace               | topic   |
| amq.topic                        | topic   |
| applications_la_uploads_pipeline | direct  |
+----------------------------------+---------+
```

You should see the list of ecxhanges.
Basically EXCHANGE is a kind of controller. Actually we can not send messages directly to Queue, we send the to an exchange.
It gets messages from Producer and then decides, to which queue to push the message (or multiple queues).

There are rulles how to do it, based on Excnage type. **TBD**.
See this nice article for details: https://www.rabbitmq.com/tutorials/tutorial-three-python.html

***BTW:*** list of exchanges can be get by `rabbitmqctl`:

```bash
rabbitmqctl list_exchanges
```

So, how can we publish the message to the Queue?
