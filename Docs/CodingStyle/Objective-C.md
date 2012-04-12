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




---

# Notes from meeting on 4/10

---


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

ui.<view>.<purpose>.png
ui.<view>.<purpose>@2x.png
ui.generic.<purpose>.png
ui.generic.<purpose>@2x.png

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

