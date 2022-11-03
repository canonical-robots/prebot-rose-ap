
## Prerequisites
**Linux**: [Docker engine](https://docs.docker.com/engine/install/ubuntu/) 

**Windows**: 
  * [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/install)
  * [Docker Desktop on Windows](https://docs.docker.com/desktop/install/windows-install/)
  
## Install and run 

**Intall FIWARE and cygnus microserices**
* Open a command terminal in the folder [docker-fiware](docker-fiware)
* Run the following command in the terminal

    ```
    sudo docker-compose up -d
    ```
* Open postman
* Import the collection [SR001-Subscriptions.postman_collection.json](docker-fiware/SR001-Subscriptions.postman_collection.json)
* Execute the three subscriptions of the collection
* To check that the installation is OK execute
    ```
    sudo docker exec -it mongo  bash
    ```
* In the mongo termina introduce **mongo** and pulse enter
* Introduce **show dbs**, the following should appear:
 
    ![](/assets/database_fiware.png)

**Intall robot program manager microservices**
* Open the  [dev.env](docker-robotProgramManager/dev.env) file to configure the enviroment variables

* Open a command terminal in the same folder [docker-robotProgramManager](docker-robotProgramManager)

* Run the following command in the terminal

    ```
    sudo docker-compose up -d
    ```

To check if the application has started correctly:
 * Open the link http://localhost:81/ on a webwroser
 * The **Robot Program Manager** application should open:
 
    ![](/assets/robot_program_manager_empty.png)

**Install process data adquisition microservices**

* Open the  [dev.env](docker-elfin_robotreporter/dev.env) file to configure the enviroment variables

* Open a command terminal in the same folder [docker-elfin_robotreporter](docker-elfin_robotreporter)

* Run the following command in the terminal

    ```
    sudo docker-compose up -d
    ```

To check if the application has started correctly:
 * Open the link http://localhost:4200/ on a webwroser
 * The **CrateDB** inferface should open:

    ![](/assets/crateDB.png)


