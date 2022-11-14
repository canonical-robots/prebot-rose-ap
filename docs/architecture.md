# PREBOTS ROSE-AP architecture
The general **architecture** of the **PREBOTS ROSE-AP** is described below:

## Contents
-   [Robot program management](#Robot&nbspprogram&nbspmanagement)
-   [Data provisioning](#Data&nbspprovisioning)

## Robot program management

The **Robot Program Management** is done by the interplay of a web application (**Robot Program Manager**) that allows managing the state of the robot programs and its generation, and two microservices:
* **Robot Post Processor** is a microservice in charge of a given **program definition** entity translating it to a concrete instance of a **robot program**. Several **Robot Post Processor microservices** could be subscribed to the **Robot Program Manager**. 
* **Robot communication service** that is in charge of **download/upload** a given **robot program** between the **FIWARE Orion Context Broker** and the **Robot**.

![](/assets/architecture_01.png)

## Data provisioning

**Data Provisioning** for the **RAMP Superset Dashboard** has been done using using the following deployment:

![](/assets/architecture_02.png)

* In this diagram the central part is the **Fiware Orion Context Broker** that centralizes the information.
* The **Robot Reporter** monitors de production activity and sends production and error reports that are then sent to the **Context Broker**.
* **Cygnus** is then used to store all the changes of the production-related entities collected by the Robot Reporter   This is done through event subscritions to the Fiware Context Broker.
* Crate updater is a deployed application that makes use of the **CRATE database**. Its role is to regularly read the **hystoric information** stored by **Cygnus** in the **Mongo database** to fill several tables defined in the **CRATE dabase**.
* The **CRATE database** data is finaly used by the **RAMP Superset Dashboad**.

In the following **diagram**, the flow of information of the **Data Provisioning** of the **ROSE-AP** can be better understood.

![](/assets/architecture_03.png)