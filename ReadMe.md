# Octopus: Ansible Automation for Poll Application Deployment Description

![Logo de mon projet](https://bugfender.com/wp-content/uploads/2018/10/automated.gif)

Octopus is an automation project aimed at deploying a polling application across multiple machines without using containers, utilizing Ansible. This project builds on the polling application developed during the Popeye project and deploys it across 5 distinct machines, each serving a specific role within the application architecture: Redis, PostgreSQL, Poll, Worker, and Result.

## General Objective
To automate the deployment of the polling application across 5 virtual instances, configuring each required service (Redis, PostgreSQL, Poll, Worker, Result) on its own machine while ensuring secure and idempotent configuration with Ansible.

## Prerequisites

- Ansible 2.9 or higher.

- 5 virtual machines based on Debian 12.

- SSH access to target machines with sudo privileges.

- Environment Setup

- Ensure that Ansible is installed on your control machine and that you have SSH access to the target instances.

- Configure your production inventory file with the necessary IP addresses and authentication information.

## Repository Structure
The repository contains the following:

- playbook.yml: The main Ansible playbook orchestrating the deployment.
poll.tar, result.tar, worker.tar folders: Archives containing the Poll, Result, and Worker services.

- group_vars directory: Contains variables applicable to all hosts.
roles directory: Contains Ansible roles defined for each service and base configuration.

## Deployment
To deploy the application, execute the following commands:

Set your Ansible Vault password in a temporary file:

- `echo verySecretPassword > /tmp/.vault_pass`
- `export ANSIBLE_VAULT_PASSWORD_FILE=/tmp/.vault_pass`

## Run the Ansible playbook:

- `ansible-playbook -i production playbook.yml`

## Security
All passwords and sensitive data should be encrypted with Ansible Vault. No clear-text passwords should be found in the repository.

## Ansible Roles

- **base**: Installs useful packages and configures instances.
- **redis**: Installs and configures Redis.
- **postgresql**: Installs PostgreSQL, creates the user and database.
- **poll**: Deploys and runs the Poll web client.
- **worker**: Deploys, builds, and runs the Java worker.
- **result**: Deploys and runs the Result web client.