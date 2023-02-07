# Week 4: Streaming Multiple Consumers
#### Presley Schumacher - February 7, 2023

> Use RabbitMQ to create a _Work Queue_ that will be used to distribute tasks among workers.

* One program will schedule tasks to our work queue, this program is called the new_task.py
* The second program will get messages from the queue and perform the task, this program is called worker.py
* We will use multiple workers so the tasks from the work queue will scale more easily.

## Before You Begin

- [x] Fork this starter repo into your GitHub.
- [x] Clone your repo down to your machine.
- [x] View / Command Palette - then Python: Select Interpreter
- [x] Select your conda environment. 

## Read

- [x] Read the [RabbitMQ Tutorial - Work Queues](https://www.rabbitmq.com/tutorials/tutorial-two-python.html)
- [x] Read the code and comments in this repo.

## RabbitMQ Admin 

RabbitMQ comes with an admin panel.
* The RabbitMQ Management is an interface that lets you monitor and handle your RabbitMQ server from a web browser.
* Queues, connections, channels, exchanges, users, and user permissions can be handled in the browser. As well as monitoring message rates and send/receive messages manually.
* Source: https://www.cloudamqp.com/blog/part3-rabbitmq-for-beginners_the-management-interface.html _This has some really useful information about the basics of RabbitMQ._

When you run the task emitter, reply y to open it. 

(Python makes it easy to open a web page - see the code to learn how.)

## Execute the Producer

- [x] Run emitter_of_tasks.py (say y to monitor RabbitMQ queues)
  * The ack(nowledgement) is sent back by the consumer to tell RabbitMQ that a message had been     received, processed, and that RabbitMQ can delete it.
  * Acknowledgements are essential for data safety.

Source: https://www.rabbitmq.com/confirms.html#basics

## Execute a Consumer / Worker

- [x] Run listening_worker.py

Will it terminate on its own? How do you know? 
  * The task does not terminate on its own. If you want to terminate, you need to use CTL + C. If you terminate a worker while it was processing a message, RabbitMQ will requeue the message and deliever the message to another consumer as long as there are other consumers online.

## Ready for Work

- [x] Use your emitter_of_tasks to produce more task messages.

## Start Another Listening Worker 

- [x] Use your listening_worker.py script to launch a second worker. 

- [x] Follow the tutorial. 
- [x] Add multiple tasks (e.g. First message, Second message, etc.)
- [x] Monitor the windows with at least two workers. 

Which worker gets which tasks? How are tasks distributed? 
  * By default, RabbitMQ will send each message to the next consumer, in sequence. On average every consumer will get the same number of messages. This way of distributing messages is called round-robin. 
  * In my example, I used 2 consumers and distributed 5 messages. Consumer number 1 got messages 1, 3, and 5. Consumer number 2 got messages 2 and 4.

## Reference

- [RabbitMQ Tutorial - Work Queues](https://www.rabbitmq.com/tutorials/tutorial-two-python.html)


## Screenshot

See a running example with at least 3 concurrent process windows here:
