# CICD PROJECT INTERVIEW QUESTIONS
## CI
- continuous integration ensures that your build is smooth and all your test got executed your code quality is maintained and image is created all of these things falls into CI process

## CD
- continuous delivery which ensures that your delivery process is done.in our case we kubernetes. kubernetes is most used platform these days.

# 1. There is a developer who has committed a change to this git repository how does your Jenkins get notified.

- There are multiple way. The most efficient way is the WEBHOOK.
-  Instead of the Jenkins watching your repository.
-   Jenkins will not watch your repository but git will send the notification to Jenkins.
-   So basically we go to Jenkins and you can get the WEBHOOK Url and you can put that in GitHub settings.
-   In GitHub settings you will have an options for WEBHOOK where u define for which actions the WEBHOOK has to be trigger.

Like it has to be triggered on COMMIT,PUSH,PULL, ISSUE. All these can be set in GitHub settings

- For each of these stages like build push we can create a docker agent.
- If you use the docker agent u can skip the installations you can skip configurations because docker images are directly available for these things.

As part of your build what happens

Unit test will run
Static code analysis

If these steps are successful then only you can go to next step.

If build stage goes failed in such case you can configure some alerts or in Jenkins you have email plugins or you can send e-mail notification or slack notification using API.

If the build passes you can integrate with SONAR qube or any other code or security scanning tool and you can verify that did it reach expected compliance does it have error  than expected range.

If there is a security vulnerabilities you can send a email notification.

If there is no security vulnerabilities you can proceed with creation of docker image.

Again use a DOCKER image or docker plugin or write a shell script and write command to build docker build.

Using the docker build you will get a DOCKER image.

As part of pipeline you will send this to docker registry or docker container registery (hub,quay.io,ECR)

these are continuous integration steps.

So GIT can talk Jenkins in multiple ways
### 1.jenkins can continuously poll this.
You can configure some build triggers in Jenkins
### 2. Efficient way is WEBHOOK
Because if you are polling continuously or if you are build triggers the problem is that Jenkins is continuously try to send request to your git and continuously fetch the information.

So you are making lot of API calls to your git.
Where as if you use WEBHOOK it will only sends notification or triggers to Jenkins whenever the WEBHOOK is triggered and the WEBHOOK is triggered only when a specific action is done performed on git that you are expecting.


# 2. what type of Jenkins file are you following or what agent are you using in your Jenkins file.

Always go with the DECLARATIVE JENKINS FILE. These are better where as compared to scripted pipeline it is more of instructured way. If you have strong development team then only suggest to go with scripted pipeline.

Where as Declarative pipeline are very easy to write and understand collaborate even one doesn't have knowledge in groovy scripts any don't have any experience in programming declarative pipelines are better.

# 3. WHAT TYPE OF AGENT YOUR USING

we are using docker agent which are very light in weight and which is very useful because you don't have install lot of things.

Like

Maven
JAVA
TESTING TOOLS
Python


Once the docker image is created then you will push the docker image to docker registry

This is continuous integration process

At the end of CI process u will have image ready this image has new tag. Now will try to push this image to docker container registery this will be last stage of CI.

once this is pushed how does your CD gets triggered.

# 4. HOW DOES CI AND CD COMMUNICATE WITH EACH OTHER

traditionally people did used ANSIBLE playbooks and some SHELL SCRIPTS and they include CD in the same CI pipeline.

Which will push artifacts to kubernetes or any of your target platform

The problem with this is that this not much scalable and also ansible shell are not designed for continuous delivery for that reason you have to choose a continuous delivery tool.

The best delivery tools in the market available are GITOPS based tools because it is similar to source code you should also create a git repository this will have your application manifest (kubernetes pod.yml, deployment.yml, service.yml) y u need to put these things in your git repository y can't you create these things in your CI pipeline that is because you don't have proper mechanism if you are doing that.


Tommorow Instead of updating kubernetes pod.yml, deployment.yml, service.yml
You just  want to something like add a new volume or new node point in such case ur CI will not come handy.

Because ur CI will triggered basically whenever there is a change in source code.
But here he has added a new volume to the pod.
In such case if you not using a proper GITOPS tool then the DEVOPS engineer should directly login to the kubernetes cluster and he has to directly update the kubernetes cluster POD.YML
there is no verification no code Audit or code review.

### ARGO IMAGE UPDATER - it will continuously monitor the docker HUB or any container registery whenever a new image is pushed into ur container image registery ARGO IMAGE UPDATER directly update the git repository with new version in the pod.yml, deployment.yml or wherever it is required.

If it is HELMCHAT it has capability of updating the HELPCHART aswell.


### ARGO CD : which is continuously watching this git hub repository and whenever there is change in the git repository take the new pod.yml , deployment.yml,HELMCHAT and deploy to kubernetes cluster.

THIS IS THE PROCESS.
![IMG_20231005_180136_106](https://github.com/PawarSavitha/maven-project/assets/114134446/5d21b973-594c-4222-b151-ad47a4443e6f)

![IMG_20231005_180136_92](https://github.com/PawarSavitha/maven-project/assets/114134446/114d9f6e-8571-419c-8681-3f973d77d9d1)
![IMG_20231005_180136_102](https://github.com/PawarSavitha/maven-project/assets/114134446/5f0b7f5e-caad-4bb0-b26e-f14c017c92a0)
