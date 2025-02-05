# Goh Chok Yao - Project Portfolio Page

## Project: Modganiser

Modganiser provides effortless module planning at your fingertips via the Command Line Interface (CLI), focused on helping
Information Security Undergraduates graduate in 4 years. It allows you to plan all 4 years of your modules
to ensure that you meet your graduation requirements.


## Summary of contributions

### Code Contributed
* Please click on this [link to my RepoSense report](https://nus-cs2113-ay2223s2.github.io/tp-dashboard/?search=chokyao&breakdown=true&sort=groupTitle%20dsc&sortWithin=title&since=2023-02-17&timeframe=commit&mergegroup=&groupSelect=groupByRepos&checkedFileTypes=docs~functional-code~test-code~other) to view my code contributions.

### Enhancements Implemented
* Implemented the Delete Module Feature
  * Added the delete method in `ModuleList` class to enable deletion of modules from the plan

* Contributed to the Edit Module Feature
  * Handled the sections on editing grade, module type and module code in `ModuleList` class

* Implemented the Save User's Name Feature
  * Handled prompting and saving of user's name on user's first time starting up of the application 
  and added the ability to retrieve saved name on subsequent start-ups.

* Implemented the Save Modules Feature
  * Added the ability to save modules and constantly update the save file as the user makes changes to 
  his/her plans.

* JUnit Testing, Assertions, Logging 
  * Added Junit Testing and assertions for the `delete` command.
  * Added logging to `delete` and `save` commands.

* PE-D Bugs 
  * Squashed PE-D bugs related to corruption of save file where a corrupted save file will result in inability to start the application.
    **PR**: [#253](https://github.com/AY2223S2-CS2113T-T09-4/tp/pull/253)
<div style="page-break-after: always;"></div>

### User Guide
* Added section on delete modules feature 

### Developer Guide
* Added sections on Storage and Print components
* Added section on delete module
* Edited the section on the edit modules command
* Added the sequence diagram for delete module, editModuleCode and editModuleType
* Added both Appendices sections (Requirements and Instructions for Manual Testing)
  * Product Scope, User Stories, Use Cases and Non-Functional Requirements

### Team-based Tasks
* Released jar file for v2.0


### Reviewing / Mentoring
* Reviewing **PRs**: 

### Contributions beyond the project team
* Found and reported [PE-D bugs](https://github.com/chokyao/ped/issues) for team [Inka](https://github.com/AY2223S2-CS2113-F10-1/tp)

