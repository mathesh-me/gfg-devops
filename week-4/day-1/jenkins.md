## Jenkins

### Important tips for Jenkins

- Instead of installing Jenkins in your local machine, which include a lot of configurations and dependencies, you can use Docker Image to run Jenkins.
- You can use the following command to run Jenkins in your local machine.

```bash
docker run -p 8080:8080 jenkins/jenkins:lts
```

### Why we need Jenkins Cluster(Or)Jenkins Master-Slave Architecture?

- **Jenkins Cluster** is nothing but a group of Jenkins servers.
- Let's consider a scenario where we have a Jenkins server and we have 1000 jobs to run.
- If we run all the jobs in a single Jenkins server, it will take a lot of resources from my master node and it will be difficult to manage.

**Example:**

- Let's say I have one Job and it involves downloading some big files from the internet.
- If I run it in my master server, it will consume lot of space and it difficult to manage.
- So, I can run it in a slave server and it will not affect my master server.

### Pipeline in Jenkins

- Instead of running a multiple stages in a multiple jobs, we can run all the stages in a single job using Jenkins Pipeline.
- **Pre-rquisties** - You need to install the `Pipeline plugin` in your Jenkins server.
- Before we installed the `Build pipeline plugin`, we used that plugin to run multiple jobs for multiple stages.
- But, after installing the `Pipeline plugin`, we can run all the stages in a single job.

### Jenkinsfile

- In Pipeline, we can write the stages in a file called `Jenkinsfile`.
- Syntax of Jenkinsfile is similar to the syntax of Groovy.
- We can write the stages in a `Jenkinsfile` and we can run all the stages in a single job.
- It uses Declarative approach.
- Example of Jenkinsfile:

```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
```

### Jenkins Pipeline Triggers

- Poll SCM - It will check the changes in the repository for every x minutes we mentioned.
- If we use `Poll SCM` trigger, It will waste lot of resources.
- So we can use `Webhook` trigger, which will trigger the Jenkins job whenever there is a change in the repository.

