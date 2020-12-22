[![PyPI status](https://img.shields.io/pypi/status/ansicolortags.svg)](https://pypi.python.org/pypi/ansicolortags/) 

# Apigee CI/CD using GitHub, GitLab CI and Maven 

## Goal

Simple implementation for a CI/CD pipeline for Apigee using GitHub repository, 
[CI/CD with GitLab](https://docs.gitlab.com/ee/ci/introduction/) and the [Apigee Deploy Maven Plugin](https://github.com/apigee/apigee-deploy-maven-plugin).

**This is not an official Google product.**<BR>This implementation is not an official Google product, nor is it part of an official Google product. Support is available on a best-effort basis via GitHub.

***

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

### Initialize a GitLab (option A) or GitHub (option B) Repository

Create a GitLab/GitHub repository to hold your API Proxy. 

To use the `Apigee-Simple-Gitlab_CI-Pipeline`
in a **GitHub** repository `github.com/my-user/my-api-proxy-repo` follow these
steps:

```bash
git clone git@github.com:g-lalevee/Apigee-Simple-Gitlab_CI-Pipeline.git
cd Apigee-Simple-Gitlab_CI-Pipeline
git init
git remote add origin git@github.com:my-user/my-api-proxy.git
git checkout -b feature/cicd-pipeline
git add .
git commit -m "initial commit"
git push -u origin feature/cicd-pipeline
```

<BR>To use the `Apigee-Simple-Gitlab_CI-Pipeline`
in a **GitLab** repository `gitlab.com/my-user/my-api-proxy-repo` follow these
steps:

```bash
git clone git@github.com:g-lalevee/Apigee-Simple-Gitlab_CI-Pipeline.git
cd Apigee-Simple-Gitlab_CI-Pipeline
git init
git remote add origin git@gitlab.com:my-user/my-api-proxy.git
git checkout -b feature/cicd-pipeline
git add .
git commit -m "initial commit"
git push -u origin feature/cicd-pipeline
```

### GitLab Configuration (option B)

Start or configure your GitLab project as described in [Using GitLab CI/CD with a GitHub repository](https://docs.gitlab.com/ee/ci/ci_cd_for_external_repos/github_integration.html).

Then, add custom environment variables APIGEE_CREDS_USR and APIGEE_CREDS_PSW, to store your Apigee User ID and password:
- Go to your project’s Settings > CI/CD and expand the Variables section.
- Click the Add Variable button.<BR>In the Add variable modal, fill in the details:
  - Key: APIGEE_CREDS_USR
  - Value: your Apigee user ID 
  - Type: Variable
  - Environment scope: All
  - Protect variable (Optional): If selected, the variable is only available in pipelines that run on protected branches or tags.
  - Mask variable (Optional): If selected, the variable’s Value is masked in job logs. The variable fails to save if the value does not meet the masking requirements.
  - Click the Add Variable button
- Click again the Add Variable button.<BR>In the Add variable modal, fill in the details:
  - Key: APIGEE_CREDS_PSW
  - Value: your Apigee user ID password
  - Type: Variable
  - Environment scope: All
  - Protect variable (Optional): If selected, the variable is only available in pipelines that run on protected branches or tags.
  - Mask variable (Optional): If selected, the variable’s Value is masked in job logs. The variable fails to save if the value does not meet the masking requirements.
  - Click the Add Variable button

## Run the pipeline

Using your favorite IDE...
1.  Update the .gitlab-ci.yml file<BR>
In global **Variables** section, change **DEFAULT_APIGEE_ORG** value by your target Apigee organization.
2.  Read carefully the **before_script** section to check if the multibranch rules match your environment naming and configuration.
3. Save
4. Commit, Push.. et voila

Use the GitLab UI to monitor your pipeline execution. Go to your GitLab project > CI/CD > Pipeline.

![GitLab CICD Pipeline](./img/GitLab-Pipeline-1.png)

You can see all stages and jobs running.

![GitLab CICD Pipeline Animated](./img/animated-pipeline.gif)

And the end of test stages you can download artifacts.

![GitLab CICD Pipeline artifacts](./img/atifacts.png)

For example, the results of integration tests with Apickli.

![GitLab CICD Pipeline apickli](./img/apickli.png)
