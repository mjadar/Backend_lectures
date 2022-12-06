# JUNIT 5


## Why write tests?
- As usual : Design > Write Code > Test
- With Testing : Design > Write Code > Write Tests > Run the tests.
- The points of writing automated test not so much to verify that the code works now ; The point is to verify on an ongoing basis that the code continues to work in the future.

## Why we need a testing framework?
- it handles your code, you prepare tests, provide test inputs and expected output. And Junit will handle your code with tests. It will verify the result.

## Why Junit5?
- JUinet 4 is > 10 years old
- Not up to date with newer testing patterns
- Not up to date with Java language features
- Monolithic architecture
- JUnit5 called also JUnit Jupiter, cuz Jupiter is the 5th planet.

## Junit5 architecture:
- Platform with a set of APIS:
    - JUPITER ( to run junit 5)
    - Vintage (to run old junit tests)
    - EXT 3rd PARTY

## Creating a JUnit Test:
- Dependencies:
    - `junit-jupiter-api` : API for writing tests using JUnit Jupiter.
    - `junit-jupiter-engine`: Implementation of the TestEngine API for JUnit jupiter.
    - `junit-vintage-engine` : A thin layer on top of JUnit 4 to allow running vintage tests.
- import static org.hunit.jupiter.api.Assertions.*;
- Add annotation `@Test` before method to say this is a test you should run it.

## Assert methods:
- Assert.assertEquals(expected, actual)
- `Assert.assertArrayEquals(expectedArray, actualActualArray)`
    - verify each item in the arrays are equal in the right position.
- `Assert.assertIterableEquals(expectedArray, actualArray)`
    - verify aech item in the iterable are equal in the corresponding positions.
- `AssertEquals(expected, actual)` ; `AssertNotEquals(expected, actual)`
    -  uses the equals() method, or if no equals() method was overridden, compares the reference between the 2 objects.
- `AssertSame(expectedObj, actualObj, msg)`
    - compares the references between the 2 objects.
- `AssertTrue/False(boolean condition)` 
    - check that a condition is true/false
- `AssertNull/NotNull(object)`
- `Assertions.assertAll(Collection executables)`
    - It asserts that all supplied executables do not throw exceptions.
    - you pass lambdas with the corresponding assertion method.
    - `assertAll( ()-> assertTrue(), ()->assertFalse(), ()->assertNull()`;

## Test Driven Development With Junit:
- **Test first, then code**
- write method and stop it (just definition+signature)
- write your test, it should fail.
- Then write your code.

## Maven urefire plugin integration:
- Maven plugin that let you run junit tests using maven.
- `maven-surefire-plugin`
- then run As > Maven Test.
```
# Run all the unit test classes.
$ mvn test

# Run a single test class.
$ mvn -Dtest=TestApp1 test

# Run multiple test classes.
$ mvn -Dtest=TestApp1,TestApp2 test

# Run a single test method from a test class.
$ mvn -Dtest=TestApp1#methodname test

# Run all test methods that match pattern 'testHello*' from a test class.
$ mvn -Dtest=TestApp1#testHello* test

# Run all test methods match pattern 'testHello*' and 'testMagic*' from a test class.
$ mvn -Dtest=TestApp1#testHello*+testMagic* test
```

## Asserting Excpetions:
- `Assert.assertThrows(excpetionType, executable, msg);`
    - the executable is a lambda function that runs the code which should return an exception.
    - the exceptionType is the expected type of exception.
```
@Test
void testDivide(){
    MathUtils mathutils = new MathUtils();
    assertThrows(ArithmeticException.class, ()->mathUtils.divide(1, 0), "divide by zero should throw");
}
```

## Life cycle and test antipatterns to avoid:
- it is the process in which the test instance is created, managed and destroyed.
- Junit create a new test instance whenever a method runs.
- `@BeforeAll`, `@AfterAll`, `@BeforeEach`, `@AfterEach`.
- `@BeforeAll` and `@AfterAll` are run before the instance is created, and after instance gets destroyed respectively ; this lead to a problem, how to call a method of a class before instanciating it?
    - Solution --> make the method static.

## Changing default TestInstance behavior:
- default behavior is Junit creates a new instance for each method.
- use annotation `@TestInstance`
- `@TestInstance(TestInstance.lifecycle.PER_METHOD)` #default
- `@TestInstance(TestInstance.lifecycle.PER_CLASS)`


## Using DisplayName and Disabled annotation:
- add this annotation before the test `@DisplayName("Testing add method")`
- `@Disabled` to skip the test.
```
@Test
@Disabled
@DisplayName("TDD method. Should not run")
```

## Conditional Execution and assumptions:
- allow to execute a test only on a certain condition.
- @EnabledOnOs( OS.LINUX )
- @EnabledOnJre(JRE.JAVA_11)
- @EnabledIf
- @EnabledIfSystemProperty
- @EnabledIfEnvironmentVariable

- use assumptions to avoid on certain failures to break the test. For eg, when a server is down the test will break, but me i wan't the test to keep workin; So use `Assumptions.assumeTrue`
```
@Test
void testConnection(){
    boolean isServerUp = false;
    Assumptions.assumeTrue(isServerUp);
    Assertions.assertEquals(...);
}
```

## Nested tests:
- use annotation `@Nested` before the class test that is nested.
- it will group the test methods inside this class together when viewing the results of test cases.
```
@DisplayName("Display name for parent class test")
class father {

    @Nested
    @DisplayName("Display name for child class test")
    class children {
        @Test

        @Test
    }
}
```  

## Using supplier for assert messages:
- `assertEquals(expected, actual, ()-> "returned "+actual+" but it should be "+expected")`
- the message will run only when the Test case will fail.

## Using repeatedTest
- `@RepeatedTest(4)` will repeat the test 4 times, and the Test will succeed only when the 4 Tests succeed.
```
@RepeatedTest(4)
void testComputeCircleRadius(RepetitionInfo repetitionInfo){
    cur = repetitionInfo.getCurrentRepetition();
    assertEquals(...);
}
```

## Tagging Tests with @Tag:
- `@Tag("math")`
- different Test runners have features to select your tags and run the correspondant Tests depending on what you have in mind.

## Using TestInfo and TestReporter:
- TestInfo + TestReporter