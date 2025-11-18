# Continuous-Integration-with-CodeBuild
 will learn what Continuous Integration means, and how to set it up using AWS CodeBuild. I'm doing this project to learn to build from scratch a CI/CD pipeline that automates the build and deployment of a web app. This is a 100% hands-on challenge
 <img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Continuous Integration with CodeBuild

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-devops-codebuild-updated)

**Author:** Darryl Brown  
**Email:** darrylbrown1991@gmail.com

---

![Image](http://learn.nextwork.org/sincere_vermilion_playful_beaver/uploads/aws-devops-codebuild-updated_35588a47)

---

## Introducing Today's Project!

In this project, I will learn what Continuous Integration means, and how to set it up using AWS CodeBuild. I'm doing this project to learn to build from scratch a CI/CD pipeline that automates the build and deployment of a web app. This is a 100% hands-on challenge

### Key tools and concepts

Services I used were Github repo, CodeArtifact, S3, IAM, EC2, Codebuild. Key concepts I learnt include Set up a CodeBuild project and connect it to a GitHub repository.
Define a build process using buildspec.yml. Store build artifacts in Amazon S3. Update CodeBuild's IAM roles to allow permissions to CodeArtifact. Troubleshoot common build errors and ensure successful builds. Set up CodeBuild to go beyond the build process - and automate testing too.

### Project reflection

This project took me approximately 2hrs.

This project is part four of a series of DevOps projects where I'm building a CI/CD pipeline! 

---

## Setting up a CodeBuild Project

CodeBuild is a continuous integration service, which means a fully build tool for your code. It takes your source code, compiles it, runs tests, and packages it up. Engineering teams use it because you don't have to manually set up and manage any build servers yourself, and you only pay for the compute time you use for building your projects.

My CodeBuild project's source configuration means the location of the code that CodeBuild will fetch, compile, and package into a file you can deploy. And I selected Github as my source provider because that's where I've stored my web app's code. 

![Image](http://learn.nextwork.org/sincere_vermilion_playful_beaver/uploads/aws-devops-codebuild-updated_fewgrhte)

---

## Connecting CodeBuild with GitHub

There are multiple credential types for GitHub, like Github app, OAuth app, Personal Access token. I used GitHub App because this is generally the simplest and most secure option. AWS manages the application and connection, reducing the need for me to handle tokens or keys directly.

The service that helped connect is AWS CodeConnections. AWS CodeConnections is like a secure bridge between AWS and your external code repositories. 

![Image](http://learn.nextwork.org/sincere_vermilion_playful_beaver/uploads/aws-devops-codebuild-updated_a7c98e2d)

---

## CodeBuild Configurations

### Environment

My CodeBuild project's Environment configuration means environment images are pre-configured versions of the build environment so I won't need to install all the software/tools/settings required to build a project. It includes settings like provisioning model determines how AWS will set up and manage everything needed for my build.

### Artifacts

Build artifacts are the tangible outputs of your build process. They're important because they're what I'll actually deploy to my servers or distribute to users.  My build process will create will create a .war file (a packaged Java web application) as the build artifact. To store them, I created an S3 bucket.

### Packaging

When setting up CodeBuild, I also chose to package artifacts in a zip. Because smaller size, organization, simplicity. 

### Monitoring

For monitoring, I enabled CloudWatch Logs, which is a monitoring service that collects and tracks logs from AWS services. In this project, CloudWatch will record everything that happens during the build process, including the commands that are run, the output of those commands, and any errors that occur.

---

## buildspec.yml

My first build failed because it means CodeBuild couldn't find the buildspec.yml file in my GitHub repository. A buildspec.yml file is needed because without this file, CodeBuild doesn't know how to build my project. 

The first two phases in my buildspec.yml file install is the "prep work" phase here, I'm telling CodeBuild to use Java 8. pre_build are tasks to do before the main building starts. I'm grabbing a security token so I can access my dependencies.  The third phase in my buildspec.yml file. build is where the actual building happens. I'm using Maven (a popular Java build tool) to compile my code. The fourth phase in my buildspec.yml file post_build are the finishing touches after the main build is done. Here, I'm packaging everything into a WAR file (a format for web applications).

![Image](http://learn.nextwork.org/sincere_vermilion_playful_beaver/uploads/aws-devops-codebuild-updated_35588a47)

---

## Success!

My second build also failed, but with a different error that said command execution. To fix this I need to grant CodeBuild's IAM role the permission to access CodeArtifact.

To resolve the second error, I gave CodeBuild service roles and permissions to access CodeArtifact, which is needed to download project dependencies.When I built my project again, I saw success.

To verify the build, I checked build artifacts in S3. Seeing the artifact tells me my code was successfully compiled and packaged. The build process completed without errors. The artifact was properly uploaded to its destination. The artifact is now available for the next step in my process (like deployment

![Image](http://learn.nextwork.org/sincere_vermilion_playful_beaver/uploads/aws-devops-codebuild-updated_d9cc6191)

---


---

---
