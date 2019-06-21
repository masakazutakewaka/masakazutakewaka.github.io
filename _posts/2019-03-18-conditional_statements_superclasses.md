---
layout: post
title:  "if...else based on superclasses of the instance in Ruby"
---

## Background
I was writing some patch for a library the other day and I had to wonder what options I have when you write `if...else` based on superclasses of the instance. 

I knew there was more than one way to put it but they were not well organized in my head so I looked up some documentation and I thought I could share the knowledge I got from this.

I will share __2 options__ in this post.

## The first one: if + is_a?
The first one is pretty straight forward but for some people who don't know, `is_a?(class)` (`kind_of?`) is a method that returns `true` if _class_ is the class of the receiver object or the superclasses of the receiver object.

Different from `instance_of?(class)` in a way that `instance_of(class)` only returns `true` when _class_ is the class of the receiver object. 


If you mix it up with `if` statement, it will look like this

```rb
class A; end
class B < A; end

if B.is_a? A
  p 'B is a subclass of A'
else
  p 'B is not a subclass of A'
end

# B is a subclass of A
```

## The other one: case
The other one is kind of interesting because all you need is `case` statement for this one. 
If you look up [the documentation for case](http://ruby-doc.org/docs/keywords/1.9/Object.html#method-i-case), it says 

> Case equality (success by a when candidate) is determined by the case-equality or “threequal” operator, ===.

So if you use `case`, it will look like this. Absolutely simple.

```rb
class A; end
class B < A; end

case B.new
when A
  p 'B is a subclass of A'
else
  p 'B is not a subclass of A'
end

# B is a subclass of A
```

This is the end.

Hopefully some people finds this helpful.

## References
- https://ruby-doc.org/core-2.6.2/Object.html#method-i-is_a-3F
- http://ruby-doc.org/docs/keywords/1.9/Object.html#method-i-case
