# Repudiation

The example demonstrates a vulnerability that can lead to repudiation by malicious users attempting to access the services provided by a server.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Run the server __insecure.ts__.

3. Pretend to be a malicous user and interact with the services by sending requests from the browser.

4. Do you think your actions can be repudiated?

## For you to do

1. Briefly explain the vulnerability.
The vulnerability in insecure.ts is the lack of proper logging and auditing mechanisms. This allows malicious users to perform actions without leaving a trace, making it difficult to track and attribute their actions. This can lead to repudiation, where users deny having performed certain actions, and there is no evidence to prove otherwise.
2. Briefly explain why the vulnerability is addressed in __secure.ts__.
The vulnerability is addressed in secure.ts by implementing proper logging and auditing mechanisms. These mechanisms record all user actions and changes, providing a traceable history of events. This ensures that any actions performed by users can be tracked and attributed, preventing repudiation and allowing for accountability.
3. Which design pattern is used in the secure version to address the vulnerability? Briefly explain how it works?
Design pattern used : Chain of responsibility design patterns as the Chain of Responsibility pattern involves passing a request along a chain of handlers. Each handler processes the request or passes it to the next handler in the chain.
In the context of secure.ts:

Middleware Handlers: Each middleware in the chain is responsible for a specific task, such as authentication, authorization, and logging.
Logging Middleware: A specific middleware is dedicated to logging user actions. It captures details of each request, such as the user identity, action performed, and timestamp.