---
layout: post
title:  "PwC JAcademy Volume 4 Kickoff"
categories: jacademy
published: false
---
# Setting up our local environment

Our goal is to set up an IDE and checkout the JAcademy project!

## IntelliJ IDEA Community edition

Community edition is at the bottom! The first download is for the ultimate edition as a trial. Some of you might have access to the Ultimate version through your universities, and you can you that if you want to. Download the version matching your OS.

`https://www.jetbrains.com/idea/download/?section=windows`

The following url is for students with access to the free educational licences of JetBrains. See if you can get a licence for the Ultimate version.

`https://www.jetbrains.com/community/education/#students`

## Project repository

Our next goal is to download the project from its git repository, and have it ready in our IDE.
There are multiple ways to do this. We will opt for having IntelliJ setting up our project.

#### Gaining access to the repository and generating a GitHub token

The JAcademy project is not public, so just having the url is not enough to download it.
In order to gain access, you will need to ask someone from the JAcademy team to give your GitHub account access.
Once you have access and can see the repository in your GitHub, you need to create a token for the next step.


First you need to see if you have access in the JAcademy project. Try out the following url (you need to be logged in!):
`https://github.com/PwC-Greece/jacademy`

Assuming you have access to the project, you next need to generate a token from your GitHub account (we will use it in order to give our IDEs access to the repo).
To generate the token, we have to do the following:

- Go to your GitHub settings (`https://github.com/settings/profile`)
- Then "Developer Settings" option (usually at the very bottom)
- Then "Personal access tokens"-> "Tokens (classic)"
- Click "Generate new token" and select the classic version
  - As a note use something like "JAcademy"
  - For expiration select 90 days
  - We need to give the following scopes:
    - repo (FULL)
    - read:org
    - read:user and user:email
- Finally, click generate token

Be careful with the token! Right after you generate it, the token will be visible, keep it temporarily in a note somewhere for the next step. 
This is the only time you can get this token. If you "lose" it, then you will need to create a new one.

#### Checking our the project from IntelliJ IDEA

The repo url is `https://github.com/PwC-Greece/jacademy.git`

![checkOutFromVersionControl.png](/assets/images/jacademy/checkOutFromVersionControl.png)

![checkOutFromVersionControl.png](/assets/images/jacademy/gitUrl.png)

Aaaaaand that's it from this guide!
Everything else will be available though the repository or by instructors themselves.

## Happy bug-hunting!

