---
layout: essay
title: Test frameworks
tags: test unit integration hibernate stability
---
Recently I was submitting a [pull request](https://github.com/hibernate/hibernate-orm/pull/731) to to address a [defect](https://hibernate.atlassian.net/browse/HHH-9142) in a well-known [Java persistence framework](http://hibernate.org). I wrote the fix (which was two lines of code), and, since there were no tests written for the current codebase, I submitted the PR.

Eventually one of the PR approvers looked it over and decided that I should write a test. Fine. I had to add Mockito (a mocking framework) to the build file since it wasn't yet used in the module at all (!!!), and I wrote up a unit test that made sure that the code would work correctly. Commit; push; done.

But no! The approver said that a unit test wasn't good enough; it needed an integration test. Huh? This is for code that up until now has had **no tests at all**. And I'm supposed to write an integration test, even though my code is two lines of a more complicated class? I explained that if the team makes it this hard to fix bugs, they'll simply be stuck with more bugs:

> I'll take a look. The simple truth is that this behavior is best captured in a unit test. A test requiring a more complex setup (like the one you described) is a test that's doomed to be broken when any of a myriad of changes happen to the source base, changes unrelated to the behavior at hand. This makes fixing the rest of the source base harder, since whomever makes the change won't know if the tests are broken because they actually broke something or because they just broke the tests.

And:

> Putting patch developers in a position where they need to learn a complex testing framework in order to fix a relatively simple bug simply means that you'll get fewer bugs fixed, since most developers don't have the time to learn all the required cruft. I'm not at all sure that fewer bug fixes is better than more bugs with "better" tests that don't catch those bugs. Obviously it's a curve, and the correct spot on the curve is not objectively verifiable.

The approver and I went back and forth on this for a while, and eventually I just broke down and wrote the damned test, mentioning that the test was likely to fail in the future and nobody will know what to do with it. The approver (eventually) approved the PR and merged the code.

Of course, when the code got merged into the next major release, it failed to compile, since the test harnesses I was using were completely gone in the new release. *&#$@@!

I told you so.
