Lecture 1 - Introduction
=========

#### Operation team ####
- Deploy
- Upgrade
- Support
- Raise and Track Issues

#### Development team
- Analyze
- Design
- Construct
- Deploy and Maintain

There is an overlap but development team mostly focus on before deployment. Operations team focuses after deployment.

Software Deployment is more than installing software.
Software Maintenance takes place after Software Deployment.
Software Maintenance is about correcting faults, improving performance or other attributes or adapting the product to a new environment.
Software Evolution is the outcome of Software Maintenance.

Software Evolution fits into `general laws` . Which are Lehman's Law:-

1. Continuing Change
2. Increasing Complexity
3. Self-Regulation
4. Invariant Work Rate
5. Conservation of Familiarity
6. Continuing Growth
7. Declining Quality
8. Feedback Driven

The Carzaniga Model 1998
![Software Deployment Process by Carzaniga](https://github.com/FeliciousX/HIT3311/blob/master/carzaniga_software_deployment_model.png?raw=true)

---

Lecture 2 - Deployment Fundamentals
=========
Focusing on the `Release` part of the Carzaniga Model
Steps in Release Activity:-
- Packaging
- Advertising

Types of Environments
- Development
- Testing
- Staging
- Live/Production

#### Package ####
A collection of files with instructions on what to do with them.
- Executables with required libs
- Meta-data
- Data files and Configuration Info

Example of Packaging methods are `ZIP`, `MSI`, `RPM`, `JAR`, `DEB`, `DMG`, etc.

#### Advertise ####
- Licensing
- Support
- Roadmap

##### Licensing #####
3 types of License:-
1. Highly Restrictive / Viral / Reciprocal (e.g. GPL)
2. Restrictive (e.g. LGPL, Mozilla)
3. Un-restrictive (e.g. BDS, Apache)

##### Support #####
Types of supports that can be given:-
- FAQ
- Email, IM or Telephone
- Issue Reporting
- Quick start Guide / User Manual
- Knowledge Base (Wiki)
- Discussion boards

##### Product Roadmap #####
Future plan of the product.
Improves customer confidence


Lecture 3 - Deployment - Install, Update and Retire
=========

## Install ##
Focusing on the `Install` part of the Carzaniga Model
Steps in Install Activity:-
- Transfer
- Configure

#### Transfer ####
Things to take into consideration while doing transfer (copying files):-

- location and file permission
- working with previous versions (SHOULDN'T THIS BE ON UPDATE? WTF)
    - override file? or multi-version?
- Checking component dependencies
- Co-ordination with multiple machines or multiple different softwares
- Content Delivery Issues
- Security
    - authorization & authentication required?
    - integrity checking? (MD5/SHA)
- Access to network
    - Needs to download missing libraries online

#### Configure ####
Once transferring is done and verified. We configure.

Things to take into consideration during configurations:-

- Registering components / libraries with OS (like Windows registry)
- Setting up data for the use in the environment (Dev, Test, Staging, Live)
- Setting up networking in a multi-system environment
- Security
    - Check file permissions to ensure product can be started up
- Configuration info must be in the `Package`

---

## Activate ##
Activate is the process of *starting-up* a software system

2 types:
- First time initial activation
- Normal activation

For a first time activation, it requires a configuration step. Additional things may be needed to be setup before product can be used.
Normally things like setting up cache files and initializing databases. Basically things that could not be done with an installer.

Activation should check
- system run-time integrity
- Authorization level
- License verification

Activation can also acquire locks on certain devices.

---

## De-Activate ##
De-Activate is the process of *shutting down* a software system

It should return all locks (on devices) and resources properly.
Partial de-activation support may be needed for many systems.

---

## De-Install ##
De-Install is the process of removing the software.

An ideal removal process should:-
- remove all software components / libraries that are unused by other system
- Un-register any libraries (Registry in Windows)
- Create an archive of data files

`ACID = (atomicity, consistency, isolation, durability) is a set of properties that guarantee that database transaction are processed reliably.`

---

## Update ##
Update Activity consists of `Transfer` and `Configure` . Just like `Install` .

While transferring, same issues needed to be considered as in `Install -> Transfer`
For `Update -> Configure` , data migration may need to be part of the configuration step.

---

## Adapt ##
The ability of the software to adapt to an external change

Things that can change:-
- External hardware and associated drivers (Video card, sound driver)
- External components (OS update)

Adaptation is generally triggered during the `Activation` step. Which makes sense.
Adaptation may trigger for an update to adapt.. or a fresh install..

---

## De-Release ##
De-Release consists of `Advertise` and `Retire`

This is the process of slowly removing support services and formally retiring a product

Normally triggered when a new release is created (depending on the type of SDLC) a previous release may be retired (For example Windows XP? )

These involves `advertising` . More like the inverse of `Release -> Advertise`.
Removing support. Removing development resources. Forcing licenses to expire.

Wait what? Forcing licenses to expire?

##### Timed Licensing #####
Some software systems are released under a timed license. You lease the software for a period of time and after that, it will cease to function.
A more effective De-Release model !
Commonly applied in large enterprise systems.

---

### Transactional Integrity ###
The following must maintain transactional integrity and might need authorization:-
- Install
- Update
- Adapt
- Active
- De-activate
- De-install

lol. Basically everything mentioned above.

Ideally... should be able to compensate for *power-failures* and *component failures*
or.. allow user to return to previous state

---

### Data Migration ###
is required when
- Installing over a previous version
- Updating components
- Adapting to changing external configuration

---

Lecture 4 - Deployment - Execution Approaches
=========
## Build Management ##
- Builds are numbers 1, 2, 3 ... 1523, 1524
- Environment is pre/post fixed to build numbers
    - e.g. T5162 (Test build 5162), S369 (Staging build 369), L337 (Live build 337)

## Deployment Approaches ##
- Manual
- Scripted
- Language Based
- Model Based

---

Lecture 5 - Deployment - Planning and Suppot
=========
### Framework for Planning ###
To plan deployment, we need information about:-
- Deployment Model (the scope)
- Constraints
    - Temporal (Time related)
        - How long will a deployment take?
        - How often do we need to deploy?
        - What is the acceptable downtime?
        - What was promised?
        - What was required?
    - Environment and Infrastructure
        - OS
        - Programming languages and culture
        - Bandwidth available vs needed
        - Security, Safety, Reliability and Legal aspects
        - Is it a fully managed or outsourced infrastructure?
        - Who owns the infrastructure?
        - Who manages the infrastructure?
        - Who is responsible for license management?
    - Automation
        - Level of automation
            - Manual , Scripted , Language , Model driven
        - Tooling and Experience of team performing the deployment
        - Availability of security permissions, tools and people to perform deployment
            - An issue when environment is controlled by an external hosting provider
    - Communication
        - Planning will need to take into consideration:-
            - Who needs to be notified?
            - Who can send out notifications? (Authorization for communication)
            - What will be communicated?
            - Support during/after the deployment process
            - How much notice is needed for downtime?

- Change pattern / properties
- Impact of deployment

### Data Migration ###
- Change
    - Data has an underlying schema
    - triggered by change (environment, upgrade, update, operations, error correction)
    - Types of change
        - Addition (e.g. Add new table)
        - Removal (e.g. Drop table)
        - Modification (e.g. Alter table , modify data)
- Approaches
    - Change will alter the database `schema`
    - Modify schema
    - Versioning the schema and data
- Strategy
    - when migrating information, must preserve the domain meaning (semantics)
    - ensures business rules and any transformations are persisted properly
    - software should provide an API for developers to pull meaningful data from database to ensure new version can import data from old version

---

Lecture 6 - Measuring Software
=========
## Measures vs Metrics ##
- *Metric* is a function measuring the distance between two objects
- *Measure* is a function mapping an attribute of a real world entity (domain) onto a symbol in a set with known mathematical relations (range)
- *Measurement* is the symbol assigned to the real world attribute by the measure. (cm, kg)

*Software Metrics* is any type of `measurement` which relates to a software system, process or related documentation

For example:-
- Lines of Code in a program
- Cyclomatic Complexity of a particular method
- the Fog Index (calculates readability of a piece of documentation)
- 0.4 x (( \# words / \# sentences) + (% words >= 3 syllables) )

In other words, `Software Measures` is a better word. `Software Metric` is widely used because people are often ignorant.

Metrics provide feedback when one is focused on a goal.

5 types Measurement Scales:-
1. Nominal
    - Puts item into categories (Human, Animal, Insects)
2. Ordinal
    - Ranks items in an order (Minor, Marginal, Major, Catastrophic)
3. Interval
    - We know the numeric scales and also the exact differences between the values (Time, Temperature in Celsius)
    - Does not describe absolute zero
    - You can + or - but cant x and /
4. Ratio
    - You can do multiplication and division!
    - Has absolute zero
    - e.g. Length of a table
5. Absolute
    - counting the number of elements in the entitiy set

Each scale captures more info than it's predecessor.

For a measure to be useful we need to know:-
- What is being measured?
- Scale of the measure (ratio? interval?)
- Range of the measure (possible values)

---

Lecture 7 - Growth in Software
=========
### Lehman's Law of Software Evolution ###
1. Continuing Change
    - After deployment, software continues to change in order to fix all the issues and meet core requirements
2. Increasing Complexity
    - Software evolution would cause its complexity to grow over time
3. Self-Regulation
4. Invariant work rate
    - Constant work rate over time
5. Conservation of Familiarity
6. Continuing Growth
    - More functions are added over time to adapt to new environment. Hence, growth.
7. Declining Quality
    - Software are seen as having a declining quality over time. To adapt and survive, it has to evolve.
8. Feedback driven

Why study growth?
- We can tell from the rate of growth if development is speeding up or slowing down.. or if it the rate is constant.
- We can understand the team is consistent with their release cycle or long breaks in between.

### Modelling Growth ###
Two dimensions in a study of growth:-
- Time
    - Release Sequence Number
        - Shows general trend
    - Calendar Time
        - Reveals the rhythm of a team
- Volumne / Complexity measure

### Types of Growth ###
1. Linear Growth
    - Complexity of system not causing a drag on the growth rate
    - Loosely coupled and modular architecture
    - If growth rate can be attribute to increase in team size, poor architecture.
    - Tools are being used to support productivity
2. Sub-Linear Growth
    - matches the expectation of Lehman's Law
    - Complexity is causing a drag on growth rate (with constant effort)
3. Super-Linear Growth
    - Plug-in based architectures

---

Lecture 8 - Growth and Change
=========
Types of Software Maintenance (Swanson, 1976):
1. Corrective
    - fixing bugs / issues / defects
    - correct processing, performance or implementation failures.
2. Perfective
    - adding features to meet expectation
    - perfecting system in terms of its performance, processing efficiency or maintainability
3. Adaptive
    - adjusting to meet external changes
4. Prevantative
    - maintenance of equipment or systems before fault occurs

So that was Swanson. Then comes Chapin in 2001 arguing that Software = Code + Documentation (I kinda agree?)

He came up with 12 types of Software Maintenance.
![Chapin Types of Software Maintenance](https://github.com/FeliciousX/HIT3311/blob/master/Chapin-Types_of_Software_Maintenance.png?raw=true)

and group them in 4 different *clusters*
1. Support Interface
    - Training
        - conducting classes for customer personnel
    - Consultive
        - confer with customer personnel / managers about the effective use of a system or the making of changes to the software
        - and advising customers / managers / stakeholders about the likely time, cost, activities, effort needed to do requested evolution / maintenance work
    - Evaluative
        - auditing
        - searching
        - examining
        - testing
        - calculating metrics
        - creating an understanding
2. Documentation
    - Reformative
        - restyles or changing the *format* of the documentation / user manual to make it better.
    - Updative
        - updating the content and coverage like replacing obsolete documentation and filling in gaps etc.
3. Software Properties
    - Groomative
        - making algorithms more elegant (easier to read but same performance)
        - Alter code readability / understandability
        - provide less-crytic error messages
    - Preventive
        - making changes that do not alter customer experience
    - Performance
        - reducing the amount of internal storage used
        - reducing the duration of out-of-service periods
        - speeding executing by replacing components
        - algorithms with faster ones
    - Adaptive
        - make system work cross-platform
        - able to use different types of database
        - changing communication protocols supported
        - changing design and implementation e.g. moving to OOP
4. Business rules
    - Reductive
        - eliminating or reducing data flow
        - limiting / eliminating some business rules from the implemented repertoire
        - replacing / constraining / removing part or all of some components or algorithms or subsystems
    - Corrective
        - refining implmentations of the existing business rules
    - Enhancive
        - Adding new stuff or functionality

### Maintenance Terminology ###
- Refactoring
- Re-engineering

A class is most likely to be:
1. Unchanged
2. Modified
3. Newly created
4. Deleted ( chance <1%)

---

Lecture 9 - Change
=========

Lecture 10 - Change and Review
==========

---

Glossary
========
- ACID (atomicity, consistency, isolation, durability) is a set of properties that guarantee that database transaction are processed reliably.
- J2EE Java Platform, Enterprise Edition
