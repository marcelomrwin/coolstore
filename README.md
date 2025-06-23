# CoolStore Monolith

This repository has the complete coolstore monolith built as a Java EE 7 application. To deploy it on JBoss 7.4 follow the instructions below


## Pre requisite

* Keycloak v20.0.5 zip installation
* podman or docker, tested with podman version 4.3.1
* maven, tested with maven version 3.8.5
* OpenJDK, tested with version 17.0.5

## Start keycloak

Extract keycloak-20.0.5.zip

```cd keycloak-20.0.5```

Start keycloak in dev mode listening on port 8081

``` ./bin/kc.sh start-dev --http-port=8081 ```

Open http://127.0.0.1:8081 in your browser


Set an administrator username and password, then login to keycloak using these credentials

Click on the "Master" dropdown, and select "Create Realm"

Click on "Browse" and locate the file realm-export.json in this repo.

Click on "Create" to create the "eap" realm

Click on "Users" and "Create new user"

Enter a username, e.g. "user1" and click on "Create"

From the next form, click on the "Credentials" tab and "Set password"

Set a password and password confirmation, and unselect "Temporary"

Click on "Save" to store the password.

Keycloak is now configured correctly

## Build and deploy the application to Openshift

Log in to OpenShift CLI

```
oc login
oc project coolstore
```

From the root of this repo, run: 

`mvn clean package -Dquarkus.kubernetes.deploy=true -DskipTests`

Navigate to your Openshift cluster route URL

![coolstore](assets/coolstore.png "coolstore")

From the coostore, click on "Sign in" in the top right

Login with the user credentials created on Keycloak, e.g. user1

You should now be able to complete the checkout process.
