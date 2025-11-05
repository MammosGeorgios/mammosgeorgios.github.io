---
layout: default
title: Academy
permalink: /academy/02-downloading-repository
include_in_nav_bar: false
---


# Download academy repository

<!-- TOC -->
* [Download academy repository](#download-academy-repository)
  * [Creating a GitHub account](#creating-a-github-account)
  * [Getting access to the JAcademy project](#getting-access-to-the-jacademy-project)
  * [Download the project to our local environments](#download-the-project-to-our-local-environments)
    * [Cloning repository](#cloning-repository)
    * [Generating token](#generating-token)
  * [Explore project files and understand its structure](#explore-project-files-and-understand-its-structure)
  * [Running React](#running-react)
    * [Check / Download nodejs](#check--download-nodejs-)
    * [Prepare project](#prepare-project)
  * [Where is Python though???](#where-is-python-though)
  * [Running postgres with docker](#running-postgres-with-docker)
  * [Next steps and homework](#next-steps-and-homework)
<!-- TOC -->


## Creating a GitHub account

Instructions can be found [here](https://docs.github.com/en/get-started/start-your-journey/creating-an-account-on-github).
_We recommend you create an account with your personal email._

## Getting access to the JAcademy project

In order to have access, we need to invite you to the project, since it's not a public repository.

Email the instructors with the following format:
- Subject: Vol5 GitHub account
- Body: 
```
First Name
Last Name
GitHub username
```

_The email you need to use will be shown on the board - rather not have the work email commited on a public git page. :)_

Once you have done the process, try to access the following url:
[JAcademy Repository](https://github.com/PwC-Greece/jacademy)

If you have done everything you need, the project will be available to you now.

## Download the project to our local environments

Next step is to use git to download the repository in our computers.
**From now on, any command shown will be bash. As such, you MUST use git bash if you are a Windows user**

### Cloning repository
```bash
# Assuming you are already on a proper directory / folder
git clone https://github.com/PwC-Greece/jacademy.git
```
You are most likely going to me prompted for a username. Write the username you have on GitHub.

Next, you will be prompted for a password. **DO NOT USE YOUR GITHUB PASSWORD!**
Instead, we want to generate a token

### Generating token
- Open [GitHub](https://github.com)
- Login if you haven't already
- On the top right, click on your profile icon (or default picture if you haven't used an avatar _yet_)
- Choose Settings
- On the next [screen](https://github.com/settings/profile), from the left side menu, open `<> Developer Settings`
- Open the small menu of `Tokens (classic)`
- Pick `Generate new token` and select classic again
- As a note use something like `pwc-academy` - not important
- Select the following rights:
  - repo
  - user
  - project
- Keep the token handy somewhere for the next minutes

_**Note:** When in terminals, in order to paste something you need to use `Ctrl+Shift+V`!_ 

## Explore project files and understand its structure

Project structure is pretty straight forward:
- devops 
  - nginx
  - postgres
  - spring-app
- guides
- react-frontend
- spring-boot-backend

_Where is Python??_

## Running React

### Check / Download nodejs 
Prerequisites:
- nodejs 
- npm

You can find instructions for download [here](https://nodejs.org/en/download)

After installation, check for both versions:
```bash
node -v
npm -v
```

### Prepare project

For the first time, you need to use npm to download all the dependencies of the React project. To do so, 
first use your terminal to go into the react-frontend directory.

Then you want to run the following command:
```bash
npm install
```
This will prepare everything for you. Once it ends, you want to run:
```bash
npm start
```

If everything was successful, your browser should have already switched to a new tab, with the project running!

## Where is Python though???

With the frontend project working, it's time to try and get a backend as well.
Let's try to use last lesson's code!

_If last week, you were unable to get it to work properly, or you simply want a cleaner solution, 
you can use the following repository (download it on a new directory though!):_
[Lesson 1 code](https://github.com/MammosGeorgios/pwc-academy-vol5-session1)

Go and start your project (and don't forget to activate your virtual environment)! 
Once you do, refresh the browser for React.

You will see that we still have some issue. In order to resolve it,
we simply need to add an extra property to our FastApi command: 

`fast dev main.py --port 8080`


## Running postgres with docker

The final step is to run the postgres db, using docker.
Assuming everyone has installed docker already, we need to go to the directory 
`./devops/docker` and run the command `./resetDb.sh`

_Assuming everything went well, the DB running, but we haven't actually connected to it, so now what?_

## Next steps and homework

- Try to run all React employee actions, with your backend
- Try to follow [this](https://fastapi.tiangolo.com/tutorial/sql-databases/) guide in order to connect to the db
- Update our Employee class in order to be a SQLModel

In order to connect to the db, you will need a url and credentials:
```
datasource.url=jdbc:postgresql://localhost:5432/pwc_jacademy_db?useSSL=false
datasource.username=root
datasource.password=root
```

So you probably want to use something like this:
```python
SQLALCHEMY_DATABASE_URL = 'postgresql://localhost:5432/pwc_jacademy_db'
engine = create_engine(SQLALCHEMY_DATABASE_URL)
```

Next week, we will give you the full example, with the full Python codebase, 
so try to experiment on your version as much as you want.

If you opt to follow the guide fully and use SQLite, let us know in the next session, 
since it's a great alternative for small scale projects, and we will discuss them both in the future

