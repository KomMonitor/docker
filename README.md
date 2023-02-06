# KomMonitor Docker

For convenience, this repository provides various ready-to-use configuration files to get started quickly with KomMonitor in a Docker environment.

## Get started
Steps to set up a first running instance of KomMonitor very quickly:  
### Start a Keycloak instance:
You'll find Docker Compose files for different Keycloak configurations within the [./keycloak](./keycloak) directory. For developing purposes, use the Keycloak configuration, which simply uses the H2 file database for persisting data. Simply run `docker compose up` [./keycloak/keycloak-h2](./keycloak/keycloak-h2). 

To use Keycloak for development purposes on your local machine, add Keycloak as an entry to your host file as described [here](./keycloak/addHostEntry.readme). Keycloak then will be available under http://keycloak:8080/.
### Configure Keycloak:
Keycloak has a preconfigured "KomMonitor" realm with several KomMonitor clients registered. However, you have to regenerate the client secrets for all of these components, since they won't be imported at startup time. These secrets later wil be used to configure the KomMonitor components. In addition, create a dummy user in the KomMonitor realm and assign the *kommonitor-creator* role.
### Configure KomMonitor
You have to adopt the configuration files within [./kommonitor/config](./kommonitor/config) to your current Keycloak setup. This means, put the regenerated client secrets in every single *.env file to the `KOMMONITOR_SWAGGER_UI_SECURITY_SECRET` and `KEYCLOAK_CREDENTIALS_SECRET` variables.
### Start KomMonitor: 
Run `docker compose up` from [./kommonitor](./kommonitor). This sets up all components of the KomMonitor stack via Docker. The Web client will be available via http://localhost:8084/.
### Start Portainer
If you wish to monitor all your Docker containers via [Portainer](https://www.portainer.io/) start an instance from the [./portainer](./portainer) directory.
