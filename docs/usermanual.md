# User & Programmers Manual. 
​
## Prerequisites
In order to use the **program manager** the following is required:
​
* Follow the installation guide [](doc/InstallationGuide.md)
* Install FIWARE and cygnus microserices
* Install robot program manager microservices
​
## Configuration
​
During the installation you can configure the environment variables to configure the application:
 * FIREWARE_SERVER_IP IP of the node running FIWARE and Cygnus
 * FIREWARE_SERVER_PORT=1026 port of the FIWARE
 * ROBOT_IP=127.0.0.1 IP of robot communication port
 * ROBOT_PORT=10003 port of the robot (for some robot models its not needed)

​
## Program definition 

A **program definition** is an entity to be stored in the FIWARE Orion Context Brocker
It represents a robot program that is composed of multiple trajectories that could be divided into several layers.
A **program definition** uses the following datatypes with the following specifications:
* **Poses** that are defined by 6 numbers:
  * First three elements correspond to the X,Y,Z coordinates in millimiters
  * Last three elements corresponds to the 3 SORA angular components in radians. 
    The SORA vector is a 3D vector with orientation given by the rotation Axis and magnitude given by total angle of rotation in radians.  
* **Joints** are defined by a 6 dimensional array [J1, J2, J3, J4, J5, J6] where Ji corresponds to the i robot joint angle in radians.  

* **Program definition** properties: 
* **partId** identifies the work to be done. Does not have necessary to identify a physical part.
* **robot** is an optional field that specifies a intended robot for the final execution of the program
* **estimatedExecutionTime** is an optional parameter expresed in seconds
* **programInput** is the object that stores the information needed for instantiting a robot program executable
  * **robotPose** reference frame of the robot with respect to the global frame
  * **piecePose** reference frame of the piece (or a work frame of reference) with respect to the global frame
  * **home** is an optional **Joints** data type that is used as initial and final postion of the robot.
  * **tools** list of tools to be used by the robot, a tool is defined by the two properties: a name and the tcp (tool center point) that is of the Pose type just defined.
  * **layers** array of layers, a layer is an enumeration of trajectories 
    * **trajectory** 
      * **tool** tool to be used for the given trajectory
      * **pathposes** poses with respect to the global frame that will be follow by the robot
      * **stopMessage** if speficied the robot will stop waiting for an event or action performed by an agent (like an operator)
      * **velocity** velocity expressed in percentage

## Sending a program defintion to the FIWARE Orion Context Broker

Send the program definition entity to the FIWARE Context Broker: 

```json
"curl [ip_address]:[port]/v2/entities[
    {
      "id": "bfd1d41b-7437-4479-8498-a41e4dff3ccf",
      "type": "laminationDefinition",
      "partId": "mixed_geometry",
      "comment": "program for superficial treatment process",
      "robot": "Elfin5",
      "estimatedExecutionTime": "65.000",
      "programInput": {
        "partId": "mixed_geometry",
        "comment": "  _  ",
        "robot": "Elfin5",
        "home": [ 0.000, -0.053, -1.610, 0.000, -1.584, 0.000 ],
        "robotPose": [ 0.000, 0.000, 0.000, 0.000, 0.000, 0.000 ],
        "piecePose": [ 0.000, 0.000, 0.000, 0.000, 1.571, 0.000 ],
        "tools": [          
          {
            "name": "roller",
            "tcp": [ -26.597, 59.309, 236.000, -0.008, 0.005, -1.149 ]
          },
          {
            "name": "sphere",
            "tcp": [ -24.551, 54.747, 236.000, 0.000, 0.000, 0.422 ]
          }
        ],
        "layers": [
          {
            "layerNumber": 1,
            "trajectories": [
              {
                "tool": "sphere",
                "pathPoses": [
                  [ -442.624, 87.069, 74.161, 2.790, -0.126, -0.034 ],
                  [ -444.369, 71.777, 31.874, 2.790, -0.126, -0.034 ],                 
                  [ -626.188, 17.750, 17.514, -2.255, -2.187, 0.000 ],
                  [ -626.188, 17.750, 30.014, -2.255, -2.187, 0.000 ],
                  [ -626.188, 17.750, 75.014, -2.255, -2.187, 0.000 ]
                ],
                "stopMessage": "Put sphere on the robot",
                "velocity": "20.000"
              },
              {
                "tool": "sphere",
                "pathPoses": [
                  [ -426.598, -49.327, 72.000, -2.211, 2.232, 0.000 ],
                  [ -426.598, -49.327, 27.000, -2.211, 2.232, 0.000 ],
                  [ -426.598, -49.327, 14.500, -2.211, 2.232, 0.000 ],                 
                  [ -425.752, 41.608, 75.000, -2.211, 2.232, 0.000 ]
                ],
                "stopMessage": "",
                "velocity": "20.000"
              }
            ]
          }
        ]
      }
    }  

]
```
### Managing the robot program definition through the **program manager**

 * Open the link http://localhost:81/ on a webwroser
 * The **Robot Program Manager** application should open:
 
    ![](/assets/robot_program_manager_01.png)

 * On the robot program definitions table are listed the **program definition** entities:
   On the Robot column, we can open the **Robot** column to select the post-processor that we want to select to build robot program executable. Usually, the name of the postprocessor matches the name of the robot for which we want to generate the executable but we could have several postprocessors for the same robot model.
   * If we press the build button a robot program entity is going to be created by the selected post-processor.
   * This robot entity just created appears on the right table **Robot programs**
 * On the **Robot programs table** the **robot program** entities are managed:
   * The new program just defined could be downloaded to the robot memory.
   * After the robot program is tested on the robot it could suffer some modifications to adapt it to the real robot enviroment, or even introducing entire new branches of code.
   * After the robot program is validated on the robot if the program has had changes it can be uploaded to back to the FIREWARE.
   * Finally we can press on the red label "not validated" to the state "validated" to indicate that this program could safely be deployed for production.

### Robot program entity

Given a program_definition_id we can retrieve from the Orion Context Broker the all the robot programs generated for that program definition:

```
curl [ip_address]:[port]/v2/entities?laminationDefinitonId=program_definition_id&options=keyValues
```

The robot program entity generated by the post-processor microservice has the following form:


```
{
  "id": "5d51f7ae-e72e-4276-ac70-10ee816d9179",
  "type": "laminationRobotProgram",
  "laminationDefinitonId": "5a1a6d4a-7d1f-4471-9f4e-7ddf2621cc65",
  "partId": "mixed_geometry",
  "comment": "Elfin5 program for superficial treatment process",
  "robot": "Elfin5",
  "estimatedExecutionTime": "65.000",
  "validated": false,
  "programCode": "PD94bWwgdmVyc2lvbj0iMS4m90SUQ9nQ9IjAiIC8+CjxGdW5", 
  "programEncoding": "base64"
}
```
* **Robot program** properties: 
  * **validated** is set to true if the robot program has already been validated and therefore can be used for normal production
  * **programCode** is the robot program generated by the post-processor given by **robot** and that is encoded with the method signaled by the property **programEncoding**
