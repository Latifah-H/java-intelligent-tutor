
---



---


## Local Machine Path ##

**File - itjava.data.LocalMachine.java**

Edit value of string "home" to project Workspace location.
eg. public static String home = "C:/Project/myworkspace/itjava/";

## autoBuild Path ##

**File - autoBuild.bat**

Edit the path of deploy-tutor location inside workspace.
eg. C:\Project\myworkspace\itjava\automate\deploy-tutor

## Project Directory Path in build.xml ##

**File - build.xml**

Set projects-dir to workspace home.
eg. 

&lt;property name="projects-dir" value="C:/Project/myworkspace/itjava/"/&gt;



## Delivery Folder Path in build.xml ##

**File - build.xml**

Edit tmp\_jar\_location to webcontent delivery folder.
eg. 

&lt;property name="tmp\_jar\_location" value="C:/Project/myworkspace/itjava/WebContent/delivery"/&gt;



## keystore Path in build.xml ##

**File - build.xml**

Edit keystore value to point to the PACTkeystore file in "lib".
eg. 

&lt;signjar jar="${tmp\_jar\_location}/${jar-file}" keystore="C:/Project/myworkspace/itjava/automate/lib/PACTkeyStore" alias="mike" storepass="pact123" /&gt;

