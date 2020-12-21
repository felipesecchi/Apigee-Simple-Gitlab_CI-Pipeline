# Apigee CI/CD using Gitlab-ci and Maven, from Github repository

## Goal

Reference implementation for a CI/CD pipeline for Apigee using
[CI/CD with GitLab](https://docs.gitlab.com/ee/ci/introduction/) and the [Apigee Deploy Maven Plugin](https://github.com/apigee/apigee-deploy-maven-plugin).

The CICD pipeline includes:

- Git branch dependent Apigee environment selection and proxy naming to allow
  deployment of feature branches as separate proxies in the same environment
- Static Apigee Proxy code analysis using [apickli](https://github.com/apickli/apickli)
- Static JS code analysis using [eslint](https://eslint.org/)
- Unit JS testing using [mocha](https://mochajs.org/)
- Integration testing of the deployed proxy using
  [apickli](https://github.com/apickli/apickli)
- Packaging and deployment of an Apigee configuration using
  [Apigee Config Maven Plugin](https://github.com/apigee/apigee-config-maven-plugin)
- Packaging and deployment of the API proxy bundle using
  [Apigee Deploy Maven Plugin](https://github.com/apigee/apigee-deploy-maven-plugin)

## Target Audience

- Operations
- API Engineers
- Security

## Limitations & Requirements

- The authentication to the Apigee management API is done using OAuth2. If
  you require MFA, please see the [documentation](https://github.com/apigee/apigee-deploy-maven-plugin#oauth-and-two-factor-authentication)
  for the Maven deploy plugin for how to configure MFA.

## Prerequisites

### GitLab

The setup described in this reference implementation is based on GitLab-ci. So, you must have a GitLab account you will use to create a project mirrored with your GitHub repository.

### API Proxy

The folder `airports-cicd-v1` includes a simple API proxy bundle, a simple Apigee configuration file as well as the
following resources:

- [Gitlab-ci file](./.gitlab-ci.yml) to define a Jenkins
  multi-branch pipeline.
- [Test Folder](./test) to hold the unit and integration
  tests.

## CI/CD Configuration Instructions


... to be continued