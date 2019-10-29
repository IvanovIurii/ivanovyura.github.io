---
layout: post
title: Multiple Consumers to listen each its own queue
author: Iurii Ivanov
tags: [python, celery, consumer, bootstep]
---

Here is an interesting case I faced during assigning multiple Celery Consumers to different queues.

Only code for now ...

```python
from celery import bootsteps, Celery
from kombu import Queue, Exchange

RABBIT_BROKER = 'amqp://guest:guest@localhost:5672/'
CELERY_TASK_QUEUE_NAME = 'task_queue'

celery = Celery(
    'test_app',
    broker=RABBIT_BROKER,
)

celery.conf.task_default_queue = CELERY_TASK_QUEUE_NAME


@celery.task
def do_something():
    print('I am doing something!')


@celery.task
def do_something_else():
    print('I am doing something else!')


class Consumer(bootsteps.ConsumerStep):
    event_queue = None
    celery_task = None

    def get_consumers(self, channel):
        return [Consumer(channel, queues=[self.event_queue], on_message=self.handle_message)]

    @classmethod
    def handle_message(cls, message):
        # after the task sent to the worker, we do not care anymore
        cls.celery_task.delay(message)
        message.ack()


def create_consumer(name, queue, exchange, routing_key, task):
    queue = Queue(queue, exchange=Exchange(exchange), routing_key=routing_key)

    attributes = {
        'event_queue': queue,
        'celery_task': task,
    }
    return type(name, (Consumer,), attributes)


def register_consumer(celery_app, task, params):
    consumer = create_consumer(
        **params,
        task=celery,
    )
    celery_app.steps['consumer'].add(consumer)


if __name__ == '__main__':
    params = {
        'name': 'ConsumerA',
        'queue': 'consumer_queue_a',
        'exchange': 'exchange_a',
        'routing_key': 'routing_key_a',
    }
    register_consumer(celery, do_something, params)

    params = {
        'name': 'ConsumerB',
        'queue': 'consumer_queue_b',
        'exchange': 'exchange_b',
        'routing_key': 'routing_key_b',
    }
    register_consumer(celery, do_something, params)
    ```
