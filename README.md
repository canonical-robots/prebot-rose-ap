# prebot-rose-ap
### ROSE-AP supporting the management of robot program definitions that can be instantiated for different robot vendors and a management system for working with them.

[![License: Apache](https://img.shields.io/github/license/saltstack/salt)](https://www.apache.org/licenses/LICENSE-2.0.html#redistribution)

This project is part of [DIH^2](http://www.dih-squared.eu/). For more information check the RAMP Catalogue entry for the
[components](https://github.com/xxx).

| :books: [Documentation](https://roboweldar-rose-ap.readthedocs.io/en/latest/) | :whale: [Docker Hub](https://hub.docker.com/u/canonicalrobots) |
| --------------------------------------------- | ------------------------------------------------------------- |



## Contents

-   [Background](#background)
-   [Install](#install)
-   [Usage](#usage)
-   [Architecture](#architecture)
-   [Contributing](#contributing)
-   [License](#license)

## Background
This **ROSE-AP** is an IoT application for defining, building, and managing robot programs.
The **use case description** exposed below better conveys an idea of the **ROSE-AP** main features.

### Use case description
1. Using a cad designer a **program_definition** is generated. This **program_definition** is a JSON document that describes a robot program defining a series of trajectories that the robot is going to follow using a specific tool and velocity.
2. The **lamination_definition** is sent to the **Management System**.
3. Using the robot **program manager front-end** we select a **program_defintion** to generate a robot program executable for a particular robot model.
4. The **robot_program generated** is downloaded to a particular robot on the factory floor.
5. The robot engineer checks that the **robot_program** generated works correctly. 
6. If the robot engineer edits the program the **program manager front-end** is used to upload the edited program to the **Management System**.
7. Once the **robot_program** has been verified the robot engineer changes the state of the **robot_program** to verified using the **program manager front-end**.


## Install

Information about how to install the IoT **Robot Program Manager** can be found at the corresponding section of the
[Installation Guide](docs/InstallationGuide.md). 

Please visit the [step-by-step guide](docs/stepbystepguide.md) to setup a demonstration.

## Architecture

A description of the architecture can be found in the [Architecture documentation](docs/architecture.md)

## Usage

Information about how to use the ROSE-APP can be found in [User & Programmers Manual](docs/usermanual.md).

## Contributing

If you'd like to contribute, start by searching through the issues and pull requests to see whether someone else has raised a similar idea or question.
Before contributing, please check out [Contribution guidelines](docs/contributing.md).

## License

[Apache2.0](LICENSE) © 2022
