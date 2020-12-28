# Sample Microservice Architecture using event souring and CQRS (command query responsibility segregation)

## 🔨🧰Development considerations:
- Please install Docker locally
- Please install Kubernetes using Minikube or docker (for local development)
- Please install Skaffold locally

## 🏛⚙️Architecture
There are a total of 6 services
- posts
  - A service which is responsible for creating posts. Tech: Nodejs with express
- comments
  - A service which is responsible for creating comments. Tech: Nodejs with express
- moderation
  - A service responsible for moderating comments. Tech: Nodejs with express
- event-bus
  - A service which handles all the events, persists them and forwards them to the subscribers. Tech: Nodejs with express
- query
  - Following principle of CQRS, query service is responsible for read events from the clients. Tech: Nodejs with express
- client
  - A react based simple front end app
  
###### No permanent storage is present, only in memory js object.

- All the communication inside the landscape happens via event-bus. This helps to increase the reliability by reducing direct dependency on services. 
- Also to increase read-time and optimize read and write sides independently, query service is used for read operations and has access to the read db. The read db is updated via events from event-bus.

## 🔨💻 Infrastructure
Each service has a Dockerfile. In the infra folder, we have all the manifests for deployments and services for individual services. Therefore the apps can be deployed easily on any cluster.
  - To ease local development, skaffold configuration is added in the base folder. This enables to set up and tear down the development cluster easily.

## 👷‍♂️👷‍♀️Development
- Please run `skaffold dev` from the root folder. This would spin up the local cluster. Exiting this would delete all objects related to this application.

###### This usecase does not (in my opinion) fits the need for event sourcing or CQRS architecture. That being said, the simplicity of this app's usecases enable us to focus on CQRS, event sourcing and their infrastructure using docker, kubernetes and skaffold

### There is a lot of things that can be added to this application (this is the minimal skeleton)
- Add permanent storage
- Add a proper event broker i.e. kafka, NATS etc
- Add automatic testing
- Add CI/CD. 
- Logging

[THIS DOC NEEDS TO BE REFINED. I WROTE IN A HURRY.. LITERALLY :P]

##### Special thanks for @StephenGrider for the wonderful course on Microservice with node js and react