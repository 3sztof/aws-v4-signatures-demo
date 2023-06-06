# AWS V4 Signatures Demo

## Introduction

This repository contains a brief introduction to the concept of AWS Signatures Version 4 (AWS V4 Signatures) and a demonstration (simple AWS deployment) of the capabilities of those signatures.

The demo consists of an API Gateway deployment secured with [AWS Identity and Access Management service (IAM)](https://aws.amazon.com/iam/). In this scenario, every request sent to the API is expected to contain an AWS V4 Signature headers (or query parameters in case of WebSocket APIs). Any requests that lack those signatures are rejected up front and don't incur any API related costs. To demonstrate the signing mechanism, the repository contains a sample client written in Python script that creates a signed request to the deployed API and receives a response from the backend Lambda function.

### Advantages of learning and adopting AWS V4 Signatures

<!-- TODO -->

### Demo solution architecture

![...](docs/target_architecture.png "Target architecture of the demo")

### Further reading

- [Authenticating Requests with AWS V4 Signatures](https://docs.aws.amazon.com/AmazonS3/latest/API/sig-v4-authenticating-requests.html)
- [AWS API Gateway](https://aws.amazon.com/api-gateway/)
- [AWS IAM](https://aws.amazon.com/iam/)
- [AWS Serverless Application Model (SAM)](https://aws.amazon.com/serverless/sam/)
  - [AWS CloudFormation](https://aws.amazon.com/cloudformation/)

---

## Deployment

### Prerequisites

- [AWS SAM - Serverless Application Model CLI](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/install-sam-cli.html)
- [Python >=3.9](https://www.python.org/downloads/)
- [Python Poetry module](https://python-poetry.org/docs/)
  - If Python has been set up already, install the Poetry versioning module by running: `pip install poetry`
- An [AWS User / Role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id.html) credentials with permissions to deploy infrastructure with SAM ([CloudFormation](https://aws.amazon.com/cloudformation/)) and access the deployed [AWS API Gateway](https://aws.amazon.com/api-gateway/) endpoint
- [Optional] [AWS Command Line Interface (CLI)](https://aws.amazon.com/cli/)

### Infrastructure

To deploy the AWS infrastructure required for the functionality demo, we will use [AWS Serverless Application Model (SAM)](https://aws.amazon.com/serverless/sam/), which is a [Command Line Interface (CLI)](https://en.wikipedia.org/wiki/Command-line_interface) and [Infrastructure as Code (IaC)](https://docs.aws.amazon.com/whitepapers/latest/introduction-devops-aws/infrastructure-as-code.html) tool that allows us to quickly provision and destroy given sets of AWS infrastructure components.

In the case of this demo, we deploy:

- an [AWS API Gateway](https://aws.amazon.com/api-gateway/) configured with IAM authorization
- an [AWS Lambda](https://aws.amazon.com/lambda/) function to handle API requests (backend)

To deploy the infrastructure with AWS Serverless Application Model CLI, simply run the following command:

```sh
sam deploy --stack-name aws-v4-signing-api-demo -t ./src/template.yaml --resolve-s3
```

> **_NOTE:_** The command should return (among other things) the URL of the provisioned API Gateway endpoint. Note it down, it will be needed when running the demo API client script.

---

## Setup

1. Assume an AWS IAM Role in your shell

    To use the demo's client Python script, we will need to make sure that it can assume an AWS identity (IAM User or Role) by using our credentials.

    To proceed, open your terminal (recommended [bash](https://www.gnu.org/software/bash/) on unix (Linux / MacOS) systems and [Powershell](https://learn.microsoft.com/en-us/powershell/scripting/overview?view=powershell-7.3) on Windows).

    - Configure the AWS credentials in the shell's environment variables (you can also use the [Official AWS Docs](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-envvars.html))

        > **_NOTE:_** The commands below (with `export VAR_NAME=VALUE` syntax) should work on all Linux / MacOS systems, on Windows, you can open Powershell and in an analogous way, set the environment variables using the following syntax: `$Env:VAR_NAME = "VALUE"`

        Run the following commands (replace the `<PLACEHOLDER>` values with your respective AWS identity credentials)

        ```sh
        export AWS_ACCESS_KEY_ID=<PLACEHOLDER>
        export AWS_SECRET_ACCESS_KEY=<PLACEHOLDER>
        export AWS_DEFAULT_REGION=<PLACEHOLDER>
        ```

        > **_NOTE:_** If you are using an AWS Role, instead of the user, you will also need to set `AWS_SESSION_TOKEN` environment variable.

    - [alternative way] Guided configuration with AWS CLI

      AWS CLI can be used to make the above configuration easier through a series of interactive questions asked by the CLI after running the following command:

      ```sh
      aws configure
      ```

    If you are having any problems configuring your terminal session with AWS credentials, please navigate to the official AWS documentation for working in CLI:
    - [IAM users](https://docs.aws.amazon.com/cli/latest/userguide/cli-authentication-user.html)
    - [IAM roles](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-role.html)

1. Prepare a Python environment

    It's recommended to create a Python virtual environment for this project in order to be 100% sure that all the dependencies are met and to prevent "polluting" the global Python installation with this project's modules. This can easily be done with Python's Poetry module.

    - make sure you have installed Python Poetry module by running: `pip install poetry`
      >  **_NOTE:_** on some systems, you might need to run `pip3` instead of `pip` (same for `python3` instead of `python`)
    - to create a Python virtual environment for this project, simply run: `poetry shell`
      >  **_NOTE:_** if the command above didn't work, you can try invoking the module directly - `python -m poetry shell`
    - install all required Python packages by running: `poetry install`

---

## Usage

1. Make an API request with the script

    Open the [demo_cli_client.py](src/demo_cli_client.py) Python script and take a look at its contents. Feel free to play with it on your own!

    To make a request to the API Gateway endpoint by running:

    ```sh
    python ./src/demo_cli_client.py
    ```

1. Make a request without the required signatures to validate the API security

<!-- TODO -->

---

## Explore & Experiment

1. API Gateway Resource Policies

<!-- TODO -->

1. Use an IAM role restricted to the API

<!-- TODO -->

---

## Cleanup

1. Destroy AWS Infrastructure

<!-- TODO -->

1. Clean up the Python Environment

<!-- TODO -->

---
<!-- 
APG Format

## Summary

## Prerequisites

## Limitations

## Product versions

## Target technology stack

## Target architecture

## Automation and scale -->
