---
description: >-
  This is a step-by-step guide that will help you to setup the project and to
  run the application on your local machine. Please follow the instructions
  below to get familiar with the basic concepts.
---

# Getting Started

## Prerequisites

### Git

All Betbook source code can be found in this GitLab namespace: [https://git.betlab.com/betbook](https://git.betlab.com/betbook).

Please make sure you have an access to this namespace.

### NodeJS & NPM

We are using default NPM capabilities for running tasks and managing project dependencies. Minimum required [NPM](https://www.npmjs.com/) version is v6.1.0, [NodeJS](https://nodejs.org/en/) - v10.6.0.

{% hint style="info" %}
Some packages are stored within [http://npm.betlab.private](http://npm.betlab.private) registry \(e.g. [ui-kit](http://ui-kit.com)\) that is only accessible by VPN \(or from office\).
{% endhint %}

### Docker

Some tools \(e.g. [Wiremock](http://Wiremock.com)\) require [Docker](https://www.docker.com/) to be installed on your local machine. No additional configuration is required at the moment.

## Installation

Get the project sources from [https://git.betlab.com/betbook/fe](https://git.betlab.com/betbook/fe). Then go to the project root folder and install all dependencies:

```text
$ npm install
```

## Running The Application

Running the application locally is easy. First, you need to get [Wiremock](http://Wiremock.com) running on your local machine:

```bash
$ npm wiremock:start
```

This tool mocks server API and simplifies the development process.

Once you get [Wiremock](http://Wiremock.com) up and running you can start the application itself:

```bash
$ npm start
```

This will run the application build process in a development mode and will make the application available at [http://0.0.0.0:8080](http://0.0.0.0:8080) with help of the [webpack-dev-server](https://github.com/webpack/webpack-dev-server).

