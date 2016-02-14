# Web-based Semi-Automatic Authoring of Intelligent Java Tutor #

## Summary ##

The current tutoring systems for the Java API lack breadth  in offered examples and effective feedback. This project is aimed at developing an Intelligent Java Tutor  that will  semi-automate the process of creating tutorials and thereby  help students  to  learn from example code snippets. The effectiveness of the system will be evaluated by conducting laboratory user studies on teachers and students.

Research shows that it is  hard  to learn  the  Java Programming language in part due to the huge number of APIs.  Understanding APIs can be difficult because they present a steep upslope in the number of concepts that must be mastered. Currently, there are two main ways for learning the
Java API. First, there are websites and various books
on Java. These resources help in finding the description of  the various Java APIs. Second, there are tutoring systems like Java Intelligent Tutoring Systems (JITS) that evaluate the students on tutorials created by the teacher. In a summative evaluation it was found that 71% students and 75% teachers who used JITS agreed that JITS promotes learning better than the  available alternatives.

However, these systems need to be configured by a human tutor  through a  time-consuming  process. The necessary configuration steps that include writing example programs, writing quizzes, mapping quiz answers to a model of knowledge, and specifying how a student’s knowledge should control the sequence of examples and quizzes in the interactive tutorial.

In order to provide a method so teachers can more quickly create effective intelligent tutors, we need to provide a new method that a) uses a widely accessible platform, b) reduces teacher’s effort to create tutorials, and c) yields tutorials which are as effective as tutorials created by teachers using the traditional method.

We propose a system that would support this method. Below are the 4 pillars of the system:

  * **Code crawler:** It will query a code  repository and return code samples in response to a teacher-specified query indicating a subject for which the teacher wishes to create a tutorial

  * **Tutorial authoring (TA) module:** For teachers to generate and refine tutorials from code snippets obtained by the code crawler.

  * **GUI:** It will display the examples and quizzes to students in a simple form-like format.

  * **Wizard:** It will recognize student errors and will evaluate the alternate ways of solving a programming problem.