# Project Management

## Software Development Process

No matter the size of the application there are a lot of steps and people involved. It's key to have some well-defined process.

The process involves developers, product owners, clients, quality assurance, customer support, operations, and marketing teams

The process is important because the life cycle involves more than just writing an application. It can extend for years

### The Process

These steps can occur different depending on the application and the team.

1. Requirements - from client
2. Design
3. Implimentation
4. Verification
5. Release
6. Maintenance

#### Requirements

* Determined by our stakeholders, including our clients and product owners
* Define the **Minimum Viable Product (MVP)** and additional desired feature
* Revisted with every development cycle

#### Design

* Led by senior development team members, with review by stakeholders, operations, and technical team
* Answers questions about key aspects including:
  * Performance
  * Reliability
  * Security
  * Serviceability
* Output of design can include pseudocode, logic diagrams, ERD, data flow diagrams, wireframes, and prototypes

#### Implimentation

* Code is written by development team, who work closely with product owners, quality assurance (testers), and operations
* Task management is crucial to stay on schedule
* Implementation includes more than writing application code:
  * Writing tests
  * Writing documentation
  * Writing code to enable oeprations to deploy and maintain the application

#### Verification

* All code is then reviewed and tested during implementation by developers and quality assurance
* After code changes are accepted, they are verified by stakeholders
  * If requirements were not met, the implementation step is repeated

#### Release

* Release an application mostly involves operations, marketing, and customer support
* It can also involve third parties, such as cloud computing providers if the deployed environments are not owned and managed by the company
* Developers are responsible for addressing deployment inssues when the code doesn't run as expected in the deployed environment

#### Maintenance

* The process never ends when the application is realeased - it has to be maintained
* No application is bug free- customers find issues, and they need to be addressed and fix in a timely manner
* Features not included in the initial application release are often released later in updates
* Bug fixes and new features must not break existing functionality



## The Tools

#### Task and requirements managments

* Trello
* Jira
* GitHub Project

#### Code Development

Source Code Repository

* GitHub
* Bitbucket
* Gitlab
* Perforce

Text Editor (IDE)

* VS Code
* Visual Studio
* Vim
* Eclipse
* Intellij
* Atom
* Sublime

#### Testing

Unit Testing (Language Dependent)

* Mocha
* Jest
* Rspec

Integration testing

* Cypress
* Selenium

#### Collaboration and Documentation

Collaboration

* Slack
* Zoom
* Google Hangout

Documentation

* GitHub README.md
* Wikis
* Google Drive
* Confluence
* Internal Company Website

#### Release and Maintenance

Issue Tracking

* Jira
* GitHub
* Trello

Deployment

* AWS
* Netlify
* Heroku
* CI/CD tools (Octopus Deploy, CircleCI, Travis, etc.)

## The Methods

#### Waterfall

All requirements, designs, schedules, and expected end products are agreed upon firmly between the development team and client before any development begins.

##### Waterfall - Pros

* As a developer, you know exactly what you will have to produce before you even start because you work with completed designs and well-defined expected results
* As a project manager, you have a clear idea of when the completed product will release because everything is well and completely documented

##### Waterfall - Cons

* It takes longer to get something released because there's so much documentation required
* When problems happen (and they will), there is little or no room to recover, which often leads to delivering late
* You rarely deliver what the client actually wants (even though it's what they THOUGHT they wanted), and no one knows until the very end!

#### Agile

An iterative approach to development, where work is broken down into user stories (user A does action B to get result C) which are released to the client as soon as they are done.

##### Agile - Pros

* As soon as basic requirements are understood, you can start coding and providing something to the client
* Less formal documentation makes happy coders
* More likely to produce what the client actually wants

##### Agile - Cons

* For the developer and client, it can feel chaotic if it's not well-managed
* Gives the client license to change their mind - which can result in unplanned rework and exploding scope and cost

## Introduction to Agile Project Management

### What is AGILE?

An ITERATIVE approach to managing software development

Aims to ensure that we develop WHAT THE CLIENT WANTS with OPTIMAL WORKLOAD for all developers with the best EFFICIENCY

#### Agile Manifesto

[Agile Manifesto]:https://agilemanifesto.org/

<u>**Individuals and interactions**</u> over process and tools

<u>**Working Software**</u> over comprehensive documentation

<u>**Customer collaboration**</u> over contract negotion

<u>**Responding to change**</u> over following a plan

That is, while there is value in the items on the right, we value the items on the left more

##### Some Key Principles

* Short Development cycles

  *Deliver working software frequently, from a couple of weeks to a couple of months, with a preference to the shorter timescale*

* Welcome Change

  *Welcome changing requirements, even late in development. Agile processes harness change for the customer's competitive advantage*

* Active participation of stakeholder

  *Business people and developers must work together daily through the project*

* Reflection

  *At regular intervals, the team reflects on how to become more effective, then tunes and adjusts its behaviour accordignly* 

### Agile Processes

#### How is Agile done?

* Planning: user stories with estimates, agreement from the client/stakeholders
* Tracking: Jira or Trello board
* Collaborating: standups and client meetings
* Iterating: incorporating client feedback and lessons learned
* Deploying: frequent released of working product to the client
* Retrospective: take a look back before moving forward again

#### Two common methodologies

* Scrum
  * FIXED CYCLE lengths with well-defined meetings for planning, working, and reflection
* Kanban
  * CONTINUOUS releases with Work In Progress (WIP) limits and less rigidly defined meeting structure

#### Common Terminology

* Scrum - the methodology or a team participating in scrum
* Iteration - on release of a product in scrum
* Sprint - one development cycle in scrum. There are multiple scrums in an iteration
* Stakeholders - people interested in the outcome of the project, i.e., the client and product owners
* Backlog - wish list of work and technical debt (existing code that needs refactoring) that is not planned for the current iteration

### User Stories

* User stories are the smallest unit of work, expressed from the perspective of the user

  *"As a [persona], I [want to], [so that]"*

* Implementation independent - focus on the who and what, not the how

* Clearly defined user stories make development easier

  * Easier to estimate (how many hours or days to complete?) and prioritise (from client's view)
  * Defined as done when the user can perform the task and gets the expected result

#### User stories examples

Consider a two-sided marketplace for buying and selling used video games. A couple of user stories might be:

* As a game seller, I want to be able to update sale prices of the games I'm selling so I can respond to the buyer demand.
* As a game buyer, I want to sort games for sale by their condition so I can view games in the best condition first.

#### Stakeholder agreement

* But wait - before you start coding, make sure everypone is on the same page
* Have a planning meeting with stakeholders to discuss the user stories and prioritsation
* Make adjustments if needed based on feedback
* End the meeting when everyone agrees to the current plan

## Using Trello

#### Project Management with Trello

* Define work streams in lists
  * Backlog (unplanned work)
  * To Do (Planned work that is ready to do)
  * In Progress
  * Review/Testing
  * Done
* Your lists may be different - decide what works as a team
  * Will be different for scrum vs kanban

#### Trello Cards

* Create on card for each user story
* Add sub-tasks, storuy points, size, or time estimate, due dates
* If estimated effort is more than a day's work, make it smaller
  * Depending on the length of the iteration, may want even smaller chunks
* Prioritise cards in lists (both backlog and to do)
  * When the team is ready to work (start of iteration/sprint in scrum), assign cards to team members and move to In Progress

## Reflection

#### Retrospective

It's Important to have a look at what was accomplishe after you release to the client

* In scrum, have a wrap up meeting at the end of the iteration, after the productd is released to the client
* In Kanban, you may do this after some agreed set of funtion (stories) is released to the client
* In either case, go over
  * What worked and what didn't
  * Agree on ways to improve going forward - not the product, the process

