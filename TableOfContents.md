# Modules #


---



---


## Query GUI ##
**Status:** <font color='gray'>Yet to begin</font>

**Module Description:** GUI for letting teacher chooses the topic. This module will be the initial face for the software. The teacher will have to choose from either a list of keywords or will enter a new topic for initiating a tutorial.

**Involved files:**

**Input:** Some way to let teachers access this software.

**Output:** Pass the query to the code crawling subsystem.

**Story points:**

  * Initially set up a page that would contain a blank text box and also a hard-coded list of topics to browse through.
  * In future, this list can be generated according to history of searches or whatever other strategy relevant.

**Other Notes:**


---


## Code crawler ##
**Status:** <font color='orange'>In Progress</font>

**Module Description:** It will query a code repository and return code samples in response to a teacher-specified query indicating a subject for which the teacher wishes to create a tutorial.

**Involved files:**
  * /build/src/itjava/model/LinkStore.java
  * /build/src/itjava/model/ResultEntry.java
  * /build/src/itjava/model/ResultEntryStore.java
  * /build/src/itjava/presenter/CodeSearchPresenter.java
  * /build/src/itjava/tests/JSoupTest.java
  * /build/src/itjava/tests/LinkStoreTest.java

**Input:** Query. i.e. name of the topic.

**Output:** A list of files or a list of lines of code that are relevant with the topic searched.

**Story points:**

  * Identify actual repositories eg. Apache, eclipse, etc. that can support querying.<font color='green' size='3'> DONE </font>
  * Does google code do something similar too? Find other projects and find out if they have some repositories or API that can be used. <font color='green' size='3'> DONE </font>
  * Set up required class structure for Matt.<font color='green' size='3'> DONE </font>
  * CodeSearchPresenter will be an interface for accessing the code search functionality. After initializing the CodeSearchPresenter object, every call to SearchNext() will return an ArrayList < ResultEntry > which is basically a collection of USEFULL code samples returned by search engines. The set up has been done in such a way that every time we perform a SearchNext(), previos results will not be returned again. <font color='green' size='3'> DONE </font>
  * CodeSearchPresenter uses LinkStore.CreateLinks to store a String[.md](.md) of urls returned by search engines. IMPLEMENT CreateLinks(). Basic structure is provided. <font color='blue' size='3'>TO BE DONE</font>
  * The array of links is provided to ResultEntryStore.createResultEntryList(). This function should iterate through all the provided links and return an ArrayList < ResultEntry >. Points to note: <font color='blue' size='3'>TO BE DONE</font>
    * Each page (i.e. actual HTML returned by the link) can consist of multiple code tags. All these codes should be converted into individual ResultEntry objects. **Do Not Collate all code tags** for a link.
    * Take notes regarding what are the type of samples of code that appear in these code tags that are not Java programs. example : SQL statements.
  * Identify initial pool of topics that can be deemed important by a Java tutor and search for topics in **normal** YAHOO search. Judge the relevance of the code samples returned for pedagogy. While doing so, note down observations regarding what makes a program fit to be a tutorial. eg. if a program has some standard Java API like Applet, File, etc. then it might serve as a better tutorial than some program that uses a lot of user defined classes.<font color='blue' size='3'>TO BE DONE</font>
  * Based upon the observations devise an algorithm that will select 10 tutorial-fit samples from all the Result Feed Entries.

  * Other Notes:


---


## Suggesting words to hide ##

**Status:** <font color='green' size='3'> DONE </font>

**Module Description:** Identifying the words of code to be hidden for tutorial. This decision will be based on the query made by the teacher and the code returned by the code crawler module.

**Involved program files:**

**Input:** The code crawler will hand over the list of files (or lines of code) along with the initial query to this module.

**Output:** It will create a list of configuration objects. Each object will consist of tutorial information and the source code. This list will be passed to the teacher for making a final choice.

**Story points:**
  * Understand the working of AST API. Work with sample files to produce AST and save various nodes of a source code in an easily accessible form. Enable addition of new node types for future. <font color='green' size='3'> DONE </font>
  * Based on the query OR common nodes, decide a strategy (TermFrequencyInverseDocumentFrequency) to find words to be blanked. Apply this strategy to multiple examples to verify sanity of the approach. Currently finding common nodes in :
    * Import declarations
    * Method invocations (example : socket.**close**();)
    * Variable declaration ( **ServerSocket** ss;)
    * Class instance creation ( ss = _new_ **ServerSocket**(0); )
    * Property Assignment ( len = intArr.**length**; )
<font color='green' size='3'> DONE </font>

  * Send the list of words and the respective source code to tutorial generation GUI subsystem. Verify whether the integration of these 2 modules work. <font color='green' size='3'> DONE </font>


**Other Notes:**


---


## GUI to select tutorial ##
**Status:** <font color='gray'>Yet to begin</font>

**Module Description:** Display the list of source code along with the respective words suggested to be blanked. The teacher should be able to see the words suggested as blank-able as a list of check boxes. These words must also be easily visible on the actual source code.

**Involved program files:**

**Input:** A list of source code and its respective blank-able words (with all the location information), i.e. the configuration object.

**Output:** Teacher selects one or more of the checkboxes and finalizes the tutorial. She should have an option of rejecting a tutorial. Also she should have an option of creating her own blank-able word from the provided source code if she doesn’t like our suggested words. (In short: o/p will be list of code and list of finalized config objects).

**Story points:**

  * Each of the page should display code and suggestion of words that can be blanked. This list of words should be provided in form of a checkbox list. Each of these words should be easily found on the main source code too. Use color coding or underline or arrow or whatever suits the purpose.

  * Set up a GUI system that will provide multiple such pages. There should be some hint for the teacher to show how many samples (i.e. pages) are available and her progress. She should be able to jump to the end if she wants to select only a few and not reach till the last sample of code.

  * Current plan should be satisfied by these actions. But for future, provide the teacher with a GUI that will let her choose words from the source code.

**Other Notes:**


---


## Create student interface-CTAT file ##
**Status:** <font color='orange'>In Progress</font>

**Module Description:** Converting code to tutorial when all information is available.
Involved program files:

**Input:** This module will be called after relevant code has been searched from the repository. It will also receive information regarding the words (& its location in the code) to be hidden in the tutorial.

**Output:** It will create a source code file that can be fed to CTAT for Java, which will eventually open it as a tutorial.

**Involved program files:**
  * /build/src/itjava/model/Tutorial.java
  * /build/src/itjava/model/TutorialStore.java
  * /build/src/itjava/model/WordInfo.java
  * /build/src/itjava/presenter/TutorialPresenter.java
  * /build/src/itjava/tests/TutorialPresenterTest.java

**Story points:**
  * The static fields of the CTAT-GUI source code file should be sought from a static class or from a text file for enabling changes in future. Identify these static fields and create required architecture. <font color='green' size='3'> DONE </font>
  * This module will be triggered along with list of config objects, i.e. the list of choices finalized by the teacher. <font color='green' size='3'> DONE </font>
  * Compile the CTAT readable java file into a class file (bytecode). Assign the path of this file to the Tutorial object so that it can be accessed easily. Find out way to compile and execute java programs from within another java program OR devise architecture to trigger it from outside.
  * Currently, CTAT has libraries that can be configured with Net Beans. So we can easily open up the student interface on providing .class file to netbeans. Figure out a way to do this independent of NetBeans.

**Other Notes:**


---


## Behavior Recorder ##
**Status:** <font color='orange'>In Progress</font>

**Module Description:** Setting up behavior recorder mechanism.

**Involved program files:** CTAT, Java, Java class file

**Input:** This module will be called after the .java file, its corresponding compiled .class file and .brd file is obtained.

**Output:** It will create a behavior recorder file (of extension .brd). This file contains complete information about how the tutor must respond to different inputs given by students for questions asked in the tutorial. The teacher can set different alert messages/hints to appear based on answers given to questions.

**Story points:**

  * BRD file creation process needs to be automated eg. Using a batch file or from within a Java program. As a first step, identify the bits and pieces of information that constitutes the .brd file. Make a list of nodes in the .brd file that represent the blank fields, messages, error words, error messages AND redundant code that can be replicated for all the .brd files. <font color='blue' size='3'>TO BE DONE</font>
  * Given a _HashMap<**WordInfo**, ArrayList<**ErrorObject**>>_, write a java program that will fill in the nodes of the **.brd** file that stand for the blank nodes. See the details of _WordInfo_ from the package **itjava.model.WordInfo**. From the observations in point 1, create a concrete class _ErrorObject_ (or whatever name is suitable) that will denote the incorrect answers entered by the teacher and respective error message. <font color='blue' size='3'>TO BE DONE</font>
  * Tweak the java program to be more modular and easier to extend for future additions. <font color='gray' size='1'>Not a priority</font>



**Other Notes:**


---


## Delivering tutorial to students ? ##
**Status:** <font color='orange'>In Progress</font>

**Input:** Apache Ant, Java file, compiled class file

**Output:** Web tutor needs to be hosted in a webserver and be available for all students.

**Story points:**
  * Understand the architecture used by CTAT to deliver tutorials.<font color='green' size='3'> DONE </font>
  * Implement one sample example on box or on any web server to verify.<font color='green' size='3'> DONE </font>
  * Note down the (manual) steps and required set up required to accomplish above 2 tasks.<font color='green' size='3'> DONE </font>
    * build.properties file in the CTAT deploy-tutor folder is edited with information regarding webserver to be used.
    * Apache ant is installed and "ant clean deploy-jars" command is executed to remove all class files, jar files, source backups and copy jar files to their destination folder.
    * After a set of Signing JAR messages transfer the entire tree of .jar files to the 'lib' folder in the webserver location.
    * The second interactive Ant target is "ant build-only" which interactively asks for the path of various files needed (java, class and brd file) and builds it.
    * After build is complete, a jar, jnlp and html file is created. These files are pasted into the webserver host location and is ready for anytime launch using Javawebstart.
  * Verify if the 'lib' folder containing jar files is generic and common for all files hosted in the webserver. Test using 2 example appliations given by CTAT.<font color='blue' size='3'>TO BE DONE</font>
  * Generate .jnlp file by programming. <font color='blue' size='3'>TO BE DONE</font>

**Other Notes:**


---


## Other Topics ##

  * **Setting up your box?**

  * **[Setting up Netbeans for CTAT](http://ctat.pact.cs.cmu.edu/index.php?id=netbeans50)**

  * **[Using GWT with NetBeans IDE](http://www.netbeans.com/kb/docs/web/quickstart-webapps-gwt.html)**

  * **[Presentation on GWT by developer at Sun](http://www.javapassion.com/ajax/GWT.pdf)**

  * **[GWT: Getting started Tutorial](http://code.google.com/webtoolkit/doc/latest/tutorial/create.html)**

  * **[GWT: Making remote procedure Calls](http://code.google.com/webtoolkit/doc/latest/tutorial/create.html)**

  * **[Maintaining the wiki](http://code.google.com/p/support/wiki/WikiSyntax)**

  * **[Help with SVN plugin for eclipse](http://agile.csc.ncsu.edu/SEMaterials/tutorials/subclipse)**


---
