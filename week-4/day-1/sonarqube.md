## SonarQube

- It is a code qulaity analysis tool.
- It will give us report of our code quality.
- It store the report data in a database.
- We also have Sonar Scanner to scan the code and send the report to SonarQube server.

### How to install SonarQube?

- We can use Docker Image to run SonarQube.
- We can use the following command to run SonarQube in our local machine.

```bash
docker run -d --name sonarqube -p 9000:9000 sonarqube:latest
```

- We can access the SonarQube server using the following URL.

```
http://localhost:9000
```

- We can use the default username and password to login to the SonarQube server.

```
username: admin
password: admin
```

You can see the below image to do the login.

![net-9](https://github.com/mathesh-me/ci-cd-dotnet-app-deployment/assets/144098846/20b90d39-025f-4900-8c3d-9e602c3c1803)


- Login to SonarQube using the default credentials.
```
Username: admin
Password: admin
```
![net-10](https://github.com/mathesh-me/ci-cd-dotnet-app-deployment/assets/144098846/a87ca754-43e7-4ac3-a159-cd8b6dba7d6e)
![net-11](https://github.com/mathesh-me/ci-cd-dotnet-app-deployment/assets/144098846/015f8636-ff1a-47e8-b578-1b3e7a5369b3)
![net-12](https://github.com/mathesh-me/ci-cd-dotnet-app-deployment/assets/144098846/4a887ab7-17bd-4a0d-8e4c-dca18d562863)


