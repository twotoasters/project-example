# Objective-C Style Guide

## Coding Styles

- Use soft tabs with 4-space indentation

````objective-c

if (someVal) {
    // 4 spaces
}

````

- Methods should have their `{` on a new line

````objective-c

- (void)completeActionWithObject:(NSObject *)object
{
	// implementation
}

````

- Use pragma marks to identify sections of your implementation. For example, all UITableView Data Source methods should be below a `#pragma mark`.

````objective-c

#pragma mark - UITableView Data Source Methods

- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView 
{
    return 1;
}

#pragma mark - My Custom Delegate Methods

- (void)myObject:(MyObject *)object didFindInformation:(MyInformation *)myInformation 
{
    // implementation
}

```` 

- Use a single empty line between functions

````objective-c

- (void)someObjectDidRespond 
{
    // implementation
}

- (void)someObjectWillRespond
{
    // implementation
}

````

## Documentation

Use the [appledoc](http://gentlebytes.com/appledoc/) style when you can to provide easy documentation with appledoc.

````objective-c

/** Designated initializer for creating an instance of this object
 *
 * @param object Requires an instance of class CustomObject to initialize
 * @returns an instance of class ThisClass fully initialized
 */
- (id)initWithObject:(CustomObject *)object;

````

## Naming 

### Project Naming and Layout

#### Project Layout

In Xcode, follow the following standard layout. All top-level Xcode groups should also follow the same pattern.

	SomeProj.xcodeproj
 	SomeProj
	├── Application | Framework
	│   ├── AppDelegate.h|.m
	│   ├── SomeProj-prefix.pch
	│   ├── Supporting Files
	|	|	├── Info.plist
	|	|	├── SomeProj-Info.plist
	│   ├── Categories
	│   ├── Protocols
	│   ├── Resources
	├── Model
	├── View
	├── Controller
	SomeProj-UnitTests
	SomeProj-IntegrationTests
	Libraries
	├── JSONKit
	├── RestKit

### Resource Naming

Resources should all be in the same Resource directory and organized as follows:

	ui.[view].[purpose].png
	ui.[view].[purpose]@2x.png

	ui.generic.[purpose].png
	ui.generic.[purpose]@2x.png

### Class Naming 

Whether they're a standard part of Cocoa or your own creation, class names are always capitalized. Class names should not be abbreviated and should be descriptive of the object you are modeling. You should always use the namespace prefix based on your current project.

	// Wrong
	ttSampleObject 
	TTSampleObjectRef
	SampleObject
	TTSampleObj
	
	// Correct
	TTSampleObject

### Method Naming

Method naming should follow [recommendations from Apple](http://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CodingGuidelines/Articles/NamingMethods.html#//apple_ref/doc/uid/20001282-BCIGIJJF). 

### Variable Naming

Variable names start with lower-case letters, but are internally capitalized wherever a new word appears:

	NSString *streetAddress = @"1 Infinite Loop";
	NSString *cityName = @"Cupertino";
	NSString *countyName = @"Santa Clara";

As we discussed, Cocoa strongly favors clear, distinct variable names over terse ones. Ambiguity frequently results in bugs, so be explicit. Variable names should not be abbreviated.

	// Wrong
	NSString *strAddr = @"1 Infinite Loop";
	
	// Correct
	NSString *streetAddress = @"1 Infinite Loop";

### Property Accessors

When creating properties, you should always synthesize the property with an instance variable prefixed with an underscore;

	// Header
	@property (nonatomic, copy) NSString *testString;
	
	// Implementation
	@synthesize testString = _testString;

### Protocol Naming

When creating protocols for use as delegates, you should alwasy model the method similar to how Apple names UITableView Data Source methods.

	// Wrong 
	- (void)finishedProcessing;
	- (void)finishedProcessingWithString:(NSString *)string;
	
	// Correct
	- (void)objectDidFinishProcessing:(NSObject *)object;
	- (void)object:(NSObject *)object didFinishProcessingWithString:(NSString *)string;

### Category Naming

Categories should be used when creating reusable extensions on existing classes. For example, creating a libray of custom colors:

	// Wrong
	#define BACKGROUND_COLOR [UIColor redColor]

	// Correct
	@interface UIColor (TTColorAdditions)
	
	- (UIColor *)TT_backgroundColor;
	
	@end

	@implementation UIColor (TTColorAdditions)
	
	- (UIColor *)TT_backgroundColor 
	{
		return [UIColor redColor];
	}
	
	@end


---

# Notes from meeting on 4/10

---

# Sample URLs of other Style Guides

- [GitHub's Ruby Guide](https://github.com/styleguide/ruby)
- [Apple's Guidlines](http://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.html)
- [Luke Redpath's Guide](http://lukeredpath.co.uk/blog/my-objective-c-style-guide.html)
- [Google's Objective-C Guide](http://google-styleguide.googlecode.com/svn/trunk/objcguide.xml)
- [Marcus Zarra's Guide](http://www.cimgf.com/zds-code-style-guide/)
- [CocoaDevCentral Cocoa Style for Objective-C - Part 1](http://cocoadevcentral.com/articles/000082.php)
- [CocoaDevCentral Cocoa Style for Objective-C - Part 2](http://cocoadevcentral.com/articles/000083.php)


# All Projects 

void function() 
{

}

---

NSString *string = @"";

---

if (someObj == nil) {

}

if (someObj) {

}

if (someObj != nil) {

}

if (! someObj) {

}

if (somethingReallyLong &&
 	(somethingElseReallyLong || 
 	 somethingElseReallyReallyLong)) {

	[self doSomething]; 	 
	[self doSomething]; 	 
}

@propery (nonatomic, assign, getter=isEditable) BOOL editable;

@synthesize editable = _editable;

BOOL _editable;

---

## Project Naming


## iOS/Mac

## Xcode Folder Structures

- SomeProj.xcodeproj
	- SomeProj
		- Application | Framework
			- AppDelegate.h|.m
			- SomeProj-prefix.pch
			- Supporting Files
				- Info.plist
				- SomeProj-Info.plist
				- ...
			- Categories
			- Protocols
			- Resources
		- Model
		- View
		- Contoller
	- SomeProj-UnitTests
	- SomeProj-IntegrationTests
	- Libraries
		- JSONKit
		- RestKit
		

## Image naming


## Workspaces

## Ternary 

One line, simple conditions

self.stringValue = isTrue ? @"YES" : @"NO";

or 

self.someObject = otherObject ? : nil;



## Logging



## Prefix

TT = Two Toasters
SXY = Sexy stuff
[project_prefix]_colorWithColor:

## Basic Coding Standards

### Header File Organization / What __is__ public?


### Blocks, Delegate naming 

- (void)object:(id)object willCompleteWithArg:(id)arg;
- (void)object:(id)object didCompleteWithArg:(id)arg;

## Android

## Ruby

