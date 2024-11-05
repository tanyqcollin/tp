---
layout: page
title: User Guide
---

AddressBook Level 3 (AB3) is a **desktop app for managing contacts, optimized for use via a Command Line Interface** (CLI) while still having the benefits of a Graphical User Interface (GUI). If you can type fast, AB3 can get your contact management tasks done faster than traditional GUI apps.

* Table of Contents
{:toc}

--------------------------------------------------------------------------------------------------------------------

## Quick start

1. Ensure you have Java `17` or above installed in your Computer.

1. Download the latest `.jar` file from [here](https://github.com/se-edu/addressbook-level3/releases).

1. Copy the file to the folder you want to use as the _home folder_ for your AddressBook.

1. Open a command terminal, `cd` into the folder you put the jar file in, and use the `java -jar addressbook.jar` command to run the application.<br>
   A GUI similar to the below should appear in a few seconds. Note how the app contains some sample data.<br>
   ![Ui](images/Ui.png)

1. Type the command in the command box and press Enter to execute it. e.g. typing **`help`** and pressing Enter will open the help window.<br>
   Some example commands you can try:

   * `list` : Lists all contacts.

   * `add n/John Doe p/98765432 g/male m/CS2103T` : Adds a contact named `John Doe` to the Address Book.

   * `delete 3` : Deletes the 3rd contact shown in the current list.

   * `clear` : Deletes all contacts.

   * `exit` : Exits the app.

1. Refer to the [Features](#features) below for details of each command.

--------------------------------------------------------------------------------------------------------------------

## Features

<div markdown="block" class="alert alert-info">

**:information_source: Notes about the command format:**<br>

* Words in `UPPER_CASE` are the parameters to be supplied by the user.<br>
  e.g. in `add n/NAME`, `NAME` is a parameter which can be used as `add n/John Doe`.

* Items in square brackets are optional.<br>
  e.g `n/NAME [t/TAG]` can be used as `n/John Doe t/friend` or as `n/John Doe`.

* Items with `...`​ after them can be used multiple times.<br>
    e.g. `m/MODULE...​` can be used as `m/CS2101`, `m/CS2101 m/CS2103T` etc.

* Items with `…`​ after them can be used multiple times including zero times.<br>
  e.g. `[t/TAG]…​` can be used as ` ` (i.e. 0 times), `t/friend`, `t/friend t/family` etc.

* Parameters can be in any order.<br>
  e.g. if the command specifies `n/NAME p/PHONE_NUMBER`, `p/PHONE_NUMBER n/NAME` is also acceptable.

* Extraneous parameters for commands that do not take in parameters (such as `help`, `list`, `exit` and `clear`) will be ignored.<br>
  e.g. if the command specifies `help 123`, it will be interpreted as `help`.

* If you are using a PDF version of this document, be careful when copying and pasting commands that span multiple lines as space characters surrounding line-breaks may be omitted when copied over to the application.
</div>

### Viewing help : `help`

Shows a message explaning how to access the help page.

![help message](images/helpMessage.png)

Format: `help`


### Adding a person: `add`

Adds a person to the address book.

Format: `add n/NAME p/PHONE_NUMBER g/GENDER m/MODULE... [t/TAG]…​`

<div markdown="span" class="alert alert-primary">:bulb: **Tip:**
A person can have any number of tags (including 0) and modules.
</div>

Examples:
* `add n/John Doe p/98765432 g/male m/CS2103T`
* `add n/Betsy Crowe t/friend g/female p/1234567 m/MA1522 m/CS2103T t/criminal`

### Listing all persons : `list`

Shows a list of all persons in the address book.

Format: `list`

### Editing a person : `edit`

Edits an existing person in the address book.

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

### Locating persons by name: `find`

Finds persons whose names or tags contain any of the given keywords.

Format: `find KEYWORD [MORE_KEYWORDS]`

* The search is case-insensitive. e.g `hans` will match `Hans`
* The order of the keywords does not matter. e.g. `Hans Bo` will match `Bo Hans`
* Only the name and tags are searched.
* Only full words will be matched e.g. `Han` will not match `Hans`
* Persons matching at least one keyword will be returned (i.e. `OR` search).
  e.g. `Hans Bo` will return `Hans Gruber`, `Bo Yang`

Examples:
* `find John` returns `john` and `John Doe` _(search by name)_
* `find colleague` returns `Bernice Yu` and `Roy Balakrishnan` _(search by tag)_
* `find alex david` returns `Alex Yeoh`, `David Li` _(search by multiple parameters)_ <br> 
  ![result for 'find alex david'](images/findAlexDavidResult.png)

### Filter persons

Filter persons who meet all specified conditions.

Format: `filter [n/name] [p/phone] [g/gender] [t/tag]... [m/module]...`
* The filter is case-insensitive. eg `hans` will match `Hans`.
* At least one of the optional fields must be provided.
* Only full words will be matched e.g. `Han` will not match `Hans`, same to all parameter except phone number.
* At least 3 digits of number must be provided to filter phone number and it will return all matching numbers that contains specified number.
* Persons matching all the given conditions will be returned (i.e. `AND` search).

<div markdown="span" class="alert alert-danger">⚠️ **Warning:**
Each parameter can only contain one keyword.
</div>

Examples:
* `filter n/John` returns `john` and `John Doe` (filter by name)
* `filter g/male t/project` returns `Bernice Yu`, `Roy Balakrishnan` and `Gabreil Lim`. (filter by gender and tag)
* `filter g/female t/family t/friend` returns `Alex Yeoh` and `David Li` (filter by gender and multiple tags)
* `filter g/male t/project m/cs1101` return `Bernice Yu` (filter by multiple conditions)

### Deleting a person : `delete`

Deletes the specified person from the address book.

Format: `delete INDEX`

* Deletes the person at the specified `INDEX`.
* The index refers to the index number shown in the displayed person list.
* The index **must be a positive integer** 1, 2, 3, …​

Examples:
* `list` followed by `delete 2` deletes the 2nd person in the address book.
* `find Betsy` followed by `delete 1` deletes the 1st person in the results of the `find` command.

### Grading a Module: `grade`

Assigns a grade to a module that a student is taking.

**Format:** `grade INDEX m/MODULE s/GRADE`

- Assigns a numerical grade (between 0 and 100) to the module identified by the `INDEX` number shown in the displayed person list.
- `INDEX` must be a positive integer.
- The grade can be any whole number between 0 and 100, inclusive.

**Examples:**
- `grade 1 m/CS2103T s/85` assigns a grade of 85 to CS2103T for the first student.
- `grade 2 m/MA1522 s/90` assigns a grade of 90 to MA1522 for the second student.


### Archiving data files `archive`

Archive the current address book to the specific file name.

The archived file and be found at `archived/FILENAME`.

Format: `archive pa/PATH`

Example: `archive pa/mybook.json`

The file name must ends with ".json" and must not contain any slash "/".

There should be only one file name provided.

#### Warning

All the entries in the current address book will be cleared.

### Load data files `load`

Load the current address book to the specific file name.

This command will only load from a folder named `archived` which is in the same folder as the `jar` file.

The archived file and be found at `load/FILENAME`.

Format: `load pa/PATH`

Example: `load pa/mybook.json`

The file name must ends with ".json", must not contain any slash "/" and must point to an existing address book .json file.

There should be only one file name provided.

#### Warning
Avoid loading non-address book .json files as it may result in unexpected behaviours

All the entries in the current address book will be discard. So archiving current address book before loading is recommended.

### Clearing all entries : `clear`

Clears all entries from the address book.

Format: `clear`

### Exiting the program : `exit`

Exits the program.

Format: `exit`

### Autocomplete

When using the program, you might have noticed that suggestions pop up when you are entering in commands. This is the autocomplete feature. 

Autocomplete searches for keywords matching the word under the caret position. For example, when you type in `ad`, autocomplete will show a list of commands matching this initial string.

Autocomplete also supports autocompletion for fields. These include: 
* Modules `m/`
* Tags `t/`
* Gender `g/`

When these prefixes are detected, autocomplete automatically displays a list of suggestions related to these fields.

![Autocomplete example when keying in gender](images/AutocompleteExample.png)

### Saving the data

AddressBook data are saved in the hard disk automatically after any command that changes the data. There is no need to save manually.

### Editing the data file

AddressBook data are saved automatically as a JSON file `[JAR file location]/data/addressbook.json`. Advanced users are welcome to update data directly by editing that data file.

<div markdown="span" class="alert alert-warning">:exclamation: **Caution:**
If your changes to the data file makes its format invalid, AddressBook will discard all data and start with an empty data file at the next run. Hence, it is recommended to take a backup of the file before editing it.<br>
Furthermore, certain edits can cause the AddressBook to behave in unexpected ways (e.g., if a value entered is outside of the acceptable range). Therefore, edit the data file only if you are confident that you can update it correctly.
</div>



--------------------------------------------------------------------------------------------------------------------

## FAQ

**Q**: How do I transfer my data to another Computer?<br>
**A**: Install the app in the other computer and overwrite the empty data file it creates with the file that contains the data of your previous AddressBook home folder.

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
**List** | `list`
**Help** | `help`
**Archive** | `archive`
