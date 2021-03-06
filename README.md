# Mozilla Experimenter

[![CircleCI](https://circleci.com/gh/mozilla/experimenter.svg?style=svg)](https://circleci.com/gh/mozilla/experimenter)
[![What's deployed on dev,stage,prod?](https://img.shields.io/badge/whatsdeployed-dev,stage,prod-green.svg)](https://whatsdeployed.io/s/uFe)

<p align="center">
  <img src="https://cdn1.iconfinder.com/data/icons/simple-arrow/512/arrow_20-128.png"><br/>
  <b>1. Design 2. Launch 3. Analyze</b>
  <br><br>
</p>

Experimenter is a platform for managing experiments in [Mozilla Firefox](https://www.mozilla.org/en-US/firefox/?utm_medium=referral&utm_source=firefox-com).

## Deployments

### Staging

<https://stage.experimenter.nonprod.dataops.mozgcp.net/>

### Production

<https://experimenter.services.mozilla.com/>

## What is an experiment?

An experiment is a way to measure how a change to your product affects how people use it.

An experiment has three parts:

1. A new feature that can be selectively enabled
1. A group of users to test the new feature
1. Telemetry to measure how people interact with the new feature

## How do I run an experiment?

<p align="center">
  <img src="https://raw.githubusercontent.com/mozilla/experimenter/164/app/experimenter/static/imgs/architecture.png"><br/>
</p>

1. Build a new feature behind a pref flag
1. Define an experiment for that feature in Experimenter
1. Send it to Shield
1. After Shield reviews and approves it, it is sent to Firefox
1. Firefox clients check whether they should enroll in the experiment and configure themselves accordingly
1. Telemetry about the experiment is collected
1. Dashboards are created to visualize the telemetry
1. Analyze and collect the results to understand how the new feature impacted users
1. Do it again!

## Installation

1.  Install [docker](https://www.docker.com/) on your machine

1.  Clone the repo

        git clone <your fork>

1.  Copy the sample env file

        cp .env.sample .env

1.  Set DEBUG=True for local development

        vi .env

1.  Create a new secret key and put it in .env

        make secretkey

1.  Run tests

        make test

1.  Setup the database

        make refresh

1.  Run a dev instance

        make up

1.  Navigate to it and add an SSL exception to your browser

        https://localhost/

Done!

## Usage

Experimenter uses [docker](https://www.docker.com/) for all development, testing, and deployment.

The following helpful commands have been provided via a Makefile:

### build

Build the application container by executing the [build script](https://github.com/mozilla/experimenter/blob/main/scripts/build.sh)

### compose_build

Build the supporting services (nginx, postgresql) defined in the [compose file](https://github.com/mozilla/experimenter/blob/main/docker-compose.yml)

### up

Start a dev server listening on port 80 using the [Django runserver](https://docs.djangoproject.com/en/1.10/ref/django-admin/#runserver)

### test

Run the Django test suite with code coverage

### lint

Run flake8 against the code

### check

Run both test and lint

### migrate

Apply all django migrations

### createuser

Create an admin user in the local dev instance

### load_locales_countries

Populates locales and countries

### load_dummy_experiments

Populates db with dummy experiments

### shell

Start an ipython shell inside the container (this lets you import and test code, interact with the db, etc)

### bash

Start a bash shell inside the container (this lets you interact with the containerized filesystem)

### ssl

Create dummy SSL certs to use the dev server over a locally secure
connection. This helps test client behaviour with a secure
connection. This task is run automatically when needed.

### kill

Stop and delete all docker containers.
WARNING: this will remove your database and all data. Use this to reset your dev environment.

### refresh

Run kill, migrate, load_locales_countries load_dummy_experiments

### up_all

Start up a normandy and delivery console instance. Prereqs. Symlink normandy and delivery console eg. `ln -s ../normandy normandy`, ensure user is assigned superuser status

### integration_test

Run the integration test suite inside a containerized instance of Firefox. You must also be already running a `make up` dev instance in another shell to run the integration tests.

### integration_vnc_up

Start a linux VM container with VNC available over `vnc://localhost:5900` with password `secret`. Right click on the desktop and select `Applications > Shell > Bash` and enter `tox -c tests/integration/` to run the integration tests and watch them run in a Firefox instance you can watch and interact with.

## API

API documentation can be found [here](https://htmlpreview.github.io/?https://github.com/mozilla/experimenter/blob/main/app/experimenter/docs/swagger-ui.html)

## Contributing

Please see our [Contributing Guidelines](https://github.com/mozilla/experimenter/blob/main/contributing.md)

## License

Experimenter uses the [Mozilla Public License](https://www.mozilla.org/en-US/MPL/)
