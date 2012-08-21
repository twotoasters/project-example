# Objective-C Style Guide

## Coding Styles

### Use soft tabs with 4-space indentation

````objective-c

if (someVal) {
    // 4 spaces
}

````

### Methods should have their `{` on a new line

````objective-c

- (void)completeActionWithObject:(NSObject *)object
{
	// implementation
}

````

### Use pragma marks to identify sections of your implementation. For example, all UITableViewDataSource methods should be below a `#pragma mark` defining that protocol.

````objective-c

#pragma mark - UITableViewDataSource

- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView 
{
    return 1;
}

#pragma mark - TTCustomProtocolDelegate

- (void)myObject:(MyObject *)object didFindInformation:(MyInformation *)myInformation 
{
    // implementation
}

```` 

### Use a single empty line between functions

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

### Constants should be used in place of literal statements. 

````objective-c

// Wrong
[self.view setFrame:(CGRect){ 22, 31.4, 320, 44 }];
[self.view setFrame:(CGRect){ 22 + 2, 31.4, 320, 44 }];
[[NSNotificationCenter defaultCenter] postNotification:@"OHAI-THERE" object:nil];

// Correct:

// Define the constant where it makes sense for the current scenario. For example, the frame sizes don't need to be global to the application and can be defined in the current class.

static const CGFloat kCustomViewFrameLeftOffset = 22.0f;
static const CGFloat kCustomViewFrameTopOffset = 31.4f;

// or

static const CGSize kCustomViewSize = (CGSize){ 320.0f, 44.0f };

// which then leads to 

[self.view setFrame:(CGRect){ kCustomViewFrameLeftOffset, kCustomViewFrameTopOffset, kCustomViewSize }];

// Offsets should be defined either as a constant or an in scope variable that describes it purpose. Error on the side of being more descriptive:

CGFloat leftOffsetFromFrame = 2.0f;
[self.view setFrame:(CGRect){ kCustomViewFrameLeftOffset + leftOffsetFromFrame, kCustomViewFrameTopOffset, kCustomViewSize }];

// Notification keys or other dictionary keys which are used in multiple locations in an application, should be defined in a `[project_prefix]Environment` header. 

extern NSString * const kTTNotificationsApplicationOffline;

// then in the '.m'.

NSString * const kTTNotificationsApplicationOffline = @"com.twotoasters.notifications.application-offline";

// which would then be used as:

[[NSNotificationCenter defaultCenter] postNotification:kTTNotificationsApplicationOffline object:nil];

````

### Constants should be preferred over the preprocessor (`#define`) when possible. 

`#define` uses the preprocessor to replace the values with the defined value or macro. For example, `#define SOME_VAL 3` replaces all samples of `SOME_VAL` with 3, but also you don't get the type safety of a constant definition of the value. Actual constants should be used in favor of preprocessor macros .

- [Preprocessor Smells](http://qualitycoding.org/preprocessor/)


### Blocks

When using blocks as a completion mechanism for UI updates, you may not know or choose the thread the block is being called on. In this case, it is best to use the "Call-Callback" pattern.

````objective-c

[myObject perfomBlock:^{
	// this could be on a background queue depending on the object's implementation. To modify the UI, you should explicitly perform it on the main queue.
	dispatch_async(dispatch_get_main_queue(), ^{
		// update UI.
	});

}];

````

### Don't initialize variables to 0 or nil in the init method; it's redundant. 

All memory for a newly allocated object is initialized to 0, so don't clutter up the init method by re-initializing variables to 0 or nil.

### NSInteger & CGFloat vs. int & float - Apple provided types should be preferred over their C types.

### Keep your header files simple a possible

The public APIs defined in the header files of the objects you create should only define what consumers should be able to call. Any methods or properties used solely by the class itself should be defined in a class extention in your implementation file.

````objective-c

@interface TTSomeObject ()
 	/// ... 
@end

````

If you need subclasses to have access to it's superclass' implemations, use a category to create a "protected" header.

You should even put 'non-public' protocols you are conforming to on your class extension:

````objective-c

@interface TTSomeObject () <UITableViewDelegate>
 	/// ... 
@end

````

## Documentation

Use the [appledoc](http://gentlebytes.com/appledoc/) style when you can to provide easy documentation with appledoc. These should be done on all public headers. If a private method is more complicated, it too should have a descriptive comment.

````objective-c

/** Designated initializer for creating an instance of this object
	@param object Requires an instance of class CustomObject to initialize
	@returns an instance of class ThisClass fully initialized
 */
- (id)initWithObject:(CustomObject *)object;

````

## Naming 

### Project and Class Prefixing 

Since objective-c doesn't expose namespacing, use prefixes to "namespace" classes and methods on categories.

	TT = Two Toasters
	[project_prefix]_colorWithColor:

### Project Naming and Layout

The top level of a project, should be structured as follows:

	README.md
	Rakefile
	Docs
	├──ProjectLog.md
	├──ReleaseLog.md
	├──FunctionalSpec.md
	├──APISpec.md
	Code
	├──**Code directory** defined below...

README should be updated to fully describe the process to build and test the application. Rakefiles should be used to automate build processes as much as possible.

Mockups should live in [InvisionApp.com](http://invisionapp.com) which is maintained by the design team. FunctionalSpec should link to shared mockups inside invision, **not in github**.

In the `Code` directory, the structure should mimic the groups in Xcode and follow this standard layout:

	SomeProj.xcodeproj
 	SomeProj
	├── Application | Framework
	│   ├── AppDelegate.h|.m
	│   ├── Supporting Files
	│   │   ├── en.lproj
	│   │   │   ├── InfoPlist.strings
	│   │   ├── SomeProj-Info.plist
	│   │   ├── SompProj-Prefix.pch
	│   │   ├── main.m
	│   ├── Categories
	│   ├── Protocols
	│   ├── Resources
	├── Models
	├── Views
	├── Controllers
	SomeProj-UnitTests
	SomeProj-IntegrationTests
	Libraries
	├── JSONKit
	├── RestKit

### Resource Naming

Resources should all be in the same Resource directory and organized as follows:

	ui-[view]-[purpose]~iphone.png
	ui-[view]-[purpose]~ipad.png
	ui-[view]-[purpose]@2x~iphone.png
	ui-[view]-[purpose]@2x~ipad.png

	ui-generic-[purpose]~iphone.png
	ui-generic-[purpose]@2x~iphone.png
	ui-generic-[purpose]~ipad.png
	ui-generic-[purpose]@2x~ipad.png

### Class Naming 

Whether they're a standard part of Cocoa or your own creation, class names are always capitalized. Class names should not be abbreviated and should be descriptive of the object you are modeling. You should always use the namespace prefix based on your current project.

````objective-c

	// Wrong
	ttSampleObject 
	TTSampleObjectRef
	SampleObject
	TTSampleObj
	
	// Correct
	TTSampleObject

````

### Method Naming

Method naming should follow [recommendations from Apple](http://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CodingGuidelines/Articles/NamingMethods.html#//apple_ref/doc/uid/20001282-BCIGIJJF). 

### Variable Naming

Variable names start with lower-case letters, but are internally capitalized wherever a new word appears:

````objective-c
	NSString *streetAddress = @"1 Infinite Loop";
	NSString *cityName = @"Cupertino";
	NSString *countyName = @"Santa Clara";
````

As we discussed, Cocoa strongly favors clear, distinct variable names over terse ones. Ambiguity frequently results in bugs, so be explicit. Variable names should not be abbreviated.

````objective-c
	// Wrong
	NSString *strAddr = @"1 Infinite Loop";
	
	// Correct
	NSString *streetAddress = @"1 Infinite Loop";
````

### Property Accessors

When creating properties, you should always synthesize the property with an instance variable prefixed with an underscore. As of Xcode 4.4, synthesize is no longer required on normal properties. The compiler automatically synthesizes properties with an "_" prefixed ivar. When defining properties via protocols, you'll still need to synthesize.

````objective-c
	// Header
	@property (nonatomic, copy) NSString *testString;

	// Implementation (when needed from protocol)
	@synthesize testString = _testString;
````

BOOL properties should define a getter that is prefixed with `is` or `has`.

````objective-c
	@propery (nonatomic, assign, getter=isEditable) BOOL editable;
````

### Protocol Naming

When creating protocols for use as delegates, you should alwasy model the method similar to how Apple names UITableView Data Source methods.

````objective-c
	// Wrong 
	- (void)finishedProcessing;
	- (void)finishedProcessingWithString:(NSString *)string;
	
	// Correct
	- (void)objectDidFinishProcessing:(NSObject *)object;
	- (void)object:(NSObject *)object didFinishProcessingWithString:(NSString *)string;
````

### Category Naming

Categories should be used when creating reusable extensions on existing classes. For example, creating a libray of custom colors:

````objective-c
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
````


## Sample URLs of other Style Guides

- [GitHub's Ruby Guide](https://github.com/styleguide/ruby)
- [Apple's Guidlines](http://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.html)
- [Luke Redpath's Guide](http://lukeredpath.co.uk/blog/my-objective-c-style-guide.html)
- [Google's Objective-C Guide](http://google-styleguide.googlecode.com/svn/trunk/objcguide.xml)
- [Marcus Zarra's Guide](http://www.cimgf.com/zds-code-style-guide/)
- [CocoaDevCentral Cocoa Style for Objective-C - Part 1](http://cocoadevcentral.com/articles/000082.php)
- [CocoaDevCentral Cocoa Style for Objective-C - Part 2](http://cocoadevcentral.com/articles/000083.php)