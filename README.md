# Spinnaker Orb [![CircleCI status](https://circleci.com/gh/CircleCI-Public/spinnaker-orb.svg "CircleCI status")](https://circleci.com/gh/CircleCI-Public/spinnaker-orb) [![CircleCI Orb Version](https://img.shields.io/badge/endpoint.svg?url=https://badges.circleci.io/orb/circleci/spinnaker)](https://circleci.com/orbs/registry/orb/circleci/spinnaker) [![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/circleci-public/spinnaker-orb/master/LICENSE) [![CircleCI Community](https://img.shields.io/badge/community-CircleCI%20Discuss-343434.svg)](https://discuss.circleci.com/c/ecosystem/orbs)

A CircleCI Orb to simplify deployments to Spinnaker.

Here are some features that the Spinnaker orb provides:

- Triggering a Spinnaker application pipeline with a webhook via the `trigger-pipeline-with-webhook` command.
- Installing the spin CLI for managing Spinnaker applications via the `install-spin` command, with a convenience option that generates a simple configuration for a locally-available Spinnaker Gate.
- `set-up-port-forwarding` enables setting up port forwarding for Spinnaker Deck and Spinnaker Gate to interact with Spinnaker through a `localhost` URL.

## Usage

See the [orb registry listing](https://circleci.com/orbs/registry/orb/circleci/spinnaker) for usage guidelines.

## Requirements

- `curl` should be present in `PATH`.

- Some of the commands require a Linux environment to execute in. Refer to the [orb registry listing](https://circleci.com/orbs/registry/orb/circleci/spinnaker) for the descriptions of each command.

## Examples

Full usage examples can be found on the Spinnaker orb's page in the orb registry, [here](https://circleci.com/orbs/registry/orb/circleci/spinnaker#usage-examples).

```
version: 2.1
orbs:
  # In this example, Spinnaker is assumed to already be
  # deployed on an AWS EKS k8s cluster.
  aws-eks: circleci/aws-eks@0.2.0
  # Replace "x.y.z" with actual orb version
  spinnaker: circleci/spinnaker@x.y.z
jobs:
  send-webhook:
    parameters:
      cluster-name:
        description: |
          Name of the EKS cluster
        type: string
      aws-region:
        description: |
          AWS region that the EKS cluster is in
        type: string
    executor: spinnaker/default-stretch
    steps:
      # Set up k8s cluster connection.
      # In this example, Spinnaker is deployed on an AWS EKS k8s cluster.
      - aws-eks/update-kubeconfig-with-authenticator:
          cluster-name: << parameters.cluster-name >>
          install-kubectl: true
          aws-region: << parameters.aws-region >>
      # Set wait to true to ensure the webhook endpoint will be
      # ready for access via localhost in the next step
      - spinnaker/set-up-port-forwarding:
          namespace: spinnaker
          wait: true
      # Send a request to a webhook endpoint pre-configured in Spinnaker
      # Ref: https://www.spinnaker.io/guides/user/pipeline/triggers/webhooks/
      - spinnaker/trigger-pipeline-with-webhook:
          webhook-endpoint: "http://localhost:8084/webhooks/webhook/myappwebhook"
          payload: "{\\\"status\\\": \\\"success\\\", \\\"jobid\\\": \\\"$CIRCLE_WORKFLOW_JOB_ID\\\", \\\"message\\\": \\\"I've got it\\\"}"
workflows:
  example-workflow:
    jobs:
      - send-webhook:
          cluster-name: my-eks-tests
          aws-region: ap-southeast-2
```

## Contributing

We welcome [issues](https://github.com/CircleCI-Public/spinnaker-orb/issues) to and [pull requests](https://github.com/CircleCI-Public/spinnaker-orb/pulls) against this repository!

For further questions/comments about this or other orbs, visit [CircleCI's orbs discussion forum](https://discuss.circleci.com/c/orbs).
