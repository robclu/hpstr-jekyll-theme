---
layout: post
title: Template Metaprogramming Basics
excerpt: "Towards a metaprogramming understanding!"
tags: [sample post, code, highlighting]
modified: 2015-09-16
comments: true
---

Template metaprogramming [[1]](https://en.wikipedia.org/wiki/Template_metaprogramming) (TMP) in C++ is a method of
generic programming which essentially uses the compiler to interpret the code and generate temporary source
code which is then used with the rest of the code. Okay, so that sounds a bit complicated! Essentially, it is
a way of performing compile-time computation, which, if used correctly, can have pretty drastic performance
improvements. However, if not used correctly it can cause code bloat and decrease performance. 

So what is it all about then? Well C++ templates are Turing complete which means that any computation which can be
expressed should be able to be computed. Let's start with the most basic (well at least in my opinion) 
data structure. Alexandrescu called this a ```typelist``` [[2]](http://www.drdobbs.com/generic-programmingtypelists-and-applica/184403813), however,
I prefer to call it a ```list```. I choose ```list``` since I will adapt the typelist to be more general 
(typelist would still be an accurate description, I just feel that when applying metafunctions to typelists, 
the name list is more appropriate). 

### What is a metaprogramming list then?

A metaprogramming list a simply a struct that holds types (classes and structs) -- from here on
referred to as *elements*. The real power of the list comes from C++'s variadic templates 
[[3]](https://en.wikipedia.org/wiki/Variadic_template) which means that the list could in theory 
(if the compiler could manage -- vairiadic templates are evaluated recursively by the compiler, and there is 
limit to the recursion depth) hold an infinite number of elements. 

A list can be defined as follows :

```cpp
template <typename... Elements>
struct list;
```

And the usage would be something like 

```cpp
using int_list = list<int, int, int>;
```

But what is the point of this list? It doesn't appear as if it has any use. Well no, not really, since the
```int``` type doesn't really do anything useful at compile time, other than specify that a variable has
an integer type. We could define a constructor inside the list struct which takes arugments which are
instances of the ```Elements``` types. For example

```cpp
template <typename... Elements>
struct list
{
    list(Elements... elements) {}
};
```

And then use the list like 

```cpp
list<int, int> new_list(2, 3);
```

But IMHO, this is not the best way of doing things. So let's look at anther approach. I will define this alternative 
approach as metaprogramming primities, as it allows the equivalent of a C++ primitive for TMP.

### Metaprogramming Primitives

It would be useful if the meta data structures could support something equivalent to the primitive types in
traditional C++. Fortunately this is possible! We can start with the two most basic ones:

* int
* size_t

All we really have to do is wrap these in a struct which allows us to access both the value and the type at
compile time. Here is how this can be done for the ```int``` type :

```cpp
template <int Value>
struct integer
{
    // Allow access to the Value
    static contexpr int value = Value;

    // Allow access to the type (using alias, requires C++11)
    using type = int;
};
```

Only the ```int``` version is shown here, but the conversion to ```size_t``` is trivial given the above code sample.

__Note__ how the alias was used for __type__. This comes up a lot in TMP. An annalogy can be made between standard 
C++ and TMP for variables and types. For TMP a type is analegous to a value in traditional C++, and the 
```using``` keyword is the method for declaring the type. For code snippet below shows this annalogy.

```cpp
//  Traditional C++ -- declare an int with a value of 3
int x = 3;

// Metaprogramming declaration of an integer with a value of 3
using x = integer<3>;
```
The defined ```integer<>``` type for the TMP language can now be used in C++ at
runtime. For example

```cpp
using x = integer<3>;

if (x::value > 4) // Do something here
```

Which leads to another point. To access TMP variables, the resolution (```::```) operator is used, rather than 
the dot (```.```) operator for objects. 

The defined ```integer<>``` class can be used with the TMP ```list``` class, to give compile-time lists, to 
essentially provide a compile-time array. The following code snippet illustrates this :

```cpp
// Create a list that has values of 2, 4, and 7
using integer_list = list<integer<2>, integer<4>, integer<7>>;
```

So now we have a list of elements for which we can access the type and value of, which provides a lot more
options that the simple int type!

The interface can be cleaned up a bit, so that we don't have to type out ```integer``` for each
list element. This is done by creating a type alias for an integer list, as follows :

```cpp
template <int... Integers>
using interger_list = list<integer<Integers>...>;
```

And now we can create integer lists more cleanly

```cpp
// Create a nice looking integer list
using nice_list = integer_list<1, 2, 3, 4, 5>;
```

The variadic template is expanded recursively during compilation (a later post will go into more detail), but 
essentially the ```nice_list``` looks like this when expanded :

```
// Essentially nice_list looks like this 
list<integer<1>, integer<2>, integer<3>, integer<4>, integer<5>>;
```

So while the TMP syntax is not the greatest (although I quite like it), it is managable, and alias's can help 
to make the code more understandable.

Currenly the list is not very useful, as the elements cannot be accessed, and operations cannot be performed 
on the list. The next step is then allow operations to be performed on the list, and to define other meta 
data structures which are more suited to specific cases -- such as hash tables and binary search trees! I'll 
get to that in the next few posts! 

At my GitHub account you can find the ```nano``` library -- a TMP library I am writing to provide a lot of 
the C++ STD library, as well as some functional features!

### References

[1] : [https://en.wikipedia.org/wiki/Template_metaprogramming](https://en.wikipedia.org/wiki/Template_metaprogramming)  
[2] : [http://www.drdobbs.com/generic-programmingtypelists-and-applica/184403814](http://www.drdobbs.com/generic-programmingtypelists-and-applica/184403813)  
[3] : [https://en.wikipedia.org/wiki/Variadic_template](https://en.wikipedia.org/wiki/Variadic_template)  
