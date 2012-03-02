### Issues

Github issues will be our main tool to break down the large scale feature specifications in the Functional Spec, into small actionable stories. All development time will be tracked against github issues, QA will be performed using issues as a functional guide, and project status will be evaluated based on issue completion; so it is important to adequately break down the project spec into small enough issue sizes. 

All github issues should be assigned to a Milestone and one or more Labels as described in the following sections.

There are examples of good issues available in the `Issues` tab for this project


### Milestones

Milestones are larger collections of issues divided where possible into common sense units of user functionality. Most views in an app as defined in the functional spec should be their own distinct milestone with a set of issues related to the user stories on that view

There are examples of good milestones available in the `Issues` tab for this project

### Labels

- **Feature** - represents one aspect of user facing value *(User can tap cancel to dismiss modal view)*
- **Bug** - represents a defect in the implementation of a delivered story *(App crashes when you tap cancel)*
- **Chore** - represents a behind-the-scenes task required to implement a story *(Setup testing server in Sinatra)*
- **QA** - represents a feature/bug that needs extra attention in QA *(Check that the details view doesnt crash in landscape orientations)*
- **Design** - Represents a task that requires assets to complete or Design work to be performed

### Quality Assurance

QA should be performed throughout the development process.  QA Responsibilities include:

- Execution of test plan criteria 
- Test all recently closed Issues marked as Feature or Bug (see above)
- Follow up on Issues flagged with the QA label


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
Troubleshooting #22 - Discussing user authentication issue with Steve
Planning - Breaking out functional spec into github issues
````