---
layout: page
title: User Guide
---

![Logo](images/StoreClass-Logo.png)

Tired of using paper or Microsoft Excel to track your student details? No worries, StoreClass is here to help! 

StoreClass (SC) is a desktop app designed exclusively for teachers from private organizations e.g. tuition centers to manage their students. As teachers, you can interact with the app by keying in your commands to StoreClass's chat bot, and your student details will be updated and saved automatically.

Paired also with a revolutionary AutoComplete feature, StoreClass helps you manage your student details more effectively, efficiently and most importantly, reliably.
## Table of Contents
* Table of Contents
{:toc}

--------------------------------------------------------------------------------------------------------------------

## Quick start

1. Before you use our program, ensure you have Java `17` or above installed in your Computer. 
   - If you are using Windows 11, see [here](https://www.youtube.com/watch?v=ykAhL1IoQUM) for an installation guide.
   - If you are using MacOS, see [here](https://www.youtube.com/watch?v=lYKHFz8YaD4) instead.

   <div markdown="span" class="alert alert-secondary">
   :question: **Why do I need to install Java?**
   Our program is coded in Java. So in order for you to use it, Java will need to be installed on your machine. Think of it as the engine for our program.
   </div>

2. Download the latest version of the `.jar` file of our program from [here](https://github.com/AY2425S1-CS2103T-W10-4/tp/releases).

3. Copy the file to the folder you want to use as the _home folder_ for StoreClass.

4. Open the terminal on your computer and run the jar file.
   - How do I run a jar file using Terminal? See [here](https://www.youtube.com/watch?v=j7A7DOZePXs)
   - After you run the jar file, A GUI similar to below should appear on your screen in a few seconds. Note how the app contains some sample data.<br>
    ![Ui](images/Ui.png)

5. Type a command of your choice in the command box and press Enter to execute it. e.g. typing **`help`** and pressing Enter will open the help window.<br>
   Here are some examples of commands you can try:

   * `list` : Lists all students and their details.

   * `add n/John Doe p/98765432 g/male m/CS2103T` : Adds a student named `John Doe` to StoreClass.

   * `delete 3` : Deletes the 3rd student shown in the current list of students.

   * `clear` : Deletes all students.

   * `exit` : Exits the program.
6. Refer to the [Features](#features) below for a more detailed overview of each command.

--------------------------------------------------------------------------------------------------------------------

## Features

<div markdown="block" class="alert alert-info">

**:information_source: Before you read on, here are some important notes about the command format that you need to know:**<br>

* Words in `UPPER_CASE` are the parameters to be supplied by you.<br>
  e.g. in `add n/NAME`, `NAME` is a parameter which can be used as `add n/John Doe`.

* Items in square brackets are optional.<br>
  e.g `n/NAME [t/TAG]` can be used as `n/John Doe t/friend` or as `n/John Doe`.

* Items with `...`​ after them can be used multiple times.<br>
    e.g. `m/MODULE...​` can be used as `m/Mathematics`, `m/Biology m/Physics` etc.

* Items with `…`​ after them can be used multiple times including zero times.<br>
  e.g. `[t/TAG]…​` can be used as ` ` (i.e. 0 times), `t/paid_tuition`, `t/paid_tuition t/smart` etc.

* Parameters can be in any order.<br>
  e.g. if the command specifies `n/NAME p/PHONE_NUMBER`, `p/PHONE_NUMBER n/NAME` is also acceptable.

* Extraneous parameters for commands that do not take in parameters (such as `help`, `list`, `exit` and `clear`) will be ignored.<br>
  e.g. if the command specifies `help 123`, it will be interpreted as `help`.

* If you are using a PDF version of this document, be careful when copying and pasting commands that span multiple lines, as space characters surrounding line-breaks may be omitted when copied over to the application.
</div>

### Viewing help : `help`

You can view the help page using this command.

![help message](images/helpMessage.png)

Format: `help`


### Adding a student: `add`

You can add a student to StoreClass using this command.

Format: `add n/NAME p/PHONE_NUMBER g/GENDER m/MODULE... [t/TAG]…​`

<div markdown="span" class="alert alert-info">:information_source: **Note:**
A student can have any number of tags (including 0) and modules.
</div>

Examples:
* `add n/John Doe p/98765432 g/male m/Math`
* `add n/Betsy Crowe t/special g/female p/1234567 m/Math m/Biology t/smart`

### Listing all students : `list`

You can show a list of all students in StoreClass.

Format: `list`

### Editing a student : `edit`

You can edit an existing student in StoreClass.

Format: `edit INDEX [n/NAME] [p/PHONE] [g/GENDER] [m/MODULE] [t/TAG]…​`

* Edits the person at the specified `INDEX`. The index refers to the index number shown in the displayed person list. The index **must be a positive integer** 1, 2, 3, …​
* At least one of the optional fields must be provided.
* Existing values will be updated to the input values.
* When editing tags, the existing tags of the person will be removed i.e adding of tags is not cumulative.
* You can remove all the person’s tags by typing `t/` without
    specifying any tags after it.

Examples:
*  `edit 1 p/91234567` Edits the phone number of the 1st person to be `91234567`.
*  `edit 2 n/Betsy Crower t/` Edits the name of the 2nd person to be `Betsy Crower` and clears all existing tags.

### Locating students by name: `find`

You can find students whose names or tags contain any of the given keywords.

Format: `find KEYWORD [MORE_KEYWORDS]`

* The search is case-insensitive. e.g `hans` will match `Hans`
* The order of the keywords does not matter. e.g. `Hans Bo` will match `Bo Hans`
* Only the name and tags are searched.
* Only full words will be matched e.g. `Han` will not match `Hans`
* Students matching at least one keyword will be returned (i.e. `OR` search).
  e.g. `Hans Bo` will return `Hans Gruber`, `Bo Yang`

Examples:
* `find John` returns `john` and `John Doe` _(search by name)_
* `find colleague` returns `Bernice Yu` and `Roy Balakrishnan` _(search by tag)_
* `find alex david` returns `Alex Yeoh`, `David Li` _(search by multiple parameters)_ <br> 
  ![result for 'find alex david'](images/findAlexDavidResult.png)

### Filter students : `filter`

You can filter students who meet all specified conditions.

Format: `filter [n/name] [p/phone] [g/gender] [t/tag]... [m/module]...`
* The filter is case-insensitive. eg `hans` will match `Hans`.
* At least one of the optional fields must be provided.
* Only full words will be matched e.g. `Han` will not match `Hans`, same to all parameter except phone number.
* At least 3 digits of number must be provided to filter phone number and it will return all matching numbers that contains specified number.
* Students matching all the given conditions will be returned (i.e. `AND` search).

<div markdown="span" class="alert alert-danger">⚠️ **Warning:**
Each parameter can only contain one keyword.
</div>

Examples:
* `filter n/John` returns `john` and `John Doe` (filter by name)
* `filter g/male t/project` returns `Bernice Yu`, `Roy Balakrishnan` and `Gabreil Lim`. (filter by gender and tag)
* `filter g/female t/family t/friend` returns `Alex Yeoh` and `David Li` (filter by gender and multiple tags)
* `filter g/male t/project m/cs1101` return `Bernice Yu` (filter by multiple conditions)

### Deleting a student : `delete`

You can delete a specified student from StoreClass.

Format: `delete INDEX`

* Deletes the student at the specified `INDEX`.
* The index refers to the index number shown in the displayed student list.
* The index **must be a positive integer** 1, 2, 3, …​

Examples:
* `list` followed by `delete 2` deletes the 2nd person in the address book.
* `find Betsy` followed by `delete 1` deletes the 1st person in the results of the `find` command.

### Undoing the last action: `undo`

Reverts the last action performed in the application, allowing you to recover data that may have been deleted or modified unintentionally.

Format: `undo`

* **Note:** This command does not work with the `list`, `filter`, or `find` commands. The reasoning behind this is that we consider them as view commands, not action commands that alter student data.

<img src="images/UndoRedoExample1.png" alt="Initial State" width="60%" />
<img src="images/UndoRedoExample2.png" alt="After Delete Command" width="60%" />
<img src="images/UndoRedoExample3.png" alt="After Undo Command" width="60%" />

Examples:
* `undo` will revert the last command executed, restoring the previous state of the address book.

### Redoing the last undone action: `redo`

Restores the last action that was undone, allowing you to recover data after an undo operation.

Format: `redo`

* **Note:** This command does not work with the `list`, `filter`, or `find` commands.

<img src="images/UndoRedoExample4.png" alt="After Redo Command" width="60%" />

Examples:
* `redo` will reapply the last command that was undone, restoring the previous state of the address book.


### Grading a Module: `grade`

You can assign a grade to a module that a student is taking.

**Format:** `grade INDEX [m/MODULE s/GRADE]`

- Assigns a numerical grade (between 0 and 100) to the module identified by the `INDEX` number shown in the displayed person list.
- `INDEX`: The index number of the student in the displayed person list (must be a positive integer).
- `m/MODULE`: The module code to which the grade is assigned.
- `s/GRADE`: The numerical grade (between 0 and 100) to assign to the module.
- You can provide multiple `m/MODULE s/GRADE` pairs to assign grades to multiple modules in a single `grade` command.
- The grade can be any whole number between 0 and 100, inclusive.

**Important Notes:**
- Each module specified in the `grade` command must be a module that the student is taking.
- The number of `m/MODULE` prefixes must match the number of `s/GRADE` prefixes.
- Grades are assigned to modules based on the order of the `m/MODULE s/GRADE` pairs provided in the command.

**Examples:**
- `grade 1 m/CS2103T s/85` assigns a grade of 85 to CS2103T for the first student.
- `grade 2 m/MA1522 s/90` assigns a grade of 90 to MA1522 for the second student.
- `grade 3 m/CS2103T s/80 m/MA1522 s/85` assigns a grade of 80 to CS2103T and 85 to MA1522 for the third student.


### Archiving data files `archive`

You can archive the current address book to a specific file name.

After archiving, you can find the archived file in the folder `archived` with the name `FILENAME` in the home folder that you've chosen to put the `jar` file of StoreClass in.

Format: `archive pa/FILENAME`

Example: `archive pa/mybook.json`

The file name must end with ".json" and must not contain any slashes "/".

There should be only one file name provided.

<div markdown="span" class="alert alert-primary">:rotating_light: **Warning:**
When you execute the archive command, all entries in the current StoreClass will be discarded.

If you choose an existing archive file as the file name when archiving, the old archive file will be overwritten.
</div>

### Load data files `load`

You can load data from an archived file into StoreClass.

You can only load from files under the folder named `archived`. This folder is located in the home folder that you've chosen to put the `jar` file of StoreClass in.

Format: `load pa/FILENAME`

Example: `load pa/mybook.json`

The file name must end with ".json", must not contain any slashes "/" and must point to an existing StoreClass .json file.

There should be only one file name provided.

<div markdown="span" class="alert alert-primary">:rotating_light: **Warning:**
It is recommended that you avoid loading non-StoreClass .json files, as it may result in unexpected behaviors

When you execute the load command, all the entries in the current StoreClass will be overwritten. So, it is recommended that you archive the current data in StoreClass before loading.
</div>

### Clearing all entries : `clear`

You can all the current entries in StoreClass with this command.

Format: `clear`

### Exiting the program : `exit`

You can exit the program with this command.

Format: `exit`

### Autocomplete

The Autocomplete feature provides real-time command suggestions as you type, helping you quickly and accurately enter commands. Autocomplete identifies keywords and suggests matches, allowing you to streamline input by selecting from relevant options instead of typing full commands or field values.

#### How It Works
Autocomplete operates based on the word at your current caret position:

* As you begin typing a command or field, suggestions will appear that match the word under your current caret position. For example, typing `ad` will display a list of commands beginning with `ad`, like `add`. 
  * Autocomplete matches with the text characters before your caret position of the word under your current caret position. For example, when typing in the command keyword `ad` and you move your cursor between `a` and `d`, autocomplete will show you all commands starting with `a`. You can utilize this to do some cool tricks as explained in the tips section below.
* Autocomplete for command keywords e.g. `clear`, `delete`, `add` applies only to the first word you type in the command box. This initial word is treated as the command.
* Autocomplete for student fields applies to all subsequent words after the first word. All subsequent words after the first are treated as student fields with specific prefixes, e.g. `m/Math`, `g/male`

<div markdown="span" class="alert alert-info"> :notebook: **Note:** Autocomplete will **not** match subsequent words after the first word you entered with command keywords! Similarly, Autocomplete will **not** match the first word you entered with student fields! </div>

#### Supported Commands
Autocomplete supports all existing command keywords when matching.

#### Supported Fields
Autocomplete currently supports the following fields with these prefixes:

| Prefix   | Field            | Description                                     |
|----------|------------------|-------------------------------------------------|
| `m/`     | Modules          | Matches **all existing** module names           |
| `t/`     | Tags             | Matches **all existing** tags                   |
| `g/`     | Gender           | Matches gender values: `male` or `female`       |
| `pa/`    | File Paths       | Matches **all existing** archived file paths    |

When these prefixes are detected, autocomplete automatically displays a list of suggestions related to these fields. The list of suggestions are generated through the existing list of students inside StoreClass.

#### Example Usage
If you begin typing `edit 1 m/M`, Autocomplete will provide suggestions for available modules starting with the letter `M`, helping you to quickly select the correct module name. Similarly, typing `t/` after the command will bring up a list of tags, allowing you to specify tags accurately without needing to remember or retype exact names.

<div markdown="span" class="alert alert-info"> :notebook: **Note:** Autocomplete is **case-insensitive**! </div>

<div markdown="span" class="alert alert-secondary">
:question: **Common Question:**
Why are there no suggestions when I type in `m/`, `t/` or `pa/`? <br>
Autocomplete searches for suggestions relevant to these fields based on the existing data in StoreClass. If there are no data or students inside StoreClass, then no suggestions will be 
generated for these fields. This usually occurs after a `clear` command.
</div>

<div markdown="block" class="alert alert-primary">
:bulb: **Tips:** for Efficient Usage <br>

1. **Start with the command**: Autocomplete only activates for commands when typing the first word. <br>
2. **Remember to use prefixes**: For fields, make sure to use the correct prefix (`m/`, `t/`, `g/`, `pa/`) to activate Autocomplete for those fields. <br>
3. **Select from suggestions using arrow keys**: Save time by selecting from the suggestion list using arrow keys rather than typing full names or values.<br>
4. **Typos**: When you accidentally type in the wrong name for an existing field, instead of holding backspace and retyping the entire field, simply move the caret position over to the 
prefix, and select from the list of suggestions. Autocomplete will replace the entire field with your selection for you.
</div>

By utilizing Autocomplete, you can input commands more quickly, reduce typos, and improve your overall efficiency in navigating the software!

![Autocomplete example when keying in gender](images/AutocompleteExample.png)

### Saving the data

StoreClass data are saved in the hard disk automatically after any command you enter that changes the data. There is no need to save manually!

### Editing the data file

StoreClass data are saved automatically as a JSON file `[JAR file location]/data/addressbook.json`. Advanced users are welcome to update data directly by editing that data file.

<div markdown="span" class="alert alert-warning">:exclamation: **Caution:**
If your changes to the data file makes its format invalid, StoreClass will discard all data and start with an empty data file at the next run. Hence, it is recommended to take a backup of the file before editing it.<br>
Furthermore, certain edits can cause the StoreClass to behave in unexpected ways (e.g., if a value entered is outside of the acceptable range). Therefore, edit the data file only if you are confident that you can update it correctly.
</div>



--------------------------------------------------------------------------------------------------------------------

## FAQ

**Q**: How do I transfer my data to another Computer?<br>
**A**: Install the app in the other computer and overwrite the empty data file it creates with the file that contains the data of your previous StoreClass home folder.

--------------------------------------------------------------------------------------------------------------------

## Known issues

1. **When using multiple screens**, if you move the application to a secondary screen, and later switch to using only the primary screen, the GUI will open off-screen. The remedy is to delete the `preferences.json` file created by the application before running the application again.
2. **If you minimize the Help Window** and then run the `help` command (or use the `Help` menu, or the keyboard shortcut `F1`) again, the original Help Window will remain minimized, and no new Help Window will appear. The remedy is to manually restore the minimized Help Window.

--------------------------------------------------------------------------------------------------------------------

## Command summary

Action | Format, Examples
--------|------------------
**Add** | `add n/NAME g/GENDER p/PHONE_NUMBER m/MODULE... [t/TAG]…​` <br> e.g., `add n/James Ho g/male p/22224444 m/CS2103T m/CS2101 t/friend t/colleague`
**Clear** | `clear`
**Delete** | `delete INDEX`<br> e.g., `delete 3`
**Edit** | `edit INDEX [n/NAME] [g/GENDER] [p/PHONE_NUMBER] [m/MODULE] [t/TAG]…​`<br> e.g.,`edit 2 n/James Lee`
**Find** | `find KEYWORD [MORE_KEYWORDS]`<br> e.g., `find James Jake`
**Grade** | `grade INDEX [m/MODULE s/GRADE]`<br> e.g., `grade 1 m/CS2103T s/85`
**Undo** | `undo`
**Redo** | `redo`
**List** | `list`
**Help** | `help`
**Archive** | `archive pa/PATH`
**Load** | `load pa/PATH`

