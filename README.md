# DOCKER-projects

# CONTAONARIZING A JAVA APPLICATION:

-  clone the repo : https://github.com/LondheShubham153/simple-java-docker.git
-  cd  simple-java-docker
-  rm -v Dockerfile
-  vim Dockerfile
-
```
cat Dockerfile
#pulling the base image
FROM openjdk:17-jdk-alpine
#creating a folder for the app to be stored
WORKDIR /app
#copy source code from host machine to container
COPY src/Main.java /app/Main.java
#compile the application code
RUN javac Main.java
# run the application
CMD ["java","Main"]

```
-  docker build -t java-app .
-   docker run java-app

# image created:
![image](https://github.com/user-attachments/assets/8cc905c9-ae88-42c5-a88d-d2a804f7da4b)
