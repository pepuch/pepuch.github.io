---
layout: post
title:  "Spring cloud contract first look"
date:   1111-11-11 00:00:00
categories: java cdc
disqus: true
displayed: false
---

I'm working mostly on the APIs services. Having more and more of them I decided to find a solution for creating contract. Martin Fowler introduced Consumer Driven Contract on [his page](https://martinfowler.com/articles/consumerDrivenContracts.html) and as I'm
using Spring the solution that I will test as first is a [Spring Cloud Contract](http://cloud.spring.io/spring-cloud-contract/spring-cloud-contract.html).

## Project description
For testing purposes I'll create as application responsible for storing and retrieving books in library  divided into frontend and backend microservices.

Let's assume that only two use cases will be implemented in the application - for listing and adding books.

### Backend

Business logic part will have only few endpoinds described in the table:

Method | Endpoint                         | Description
-------|----------------------------------|----------------------
GET    | /library                         | Get all books from library
GET    | /library/{bookId}                | Get one book from library
PUT    | /library                         | Add book to the library

### Frontend
<!-- http://framebox.org/AcqZD -->

Frontend application will present list of all available books
<img style="margin: 0;width: 100%;" src="http://localhost:4000/assets/cdc_mockup_list_of_books.jpg"/>
and posibility to add a new one
<img style="margin: 0;width: 100%;" src="http://localhost:4000/assets/cdc_mockup_add_book.jpg"/>

## Implementation


