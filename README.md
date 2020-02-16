# Chitter Challenge #

This app is a basic social media platform for Makers students based on the popular platform 'Twitter'.

Users can post messages about their learnings and thoughts, which all students can see. Currently there is no user functionality, students can post a username, but it is a bit of a free for all! Students can steal each other's usernames and edit/delete other student's posts. Might be time for a security update...

I created this programme as part of a challenge at [Makers Academy](https://makers.tech). See [Specification](#Specification) for more information on the programme's requirements.

* [Getting started](#Getting-Started)
* [Useage](#useage)
* [Running tests](#Running-tests)
* [Specification](#Specification)
* [How I built it](#How-i-built-it)


## Getting Started ##

1. Fork this repo, and clone to your local machine. Navigate into the folder.
2. Run the command `gem install bundle` (if you don't have bundle already)
3. When the installation completes, run `bundle`

## Useage ##

1. Connect to psql
2. Create the database using the psql command `CREATE DATABASE chitter;`
3. Connect to the database: `\c chitter;`
4. Open /db/migrations/01_create_bookmarks_table.sql and run the command in the file in your terminal.

This is a web app which you can run on your local server. You will need to use the command line and a browser. In the command line type:

```shell
$ rackup
```

Open your browser and visit [localhost:9292](http://localhost:9292/).
Enter your name and start playing!

## Running tests ##

1. Note: to run tests in your local environment you will need to set up the test database. Rerun steps 1-4 above in useage, but replace the database name with `chitter_test` - ie `CREATE DATABASE chitter_test;` and `\c chitter_test;`
2. In your command line type:

```shell
$ rspec
```

## Specification ##

See original challenge instructions [here](Challenge-instructions.md)

### User Stories ###

```
STRAIGHT UP

As a Maker
So that I can let people know what I am doing  
I want to post a message (peep) to chitter

As a maker
So that I can see what others are saying  
I want to see all peeps in reverse chronological order

As a Maker
So that I can better appreciate the context of a peep
I want to see the time at which it was made
```

*below stories still to be implemented*

```
As a Maker
So that I can post messages on Chitter as me
I want to sign up for Chitter

HARDER

As a Maker
So that only I can post messages on Chitter as me
I want to log in to Chitter

As a Maker
So that I can avoid others posting messages on Chitter as me
I want to log out of Chitter

ADVANCED

As a Maker
So that I can stay constantly tapped in to the shouty box of Chitter
I want to receive an email if I am tagged in a Peep

```

### Functionality ###

1. You don't have to be logged in to see the peeps.
2. Makers sign up to chitter with their email, password, name and a username (e.g. samm@makersacademy.com, password123, Sam Morgan, sjmog).
3. The username and email are unique.
4. Peeps (posts to chitter) have the name of the maker and their user handle.
5. Your README should indicate the technologies used, and give instructions on how to install and run the tests.

## How I built it ##

### Sequence Diagrams ###

User stories 1-3

![Sequence Diagram 1](public/README-images/excalidraw-sequence-diagram-1.png)

### Class Diagrams ###

1. 

| Object: |**Tweet**| | ||
|:------:|:------------:|:-:|:-:|:-:|
|**Attributes:**|Text|Time|Username|||
|**Class Methods:**|Create|All|Find|Delete

2. 

| Object: |**User**| | 
|:------:|:------------:|:-:|
|**Attributes:**|Username|email|password|
|**Class Methods:**|Create|Find |


### Database Designs ###

Table: Tweets

| id | username | tweet | time |  
|:--:|:-------:|:-----:|:----:|
| PK | FK(users) | string | time |  
|1|lookupdaily|"Would you look at the weather"| 2020-01-13 11:20 GMT |

Table: Users

| username | name | email | password | signup_date |
|:--------:|:-----:|:-----:|:--------:|:-----------:|
| string(PK) | string | string | string(authenticated?) | date |
|1|lookupdaily| Liz Daly | test@gmail.com| *** | 2020-01-13 11:00 GMT |

### Designing tests ###

When planning my code I thought about the tests I might need, and tried to order them by simplicity

#### Feature tests ####

1. When visiting app - user sees all tweets with a timestamp
2. User sees all tweets in reverse chronological order
3. User can sign up and gets a confirmation message
4. User can log in
5. User can add a tweet *when* logged in
5. User can log out


#### Unit Tests ####

1. Tweet.all runs a database query to show all tweets with time stamp
2. Tweet.all orders tweets in reverse chronological order
3. User.create adds a user to a database table
4. Object on user?? Adds a users details to session
5. Object on user?? Removes a users details from session
6. Tweet.create adds a new tweet IF session contains a user

#### Edge Cases ####

* Null fields
* User tries to sign up with a username or email that already exists
* User enters '' or "" in body

## Further Improvements ##

To complete the challenge this weekend, my main focus was to create a CRUD Database web app. I would like to return to this challenge and implement registration and user authentification which should allow the following developments:

* Tweets displayed in reverse time order
* If a user tries to create a peep when not signed in the app asks them to log in
* User can only see 'edit' and 'delete' buttons on peeps they have posted
* User can tag other users in peeps

I would also like to explore the use of Rake to pass Travis CI tests on pull request.