---
layout: post
title: "Notes on Effective Java(1) - Common Methods to all Objects"
description: "This post covers the third chapter of Effective Java, talking about equals, hashCode, toString and so on"
category: Effective Java
tags: [Java]
---
{% include JB/setup %}

##Concerns when overriding equals( )##

First of all, 5 rules to follow when overriding `equals()` function:

1. Reflexive, ie `a.equals(a)`
2. Symmetric, ie `a.equals(b) => b.equals(a)`. This may be violated when comparing with subclasses
3. Transitive, ie `a.equals(b) & b.equals(c) => a.equals(c)`
4. Consistent, if `a.equals(b)` then we always have `a.equals(b)` if the compared fields of `a` and `b` are not changed.
5. Non-nullity, that `a.equals(null) == false`

Secondly, there are some guidance to override `equals()`

1. Using `==` to check whether the parameter is the reference of `this`, which is an optimization.
2. Using `instanceof` to check whether the parameter is of the same type. Pay attention here that `null` value can be chekced here as well by `instanceof`
3. Casting the parameter to the correct type.
4. Checking every “significant” field in the class. Especially, 
    + to avoid `NullPointerException` when checking the `null` valued fields, we can use `field == null? o.field == null: field.equals(o.field)`
    + for the optimization, check the fields that are mostly unlike to equal first.
5. When it is finished, testing the 5 rules mentioned above.


<br/>

##Always **override hashCode( )** when overriding equals##
  
As a matter of fact, we **must** override hashCode in every class that overrides equals. There is a contract of `hashCode()`:

> Whenever it is invoked on the same object more than once during an execution of an application, the hashCode method must consistently return the same integer, provided no information used in equals comparisons on the object is modified. This integer need not remain consistent from one execution of an application to another execution of the same application.

All in all, a good `hashCode()` function tends to produce equal hash codes for the objects that are equal and unequal ones for unequal objects. Although achieving this ideal can be diffcult, fortunately we have a recipe to achieve a fair approximation from [Effective Java](http://www.amazon.co.uk/Effective-Java-Edition-Joshua-Bloch/dp/0321356683). 

2. For each significant field f in your object (each field taken into account by the equals method, that is), do the following:
      


##Conclusion##