# Onboarding
Here is a couple of things to do and read to get you onboard asap!

### before_action
Be sure to have a good picture of yourself! You'll use it as a profile picture for Slack, Clubhouse, GSuite, Steeple, etc.

## General info

### Offices
The office is located at 11 avenue Parmentier, 75011 Paris. We will give you the codes and a key of the office.
**COVID Note**: Right now, we're trying to work from home as much as possible. We'll see how to plan some "field" days to start !

### What time should I arrive/start ?
- Start before 10am

### Hardware
Upon you arrival, you should receive:
- a recent version of a Mac Book Pro 13", either brand new or recent and formatted
- a wireless mouse and keyboard
- a spot within the Product / Tech Team with a chair and a second screen
If you need any pencils, notebook, etc. feel free to ask Christophe, our Happyness Manager.

### GSuite Organization
A @woo.paris email address will be created for you. This email address will let you access all our GSuite ressources: email, calendar, drives, etc.

### Tools
Regarding tools and processes:
- Clubhouse is our number 1 tool when managing product sprints.
- Internal communication goes through Slack
- Emails are for external communication: WOÔ|Poulpes <-> Client
- Code is on GitHub other materials are stored on Google Team Drives
- Planning and scheduling is made easy with a well-informed Google Calendar

#### Github
We use GitHub to collaborate, you'll be part of the [Poulpe GitHub](https://github.com/Poulpes) organisation.

#### Clubhouse
We'll add you to the [Clubhouse](https://clubhouse.io/) organisation **with your @woo.paris address**.

#### Design
[Sketch](https://www.sketchapp.com/), [Invision](https://www.invisionapp.com/), [Figma](https://www.figma.com/)... depending on the projects, we may use different solution.

#### Slack
We use Slack... a lot for internal communications, logs, bugs monitoring, lead acquisition, time tracking, etc.
- You'll be invited to join our slack: https://woo.slack.com/ with your *@woo.paris* address.
- Be sure to download the Desktop App (https://slack.com/intl/fr-fr/downloads/osx)
- Be sure to setup your profiles with your profile picture *(see before_action ☝️)*.

#### Email
You should have received an invitation to complete the creation of your *first_name@woo.paris* GSuite account. You'll be using this email address for external communication and access to various service.

Using an email client or the Gmail interface, is up to you! Instructions to set up your client can be found [here](https://support.google.com/mail/answer/7126229?visit_id=636734694420902249-1983367045&rd=1).

#### Drive
With your *@woo.paris*  account you'll have access to our Drive. Each project has its own Drive Folder account with Input Data (requirements, mockup, etc.).

If you need to create materials *(other than code !)* such as explanatory notes, commented mockups, dev notes, data exports, etc.. 2 options:
1) It's only fo you! It does not make any sense to share it with the rest of the team -> **Host it wherever you want but not in the WOÔ drive**
2) It makes sense to share it with the rest of the team... or someone may find it useful later on -> **Do store it in the `Ressources` folder of the project in the drives**

If you don't know, default to option 2.

#### Calendar
We use Google Calendar for planning and scheduling purpose. With your *@woo.paris* you'll have access to everyone's calendar.
- Fill in your calendar! It'll be shared and everyone we'll use it to check your availabilities when scheduling meetings or events

#### Nikabot
[Nikabot](https://www.nikabot.com) is a Slack Bot we're using to keep track of time spent on every projects/products. Once connected to the WOÔ Slack you'll receive a daily reminder around 6:30pm to fill in your day activity: **Name of project | Time spent**.

With these logs, we consolidate on a monthly basis the time already spent on the project and (s)he can
- anticipate delay and take the appropriate measures
- change features priority in the backlog
- check the economic health of the project
**Filling your Nikabot on daily basis is critical.**

#### Steeple
Steeple is an Entreprise Social Network, news and "fun" are shared on the platform. You will be invited with your _@woo.paris_ email.

#### Other technical tools and services

80% of our project are hosted on Heroku so make sure to have an account on it: either a new one with your *@woo.paris* email or your current heroku account.
The `heroku-cli` tools come handy for working on our projects. Set up instructions are 👉https://devcenter.heroku.com/articles/heroku-cli.
The other 20% are either hosted on GitHub Pages, Scalingo or directly by the client.

[PostmarkApp](https://postmarkapp.com/), [SendGrid](https://sendgrid.com/), [Cloudinary](https://cloudinary.com/), [AWS](https://aws.amazon.com/fr/), [Gandi](https://www.gandi.net/fr), [Notion](https://www.notion.so/), etc. are some other services you'll come across.

### Salary
In order to be paid, please complete your profile on Payfit 😅 It's also on Payfit that you can arrange your holidays 🕶.

### Health Insurance
[Wemind](https://www.wemind.io/) is our Health Insurance. You will have an account and be able to track your health processes there. In case of problem, don't hesitate to ping @naomi our HR Manager.

## Coding

### Technical Setup
There is no strict technical setup imposed, you can work with your custom shortcuts and own fancy terminal as long as it's convenient for you and the rest of the team:
- to version your code with **git** and collaborate with **Github**
- to work on Ruby On Rails projets with ruby versions installed and managed by **[rbenv](https://github.com/rbenv/rbenv)**.
> *The ruby and rails versions will vary from project to project. You'll have to install them accordingly.*
- to work on [Yarn](https://yarnpkg.com/en/) and [npm](https://www.npmjs.com/) package manager projects, either as a part of a larger Rails application or as a pure front end app.

Same thing apply for your editor: Sublime, VSCode, Atom whatever you want as along as you're efficient with it :)

At this time *(January 2020)* everyone in the team has a configuration 100% adapted from **[Le Wagon Setup](https://github.com/poulpes/setup)**: **Do check it !**

### Poulpe Conventions
There's no such thing right now! For some projects we took time to write down some principles... for some others we didn't... some projects are brand new, some others... are not. Right now and generally speaking:
- for RoR we tend to agree with [these best practices](https://www.sitepoint.com/10-ruby-on-rails-best-practices-3/). (except for the *Fat Models, Skinny Controllers and Concerns* principle)
- for pure frontend app (React) we tend to like the [standard.js](https://standardjs.com/) convention
- for CSS we try to follow a component based approach and we try to take time at the start of the CSS dev to define the UIKit of the project.

### Getting to know the codebase
Be patient, you'll have the time to meet the codebase ! On your first days we'll share with your our main YOÔ Paris repo wiki with getiing started instructions and additionnal introduction.

## A Poulpe's  Life

Here is a couple of topics related to our daily organisation and life.

### Sprints / Routine
You'll quickly get to know our product / development routine. Basically it works like this:
- **Tuesday Week 0 - Sprint Kickoff**
> New stories are introduced and discussed from a product and technical point of view. Developpers ask questions about some details (product/tech wise), précisions, mockups, etc. A reviewer of te story is designated and a number of points is estimated by the team for the story. The owner of the story has already been assigned by Karine and Thomas previously _(see Whath am I gonna work on ? 👇)_.

- **Wednesay Week 0 - 1-1 with Thomas**
> Now it's the time for a private 1-1 with Thomas to discuss everything: technical difficulties, wishes, frustrations, etc.

- **Friday Week 0 - Mid Sprint Team Meeting**
> Due to Covid, we've added a new team meeting on friday, just to catch up with everyone. Time to share your update on your work and also time to hear about customers and products stories with Aurelia .

- **Tuesday Week 1 - Mid Sprint Team Meeting**
> Quick followup on everyone's work !

- **Wednesay Week 1 - 1-1 with Thomas**
> Yes, the 1-1 with Thomas are weekly !

- **Friday Week 1 - Sprint End Team Meeting**
> End of the sprint team meeting: catchup with everyon's work, problems reviews.

### What am I gonna work on ?
When it comes to planning, we're deciding the *who's gonna work on what ?* by trying to optimise various factors:
- **Availability**
	Obviously, we're trying to smooth the workload of everyone.

- **Technical affinity and skills**
	The basics:
	- You're a frontend expert and you don't want to know what's a migration ? You're not gonna work backend.
	- You're a junior backend dev, you won't be in charge of the app architecture *...but you'll have time to discuss it with the lead dev*.

	In addition, we're trying to meet your development expectation:  You're backend but you're keen on learning some frontend, we'll do our best to accommodate it. This will happen as long as:
	- you'll tell us ;) (yearly meetings 👇)
	- it does not jeopardise the whole planning
	- we have the opportunities

- **Team rotation**
	Ideally we want everyone to have the opportunity to work with everyone.

### Technical Articles
Apart from building things... we also want to write product or technical related articles. We've published [one](https://medium.com/@agencepoulpe/le-marketing-dinfluence-a-son-bar%C3%B4m%C3%A8tre-1caa520c7d50) about YÔO and one about [resteo](https://medium.com/@agencepoulpe/de-la-data-analytics-en-restauration-ebe9c4d86e23) and we plan to carry on a ~~monthly~~ ~~tri-monthly~~annual basis. (*oupsy*) If you fancy writing stuff, you'll have a chance.

The point is, if you want to contribute by:
- shipping features on Poulpe side projects
- packaging librairies or tools
- helping organising parties
- suggesting/designing/prototyping new products/services
- writing down articles
- sharing resources and increasing Poulpe's knowledge base
- presenting us some works
- participate on our social networks
- etc.

You're more than welcome!

