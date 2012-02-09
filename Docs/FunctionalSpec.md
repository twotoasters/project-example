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

### Deployment Targets
	Supported devices/os versions should be listed here
- iOS 4.2+

---

## 1. Initial user experience 

### 1.1 Launch Splash Screen

#### Overview

Default launch screen is a static Default.png loaded at app launch. And then displayed for 3 seconds after the application has loaded.

#### Mockups

<img src="https://github.com/twotoasters/project-example/raw/master/Design/Mockups/Default.png" width="240px">

#### API Usage

- None.

#### Stories

- The user launches the app and is presented with a default launch screen
	- The user has already logged in and is routed to (1.2 Home)
	- The user is not logged in and is routed to (1.3 Login)
	
- The user launches the app and is routed to (1.2 Home), but the Access Token has expired or has been revoked.
	- The user is returned to 1.1 and then sent to (1.3 Login)


### 1.2 Home

#### Overview

The home view is the primary landing page for the application, it provides users a view of recently added albums. Users can also access other featured lists "Top Ten" and "Genres" via the top segmented control. 

#### Mockups

<img src="https://github.com/twotoasters/project-example/raw/master/Design/Mockups/screen1.png" width="240px">

#### API Usage

**GET** `/albums/new`

#### Stories

- The user launches the app and is presented with the home screen
- The user can see the top four featured albums with their special promotional images
- The user can tap on any of the top four featured albums images to go to the album details view 2.1
- The user can view a list of new release albums sorted by date
	- The user can see the album title, artist, average rating, rating count, and album art
- The user can tap on any of those albums in the list to go to the album details view 2.1
- The user can tap on the "Top Tens" or "Genres" segment button to go to 1.2.1 and 1.2.2 respectively
