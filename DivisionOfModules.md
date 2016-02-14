# Division of the Project in modules #


---



---


## Query GUI ##
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

**Module Description:** It will query a code repository and return code samples in response to a teacher-specified query indicating a subject for which the teacher wishes to create a tutorial.

**Involved files:**

**Input:** Query. i.e. name of the topic.

**Output:** A list of files or a list of lines of code that are relevant with the topic searched.

**Story points:**

  * Identify actual repositories eg. Apache, eclipse, etc. that can support querying.<font color='green'> DONE </font>
  * Does google code do something similar too? Find other projects and find out if they have some repositories or API that can be used. <font color='green'> DONE </font>
  * Get Google Code Search working in eclipse. Research on information provided by each feed. Create a simple test file that fires a query and prints 10 different samples with lines of code more than 10 and lines of code less than 100. Do not consider comments as line of code.
  * Identify initial pool of topics that can be deemed important by a Java tutor and search for topics using . Judge the relevance of the code samples returned for pedagogy. While doing so, note down observations regarding what makes a program fit to be a tutorial. eg. if a program has some standard Java API like Applet, File, etc. then it might serve as a better tutorial than some program that uses a lot of user defined classes.
  * Based upon the observations devise an algorithm that will select 10 tutorial-fit samples from all the ResultFeedEntries. <font color='red'>MOST IMP</font>

  * Other Notes:


---


## Suggesting words to hide ##

**Module Description:** Identifying the words of code to be hidden for tutorial. This decision will be based on the query made by the teacher and the code returned by the code crawler module.

**Involved program files:**

**Input:** The code crawler will hand over the list of files (or lines of code) along with the initial query to this module.

**Output:** It will create a list of configuration objects. Each object will consist of tutorial information and the source code. This list will be passed to the teacher for making a final choice.

**Story points:**
  * Understand the working of AST API. Work with sample files to produce AST and save various nodes of a source code in an easily accessible form. Enable addition of new node types for future. <font color='green>DONE</font'><b><ul><li>Based on the query OR common nodes, decide a strategy to find words to be blanked. Apply this strategy to multiple examples to verify sanity of the approach.</b><font color='orange'>IN PROGRESS</font><b></li><li>Send the list of words and the respective source code to tutorial generation GUI subsystem.</li></ul></b>

<b>Other Notes:</b>

<hr />

<h2>GUI to select tutorial</h2>

<b>Module Description:</b> Display the list of source code along with the respective words suggested to be blanked. The teacher should be able to see the words suggested as blank-able as a list of check boxes. These words must also be easily visible on the actual source code.<br>
<br>
<b>Involved program files:</b>

<b>Input:</b> A list of source code and its respective blank-able words (with all the location information), i.e. the configuration object.<br>
<br>
<b>Output:</b> Teacher selects one or more of the checkboxes and finalizes the tutorial. She should have an option of rejecting a tutorial. Also she should have an option of creating her own blank-able word from the provided source code if she doesn’t like our suggested words. (In short: o/p will be list of code and list of finalized config objects).<br>
<br>
<b>Story points:</b>

<ul><li>Each of the page should display code and suggestion of words that can be blanked. This list of words should be provided in form of a checkbox list. Each of these words should be easily found on the main source code too. Use color coding or underline or arrow or whatever suits the purpose.</li></ul>

<ul><li>Set up a GUI system that will provide multiple such pages. There should be some hint for the teacher to show how many samples (i.e. pages) are available and her progress. She should be able to jump to the end if she wants to select only a few and not reach till the last sample of code.</li></ul>

<ul><li>Current plan should be satisfied by these actions. But for future, provide the teacher with a GUI that will let her choose words from the source code.</li></ul>

<b>Other Notes:</b>

<hr />

<h2>Create student interface-CTAT file</h2>

<b>Module Description:</b> Converting code to tutorial when all information is available.<br>
Involved program files:<br>
<br>
<b>Input:</b> This module will be called after relevant code has been searched from the repository. It will also receive information regarding the words (& its location in the code) to be hidden in the tutorial.<br>
<br>
<b>Output:</b> It will create a source code file that can be fed to CTAT for Java, which will eventually open it as a tutorial.<br>
<br>
<b>Story points:</b>
<ul><li>The static fields of the CTAT-GUI source code file should be sought from a static class or from a text file for enabling changes in future. Identify these static fields and create required architecture.<font color='green>DONE</font'><b></li><li>This module will be triggered along with list of config objects, i.e. the list of choices finalized by the teacher.</b><font color='green>DONE</font'><b></li><li>Compile the CTAT readable java file into a class file (bytecode). Assign the path of this file to the Tutorial object so that it can be accessed easily. Find out way to compile and execute java programs from within another java program OR devise architecture to trigger it from outside.<br>
</li><li>Currently, CTAT has libraries that can be configured with Net Beans. So we can easily open up the student interface on providing .class file to netbeans. Figure out a way to do this independent of NetBeans.</li></ul></b>

<b>Other Notes:</b>

<hr />

<h2>Behavior recorder</h2>

<b>Module Description:</b> Setting up behavior recorder mechanism.<br>
<br>
<b>Involved program files:</b>

<b>Input:</b> This module will be called after...<br>
<br>
<b>Output:</b> It will ...<br>
<br>
<b>Story points:</b>

<b>Other Notes:</b>

<hr />

<h2>Delivering tutorial to students ?</h2>

<hr />

<h2>Other Topics</h2>

<ul><li><b>Setting up your box?</b></li></ul>

<ul><li><b><a href='http://ctat.pact.cs.cmu.edu/index.php?id=netbeans50'>Setting up Netbeans for CTAT</a></b></li></ul>

<ul><li><b><a href='http://www.netbeans.com/kb/docs/web/quickstart-webapps-gwt.html'>Using GWT with NetBeans IDE</a></b></li></ul>

<ul><li><b><a href='http://www.javapassion.com/ajax/GWT.pdf'>Presentation on GWT by developer at Sun</a></b></li></ul>

<ul><li><b><a href='http://code.google.com/webtoolkit/doc/latest/tutorial/create.html'>GWT: Getting started Tutorial</a></b></li></ul>

<ul><li><b><a href='http://code.google.com/webtoolkit/doc/latest/tutorial/create.html'>GWT: Making remote procedure Calls</a></b></li></ul>

<ul><li><b><a href='http://code.google.com/p/support/wiki/WikiSyntax'>Maintaining the wiki</a></b></li></ul>

<ul><li><b><a href='http://agile.csc.ncsu.edu/SEMaterials/tutorials/subclipse'>Help with SVN plugin for eclipse</a></b></li></ul>

<hr />