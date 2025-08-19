# Continuous Integration with CodeBuild
### eedontoh@outlook.com


## Introducing Today's Project!

In this project, we demonstrate continous integeration CI with CodeBuild. I'm doing
this project to learn how AWS CodeBuild is utilised to automate the build process for
web app

### Key tools and concepts

Services used were AWS:
CodeBuild
CodeArtifact
Amazon S3
GitHub
IAM

Key concepts learnt includes:
Creating and configuring a CodeBuild project 
Connecting CodeBuild project to GitHub repo.
Defining the build process using buildspec.yml
Automating testing using CodeBuild

### Project reflection

This project took me approximately 2. 5 hrs. The most challenging part was properly
configuring the buildspec.yml to automate the build process. It was most rewarding to
figure out ways around troubleshooting bugs and error bumps.


## Setting up a CodeBuild Project

CodeBuild is a continuous integration service, which means it automatically run tests,
compiles code and makes sure new changes play nicely with the existing code.
Engineering teams use it because it abstracts away the setting up of build servers.

CodeBuild project's source configuration means setting up the location of where the
web-app code is, so CodeBuild can fetch, run, test, compile and package the code
into a deployable file. I selected Github since that is where the source code lives
![CodeBuild Home Page](https://github.com/user-attachments/assets/f4f40ab4-f4d4-4375-bab8-f8547f477e07)

## Connecting CodeBuild with GitHub

There are multiple credential types for GitHub, like Github App, Personal Access
Tokens and OAuth App. I used GitHub App because it is the simplest and most
secured option. AWS manages the application and connection.

The service that helped connect to Github was AWSCodeConnections. It handles all
the authentication complexities of managing API keys, tokens (like GitHub's Personal
Access Tokens!) or SSH credentials so we focus on building applications
![Github App Succesfull Connection](https://github.com/user-attachments/assets/ddeb4a48-ac5e-4768-ab60-3bb3a558fcf2)


## CodeBuild Configurations

### Environment

The CodeBuild project's Environment configuration means defining the environment
where our builds will run. This includes settings like the provisioning model, operating
system, runtime, and compute resources, environment image among others.

### Artifacts

Build artifacts are the tangible outputs from a build process. They're important
because it packages up everything a server need to host the web app in one bundle.
The build process creates WAR files. To store them, an S 3 bucket was created.

### Packaging

When setting up CodeBuild, the artifact was packaged as a zip file for convenience,
cost efficiency and simplicity.

### Monitoring

For monitoring, CloudWatch Logs, which is are monitoring services essential for
tracking build progress, debugging errors, and auditing build activities.


## buildspec.yml

The first build failed because CodeBuild couldn't find the buildspec.yml file in the
GitHub repo as it wasnt created yet. A buildspec.yml file is needed because It
automate the build process as code as it can be reviewed, versioned and even
evolved.

The first two phases in the buildspec.yml file are the install and pre-build phases.
The third phase in the buildspec.yml file is the build phase. The fourth
phase in the buildspec.yml file is the artifact phase.
![buildspec yml](https://github.com/user-attachments/assets/63792e97-2765-41a0-a180-bdd690466b4a)


## Success!

My second build also failed, but with a different error that said the
DOWNLOAD_SOURCE phase succeeded this time, but other phases might have failed.
To fix this, CodeBuild's IAM role is granted permission to access CodeArtifact.

To resolve the second error, CodeBuild's IAM role granted permission to access
CodeArtifact. The project was built again and it was successfull this time round.

To verify the build, the s 3 code was successfully compiled and packaged. Seeing the
artifact tells me: a. The build process completed without errors b.The artifact was
properly uploaded to its destination. c.The artifact is now available.

<img width="1830" height="1464" alt="build_success" src="https://github.com/user-attachments/assets/03dc1ced-a13b-4836-b77c-709a28abeec3" />


