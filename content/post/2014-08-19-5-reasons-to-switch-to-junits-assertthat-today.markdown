---
author: varokas
comments: true
date: 2014-08-19 04:34:24+00:00
layout: post
slug: 5-reasons-to-switch-to-junits-assertthat-today
title: 5 reasons to switch to JUnit's assertThat(...) today
wordpress_id: 908
categories:
- Software Engineering
---

![junit-logo](images/2014/08/junit-logo.png)

It bugs me that a good number of Java developers still use these two assert methods when dealing with JUnit.

[code language="java"]
assertEquals(expected, actual);
assertTrue(i > 0);
[/code]

Yes, there are more asserts methods, but these two guys are pretty much what you'd use all the time.

My main problem with assertEquals(..) is that I always get the parameters order messed up between the "actual" and "expected". That does not matter a lot until you have an assertion failure and the error messages report the swapped value.

For assertTrue(..) we use that for virtually everything else, because assertEquals(true, expression) simply is lame. We need to comes up with all the logic in assertion ourselves, which is also lame. It is also guaranteed that you'd always have to put in some descriptive message in assertTrue(...) for it to make sense when the test is failing.

JUnit testing is way too uncool, until you've met the awesome assertThat(...).

And here's the reason why you should change the way you do JUnit right now!



## 1. It reads from left to right



That's how all code should be read and understand.

[code language="java"]
  int inputValue = 2;
  int expectedValue = 2;

  assertThat(compute(), is(expectedValue));
[/code]



## 2. It is expressive



Even if you don't buy the "left-to-right" argument. assertThat(..) reads much better in almost every situations.
[code language="java"]
  int smaller = 2;
  int larger = 3;

  /* pretty isn't it? */
  assertThat(larger, is(greaterThan(smaller)));
[/code]



## 3. It produces readable error messages



Expressive language helps in generating an expressive error message.

Would you rather have just "OMG, something is wrong".

[code language="java"]
  int smaller = 2;
  int larger = 3;

  //you'll get this message: "java.lang.AssertionError". WTH?
  assertTrue(smaller > larger);
[/code]

Or a detailed message on what is to expect, what is the actual value, pretty much for free?

[code language="java"]
        int smaller = 2;
        int larger = 3;

        //Gives you:
        //  java.lang.AssertionError:
        //  Expected: is a value greater than <3>
        //       but: <2> was less than <3>
        //
        // Clear, concise, effortless
        assertThat(smaller, is(greaterThan(larger)));
[/code]



## 4. It works really well with collections



One of the most miserable things you have to do with traditional assert is to loop through a list to look for some item. Using assertThat feels especially great once you realized how much code you don't have to write (and to come back to read later).

[code language="java"]
        List<Integer> fibonacci = Arrays.asList(1,2,3,5,8,13);

        //Don't do this, please
        boolean found = false;
        for(int i : fibonacci) {
            if( i == 5) found = true;
        }
        assertTrue( "number 5 is in list", found );

        //assertThat is way better
        assertThat(fibonacci, hasItem(5));
        assertThat(fibonacci, not(hasItem(lessThan(0))));
[/code]



## 5. You can actually start using it right now, without any changes



assertThat(..) is part of JUnit4 for so long. just open up your project and try it. It already is there for you to use!

Note that we almost always want to pair it with hamcrest-library to get all the useful matchers by default. So stick that into your pom.xml as well. For more information, look at [hamcrest tutorial](https://code.google.com/p/hamcrest/wiki/Tutorial)



## Bonus



Here's a [github](https://github.com/varokas/kata-java/blob/master/src/test/java/com/varokas/test/AssertThatTest.java) link to the code. If you prefer to take it all together at once.

These are some of the assertions I use all the time.

[code language="java"]
        //Imagine writing all these by hand...
        //
        //ps. (are you doing this everyday?)

        //String stuff
        assertThat("iGNoreMyCasePlease", equalToIgnoringCase("ignoreMyCasePlease"));
        assertThat(null, isEmptyOrNullString());

        //Math stuff
        assertThat(4, both(greaterThan(3)).and(lessThan(5)));

        //Collections Stuff
        assertThat(new ArrayList<Integer>(), is(empty()));

        assertThat(Arrays.asList(1,2,3), hasItem(1));
        assertThat(Arrays.asList(1,2,3), containsInAnyOrder(3, 1, 2));
        assertThat(Arrays.asList(1,2,3), hasSize(greaterThan(0)));

        //Map Stuff
        Map<Integer, String> numbers = new HashMap<Integer, String>();
        numbers.put(1, "one");
        numbers.put(2, "two");
        numbers.put(3, "three");

        assertThat(numbers, hasEntry(1, "one"));
        assertThat(numbers, hasKey(2));
        assertThat(numbers, hasValue("three"));

        assertThat(numbers, hasKey(greaterThan(0)));
[/code]
