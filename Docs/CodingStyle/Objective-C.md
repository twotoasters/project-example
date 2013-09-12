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

Use the name of the class for where applicable (ex: `UITableViewDataSource` not `Table View Datasource`) so that they can be clicked through to their definition.

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

### All values should have context. Avoid "magic numbers" (or strings).

Using literals are fine if they are given a context such as membership in a constraint or format string or as returned by a method such as `tableView:heightForRowAtIndexPath:`

If you are using a number in more than one place in the code and it represents the same thing then it should become a constant.

````objective-c

// Metrics Dictionary

// Wrong
[NSLayoutConstraint constraintsWithVisualFormat:@"H:|-5-[view]-5-|" options:0 metrics:nil views:views];
[NSLayoutConstraint constraintsWithVisualFormat:@"V:|-5-[view]-5-|" options:0 metrics:nil views:views];[[NSNotificationCenter defaultCenter] postNotification:@"OHAI-THERE" object:nil];

// Correct:

NSDictionary *metrics = @{ @"padding" : @5 };
[NSLayoutConstraint constraintsWithVisualFormat:@"H:|-padding-[view]-padding-|" options:0 metrics:metrics views:views];
[NSLayoutConstraint constraintsWithVisualFormat:@"V:|-padding-[view]-padding-|" options:0 metrics:metrics views:views];

// Notification keys or other dictionary keys which are used in multiple locations in an application, should be defined in a `[project_prefix]Environment` header. 

extern NSString * const kTTNotificationsApplicationOffline;

// then in the '.m'.

NSString * const kTTNotificationsApplicationOffline = @"com.twotoasters.notifications.application-offline";

// which would then be used as:

[[NSNotificationCenter defaultCenter] postNotification:kTTNotificationsApplicationOffline object:nil];

````

### Constants should be preferred over the preprocessor (`#define`)

Constants in global namespace should always start with a lowercase "k"

````objective-c

// Header
extern NSString * const kTTAPIBaseURL;
extern NSString * const kTTNotificationLocationUpdated;

// Implementation
NSString * const kTTAPIBaseURL = @"http://www.twotoasters.com";
NSString * const kTTNotificationLocationUpdated = @"com.twotoasters.notification.locationUpdated";

````

`#define` uses the preprocessor to replace the values with the defined value or macro. For example, `#define SOME_VAL 3` replaces all samples of `SOME_VAL` with 3, but also you don't get the type safety of a constant definition of the value. Actual constants should be used in favor of preprocessor `#define` constants.



- [Preprocessor Smells](http://qualitycoding.org/preprocessor/)


### Blocks

When using blocks as a completion mechanism for UI updates, you may not know or choose the thread the block is being called on. In this case, it is best to use the "Call-Callback" pattern.

````objective-c

[myObject perfomBlock:^{
	// this could be on a background queue depending on the object's implementation. 
	// To modify the UI, you should explicitly perform it on the main queue.
	dispatch_async(dispatch_get_main_queue(), ^{
		// update UI.
	});

}];

````

If your block is being copied it needs change all references to self to weak references. You should convert the weak reference back to a strong reference before dereferencing. 

You should turn your weak reference to self into a strong reference in the block if and only if another thread could change the retain count of self during the block's execution.

````
    // stack block
    void (^stackBlock)(void) = ^{
        [self updateUI];
    };

    stackBlock();

    // weak block
    __weak typeof(self) weakSelf = self;
    [apiClient perfomAction:^{
        [weakSelf updateUI];
    }];
    
    // weak block with potential for self to change
    NSInteger localInt = _someIvarInt;
    __weak typeof(self) weakSelf = self;
    [apiClient perfomAction:^{
        typeof(self) strongSelf = weakSelf;
        // ...
        [strongSelf updateUIWithInt:localInt];
    }];

````

Rule: You should always check that a block is not nil before executing.

### Dot syntax

Since it's more convenient than the original bracket syntax for calling methods, dot syntax is often OK to use even without a corresponding `@property`.

Dot syntax is not OK for class methods. For example, you would not call `NSApplication.sharedApplication` nor `NSObject.alloc`, but it's OK to call `@"Example string".length`.

In the "setter" case, any dot syntax instance method call is OK.

In the "getter" case, don't use dot syntax when the method returns `void` or is in the `init` family. So you would not call `tableView.reloadData` nor `[NSObject alloc].init`, even though `tableView.indexPathForSelectedRow` is OK.

### Don't initialize instance variables to 0 or nil in the init method; it's redundant. 

All memory for a newly allocated object is initialized to 0, so don't clutter up the init method by re-initializing variables to 0 or nil.

### NSInteger & CGFloat vs. int & float - Apple provided types should be preferred over their C types.

Note, use these types in the correct context. For example a CGFloat should refer to something that will eventually be passed back into Core Graphics, NSTimeInterval should only be used in place of a double if it is representing a time interval.

### Keep your public header files simple

The public APIs defined in the header files of the classes you create should only define what consumers should be able to call. Any methods or properties used solely by the class itself should be defined in a class extension in your implementation file.

````objective-c

#import <Foundation/Foundation.h>
#import "TTDataProtocol.h"

@class TTObjectManager;

typedef void(^TTAPICompletionBlock)(id response, NSError *error);

@interface TTAPIClient : NSObject

@property (readonly) NSManagedObjectContext *mainContext;

/** Fetch Items from the API for the specified page
@param page The page to load items from where page identifies the range of items to load. Required
@param completionOrNil A completion block to perform when the items are completed
*/
- (void)fetchItemsInPage:(TTPage *)page completion:(TTAPICompletionBlock)completionOrNil;

@end


----------------

#import "TTAPIClient.h"

@interface TTAPIClient ()

@property (readwrite) NSManagedObjectContext *mainContext;

@end

````

If you need subclasses to have access to it's superclass's implementations, use a category to create a "protected" header.

You should import your superclass header file and any public protocols your class conforms to. Other classes should be forward declared with `@class`.

You should even put 'non-public' protocols you are conforming to on your class extension:

````objective-c

@interface TTSomeObject () <UITableViewDelegate>
//
@end

````

## Documentation

Use the [doxygen](http://www.stack.nl/~dimitri/doxygen/) style for comments. These should be done on all public headers. If a private method is more complicated, it too should have a descriptive comment.

````objective-c

/** Designated initializer for creating an instance of this object
	@param object Requires an instance of class CustomObject to initialize
	@returns an instance of class ThisClass fully initialized
 */
- (id)initWithObject:(CustomObject *)object;

````

## Naming 

### Project and Class Prefixing 

Since objective-c doesn't expose namespacing, use prefixes to "namespace" classes and methods on categories. Prefixes should be three characters.

	TWT = Two Toasters
	[project_prefix]_colorWithColor:

### Project Directory Structure

The top level of a project, should be structured as follows:

	README.md
	Rakefile
	Docs
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
	│   ├── Environment.h|.m
	│   ├── Supporting Files
	│   │   ├── en.lproj
	│   │   │   ├── InfoPlist.strings
	│   │   ├── SomeProj-Info.plist
	│   │   ├── SompProj-Prefix.pch
	│   │   ├── main.m
	│   ├── Resources
	├── Models
	├── ModelControllers	
	├── Views
	├── ViewControllers
	SomeProj-UnitTests
	SomeProj-IntegrationTests
	Libraries
	├── JSONKit
	├── RestKit

This layout is a guideline but can be modified by the project lead as needed, what is important is to mirror the top level group structure in Xcode to folders on the file system and to maintain that structure as the project continues.

### Class Naming 

Whether they're a standard part of Cocoa or your own creation, class names are always capitalized. Class names should not be abbreviated and should be descriptive of the object you are modeling. You should always use the namespace prefix based on your current project.

````objective-c

	// Wrong
	ttSampleController
	TTSampleControllerRef
	SampleController
	TTSampleCtrlr
	NSHttpUrlRequest
	
	// Correct
	TTSampleObject
	NSHTTPURLRequest

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

Properties that are expressed as an adjective may define a getter that is prefixed with `is` or `has`.

````objective-c
	@propery (nonatomic, assign, getter=isEditable) BOOL editable;
````

### Protocol Naming

When creating protocols for use as delegates, you should model the method similar to how Apple names UITableView Data Source methods.

````objective-c
	// Wrong 
	- (void)finishedProcessing;
	- (void)finishedProcessingWithString:(NSString *)string;
	- (void)finishedProcessingWithString:(NSString *)string andImage:(UIImage *)image;
	
	// Correct
	- (void)objectDidFinishProcessing:(NSObject *)object;
	- (void)object:(NSObject *)object didFinishProcessingWithString:(NSString *)string;
	- (void)object:(NSObject *)object didFinishProcessingWithString:(NSString *)string image:(UIImage *)image;
````

### Category Naming

Categories should be used when creating reusable extensions on existing classes. For example, creating a libray of custom colors:

````objective-c
	// Wrong
	#define BACKGROUND_COLOR [UIColor redColor]

	// Correct
	@interface UIColor (TWTColorAdditions)
	
	- (UIColor *)twt_backgroundColor;
	
	@end

	@implementation UIColor (TWTColorAdditions)
	
	- (UIColor *)twt_backgroundColor 
	{
		return [UIColor redColor];
	}
	
	@end
````


## Sample URLs of other Style Guides

- [GitHub's Ruby Guide](https://github.com/styleguide/ruby)
- [Apple's Guidelines](http://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.html)
- [Luke Redpath's Guide](http://lukeredpath.co.uk/blog/my-objective-c-style-guide.html)
- [Google's Objective-C Guide](http://google-styleguide.googlecode.com/svn/trunk/objcguide.xml)
- [Marcus Zarra's Guide](http://www.cimgf.com/zds-code-style-guide/)
- [CocoaDevCentral Cocoa Style for Objective-C - Part 1](http://cocoadevcentral.com/articles/000082.php)
- [CocoaDevCentral Cocoa Style for Objective-C - Part 2](http://cocoadevcentral.com/articles/000083.php)
