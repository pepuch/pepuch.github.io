---
published: false
layout: post
title:  "Javaslang ... exception handling"
date:   2017-01-2****0 10:18:00
categories: java javaslang
disqus: true
---

While working with java it may be that one of the called method throws exception. The problem is that you need to catch it which may be annoying because it's
not always needed. 

The first time that I've used `Try.of()` was in a method responsible for searching person by name. What I wanted to return was `Optional<Person>`
because the person that should be found doesn't need to exist. As `getSingleResult()` method throws `NoResultException` it needed to be catched. That's the first implementation of it.

{% highlight java %}
public Optional<Person> findByName(final String name) {
	try {
		return Optional.of(entityManager
			.createQuery("SELECT ...", Person.class)
			.setParameter("name", name)
			.getSingleResult());
	} catch(final NoResultException e) {
		return Optional.empty();
	}
}
{% endhighlight %}

Luckily javaslang has `Try.of()` method that replaces `try ... catch` and code looks definitely more readable.

{% highlight java %}
public Optional<Person> findByName(final String name) {
	return Try.of(entityManager
		.createQuery("SELECT ...", Person.class)
		.setParameter("name", name)
		.getSingleResult())
		.toJavaOptional();
}
{% endhighlight %}
 
### Summary
My first impression of using `Try` is that it's most useful in simple cases like

{% highlight java %}
Try.of(bunchOfWork()).getOrElse(returnSomethingElse());
Try.of(bunchOfWork()).toJavaOptional();
{% endhighlight %}

but it is also possible to use it for example as part of java 8 stream.

{% highlight java %}
Arrays.asList("1", "a", "2", "b").stream()
    .map(num -> Try.of(() -> Integer.parseInt(num)).toOption())
    .flatMap(Option::toJavaStream)
    .collect(Collectors.toList());
{% endhighlight %}

Other examples of using `Try` are availabe on my [github project](https://github.com/pepuch/javaslang-tests/tree/master/src/main/java/io/github/pepuch/exceptionhandling).