# GHA Matrix Testing

A simple repo to demonstrate how you can configure GitHub actions to run the same workflow across multiple environments
dynamically.

## Repository configuration

Create a repo level environment variable that is a JSON array for each "client" we will deploy to:

![](./screenshots/repo-var-overview.png "Overview of repository variables configuration")

![](./screenshots/repo-var-edit.png "Edit view of repository variables configuration")

Then create an environment for each client and add the required configuration:

![](./screenshots/environments-overview.png "Overview of environments configuration")

Note for the case of this example the only configuration is a single secret, but this secret must exist in all
environments (or a default at the repo level).

Then create the workflow. 

This repo includes an [example](./.github/workflows/demo.yml) that has a single job that is required ***before*** deployment
(a compile style step) but there could be 0 or many depending on your requirements. The core is then to define a job that
uses the repository environment variable as the jobs matrix. You can then use that name to pick an environment. This pattern
could be expanded if you wanted to by making the JSON more complex e.g. you may want multiple environments per client.

## Why?

Looking for a mechanism to deploy the same deployable to multiple clients without needing to change the yaml
configuration for every client or duplicate code.