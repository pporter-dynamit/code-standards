# Objective-C Syntax/Style Guidelines

## Commenting

Comments should be brief and explain the "Why?", not the "How?". Additionally, the following style guidelines should be followed when writing comments:

```objective-c
/**
 <Class description>. Use block comment style with an extra asterisk.
*/
@interface XYZFoobar

/// <Property/variable description>. Single-line or property comments should use three slashes.
@property (nonatomic, copy) NSString *someProperty;

#pragma mark - <Pragma Comment describing method groupings>

/**
 <Method description>. Use block comment style with an extra asterisk.

 @param <name> a(n) `<className>` <description>.

 @returns `<className>` <description>.

 @discussion <Optional edge case, etc. discussion.>
 ...extra directives may appear here...
 ...see https://developer.apple.com/library/mac/documentation/DeveloperTools/Conceptual/HeaderDoc/intro/intro.html...
 */
- (CGFloat)xyzWithFoo:(NSInteger)foo;

@end
```

## Annotations

* Use `nonnull` and `nullable` when declaring types in Objective-C code that will eventually integrate with Swift code.
* When applicable, use `NS_ASSUME_NONNULL_BEGIN` and `NS_ASSUME_NONNULL_END` when it saves typing.
* Annotate designated initializers with `NS_DESIGNATED_INITIALIZER`.
* When expecting to integrate with Swift, parameterize collection types with key or value types. For example, `NSArray<NSString *>`.

# Micro and Macro Patterns

* Prefer functions and methods over complicated macros when possible. Macros are unusable in the debugger.
* Be judicious in your usage of parenthesis when defining a macro. By their nature as simple text substitutions, unsafely written macros can have unintended results.[^1]
* Avoid singletons in favor of composition and dependency injection.[^2]
* When choosing to write a singleton, ensure that creation and initialization is thread-safe by wrapping it in a `dispatch_once(...)` block.
* Always pass in an `NSError` pointer when such error reporting is provided by an API. Always check if there is a value returned that indicates an error.
* `NSError` should be used for recoverable, user-facing problems, such as a network request that has failed. `NSException` should be used for programmer errors and should all be resolved before deployment. Additionally, `NSAssert` may be used to catch programmer errors as well.
* (Almost) never leave `NSLog` statements in a production build. Use a macro that checks the `DEBUG` flag or a comprehensive logging system to keep unneeded information out of release builds.
* When referring to values in an `NSDictionary`, especially when they are used more than once, declare the key names as `static NSString * const`. This also applies to key names when implementing adherence to `NSCoding` or when saving values in `NSUserDefaults`, for example.
* When manipulating a `UIView` in code, prefer creating and updating `NSLayoutConstraints` instead of direct `frame` access.
* Always use the `CGRect...()` functions instead of directly accessing properties off of the `frame`.

# Code Organization

* Group related `#import` declarations together.
* When importing Frameworks, prefer `@import` over `#import`.
* Partition class implementations into logically grouped methods, such as those implementing a certain protocol or overriding template methods in a superclass.
* Mark each grouping of methods with a single `#pragma mark - <Group Description>`. For example, methods overriding `UIViewController` defaults should be grouped under `#pragma mark - UIViewController`. Always use the exact name of a protocol or class as the description when applicable.
* Don't use Precompiled Prefix Headers. It obscures dependencies.
* Don't require consumers of your large API to `#import` a multitude of files. Provide an umbrella header file that exposes all of the most important and most often-used parts of your library. See `<UIKit/UIKit.h>` for an excellent example.

# Classes

* Classes should be named with a 3-letter uppercase prefix indicating the project or company that they belong to.
* `init` methods should return `instancetype`, not `id`.
* If the class is a subclass of `UIView`, it should be `IB_DESIGNABLE` and all public UI properties should be `IB_INSPECTABLE`.
* Ensure that all properties exposed to the user that are not meant to be manipulated are clearly declared as `readonly`.
* Protocol adherence declarations that do not need to be user-facing should be kept in the `.m` file.
* Not everything needs to be a class! For example, keep related, reusable constants in their own file without any class declarations.

# Protocols

* Methods that need not be implemented by a delegate object should be marked as `@optional`.
* Likewise, use the `@required` annotation to be explicit about required methods as well.

# Storyboards

* In apps of sufficient complexity, split up Storyboards into multiple files to reduce Xcode memory usage and merge conflicts.

# Categories

* The usage of categories should be encouraged when a provided API does not provide an operation that is useful and that behavior will be repeated throughout the codebase.
* Don't create umbrella categories. Provide specific functionality in each category, and split them up when they become too large or the purpose unclear.
* Category files should be named for the behavior they provide. For example, `NSArray+Functional.h` may provide `reduce`, `map`, or `filter`-type methods on  `NSArray`.
* All category methods should have a named prefix based on the project or category they may be found in. This should follow the naming scheme `<abbreviation>_<methodname>`. This reduces the chance of naming conflicts. For example, `func_map` for the previously mentioned `map` method in `NSArray+Functional.h`.

# Project Organization

* Provide a `README` file with sufficient documentation for a new developer to get the project building, running, and deployed successfully.
* Never keep all your files in a single folder. Group classes and files first by module/use and then by type (`Views`, `ViewControllers`, `Helpers`, ...).
* All files included in an Xcode grouping should be located in a folder on-disk with an identical name and hierarchy.
* Always store the required Provisioning Profiles, certificates, etc. for an app in the project's source control.
* Build schemes, targets, profiles, etc. should not have spaces in their names. This simplifies the job for build scripts.

# Developer Center and iTunes Connect

* Provide registered devices with clear, concise names. Follow a naming standard such as `<Client>-<Name>-<Device Type>`. For example, `Dynamit-ColinDrake-iPhone6`.

---

# Footnotes

[^1]: The pitfalls of [Macro Parenthesis](https://docs.freebsd.org/info/cpp/cpp.info.Macro_Parentheses.html)
[^2]: [Dependency Injection in iOS](http://www.objc.io/issues/15-testing/dependency-injection/)
