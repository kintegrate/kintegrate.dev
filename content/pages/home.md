---
title: Home
date: Last Modified
permalink: /
eleventyNavigation:
  key: Home
  order: 0
  title: Home
---

# Introduction

This guide contains tutorials and samples to get your apps quickly integrated with Kin. The content here supplements [Kin's SDK documentation](https://docs.kin.org/intro), which gives a more technical overview of the ecosystem.

However, the content here is designed to give you the main concepts you need to quickly set up Kin, with **the goal of 30 minute set ups** for your server and for your apps.

### Who this for

This guide is designed for:

1. Existing apps that want to integrate Kin
2. Developers wanting to build from the ground up with Kin in mind

### Basic requirements
As a developer, you will need basic knowledge of:
1. Git Repos
2. Command Line Interfaces
3. A free account on [Heroku](https://heroku.com/)

The server side tutorials are created on Heroku which abstracts services on AWS. However, the server code can easily be ported anywhere.


### Contributing
We welcome contributions to the guide and code referenced in it as well. Please see [CONTRIBUTING.md](https://github.com/kintegrate/homepage/blob/main/CONTRIBUTING.md) for details


---
## Getting Started
1. Go through the [Getting Started](https://kintegrate.netlify.app/tutorials/getting-started/) guide to register your app for rewards from the Kin Rewards Engine. This will give you environment variables you will later use in your apps and on your server.


2. Pick a [Tutorial](https://kintegrate.netlify.app/tutorials/) language of your choice and follow the steps to create a Kin Integrated App. You will need a tutorial both for:
    * Your app - e.g. Android, iOS, Unity
    * Your server - e.g. NodeJS, Python

For pure code samples, you can grab a [starter kit](https://kintegrate.netlify.app/starters/) and download to get running in 10 minutes or less. The starter kits contain:

1. A list of dependencies to pull to your app
2. A wrapper file that you drop into your app to immediately integrate Kin
3. A demo app using the wrapper file you can immediately fire away

### Wrapper files
The wrapper file is a simple abstraction that you drop to your app that:

1. Gives it an address on the Kin blockchain
2. Enables it to send and receive Kin
3. Enables it to check and display the Kin balance

Wrapper files for the server enable your server to:

1. Send Kin to your apps
2. Listen for transactions your apps make and reward them accordingly
