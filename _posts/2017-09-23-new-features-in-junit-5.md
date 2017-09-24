---
title: New features in JUnit 5
---

A new major version of JUnit was released on September 10, 2017. The codebase was upgraded, so Java 8 or higher is required at runtime and it consists of three submodules now.
> JUnit 5 = JUnit Platform + JUnit Jupiter + JUnit Vintage  

1. *JUnit Platform* - Provides the foundation for the test runners
2. *JUnit Jupiter* - Defines the API.
3. *JUnit Vintage* - Supports running old JUnit 3 and JUnit 4 tests

# Should i upgrade?
Yes, there is no reason why you should not upgrade. The old and the new tests can coexist. It would not be possible to upgrade all tests at once. How the migration works can be found here: [http://junit.org/junit5/docs/current/user-guide/#migrating-from-junit4](http://junit.org/junit5/docs/current/user-guide/#migrating-from-junit4)

# My top 3 new features
## 1. Parameterized tests
Ever had an enum with multiple values and you wanted to test your code with all values as parameter? Then you know that it was very unlovely to write a test for it. I often made a for-each loop inside the test to check the behaviour with all inputs, but that does not look very clean because the assertions are inside the loop. With the JUnit 5 test method parameters it becomes much cleaner. You can simply use an enum as source to test with all possible values:

```
@ParameterizedTest
@EnumSource(TimeUnit.class)
void testWithEnumSource(TimeUnit timeUnit) {
    assertNotNull(timeUnit);
}
```

There is also the possibility to use other sources like: @ValueSource, @MethodSource, @CsvSource and @ArgumentsSource.

## 2. Lambda Support
Everyone loves lambdas, right? So why not using it in tests? For me testing exceptions looks much cleaner with a lambda used:

```
@Test
void assertThrowsException() {
    String str = null;
    assertThrows(IllegalArgumentException.class, () -> {
      Integer.valueOf(str);
    });
}
```

Another example would be an grouped Assertion. All failures are reported together and can be solved in one go:

```
@Test
void groupedAssertions() {
  assertAll("person",
    () -> assertEquals("John", person.getFirstName()),
    () -> assertEquals("Doe", person.getLastName())
  );
}
```

## 3. Nested Tests

Nested Tests in combination with the @DisplayName annotation can now represent real scenarios. This comes in handy for integration tests where more components are involed. A possible use case for the project I am working on are the CDI-Unit and Selenium Tests. I currently did not use this feature. I will update this topic with an example when I have used it.
# Using JUnit 5 with Mockito
To mock all the components I was using Mockito. Of course using Mockito with JUnit 5 is still possible and usefull . Just make sure that Mockito 2.x is used. Instead of the previous JUnit Runner `@RunWith(MockitoJUnitRunner.class)` the new  Mockito Extension `@ExtendWith(MockitoExtension.class)` must be used.

Happy testing! :)

### Further reading
[http://junit.org/junit5/docs/current/user-guide/](http://junit.org/junit5/docs/current/user-guide/)