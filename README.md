# prebot-rose-ap
### ROSE-AP supporting the management of robot program definitions that can be instantiated for different robot vendors and a management system for working with them.

[![License: Apache](https://img.shields.io/github/license/saltstack/salt)](https://www.apache.org/licenses/LICENSE-2.0.html#redistribution)

| :whale:  [DockerHub](https://hub.docker.com/u/ittipl) |

## Use case description
1. Using a cad designer a **program_definition** is generated. This **program_definition** is a JSON document that describes a robot program defining a series of trajectories that the robot is going to follow using a specific tool and velocity.
2. The **lamination_definition** is sent to the **Management System**.
3. Using the robot **program manager front-end** we select a **program_defintion** to generate a robot program executable for a particular robot model.
4. The **robot_program generated** is downloaded to a particular robot on the factory floor.
5. The robot engineer checks that the **robot_program** generated works correctly. 
6. If the robot engineer edits the program the **program manager front-end** is used to upload the edited program to the **Management System**.
7. Once the **robot_program** has been verified the robot engineer changes the state of the **robot_program** to verified using the **program manager front-end**.



