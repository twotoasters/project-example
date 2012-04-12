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

switch (someEnum) {
	case
}

@propery (nonatomic, assign, getter=isEditable) BOOL editable;

@synthesize editable = _editable;

BOOL _editable;

- (BOOL)isEditable {
	return _editable;
}

- (void)setEditable:(BOOL)editable {
	_editable = editable;
}

@interface CALayer ()

- (void)clearString;

@end

@implementation NSString (MYSTRINGADDITIONS)

- (void)clearString {
	self = @"Charlie";
}

@end



---

- (void)doSomethingAwesome 
{
	// do something big and sync
}

- (void)doSomethingAwesomeWithCompletionHandler:(void (^)(void))handler {
	[self doSomethingAsyncWithCompletion:^ {
		handler();
	}];
}


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

