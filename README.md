[![PyPI status](https://img.shields.io/pypi/status/ansicolortags.svg)](https://pypi.python.org/pypi/ansicolortags/) 

# Apigee CI/CD using Gitlab-ci and Maven, from Github repository

## Goal

Reference implementation for a CI/CD pipeline for Apigee using
[CI/CD with GitLab](https://docs.gitlab.com/ee/ci/introduction/) and the [Apigee Deploy Maven Plugin](https://github.com/apigee/apigee-deploy-maven-plugin).

The CICD pipeline includes:

- Git branch dependent Apigee environment selection and proxy naming to allow
  deployment of feature branches as separate proxies in the same environment
- Static Apigee Proxy code analysis using [apigeelint](https://github.com/apigee/apigeelint)
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

The setup described in this reference implementation is based on GitLab CI. So, you must have a GitLab account you will use to create a project mirrored with your GitHub repository or to clone this GitHub repository.

#### Option A: **Import** this GitHub repository into a GitLab project.

Using the GitLab importer, you can import your GitHub repositories to GitLab.com or to your self-managed GitLab instance. <BR>GitLab Guide: [Import your project from GitHub to GitLab](https://docs.gitlab.com/ee/user/project/import/github.html#import-your-github-repository-into-gitlab)



#### Option B: **Mirror** this GitHub repository to a GitLab project.

With GitLab CI/CD for GitHub, users can create a CI/CD project in GitLab connected to an external GitHub code repository. This will automatically configure several components:

- Pull mirroring of the repository.
- A push webhook to GitLab triggers CI/CD immediately once a code is committed.
- GitHub project service integration webhooks CI status back to GitHub.

To configure it, clone this Github repository and configure GitLab for GitHub.<BR> GitLab Guide:
[Using GitLab CI/CD with a GitHub repository](https://docs.gitlab.com/ee/ci/ci_cd_for_external_repos/github_integration.html).

### API Proxy

The folder `airports-cicd-v1` includes a simple API proxy bundle, a simple Apigee configuration file as well as the
following resources:

- [.gitlab-ci file](./.gitlab-ci.yml) to define a GitLab
  multi-branch pipeline.
- [Test Folder](./test) to hold the unit and integration
  tests.

## CI/CD Configuration Instructions


... to be continued