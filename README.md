# Welcome to spring-boot-postgres Sample project

Simple SpringBoot application using a database and provide a basic API.

## Docker

You need to have docker installed and to be in the docker directory of this project.
Then you can just use this command to get a ready stack springboot + postgresql.
`docker-compose up -d`
Check docker-compose file to see the external port to use to reach the spring-boot app : 

for example http://localhost:8888/health (monitoring service)

or you can use the main app feature by adding user with a post, for example with curl :
`curl -X POST "http://localhost:8888/user/jon.snow"`

and http://localhost:8888/user to check the result.

### build new image
Use the Dockerfile provided and add jar file + application.yml in the same directory then run this command :
`docker build . -t <IMAGE_NAME>`

## Application Configuration

One way to configure Spring applications is to use YAML configuration files.
Springboot, loads the application properties outside of your packaged jar from the `application.yml` file.

Following is a simple YAML file that contains configuration for use PostgreSQL database datasource.

```yaml

spring:
  datasource:
    url: jdbc:postgresql://localhost:5432/sampledb
    username: sampleuser
    password: sampleuserpassword
    platform: POSTGRESQL
  jpa:
    hibernate:
      ddl-auto: create-drop
    show-sql: true
server:
  port: 8080

endpoints:
  health:
    sensitive: false

management:
  security:
    enabled: false
```

For the development mode the dev profile load the properties from `src/main/resources/config/dev/application-dev.yml`.

## Application Usage

To add a user make a **POST** like this example : `http://localhost:8080/user/jon.snow`

To list all users : `http://localhost:8080/user`

Others useful endpoints:

- `/info`
- `/health`
- `/env`


## Developpement instructions

### Run Application Locally

```mvn -Dspring.profiles.active={dev-prod} spring-boot:run```

### Run Integration Tests

```mvn test```

###  Build

```mvn package```

