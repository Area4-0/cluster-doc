# Introduction

This documentation describes how to configure an autoscaling system for self-hosted GitHub Actions runners.
The following sections document the installation process of Actions Runner Controller (ARC from now on), a Kubernetes operator maintained directly by Github that dynamically provisions and scales runners as Kubernetes pods.

## Prerequisites
- Basic knowledge of what GitHub Actions runners are, in particular self-hosted ones. Check out the official [documentation](https://docs.github.com/en/actions/concepts/runners/self-hosted-runners).
- Basic knowledge of Kubernetes, this guide uses k3s, a lightweight Kubernetes distribution. Check out the official [documentation](https://docs.k3s.io/).
- Basic knowledge of Helm. Check out the official [documentation](https://helm.sh/docs/intro/introduction)
