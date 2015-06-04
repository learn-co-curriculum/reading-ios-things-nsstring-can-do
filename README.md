# NSString
----
## Objectives:
1. Understand the basic nature of a string.
2. Learn the primary ways of manipulating strings.
3. Understand string interpolation (string formatting).

## Introduction

As we've already mentioned that a string is a type of variable which is used to store information as text. While they can have slightly different mechanics, they are common among all higher-level programming languages. In Objective-C, the base string class is `NSString`. 

**// Flat-fact:** *The* `NS-` *prefix on the Objective-C classes in the CoreFoundation library refer to the NeXTSTEP computer, the product of Steve Jobs' company NeXT, Inc. He had founded it in 1976 but focused on it after he was forced out of Apple in 1985. Apple later acquired NeXT, Inc. in 1997 and the NeXTSTEP operating system became part of the framework for Mac OS and iOS.*

We've already shown a few examples of the methods on `NSString`, namely `uppercaseString`, `lowercaseString`, `capitalizeString`, and `stringByAppendingString:`. These are just a few of the way you can manipulate strings.

## Creating Strings

In the previous examples, we've already shown how to create a string:

```objc
NSString *welcome = @"Welcome to the Flatiron School!";
```

It's that easy.

**Top Tip:** *Avoid naming your instance variables after their class name, e. g.* `NSString *string` *or* `NSInteger int`. *While it's unlikely, doing this could cause the language to collide with itself. Be descriptive with your variable names. Their purpose should be obvious just from the variable name.*

## Manipulating Strings

### Changing a String's Case

Manipulating the case of a characters in a string can sometimes be useful. Calling `lowercaseString` converts all of the uppercase characters to lowercase characters, calling `uppercaseString` does the opposite, and calling `capitalizedString` will capitalize only the first letter of each word, as separated by a space or punctuation mark.

***A Note on Type Cases:***

The Objective-C language utilizes a fusion of what are called "camel case" and "capital case." Both of these omit spaces in favor of capitalizing the first letter of each word. They differ in that camel case begins with a lowercase letter, while capital case begins with an uppercase letter. It is considered good practice to use camelCase 

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

**Top Tip:** *When typing a name in camel case which beings with an acronym, lowercase the entire acronym, as in* `apiClient` *and* `jsonResponse`.

### String Length

Sometimes you need to know how many characters are in a string that you don't have (perhaps one provided by a user). Every `NSString` variable automatically keeps track of how many characters it contains. There's a simple method named `length` that will ask the recipient string how many characters it contains in the form of an `NSUInteger`.


```objc
NSString *username = @"mark";
NSUInteger usernameLength = [username length];

NSLog(@"%lu", usernameLength);
```
This will print the string's length which is `4`.

### String Concatenation

The act of combining strings is often referred to as "concatenation". The method call in Objective-C uses the word "append" to describe itself as a concatenation method.

```objc
NSString *welcome = @"Welcome to ";
welcome = [welcome stringByAppendingString:@"the Flatiron School!"];

NSLog(welcome);
```

### String Division

If strings can be combined, then they can be separated too. There are some handy methods which allow you to split a string based on a variety of criteria.


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

NSLog(where);
```
This prints: `Flatiron School!`.

**Top Tip:** *The numbering of indexes begins at* `0`, *so the first character in a string is at "index 0". In the example above* `Flatiron School!` *begins at "index 15" or the 16<sup>th</sup> letter. This is true for array indexes also.*

### Replacing Substrings

The `stringByReplacingOccurencesOfString:withString:` method allows you to just that—create a new string with each of its selected component type replaced with a new component. That could be something as simple as replacing an `&amp` with the word "and".

```objc
NSString *instructorNames = @"Joe, Tim, Tom, Jim, &amp Mark!";
instructorNames = [instructorNames 
    stringByReplacingOccurencesOfString:@"&amp" withString:@"and"];

NSLog(instructorNames);
```
This will print: `Joe, Tim, Tom, Jim, and Mark!`.

We can a run it a second time to replace each comma (`,`) with an exclamation point (`!`).

```objc
NSString *instructorNames = @"Joe, Tim, Tom, Jim, and Mark!"
instructorNames = [instructorNames 
    stringByReplacingOccurencesOfString:@"," withString:@"!"]; 

NSLog(instructorNames);
```
This will print: `Joe! Tim! Tom! Jim! and Mark!`.

### String Comparators

You can compare two strings to see if they are a match. There are several methods of varying precision that you can use to do this. Using the `isEqualToString:` method will only return `true` if the strings are exactly alike. This is useful for something like a password check:

```objc
NSString *password = @"p@ssw0rd";
BOOL isValidPassword = [password isEqualToString:@"p@ssw0rd"];

if (isValidPassword) {
    NSLog(@"Welcome to the Flatiron School!");
}
```
There is the `caseInsensitiveCompare` method which will ignore capitalization. It's equivalent to running `lowercaseString` on both strings and then comparing them with `isEqualToString:`, but that's more code and more work.

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

A number saved as a string is visible to the processor as text—that's fine for humans to read, but math can't be operated on it. To convert a string to an `NSInteger`, there's a handy method named `integerValue` that you can run on a string which contains a value you wish to access. There's a method to convert a string to each of the data types. Here's an example of the `integerValue` method:

```objc
NSString *ageString = @"29";
NSInteger age = [ageString integerValue];

age++;  // birthday party!

NSLog(@"%lu", age);
```
This will print: `30`.

There are also methods (namely `floatValue` and `boolValue`) for converting strings to other data types. We'll explain what these are in the next reading.

**Note:** *The* `<#type#>Value` *methods can only convert numbers from* `NSString` *which are in the* ***decimal number system.*** *You cannot convert from binary, octal, hexadecimal, or anything else, and failed conversions default to* `0`*!*

## String Interpolation (a.k.a. Formatting)

String formatting is useful when you need to create a string that contains other string variables. As in, the content of the string itself must vary during the application's run time. Any string can be set to the result of an interpolation that incorporates the values of other variables.

#### NSLog()

You've already been introduced to the function of `NSLog()` printing simple strings to the debugger console. However, `NSLog()` accepts an **interpolated string** as its first argument, and a theoretically-endless list of variables to include. The only limitation is that each variable must be matched up ***sequentially*** with a format specifier ***of the correct type*** in the interpolated string.

#### Format Specifiers

Format specifiers fulfill the role of designating where a value belongs within the interpolation string. You'll primarily use `%@` for strings, though for integers and data types (which we'll explain later), the common format specifiers you'll use are


| Specifier | Description |
|:---------:|:----------- |
| `%@`      | Description |
| `%li`     |  |





**Top Tip:** *The* `NSString` *notation for the '%' ("percent sign" or "modulus") itself is* `%%`. 

====^ Mark ^====

Woah, that sounds awfully fancy. Remember before when we NSLog'd our greeting?


```objc
NSString *greeting = @"Welcome to The Flatiron School!";


NSLog(greeting); // prints Welcome to The Flatiron School!
```
Well what if you wanted to say something else, as well your variable? 
Using variables, we can do this:


```objc
NSString *greeting = @"Welcome to The Flatiron School!";


NSLog(@"Hi, my name is Chris! %@", greeting); 
// prints Hi, my name is Chris! Welcome to the Flatiron School!
```
This is called *string interpolation* (don't worry about remembering the term), and what it means is that we can write an ordinary string and enter variables into it using *format specifiers*.


**Format specifiers are simply placeholders.** They always start with a % and have a single character depending on what type of variable is being passed in. The format specifier we use for strings is `%@`, as shown in the example.


Once a string has format specifiers in it, put a comma and list the variables that you want to enter as they appear in the string (in order!). So let's try it out:


```objc
NSString *myName = @"Tom";
NSInteger myAge = 24;


NSLog(@"My name is %@ and I am %ld years old.", myName, myAge);
// prints "My name is Tom and I am 24 years old." 
```
Here we see the `%@` gets replaced with `myName`, and the `%ld` gets replaced with `myAge`.


Documentation on format specifiers [lives here](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/Strings/Articles/formatSpecifiers.html). You can take a look, but **don't worry about memorizing them** — the important part is that you're aware of how these placeholders work. Plus, XCode has built-in features to help with these, and you'll start to remember after you use them enough times. :)


---
This may be a lot to take in all at once, but the best part is **now you have everything you need to know to start using variables in Objective-C!**

