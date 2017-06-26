---
layout: post
title:  "Spring cloud contract first look"
date:   2017-04-28 10:40:00
categories: java cdc
disqus: true
displayed: true
---


I'm working mostly on the APIs services. Having more and more of them I decided to find a solution for creating contract. Martin Fowler introduced Consumer Driven Contract on [his page](https://martinfowler.com/articles/consumerDrivenContracts.html) and as I'm
using Spring the solution that I will test as first is a [Spring Cloud Contract](http://cloud.spring.io/spring-cloud-contract/spring-cloud-contract.html).

## Project description
For testing purposes I'll create application responsible for storing and retrieving books in library  divided into frontent and backend application.

### Backend

It will have only few endpoinds described in table below:

Method | Endpoint                         | Description
-------|----------------------------------|----------------------
GET    | /library                         | Get all books from library
GET    | /library/{bookId}                | Get one book from the library
PUT    | /library                         | Add book to the library

### Frontend
<!-- http://framebox.org/AcqZD -->

Frontent application will present list of all available books and possibility to add a new one:

![CDC mockup]({{ site.url }}/assets/cdc-mockup.jpeg)

