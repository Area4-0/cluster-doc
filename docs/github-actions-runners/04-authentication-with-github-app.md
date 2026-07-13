# Authentication with a GitHub App

This page explains how to create and configure a GitHub App to authenticate yourself to GitHub API.

## What is a GitHub App?

A GitHub App is an identity that can act on GitHub's API independently from
any single user account. Unlike a personal access token, which is tied to a
specific user and inherits all of their permissions, a GitHub App has its own
scoped permissions and is installed on the specific organizations or
repositories it needs to access.

## Creating a GitHub App

From your profile/organization go to `Settings` **>** `Developer Settings` **>** `GitHub Apps`, you should now see a `New GitHub App` button.

Now that you are on the `Create GitHub App` page, you must provide a unique name for your app, something like 'API-authentication-app', and an `Homepage URL`, here you can just insert your profile/organization URL.

Leave the `Identifying and authorizing users` and `Post installation` sections to the default/blank values, next disable the `Active` checkbox in the `Webhook` section.

In the `Permissions` section you can specify what permissions your app should have when installed, it is recommended to grant just the permissions needed.
If you are reading this to authenticate ARC, there are three different scenarios depending at what level you want your runners to be registered on:

- If you intend to use the runners for a specific repository on your personal profile, you will just need: `Administration (Repository permissions): Read and write` permissions.
- If you intend to use the runners for a specific repository inside an organization, you will need `Administration (Repository permissions): Read and write` and `Self-hosted runners (Organization permissions): Read and write` permissions.
- If you intend to use the runners for an organization, you will just need `Self-hosted runners (Organization permissions): Read and write` permissions.

Lastly, for the `Where can this GitHub App be installed?` option, you are free to choose the most appropriate setting.

You can now create your App.

## Generating a private key

After creating the App, scroll down in the `General` tab to the `Private keys` section, then click on `Generate a private key`.
This downloads a `.pem` file that contains your App private key.

## Installing the App

Go to the `Install App` tab and select the account/organization you want to install the App on. Now you can also choose to grant the permissions the App needs to all repositories or just the ones you select.

## Retrieving the credentials you will need

Once created and installed, you'll need these three values to authenticate as the App:

- **App ID**: shown on the App's settings page.
- **Private key**: the `.pem` file downloaded earlier.
- **Installation ID**: Go to `Settings` **>** `Applications` / `GitHub Apps` (depending if you are on a normal account or an organization) and click on the `Configure` button of your App. Now check the URL, you should see something like `/installations/130228035`, the last number is your Installation ID.

If your goal is to authenticate ARC, you can now go back to the installation page [here](./03-installing-arc.md).
If your goal is to authenticate to GitHub REST API, check out [this page](https://docs.github.com/en/apps/creating-github-apps/authenticating-with-a-github-app/authenticating-as-a-github-app-installation) that will explain you how to use these credentials.