# Developer Guide

## Acknowledgements

{list here sources of all reused/adapted ideas, code, documentation, and third-party libraries -- include links to the original source as well}


## Architecture

---

The Diagram below shows an overview of how components are linked together to produce Modganiser.

{image}

Main components of the architecture
`Duke` has a class called `Duke`.

* It starts the app up at the beginning and passes the relevant inputs to the `Parser` to be parsed.
* It saves the name of the user for future uses.
* It ends the program when called to.

Modganiser consists of :

1. `Storage`
2. `Parser`
3. `ModuleList`
4. `Print`

**How the components interact with each other**

When using the command `add /CS2113T /4 /CORE /1 /1` ,
The Sequence Diagram shows how the components interact with each other: 

{image}

### **Storage Component**

Firstly, the {explain workflow}

{uses}
*  It can save the name of the user into a file.
* The program can load data from the file when Modganiser starts up again.
* It can save changes to the file after each change such as an addition or deletion. 
This is done by using the methods 


### **Parser Component**

Firstly, the {explain workflow}

{uses}
* It calls the relevant methods according to the user input 


### **ModuleList Component**

Firstly, the {explain workflow}

{uses}
*

### **Print Component**


Firstly, the {explain workflow}

{uses}
*



## Design & implementations

---
### Proposed Implementation : **Manpage**

The Manpage is a class that is used to display parts of the manpage that is requested by the user.
It has multiple methods for separate features.

The sequence by which the ManPage class handles the `man` command is as follows:
1) The `Parser` class extracts the other fields of the user input, and calls upon the `checkUserInput()` method, 
if the command is not `man`, it will additionally call upon the `checkManPageInput()`.

2) It then uses the respective methods in the ManPage class to print out the requested feature.

`Manpage#printManPage()` - Prints the Command Summary.

`Manpage#printManPageAdd()` - Prints description of how to use the add feature.

`Manpage#printManPageList()` - Prints description of how to use the list feature.

`Manpage#printManPageEdit()` - Prints description of how to use the edit feature.

`Manpage#printManPageFind()` - Prints description of how to use the find feature.

`Manpage#printManPageDelete()` - Prints description of how to use the delete feature.

`Manpage#printManPageCalculator()` - Prints description of how to use the grade calculator.

`Manpage#printManPageUpdateGrade()` - Prints description of how to input grades.

`Manpage#printManPageExit()` - Prints description of how to use the exit feature.

![ManPage](diagrams/ManPage.png)

### Design Considerations : **Manpage**

**Alternative 1** : Prints the manual page individually as features. 
Pros: Avoids wordy and long manual page when command is man, ability to have more description
for specific features. Avoids long methods. 
Cons: Extra step of typing another command to understand a feature well.

**Alternative 2**: Combining all feature descriptions in a single manual page. 
Pros: Avoid extra step of typing another command to understand a feature well.
Cons: Wordy and long manual page when command is man, user has to scroll through
a long manual page to find what they need. Long method.

### Implementation: **Parser**

The `Parser` is a class that handles the commands keyed in by the user.  
It has multiple checks to ensure that the user keys in valid commands. 

<!---elaborate more on the class, still unsure of the format...--->
<!---insert other commands here, still unsure of the format...(should it all be under Parser class or separate?)--->

### Implementation: **Find Modules Feature**

The find modules features is facilitated by the `Parser`, `ModuleList` and `Module` Classes. `Parser` helps to check
for user input to determine is user doing a search via a module name or module type, which will then invoke the 
`findModuleByName` and `findModuleByType` methods respectively. If any modules are found, the ChatBot will print out
all the modules, else the ChatBot will return a message to the user, saying that no modules were found with the search
term they used.

Given below is an example usage scenario and how the findModuleByName mechanism behaves at each step.

Step 1: The user launches the application for the first time. The ChatBot will be initialised with an empty ArrayList
of Modules.

Step 2: The user executes `add /CS2113T CS2101 /4 /CORE /2 /2` to add two modules into the ChatBot via the addModules 
feature

The following object diagram shows the current state of the ChatBot:
![FindModule](diagrams/FindTwoModules.png)

<small><i>Figure ???</i></small>

Step 3: The user now wants to find the details of the modules he has just added. He executes `find /name /CS` which
will call `findModuleByName`. This method will then print out all the modules that have the keyword "CS" in their
module name.

The following sequence diagram shows how the `findModuleByName` operation works:

![FindModule](diagrams/FindModule.png)

<small><i>Figure ???</i></small>

`grade` command:

The `grade` command is used by the user to update the grade of modules that have already been completed.  

The sequence by which the Parser class handles the `grade` command is as follows:  
1) The `Parser` class extracts the other fields of the user input, and calls upon the `updateModuleGrade()` method
in the `ModuleList` class.  
2) The method then loops through the moduleList array to find the moduleCode that requires a grade update. 
3) If the module is found, it calls the `Module` object method `setGrade()` to update the grade field
and prints a success message by calling the `printUpdatedModuleGrade()` method of the `Print` class.
4) Else, it prints an error message by calling the `printInvalidModule()` method of the `Print` class.  

The sequence of events above can be represented with the following sequence diagram:

![gradeCommand](diagrams/GradeCommand.png)

<small><i>Figure ???</i></small>

`calculateCAP` command:

The `calculateCAP` command is used by the user to calculate the Cumulative Average Point (CAP) of graded modules.

The sequence by which the Parser class handles the `calculateCAP` command is as follows:
1) The `Parser` class extracts the other fields of the user input, and calls upon the `calculateCAP()` method
   in the `ModuleList` class.
2) The method then loops through the moduleList array to find modules that have been graded.
3) It checks if the module grade should be counted by self-invocation of the `shouldCountModule()` method
4) If it is, proceeds to obtain the grade value by self-invocation of the `getGradeValue()` method.
5) Calculates the required grade values, and finally calls the `printCalculatedCAP()` of the `Print` class to display
the result to the user

The sequence of events above can be represented with the following sequence diagram:

![calculateCAP](diagrams/CalculateCAP.png)

<small><i>Figure ???</i></small>

`add` command:

The `add` command is used by the user to add a module or multiple modules at once.

The sequence by which the Parser class handles the `add` command is as follows:
1) The `Parser` class extracts the necessary fields from the user input, and calls upon the `addModule`
   method in the `ModuleList` class in a loop.
2) The method then checks the type of module that is being added, then calls the relevant 
   constructor (`Core`, `UE`, `GE`, `Internship`).
3) The `addModule` method returns the module that is added to the `Parser` class.
4) The `getModuleListSize` method is called from `ModuleList` class.
5) The `printAddedModule` method is called from the `Print` class to display the result to the user.

The sequence of events above can be represented with the following sequence diagram:

![addInputCommand](diagrams/AddInputCommand.png)

<small><i>Figure ???</i></small>

`edit` command:

The `edit` command is used by the user to make changes to fields in the module description.

The sequence in which the `Parser` class handles the `edit` command is as follows:
1) The `Parser` class extracts the other fields of the user input, and calls upon the `editModuleField()` method
   by self-invocation. 
2) The method then uses a `switch` statement to evaluate the module field that the user wants to update.
3) After checking the field to be updated, the appropriate method within the `ModuleList` class is called upon to
   make the changes specified by the user.
4) If the user wants to update Modular Credits, the `editModularCredits()` method is called. 
   This method directly modifies the `modularCredits` attribute of the `Module` object.
5) If the user wants to update Module Type, the `editModuleType()` method is called.
   This method removes the existing `Module` object and adds a new `Module` object of the new type specified
   by the user. The `getModuleCode()`, `getModularCredits()`, `getYear()`, `getSemester()` and `getGrade()`
   methods in the `Module` class are also called upon to obtain the respective fields required to create the new
   `Module` object. 
6) If the user wants to update the Year, the `editYear()` method is called.
   This method directly modifies the `year` attribute of the `Module` object.
7) If the user wants to update the Semester, the `editSemester()` method is called.
   This method directly modifies the `semester` attribute of the `Module` object.

![editCommand](diagrams/EditCommand.png)

<small><i>Figure ???</i></small>

`delete` command:

The `delete` command is used by the user to delete a module which is specified by the user.

The sequence in which the `Parser` class handles the `delete` command is as follows:
1) The `Parser` class extracts the necessary fields from the user input, and calls upon the `deleteModule`
   method in the `ModuleList` class.
2) The method then loops through the moduleList array, attempting to find a module with the module code
   that was specified by the user.
3) If a corresponding module is found, the `deleteModule` method will remove the module from the moduleList array
   and return the deleted `Module` object. Otherwise, the `deleteModule` method returns `null`.
4) If a deleted `Module` object is returned from `deleteModule`, the `Parser` class calls upon
   `printDeletedModule()` of the `Print` class. Otherwise, the `Parser` class calls upon `printNoDeletedModuleFound()`
   of the `Print` class. This displays to the user the result of the `delete` command.

![deleteModule](diagrams/DeleteModule.png)

<small><i>Figure ???</i></small>

## Product scope
### Target user profile

Our target user profile is Information Security students in NUS.

### Value proposition

Modganiser is effortless module planning, at your fingertips via the
Command Line Interface (CLI). It helps Information security 
students graduate in time by giving you a platform to plan all 4 years
of your modules to ensure that you meet graduation requirements (UE/GEs).
If you can type fast, Modganiser can get your schedule up faster than
traditional GUI apps.


## User Stories

| Version | As a ... | I want to ...             | So that I can ...                                           |
|---------|----------|---------------------------|-------------------------------------------------------------|
| v1.0    | new user | see usage instructions    | refer to them when I forget how to use the application      |
| v2.0    | user     | find a to-do item by name | locate a to-do without having to go through the entire list |

## Non-Functional Requirements

1. Should work on any mainstream OS as long as it has Java 11 or above installed.
2. Should be able to hold up to 1000 persons without a noticeable sluggishness in performance for typical usage.
3. A user with above average typing speed for regular English text (i.e. not code, not system admin commands)
should be able to accomplish most of the tasks faster using commands than using the mouse.

## Glossary

Mainstream OS: Windows, Linux, Unix, OS-X

## Instructions for manual testing
