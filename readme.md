# Onboarding
Here is a couple of things to do and read to get you onboard asap !

## before_action
Be sure to have a good black and white picture of yourself ! You'll use it as a profile picture for Slack, Trello, GSuite, etc.

## Coding

### Technical Setup
There is no strict technical setup imposed, you can work with your custom shortcuts and own fancy terminal as long as it's convenient for you and the rest of the team:
- to version you code with **git** and collaborate with **Github**
- to work on Ruby On Rails projets with ruby versions installed and managed by **[rbenv](https://github.com/rbenv/rbenv)**.
	*The ruby and rails versions will vary from project to project. You'll have to install them accordingly.*
- to work on [Yarn](https://yarnpkg.com/en/) and [npm](https://www.npmjs.com/) package managed projects, either as a part of a larger Rails application or as a pure front end app.

Same thing apply for your editor: Sublime, Atome whatever you want as along as you're efficient with it :)

At this time *(September 2018)* everyone in the team has a configuration 100% inspired from **[Le Wagon Setup](https://github.com/lewagon/setup)** : **Do check it !**

### Poulpe Coding Conventions
There's no such thing right now ! For some projects we took time to write down some principles... for some others we didn't... some projects are brand new, some others... are not. Defining some conventions is on the agenda. Right now and generally speaking:
- for RoR we tend to agree with [these best practices](https://www.sitepoint.com/10-ruby-on-rails-best-practices-3/). (except for the *Fat Models, Skinny Controllers and Concerns* principle)
- for pure frontend app (React) we tend to like the [standard.js](https://standardjs.com/) convention
- for CSS we try to follow a component based approach and we try to take time at the start of the CSS dev to define the UIKit of the project.

At last, we're not big on linting and editor plugin and other cool stuff... so if you 're keen on rubocoping, let's share that on the upcoming projects !

### GitHub
We use GitHub to collaborate.

Right now *(Septembre 2018)*, the [Poulpe GitHub](https://github.com/Poulpes) is not an organisation account. We'll transition to an Organisation Account soon.

In the meantime, repo are created by the lead dev and access are given repo/repo by the lead dev.

On some projects, we use GitHub Wiki to write down app documentation. Generally speaking, we're trying to document our apps more and more through good PR and `.readme` files. (Check StackEdit 👇)

### Heroku
80% of our project are hosted on Heroku so make sure to have an account on it : either a new one with your *@poulpe.co* email or your current heroku account.

The `heroku-cli` tools come handy for working on our projects. Set up instructions are 👉https://devcenter.heroku.com/articles/heroku-cli.

The other 20% are either hosted on GitHub Pages, Scalingo or directly by the client.

SO, postmark, sendgrid, papertrail, amazon, cloudinary, etc. andfor desogns

### StackEdit
[StackEdit](https://stackedit.io) comes handy when to writing down your dev technical notes, preparing your PR, `.readme` files. It's free to use and you can sync files with Google Drive and GitHub.

### Other tools and services

[PostmarkApp](https://postmarkapp.com/), [SendGrid](https://sendgrid.com/), [Cloudinary](https://cloudinary.com/), [AWS](https://aws.amazon.com/fr/), [Gandi](https://www.gandi.net/fr), etc. are some other services, you'll come across. 

### Design

[Sketch](https://www.sketchapp.com/), [Invision](https://www.invisionapp.com/), [Figma](https://www.figma.com/)... depending on the projects, we may use different solution. 80% of the time we end up working with Sketch files.

## Project Management

### Principles
Each project is managed by a single project manager. 95% of the time, the project manager is also the lead dev of the project. (S)he is in charge of:
- dealing with the clients (requirements, explanations, more explanations, always more explanations)
- meeting the deadlines and getting everyone's concerned on time
- make sure everyone knows his/her what/why/when to do
- organising the dev among the team
- the architecture of the app an the main technical choices
- reading/commenting/merging the PR and deploying in prod
- following the time spent on the project

### Tools
Regarding tools and processes:
- Trello is our number 1 tool when managing project.
- Internal communication goes through Slack
- Emails are for external communication: Poulpes <-> Client
- Code is on GitHub other materials are stored on Google Poulpe's Team Drives
- Planning and scheduling is made easy with a well-informed Google Calendar

#### Trello
**Make sure to create an account on [Trello](https://trello.com) with your @poulpe.co address**. We'll add you to the team.

Every project has its own board. The precise name and number of lists may vary from projects to projects but you'll aways somehow find:
- an "INPUT" or "NOTES" card giving access to input data of the projects: requirements, maquettes, notes, etc.
- a backlog list
- an in-progress list
- a done list

We've been trying some other tools (GitHub issues, Jira, etc.) but Trello feels the more practical/convenient/simple to collaborate on each project and to onboard client in the project management process.

#### Slack
We use Slack... a lot for internal communications *(project related, agency related, life related, etc.)* and even for external communication with some clients.
- You'll be invited to join our slack: https://les-poulpes.slack.com/ with your *@poulpe.co* address.
- Be sure to download the Desktop App (https://slack.com/intl/fr-fr/downloads/osx)
- Be sure to setup your profiles with your B&W profile picture *(see before_action ☝️)*.

#### Email
You should have received an invitation to complete the creation of your *first_name@poulpe.co* GSuite account. You'll be using this email address for external communication and access to various service.

Using an email client or the Gmail interface, is up to you ! Instructions to set up your client can be found [here](https://support.google.com/mail/answer/7126229?visit_id=636734694420902249-1983367045&rd=1).

#### Drive
With your *@poulpe.co*  account you'll have access to our Team Work Drive. Each project has its own Drive Folder account with Input Data (requirements, mockup, etc.).

If you need to create materials *(other than code !)* such as explanatory notes, commented mockups, dev notes, data exports, etc.. 2 options:
1) It's only fo you ! It does not make any sense to share it with the rest of the team -> **Host it wherever you want but not in the Poulpe drive**
2) It makes sense to share it with the rest of the team... or someone may find it useful later on -> **Do store it in the `Ressources` folder of the project in the team drives**

If you don't know, default to option 2.

We encourage you to **sync/stream** the team drives to your local drive with the **Google Drive File Stream**. To do that:
- Install Google Drive File Stream either:
	- online: https://support.google.com/drive/answer/7329379 **(without uninstalling Google Drive 👇)**
	- with your terminal: `$ brew cask install google-drive-file-stream`
- Connect your *@poulpe.co* account and start syncing

If you want to keep your Personal Google Drive Back Up and Sync functionalities: no problem. Just be sure to keep the Google Drive Back Up and Sync add-on installed and connect to your Google personal account.

#### Calendar
We use Google Calendar for planning and scheduling purpose. With your *@poulpe.co* you'll have access to:
- everyone's calendar
- the team calendar (named the Team Calendar / poulpe.co_8m31vtbdv5k9o20ck8r7m2emfg@group.calendar.google.com)

The principles:
- Fill in your calendar ! It'll be shared and everyone we'll use it to check your availabilities when scheduling meetings or events
- Use the Team Calendar when creating an event concerning everyone in the team !

#### Nikabot
[Nikabot](https://www.nikabot.com) is a Slack Bot we're using to keep track of time spent on every projects. Once connected to the Poulpe Slack you'll receive a daily reminder around 6:30 to fill in your day activity: **Name of project | Time spent**.

With these logs, the project manager consolidate on a weekly basis the time already spent on the project and (s)he can
- anticipate delay and take the appropriate measures
- change features priority in the backlog
- check the economic health of the project

**Filling your Nikabot on daily basis is critical.**

#### Others
When creating/editing other documents we tend to stick to Google Apps: Google Docs, Google Sheet, Google Slides.

## A Poulpe's  Life

Here is a couple of topics related to our daily organisation and life.

### What am I gonna work on ?
When it comes to planning, we're deciding the "who's gonna work on what" by trying to optimise various factors:
- **Availability**
	Obviously, we're trying to smooth the workload of everyone.
- 
- the opportunity to work from A to Z on a project
- the level of skills required
- the technical affinity
- 
#### Yearly Meeting
### Meetings
### Side and side Project
### What time should I arrive ?
### Can I work from home ?
### Equipment


### Social Network

## A one last thing...
We'll be more than happy to get your feedbacks on this readme

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbNTE3MTA0NTM0LC01ODM4MDI2MTMsMjAxOT
c5NTA1MV19
-->