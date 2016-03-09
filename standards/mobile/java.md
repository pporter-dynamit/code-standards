# Java Syntax/Style Guidelines

## Java Lanaguage Rules
* Handle every Exception in some principled way. Don't write code to completely ignore an exception like this:
```java
void setServerPort(String value) {
    try {
        serverPort = Integer.parseInt(value);
    } catch (NumberFormatException e) { }
}
```
* Don't catch generic exceptions. In almost all cases, it is inappropriate to catch generic Exception or Throwable. Instead, catch each exception separately, refactor code to have more fine-grained error handling, or re-throw the exception.
* Don't use finalizers as there is no guarantee that they will be called. Instead, define a `close()` method and document when exactly that method needs to be called.

## Style Rules
* Use Javadoc standard comments. Describe what a class, interface, or method does, not how it does it.
* Write short methods. Methods exceeding 40 lines indicate that it may be time to break it up into multiple methods if it does not harm the structure of a program.
* Use the default Android code formatter built into Android Studio. This defaults to 4-space indents for blocks. Command-Option-L on OS X will trigger auto-formatting on a currently open file.
* Use standard brace style. Braces do not go on their own line; they go on the same line as the code before them. For example:
```java
class MyClass {
    int func() {
        if (something) {
            // ...
        } else if (somethingElse) {
            // ...
        } else {
            // ...
        }
    }
}
```
* Braces should always be used around conditional bodies even if there is only one statement in the body. For example, this should not be done:
```java
if (condition)
    body();  // bad!
```
* Naming convention for `public static final` fields are `ALL_CAPS_WITH_UNDERSCORES`
* Each line of code should be no more than 100 characters long.
* Annotations should precede other modifiers for the same language element. Simple marker annotations (e.g. @Override) can be listed on the same line with the language element. If there are multiple annotations, or parameterized annotations, they should each be listed one-per-line in alphabetical order.
* When naming variables, methods, and classes, treat acronyms and abbreviations as words. i.e. `XmlHttpRequest`
* Use TODO Comments:
```java
// TODO: Change this to use a flag instead of a constant
```
* Log sparingly as it can have a significant impact to performance.
* Be consistent in your code.

# Best Practices
* Communication between Activities, Fragments, Services, etc... should be done with an event bus.
* Dependency injection should be used to separate configuration from usage.

# Gradle
* Configurations that can be generated at compile time should be written to a property file via Gradle. This allows for different configurations on each release type.
* Always create a development key that is packaged with the project. This allows for QA builds to use the same signing config if multiple developers are working on a single project.
* A proguard configuration should be used for release builds. At a minimum, this should remove all logging statements, remove any usused code, and obfuscate any private classes or interfaces.

# Project Organization
* Always store the required signing keys and configurations for an app in the project's source control.
