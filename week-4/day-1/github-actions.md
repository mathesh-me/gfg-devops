## GitHub Actions

Instead of creating Jenkins server, creating EC2 instance, installing Jenkins, and configuring Jenkins, we can use GitHub Actions to run our CI/CD pipeline.

### What is GitHub Actions?

- **GitHub Actions** is a CI/CD service provided by GitHub.
- It allows us to automate our workflow from the GitHub repository.

### GitHub Actions Workflow

- **Workflow** is an automated process that you can set up in your repository to build, test, package, release, or deploy any project on GitHub.
- We have to create .github/workflows directory in our repository and we have to write the workflow in a file called `YAML` file.
- We can write the workflow in a file called `YAML` file and we can run the workflow using the triggers.

### Example of GitHub Actions Workflow

```yaml
name: CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
    build:
        runs-on: ubuntu-latest
    
        steps:
        - uses: xxxxxxxxxxxxxxxx@xx
        - name: Set up JDK 11
        uses: xxxxxxxxxxxxxxxxxx@xx
        with:
            java-version: '11'
        - name: Build with Maven
        run: mvn -B package --file pom.xml
```

### GitHub Actions Hosted Runners

- **GitHub Actions Hosted Runners** are virtual machines that are hosted by GitHub.
- We can use the GitHub Actions Hosted Runners to run our CI/CD pipeline.
- It's just like using Jenkins with EC2 instance.

We can always refer to the [official documentation](https://docs.github.com/en/actions) for more information.<br>

You can use this link to use already creted codes for GitHub Actions: https://github.com/actions 


    

