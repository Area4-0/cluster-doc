# Introduction

This documentation describes how to configure an autoscaling system for self-hosted GitHub Actions runners.
The following sections document the installation process of Actions Runner Controller (ARC from now on), a Kubernetes operator maintained directly by Github that dynamically provisions and scales runners as Kubernetes pods.

## Prerequisites
- Basic knowledge of what GitHub Actions runners are, in particular self-hosted ones. Check out the official [documentation](https://docs.github.com/en/actions/concepts/runners/self-hosted-runners).
- Basic knowledge of Kubernetes, this guide uses k3s, a lightweight Kubernetes distribution. Check out the official [documentation](https://docs.k3s.io/).
- Basic knowledge of Helm. Check out the official [documentation](https://helm.sh/docs/intro/introduction)

## Summary

1. [Setting up k3s and Helm](./02-setting-up-k3s-and-helm.md): this section documents the needed steps to set up a working k3s cluster (composed of just the Control Plane) and Helm.
2. [Installing ARC](./03-installing-arc.md): this section documents how to configure and install the two Helm charts that compose ARC, doing so
requires authenticating to GitHub. This is covered in [Authentication with a GitHub App](./04-authentication-with-github-app.md).
3. [Adding nodes to the k3s cluster](./05-adding-nodes-to-the-cluster.md): this section documents how you can expand your cluster by adding more nodes, either manually or through a more automated approach.