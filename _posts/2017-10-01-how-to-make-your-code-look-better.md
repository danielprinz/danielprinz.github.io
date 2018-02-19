---
title: How to make your code look better
layout: post
categories: coding
---

Do you hear your colleagues screaming WTF when you ask them to review your code?

![wtfs](/img/2017-10-01-how-to-remove-code-smells/amout_of_wtfs.png){:width="350px"}

I hope not.It should be every developers goal to make the code readable and easy to understand. I like using [SonarQube](https://www.sonarqube.org/) to make problems in the code visible. There are plugins for many IDEs to identify most of the bugs, code smells and vulnerabilities even before the code is checked in.  

# Here are some recommendations to make your code look better:
## Use the functional programming style
One way to increase the readability of the code is using a functional programming style. Focus on the **what** and not so much on the **how.** In the following example the prime numbers between 1 and 100 are calculated. Which solutions is easier to understand?

### Imperative
{% gist danielprinz/cb27657df88ed1f6c6047322748763a4 %}

### Functional
{% gist danielprinz/70d3d78949b5648ec39ebff115553c4e %}

## Use Single-Responsibility Methods
Did you every try to read two websites at once? If you want to understand the content you have to read the sites consecutively. So it is with code. Reading an method that does two or more things at once it very hard to understand and will likely be never reusable. So try to split it into small pieces and then see the difference.

### Doing two things in one method
{% gist danielprinz/db9448303e65202d6b752355537269b4 %}

### One method for every resposibility
{% gist danielprinz/8a80be5bd125ccc254064b3bf397200c %}


This post was inspired by the IntelliJ IDEA Blog posts about code smells: [https://blog.jetbrains.com/idea/tag/code-smells/](https://blog.jetbrains.com/idea/tag/code-smells/)
