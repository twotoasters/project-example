### Issues

Github issues will be our main tool to break down the large scale feature specifications in the Functional Spec, into small actionable stories. All development time will be tracked against github issues, QA will be performed using issues as a functional guide, and project status will be evaluated based on issue completion; so it is important to adequately break down the project spec into small enough issue sizes. 

All github issues should be assigned to a Milestone and one or more Labels as described in the following sections.

There are examples of good issues available in the `Issues` tab for this project

**Things to Remember**

- All Issues should have at least one label
- All Issues must be associated with a Milestone

---

### Milestones

Milestones are larger collections of issues divided where possible into common sense units of user functionality. Most views in an app as defined in the functional spec should be their own distinct milestone with a set of issues related to the user stories on that view

There are examples of good milestones available in the `Issues` tab for this project

---

### Labels

- **Feature** - Represents one aspect of user facing value *(User can tap cancel to dismiss modal view)*
- **Bug** - Represents a defect in the implementation of a delivered story *(App crashes when you tap cancel)*
- **Chore** - Represents a behind-the-scenes task required to implement a story *(Setup testing server in Sinatra)*
- **QA** - Represents a feature/bug that needs extra attention in QA *(Check that the details view doesnt crash in landscape orientations)*
- **Design** - Represents a task that requires assets to complete or Design work to be performed
- **Staged** - Represents a task that has been completed but not yet merged to Master.  This is a temporary tag.

---

### Code Review Process

- stuff goes here eventually

---

### Versioning of Builds

In order to log bugs for features that have been confirmed as finished on a specific build and to better track fixes and ensure that bugs are being regressed on proper builds, a standard versioning system is suggested below. The below standards will allow developers to easily assign finished stories, tasks, and fixed bugs to specific build versions. This will allow the testing group to sort stories, tasks and bugs by those build versions for focusing test runs and properly regressing fixed bugs.

#### Versioning Standards

Each project should follow the below standards for version naming when pushing a build to TestFlight or Hockey App. 

 - The format for versions will look as follows W.X.Y.Z 
 - W.X will be reserved for designating build numbers post launch and will conform to the standards for submission to Apple and Google
 - Y will be the number of the current sprint being worked on
 - Z will be the number of the build submitted to QA for testing with the initial build of a sprint being W.X.Y.0
 - The final approved build of a sprint will have a Z value of whatever the last build of the sprint is. 

#### Examples

 - The third build in sprint 5 would have the following version:  0.0.5.2
 - The final build in sprint 5 was the 8th build created it would have the following version: 0.0.5.7

#### In-App Version Display

Build versions should be displayed within our apps in the Help or About screen of the app to allow for quick viewing by testers versus having to leave the app and check the TestFlight or Hockey App for this information. This information could also help users and clients reference the build number when discussing issues, allowing them to determine if there is a need to update their app to a newer version. 

### Usage of Versioning

#### Developers

Developers will be required to assign a version to completed Stories, Tasks, and Bugs within Jira. This will allow testers to sort through these items using the version to determine completed stories they need to test and completed bugs that need to be regressed.

#### Testers

Testers will be required to assign a version to bugs being logged to inform developers as to which build the bug was found on.

---

### Quality Assurance

QA should be performed throughout the development process.  QA Responsibilities include:

- Execution of test plan criteria 
- Test all recently closed Issues marked as Feature or Bug (see above)
- Follow up on Issues flagged with the QA label

---


### Creating the Functional Specification Document

For each section in the document, insert something like this:

    <a name="1.2.1" />

    ### 1.2.1 Search Modal

Then, when you have a reference to that section, do it like so:

After the user has searched using the search modal view, [1.2.1](#1.2.1), the map will set a zoom level above the coordinates of the search

When viewed on Github the spec will now have a link to section that you can press to jump to that section in the document.

---

### Time Tracking

Harvest entries should follow one of the following templates

- **Coding** `#issue number` - `description`
- **Reviewing** `#pull request number`
- **Designing** `#issue number` - `description`
- **Troubleshooting** `#issue number` - `description`
- **Testing** `#issue number` - `description`
- **Planning** - `description`
- **Deploying** - `description`
- **Standup**
- **Source Code Management**

**Examples**

````
Coding #41 - User Sign Out
Reviewing #17
Troubleshooting #22 - Discussing user authentication issue with client
Planning - Breaking out functional spec into github issues
````
