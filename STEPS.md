# Steps to reproduce this CI/CD demo

The following steps are required to realize this CI/CD setup 

## Prepare the Integration pull-request github actions

Pull requests from developer orgs will be run against the integration org.

This requires setting up a pull-request YAML file for our first github action

### Create github secrets for Int org

In VScode, connect to your int org and run the following command:

```
sf org display -o [your INT alias] --verbose
```

Note the Sfdx Auth Url from the output. NB: This is sensitive information.

- In Github, go to your repository’s settings, expand Secrets and Variables from the left menu, and select Actions
- Create a new Repository secret
- Name the secret **SFDX_INTEGRATION_URL**
- Copy and Paste the Sfdx Auth Url value into the Secret field

### Create the pull-request github action

In your project root create a .github folder, and workflows folder within.

In the workflows folder create a file called **pr-develop-branch.yml**

The content to be put in that file can be found in this repo.






