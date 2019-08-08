# Spinnaker Orb [![CircleCI status](https://circleci.com/gh/CircleCI-Public/spinnaker-orb.svg "CircleCI status")](https://circleci.com/gh/CircleCI-Public/spinnaker-orb) [![CircleCI Orb Version](https://img.shields.io/badge/endpoint.svg?url=https://badges.circleci.io/orb/circleci/spinnaker)](https://circleci.com/orbs/registry/orb/circleci/spinnaker) [![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/circleci-public/spinnaker-orb/master/LICENSE) [![CircleCI Community](https://img.shields.io/badge/community-CircleCI%20Discuss-343434.svg)](https://discuss.circleci.com/c/ecosystem/orbs)

A CircleCI Orb to simplify deployments to Spinnaker.

Here are some features that the Spinnaker orb provides:

- Triggering a Spinnaker application pipeline with a webhook via the `trigger-pipeline-with-webhook` command.
- Installing the spin CLI for managing Spinnaker applications via the `install-spin` command, with a convenience option that generates a simple configuration for a locally-available Spinnaker Gate.
- `set-up-port-forwarding` enables setting up port forwarding for Spinnaker Deck and Spinnaker Gate to interact with Spinnaker through a `localhost` URL.

## Usage

See the [orb registry listing](http://circleci.com/orbs/registry/orb/circleci/spinnaker) for usage guidelines.

## Requirements

- `curl` should be present in `PATH`.

- Some of the commands require a Linux environment to execute in. Refer to the [orb registry listing](http://circleci.com/orbs/registry/orb/circleci/spinnaker) for the descriptions of each command.


## Contributing

We welcome [issues](https://github.com/CircleCI-Public/spinnaker-orb/issues) to and [pull requests](https://github.com/CircleCI-Public/spinnaker-orb/pulls) against this repository!

For further questions/comments about this or other orbs, visit [CircleCI's orbs discussion forum](https://discuss.circleci.com/c/orbs).