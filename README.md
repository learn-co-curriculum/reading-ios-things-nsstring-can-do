#
#Things NSString Can Do

##Creating & Initializing Strings
```objc
+ (instancetype)stringWithFormat:(NSString *)format, ...

// Examples
NSString *name = @"Raylan";
NSString *fullName = [NSString stringWithFormat:@"%@ Givens", name];
```

##Getting a String's Length
```objc
@property(readonly) NSUInteger length

// Examples
NSString *randomSentence = @"Fun in the sun!";
NSUInteger sentenceLength = [randomSentence length]; // sentenceLength is equal to 15
```

##Getting Characters & Bytes
```objc
- (unichar)characterAtIndex:(NSUInteger)index

// Examples
NSString *randomSentence = @"Fun in the sun!";
[randomSentence characterAtIndex:2]; // returns 'n'
```

##Combining Strings

```objc
- (NSString *)stringByAppendingFormat:(NSString *)format, ...
- (NSString *)stringByAppendingString:(NSString *)aString

// Examples
NSString *nameTag = @"Chris";
[nameTag stringByAppendingFormat:@", Instructor @ The Flatiron School"]; // returns 'Chris, Instructor @ The Flatiron School'
[detailedNameTag stringByAppendingString:@", 11 Broadway, Suite 260, NY, NY 10004"]; // returns 'Chris, Instructor @ The Flatiron School, 11 Broadway, Suite 260, NY, NY 10004'
```

##Dividing Strings

```objc
- (NSArray *)componentsSeparatedByString:(NSString *)separator
- (NSString *)substringFromIndex:(NSUInteger)anIndex

// Examples
NSString *firstNames = @"Zach, Joe, Chris, Al";
[firstNames componentsSeparatedByString:@", "]; // returns [Zach, Joe, Chris, Al]

[firstNames substringFromIndex:6]; // returns 'Joe, Chris, Al'

```

##Replacing Substrings
```objc
- (NSString *)stringByReplacingOccurrencesOfString:(NSString *)target withString:(NSString *)replacement

// Example
NSString *genericGreeting = @"Hi! My name is Chris";
NSString *modifiedGreeting = [genericGreeting stringByReplacingOccurrencesOfString:@"Chris" withString:@"Joe"];
NSLog(@"%@", modifiedGreeting); prints 'Hi! My name is Joe!'

```

##Identifying & Comparing Strings

```objc
- (BOOL)hasPrefix:(NSString *)aString
- (BOOL)hasSuffix:(NSString *)aString
- (BOOL)isEqualToString:(NSString *)aString

// Examples

NSString *songInfo = @"Ben E. King - Stand By Me";
NSLog(@"%@", [songInfo hasPrefix:@"Ben E."] ? @"YES" : @"NO"); // prints YES
NSLog(@"%@", [songInfo hasSuffix:@"By Me"] ? @"YES" : @"NO"); // prints YES
NSLog(@"%@", [songInfo isEqualToString:@"Ben E. King - Stand By Me"] ? @"YES" : @"NO"); // prints YES
```

**Note-** these comparison methods are all case-sensitive

##Changing Case
```objc
@property(readonly, copy) NSString *capitalizedString
@property(readonly, copy) NSString *lowercaseString
@property(readonly, copy) NSString *uppercaseString

// Examples

NSString *bookTitle = @"a Walk among The tombstones";
NSLog(@"%@", [bookTitle capitalizedString]); // prints 'A Walk Among The Tombstones'
NSLog(@"%@", [bookTitle lowercaseString]); // prints 'a walk among the tombstones'
NSLog(@"%@", [bookTitle uppercaseString]); // prints 'A WALK AMONG THE TOMBSTONES'
```

##Getting Numeric Values

|data type| method call|
|------------|:--------------:|
|double|`@property(readonly) double doubleValue` |
|float|`@property(readonly) float floatValue`|
|int|`@property(readonly) int intValue`|
|NSInteger|`@property(readonly) NSInteger integerValue`|
|BOOL|`@property(readonly) BOOL boolValue`|

**Note**- to get the NSNumber value of an NSString, you must first convert the
NSString to an NSInteger (or CGFloat, int, float, etc.) and convert the result
into an NSNumber:

```objc
NSString *numericString = @"123";
NSInteger stringInteger = [numbericString integerValue];
NSNumber *convertedNumber = [NSNumber numberWithInteger:stringInteger]; // convertedNumber is equal to @123
```
