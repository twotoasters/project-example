# Project Functional Spec

## Version History
- 2011-11-14 Josh Johnson - Initial Version
- 2011-11-15 Josh Johnson - Updated after 11/15 Conference Call
- 2011-11-20 Josh Johnson - Updated after 11/20 Conference Call
- 2011-11-22 Josh Johnson - Removed unneeded items from pending, included answered questions, updated API

---

### General Questions

	Good place to place general questions and mark assumptions on the general functional spec of the application these 
	should be brought up with the client and clarified as well as documented here.

1. Is load screen really meant to be a progress bar? iOS load screens are static images.
2. Should the app support landscape mode? - Expecting no
don't display anywhere in current design mockups. This also doesn't specify if the matched username belongs to the user.
3. What happens when user is not connected to network?

### Minimum requirements for iOS App
	Supported devices/os versions should be listed here
- iOS 4

---

## 1. Initial user experience 

### 1.1 Launch Screen

#### Overview

Default launch screen is a static Default.png loaded at app launch. 

#### Screen Mockups

<img src="https://github.com/twotoasters/project-example/raw/master/Design/Mockups/Default.png" width="240px">

#### API Usage

- None.

#### Stories

- The user launches the app and is presented with a default launch screen
	- The user has already logged in and is routed to (x.x Connections)
	- The user is not logged in and is routed to (x.x Login View)
	
- The user launches the app and is routed to (x.x Connections), but the Access Token has expired or has been revoked.
	- The user is returned to the beginning of the process for authenticating the service that has expired and sent to (x.x Login)
