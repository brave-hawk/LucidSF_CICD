# Steps to reproduce this CI/CD demo

The following steps are required to realize this CI/CD setup

## Prepare the Integration pull-request github actions

Pull requests from developer orgs will be run against the integration org.

This requires setting up a pull-request YAML file for our first github action

### Create github secrets for INT org

In VScode, connect to your Integration org and run the following command:

```
sf org display -o [your INT alias] --verbose
```

Note the Sfdx Auth Url from the output. NB: This is sensitive information.

- In Github, go to your repository’s settings, expand Secrets and Variables from the left menu, and select Actions
- Create a new Repository secret
- Name the secret **SFDX_INTEGRATION_URL**
- Copy and Paste the Sfdx Auth Url value into the Secret field

### Create github secrets for Production org

In VScode, connect to your int org and run the following command:

```
sf org display -o [your PROD alias] --verbose
```

Note the Sfdx Auth Url from the output. NB: This is sensitive information.

- In Github, go to your repository’s settings, expand Secrets and Variables from the left menu, and select Actions
- Create a new Repository secret
- Name the secret **SFDX_PRODUCTION_URL**
- Copy and Paste the Sfdx Auth Url value into the Secret field

### Create the pull-request github action

In your project root create a .github folder, and workflows folder within.

In the workflows folder create a file called **pr-develop-branch.yml**

The content to be put in that file can be found in this repo.

In the project root, also add the parsePR.js file found in this repo

### Test the PR action

Create a **develop** branch from the main branch

From the **develop** branch, create a feature branch called:

```
feature/SFDC-Trigger-Framework
```

Make some changes to it: example, add the Apex classes from the TriggerHandler framework (found in this repo)

In the PR body, be sure to add

```
Apex::[all]::Apex
```

to run all tests

or

```
Apex::[TriggerHandler_Test]::Apex
```

to run only this specific test

## Add the actions to deploy to Integration and Production orgs

We shall add the YAML actions to deploy the validated PR to the INT and PROD orgs

## Create actions for when a change is pushed/merged into the develop branch

In the .github/workflows folder, create a file and name it: **push-develop-branch.yml**

Add the content in this repo to the file

## Create actions for when a change is pushed/merged into the main branch

In the .github/workflows folder, create a file and name it: **push-main-branch.yml**

Add the content in this repo to the file
