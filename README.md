# Vikunja
Vikunja todo applicaiton deployed in k8s.

## Quick Start Guide

We will cover the following step-by-step to setup your local environment.

1. Install prerequisites:

* [DevBox](https://github.com/jetify-com/devbox) - Devbox is a command-line tool that lets you easily create isolated shells for development. 
* [Podman Desktop](https://podman-desktop.io/docs/installation) -  Graphical user interface (GUI), provides a user-friendly environment for managing containers and Kubernetes workloads

2. Create a kind cluster using podman: [Click Here](https://podman-desktop.io/docs/kind/creating-a-kind-cluster)

3. Initiate DevBox Shell from CLI

    ```bash
    devbox shell
    ```

4. Start Application

    ```bash
    task app:start
    ```

5. Verify the Application is running:

    ```bash
    task app:ping
    ```

6. Follows the Applications logs:

    ```bash
    task app:logs
    ```
7. Bonus: See what other tasks are availible
    
    ```bash
    task --list
    ```

## Docs

[Click Here](./docs/README.md) To go to the docs.