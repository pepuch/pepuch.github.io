---
layout: post
title:  "Javaslang ... exception handling"
date:   2017-01-28 10:40:00
categories: java javaslang
disqus: true
displayed: false
---

While working with java it's annoying while called method throws exception. If you chosen to handle it with `try ... catch` you may have a feeling that `try ... catch` notation is redundant. The solution may be Javaslang `Try` class.

The first time I've used it was in a method responsible for searching person by name and that's the first implementation of it.

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

As you can see `try ... catch` makes the code less readable. Luckily javaslang has `Try.of()` method that replaces `try ... catch` and code looks definitely more readable.

{% highlight java %}
public Optional<Person> findByName(final String name) {
	return Try.of(entityManager
		.createQuery("SELECT ...", Person.class)
		.setParameter("name", name)
		.getSingleResult())
		.toJavaOptional();
}
{% endhighlight %}
 
My first impression of using `Try` is that it's mostly useful in simple cases like

{% highlight java %}
Try.of(bunchOfWork()).getOrElse(returnSomethingInCaseOfException());
Try.of(bunchOfWork()).toJavaOptional();
Try.run(bunchOfWork); // for voids
{% endhighlight %}

but it is also possible to use it for example as part of java 8 stream.

{% highlight java %}
Arrays.asList("1", "a", "2", "b").stream()
    .map(num -> Try.of(() -> Integer.parseInt(num)).toOption())
    .flatMap(Option::toJavaStream)
    .collect(Collectors.toList());
{% endhighlight %}

Other examples of using `Try` are availabe in [javaslang-tests project](https://github.com/pepuch/javaslang-tests/tree/master/src/main/java/io/github/pepuch/exceptionhandling).

#### Links
- [Javaslang home page](http://www.javaslang.io/)
- [`Try` class documentation](http://www.javaslang.io/javaslang-docs/#_try)
- [javaslang-tests project](https://github.com/pepuch/javaslang-tests)