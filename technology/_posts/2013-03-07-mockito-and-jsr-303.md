---
layout: techpost
title: Mockito and JSR-303
tags: mockito annotation design testing junit
---

My current client maintains contracts to insure methods are called with the right parameters. Sad thing is that they way they’ve done this to date has involved writing statements into their interface implementation classes. There are several downsides to this approach:

1.  There’s no way to validate that unit tests using mocks of the interfaces are adhering to the contract.
2.  Every implementation must write the same contract code again and again
3.  Developers calling the interface must look at the implementations to determine what the contract is to which they must adhere.Often we use annotations to define simple contracts for APIs. I was hoping Mockito had some kind of system in place to verify that invocations on mocks met the spec in the annotated interface, but no joy. So, I wrote one. You can get a copy from [my GitHub fork](https://github.com/koehn/mockito). Of course, I submitted a [pull request](https://github.com/mockito/mockito/pull/9) to the [Mockito](http://www.mockito.org/) people to try to get them to mainline it. We'll see what they think.

So now you can have an interface like this:

    public interface Foo {
        @NotNull String getMessage();
        @NotNull Bar getBar(@NotNull String barId);
    }

And when you create your mock like this:

    Foo foo = mock(Foo.class, withSettings().validate().validatorFactory(
        Validation.buildDefaultValidatorFactory());

Then, if you call this from your class under test:

    foo.getBar(null)

Mockito will automatically throw an exception indicating you've violated Foo's contract.

It works both ways too! Let's say you forgot to mock out a call to `getBar()`` above. If your test does something against your mock like:

    Bar bar = foo.getBar("123");

Mockito will throw an exception because the interface says the result may not be null, but your mock will in fact return null from this method (because `null` is the default value Mockito returns).
