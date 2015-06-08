# NSString
----
## Objectives:
1. Understand the basic nature of a string.
2. Learn the primary ways of manipulating strings.
3. Learn how to create an interpolated string (a.k.a. "format string").

## Introduction

We've already mentioned that a string is a type of variable which is used to store information as text. You can think of a string as "a string of characters". While they can have slightly different mechanics between languages, they are common among all higher-level programming languages. In Objective-C, the base string class is `NSString`. 

**// Flat-fact:** *The* `NS-` *prefix on the Objective-C classes in the CoreFoundation library refer to the NeXTSTEP computer, the product of Steve Jobs' company NeXT, Inc. He had founded it in 1976 but focused on it after he was forced out of Apple in 1985. Apple later acquired NeXT, Inc. in 1997 and the NeXTSTEP operating system became part of the framework for Mac OS and iOS.*

We've already shown a few examples of the methods on `NSString`, namely `uppercaseString`, `lowercaseString`, and `stringByAppendingString:`. These are just a few of the ways you can manipulate strings.

## Creating Strings

In the previous examples, we've already shown how to create a simple string using the "string literal" syntax:

```objc
NSString *welcome = @"Welcome to the Flatiron School!";
```
It's that easy. 

There are many ways of creating strings, but this is the most common, especially for static strings.

**Top Tip:** *Avoid naming your variables directly after their class name, e. g.* `NSString *string` *or* `NSInteger integer`. *A variable's purpose should be obvious just from its name. In most cases, you can find a much more descriptive name than simply the name of its class. While you'll see variable names like* `NSString *myString` *in answers on help forums such as Stack Overflow, they are intentionally generic for the scope of the question.*

## Manipulating Strings

### Changing a String's Case

Manipulating the case of a characters in a string can sometimes be useful. Calling `lowercaseString` converts all of the uppercase characters to lowercase characters, calling `uppercaseString` does the opposite, and calling `capitalizedString` will capitalize only the first letter of each word, as separated by a space or punctuation mark.

***A Note on Type Cases:***

The Objective-C language utilizes a fusion of what are called "camel case" and "capital case." Both of these omit spaces in favor of capitalizing the first letter of each word. They differ in that camel case begins with a lowercase letter, while capital case begins with an uppercase letter.

```
camelCaseIsUsedToNameInstanceVariablesAndMethods
CapitalCaseIsUsedToNameClasses
```
Some other cases include:

```
PascalCaseIsAnotherNameForCapitalCase
hypen-case-is-common-in-bash
snake_case_is_common_in_windows
```
It is considered good practice to use camelCase for variable and method names, and reserve capital case for class names. We'll explain this distinction between instances and classes in a later reading; for now, just recognize that there *is* a distinction.

**Top Tip:** *When typing a name in camel case which begins with an acronym, it is considered good practice to type the entire acronym in lowercase, as in* `apiClient` *and* `jsonResponse`. *However, you will notice that Apple does not follow this guideline on the framework methods.*

### String Length

Sometimes you need to know how many characters are in a string—usually one that you won't have until run time (perhaps one provided by a user). Every `NSString` variable automatically keeps track of how many characters it contains. There's a simple method named `length` that will ask the recipient string how many characters it contains in the form of an `NSUInteger`.


```objc
NSString *username = @"mark";
NSUInteger usernameLength = [username length];

NSLog(@"%lu", usernameLength);
```
This will print the string's length which is `4`.

### String Concatenation

The act of combining strings is often referred to as "concatenation". Objective-C methods which concatenate strings typically contain the word "append", such as the `stringByAppendingString:` method.

```objc
NSString *welcome = @"Welcome to ";
welcome = [welcome stringByAppendingString:@"the Flatiron School!"];

NSLog(@"%@", welcome);
```

### String Division

If strings can be combined, then we can expect that they can be separated too. There are some handy methods which allow you to split a string based on a variety of criteria.


```objc
NSString *instructorNamesFromCSV = @"Joe,Tim,Jim,Tom,Mark";
NSArray *instructorArray = 
    [instructorNamesFromCSV componentsSeparatedByString:@","];

NSString *mark = instructorArray[4];
NSLog(mark);
```
This prints: `Mark`.

```objc
NSString *welcome = @"Welcome to the Flatiron School!";
NSString *where = [welcome substringFromIndex:15];

NSLog(@"%@", where);
```
This prints: `Flatiron School!`.

**Top Tip:** *The numbering of indexes begins at* `0`, *so the first character in a string is at "index 0". In the example above* `Flatiron School!` *begins at "index 15" or the 16<sup>th</sup> letter. This is true for array indexes also.*

### Replacing Substrings

The `stringByReplacingOccurencesOfString:withString:` method allows you to do just that—create a new string with each of occurence of the first substring replaced with a new substring. That could be something as simple as replacing an `&amp;` with the word "and".

```objc
NSString *instructorNames = @"Joe, Tim, Tom, Jim, &amp; Mark!";
instructorNames = [instructorNames 
    stringByReplacingOccurencesOfString:@"&amp;" withString:@"and"];

NSLog(@"%@", instructorNames);
```
This will print: `Joe, Tim, Tom, Jim, and Mark!`.

We can a run it a second time to replace each comma (`,`) with an exclamation point (`!`).

```objc
NSString *instructorNames = @"Joe, Tim, Tom, Jim, and Mark!"
instructorNames = [instructorNames 
    stringByReplacingOccurencesOfString:@"," withString:@"!"]; 

NSLog(@"%@", instructorNames);
```
This will print: `Joe! Tim! Tom! Jim! and Mark!`.

### String Comparators

You can compare two strings to see if they are a match. There are several methods of varying precision which you can use to do this. Using the `isEqualToString:` method will only evaluate as true (return `YES`) if the strings are exactly alike. This is useful for something like a password check:

```objc
NSString *password = @"p@ssw0rd";
BOOL isValidPassword = [password isEqualToString:@"p@ssw0rd"];

if (isValidPassword) {
    NSLog(@"Welcome to the Flatiron School!");
}
```
**Top Tip:** *A common mistake in comparing strings is using the* `==` *("is identical to") comparator which will only return* `YES` *if the two strings are the exact same instance. This will rarely be the case when comparing strings so the* `isEqualToString` *method—which evaluates if the strings are equivalent—will almost always be the check that you want.* 

There is the `caseInsensitiveCompare:` method which will ignore capitalization. It's equivalent to running `lowercaseString` on both strings and then comparing them with `isEqualToString:`, but that's more code and more work.

```objc
NSString *username = @"mark";
NSString *uppercaseUsername = @"MARK";

BOOL isUniqueUsername = [username caseInsensitiveCompare:uppercaseUsername];

if (!isUniqueUsername) {
	NSLog(@"That username is already taken.");
}
```

The `compare:options:range:locale` method family will be useful once you learn how to select these different parameter types. For now, just learn about the two methods above.

#### Converting to NSInteger

A number saved as a string is visible to the processor as text—that's fine for humans to read, but math can't be performed on it. To convert a string to an `NSInteger`, there's a handy method named `integerValue` that you can run on a string which contains a value that you wish to access. While there's a method to convert a string to each of the data types, here's an example of the `integerValue` method:

```objc
NSString *ageString = @"29";
NSUInteger age = [ageString integerValue];

age++;  // birthday party!

NSLog(@"%lu", age);
```
This will print: `30`.

There are also methods (namely `floatValue` and `boolValue`) for converting strings to other data types. We'll explain what these are in the next reading.

**Note:** *The* `<#type#>Value` *methods can only convert numbers from* `NSString` *which are in the* ***decimal number system.*** *You cannot convert from binary, octal, hexadecimal, or anything else, and failed conversions default to* `0`*!*

## String Interpolation (a.k.a. Formatting)

String formatting is useful when you need to create a string that contains other string variables. As in, the content of the string itself must vary during the application's run time. Any string can be set to the result of an interpolation that incorporates the values of other variables.

The anatomy of an interpolated string is in two parts:
   
   * the string that you wish to be formatted which includes the format specifiers, referred to as the "**format string**", and
   * the list of variables, separated by commas (`,`), which match up ***sequentially*** with a format specifier ***of the correct type*** in the format string.

The result of combining the listed variables into the format string is called the "**interpolation string**".

#### NSLog()

You've already been introduced to `NSLog()` by printing a simple string to the debugger console. However, as you may have noticed in the examples in these readings, `NSLog()` actually accepts a format string as its first argument followed by a theoretically-endless list of variables to include. As far as `NSLog()` is concerned, a simple string is just a format string without any formatters.

#### Format Specifiers

Format specifiers fulfill the role of designating where a value belongs within the format string. You'll primarily use `%@` for strings, though for integers and data types (which we'll explain later), the most common format specifiers which you'll use are:


| Specifier | Description |
|:---------:|:----------- |
| `%@`      | Variables which are not data types (i.e. `NSString`, `NSNumber`). |
| `%li``%ld`| `NSInteger` |
| `%lu`     | `NSUInteger` |
| `%f`      | `CGFloat` |


**Top Tip:** *The* `NSString` *notation for the '%' ("percent sign" or "modulus") itself is* `%%`. 

Xcode will suggest a change if you enter a format specifier which doesn't correctly match up with the type of the variable that it links to, so don't stress yourself out about memorizing [all of the different format specifiers](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/Strings/Articles/formatSpecifiers.html) available for you to use. Most of the ones not including in the table above only have specific situations for which you'll need them and Xcode should point them out to you anyway.

#### Creating an Interpolated String

In addition to `NSLog()`, you can submit a string interpolation to any method which calls for a "format" argument. Common methods which you'll see are `NSString`'s `stringWithFormat:` and `stringByAppendingFormat:` methods, `NSMutableString`'s `appendFormat:` method, and `NSPredicate`'s `predicateWithFormat:` method.

We mentioned above when discussing `NSLog()` that the anatomy of an interpolated string is in two parts, the format string, and the list of variables:
   
```objc
NSString *flatironSchool = @"the Flatiron School";
NSString *kawaiiFace = @"(づ｡◕‿‿◕｡)づ";

NSLog(@"Welcome to %@! %@", flatironSchool, kawaiiFace);
```
This will print: `Welcome to the Flatiron School! (づ｡◕‿‿◕｡)づ`.

**Top Tip:** *Be certain to close the format string with the trailing double-quote (*`"`*) before the comma (*`,`*) separating it from the first variable. A common mistake is wrapping the comma inside the double-quotes which then makes the comma a part of the format string and not part of your code. This causes the compiler to complain.*

Let's write a string interpolation which mixes a string variable with an integer variable:

```objc
NSString *mark = @"Mark";
NSUInteger marksAge = 29;

NSString *greeting = [NSString stringWithFormat:@"Hello, my name is %@! I am %lu years old", mark, marksAge]; 

NSLog(@"%@", greeting);
```
This will print: `Hello, my name is Mark! I am 29 years old`.

Did you notice how we called the `stringWithFormat:` method by sending it to `NSString` itself? That's because `stringWithFormat:`'s purpose is to create a new string—not to modify an existing string—so it's a method call that has to be sent to `NSString` itself. This makes `stringWithFormat:` a **class method**. We'll discuss this distinction in more detail when we talk about inheritance.


