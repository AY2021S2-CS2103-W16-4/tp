---
layout: page
title: User Guide
---

EzManage is a **desktop app for managing students, tutors and classes, optimized for use via a Command Line Interface** (CLI) while still having the benefits of a Graphical User Interface (GUI). It is named as EzManage as it allows tuition centres managers to easily manage students, tutors and classes all in one single web application.

* Table of Contents
{:toc}

--------------------------------------------------------------------------------------------------------------------

## Quick start

1. Ensure you have Java `11` or above installed in your Computer.

1. Download the latest `ezmanage.jar` from [here](https://github.com/AY2021S2-CS2103-W16-4/tp/releases).

1. Copy the file to the folder you want to use as the _home folder_ for your EzManage.

1. Double-click the file to start the app. An example of the GUI is shown below. Note how the app contains some sample data.<br>
   ![Ui](images/Ui.png)

1. Type the command in the command box and press Enter to execute it. e.g. typing **`help`** and pressing Enter will open the help window.<br>
   Some example commands you can try:

   * **`list persons`** : Lists all students and tutors.

   * **`add_person`**`tp/student n/John Doe p/98765432 e/johnd@example.com a/John street, block 123, #01-01` : Adds a student named `John Doe` to the Contact List.

   * **`delete_person`**`t/3` : Deletes the tutor with the ID `t/3` from the Contact list.
     
   * **`assign`** : `assign s/3 t/2 c/1` Assigns student(s) or tutor to a specific class.

   * **`clear`** : Deletes all contacts.

   * **`exit`** : Exits the app.

1. Refer to the [Features](#features) below for details of each command.

--------------------------------------------------------------------------------------------------------------------

## Features

<div markdown="block" class="alert alert-info">

**:information_source: Notes about the command format:**<br>

* Words in `UPPER_CASE` are the parameters to be supplied by the user.<br>
  e.g. in `add_person n/NAME`, `NAME` is a parameter which can be used as `add_person n/John Doe`.

* Items in square brackets are optional.<br>
  e.g `n/NAME [tag/TAG]` can be used as `n/John Doe tag/friend` or as `n/John Doe`.

* Items with `…`​ after them can be used multiple times including zero times.<br>
  e.g. `[tag/TAG]…​` can be used as ` ` (i.e. 0 times), `tag/friend`, `tag/friend tag/family` etc.

* Parameters can be in any order.<br>
  e.g. if the command specifies `n/NAME p/PHONE_NUMBER`, `p/PHONE_NUMBER n/NAME` is also acceptable.

* If a parameter is expected only once in the command but you specified it multiple times, only the last occurrence of the parameter will be taken.<br>
  e.g. if you specify `p/12341234 p/56785678`, only `p/56785678` will be taken.

* Extraneous parameters for commands that do not take in parameters (such as `help`, `exit` and `clear`) will be ignored.<br>
  e.g. if the command specifies `help 123`, it will be interpreted as `help`.

</div>

### Viewing help : `help`

Shows a message explaining how to access the help page.

![help message](images/helpMessage.png)

Format: `help`

### Adding a tutor: `add_person`

Adds a tutor to the address book.

Format: `add_person pt/tutor n/NAME p/PHONE_NUMBER e/EMAIL a/ADDRESS [tag/TAG]…​`

<div markdown="span" class="alert alert-primary">:bulb: **Tip:**
A person can have any number of tags (including 0)
</div>

Examples:
* `add_person pt/tutor n/John Doe p/98765432 e/johnd@example.com a/John street, block 123, #01-01`
* `add_person pt/tutor n/Betsy Crowe e/betsycrowe@example.com a/Newgate Prison p/1234567 tag/criminal`

### Adding a student: `add_person`

Adds a student to the address book.

Format: `add_person pt/student n/NAME p/PHONE_NUMBER e/EMAIL a/ADDRESS [tag/TAG]…​`

<div markdown="span" class="alert alert-primary">:bulb: **Tip:**
A person can have any number of tags (including 0)
</div>

Examples:
* `add_person pt/student n/John Doe p/98765432 e/johnd@example.com a/John street, block 123, #01-01`
* `add_person pt/student n/Betsy Crowe e/betsycrowe@example.com a/Newgate Prison p/1234567 tag/criminal`

### Adding a session: `add_session`

Adds a session to the address book.

Format: `add_session d/DAY t/TIMESLOT s/SUBJECT [tag/TAG] …
`

<div markdown="span" class="alert alert-primary">:bulb: **Tip:**
A session can have any number of tags (including 0)
</div>

* A new session will have a unique session ID assigned after creation. 
* DAY should match the format of a valid day in the week.
* TIMESLOT should be in the format `HH:MM to HH:MM` and the end time should only be after the start time.

Examples:
* `add_session d/Saturday ts/13:00 to 15:00 s/Math tag/Hard`

### Listing all persons : `list`

Shows a list of all persons in the address book.

Format: `list persons`

### Listing all students : `list`

Shows a list of all students in the address book.

Format: `list students`

### Listing all tutors : `list`

Shows a list of all tutors in the address book.

Format: `list tutors`

### Listing all sessions : `list`

Format: `list sessions`

Shows a list of all sessions in the address book.

### Viewing a tutor : `view`

Views an existing tutor's details.

Format: `view t/ID`

* Views the tutor with the specified tutor ID.
* Tutor’s name, contact number, existing classes, email and address will be given.

Example:
* `view t/1` views the details of the tutor with tutor ID 1.

### Viewing a student : `view`

Views an existing student's details.

Format: `view s/ID`

* Views the student with the specified student ID.
* Student’s name, contact number, email and address will be given.

Example:
* `view s/1` views the details of the student with student ID 1.

### Viewing a session : `view_session`

Views an existing session's details.

Format: `view_session c/ID`

* Views the specified session with the specified session ID.
* Left Panel will show the session's information such as the session ID, day
  time slot, subject, tags and assigned tutor (if any).
* Right Panel will show the specifed session's list of assigned students (if any).

Example:
* `view_session c/1` views the details of the session with session ID c/1 on the Left Panel
and views the list of assigned students (e.g. students s/1, s/2) on the Right Panel.

### Editing a student : `edit_person`

Edits an existing student in the address book.

Format: `edit_person s/ID [n/NAME] [p/PHONE] [e/EMAIL] [a/ADDRESS] [tag/TAG]…​`

* Edits the student at the specified student ID (in the format `s/ID`). The student ID can be found from the displayed student list. 
* At least one of the optional fields must be provided.
* Existing values will be updated to the input values.
* When editing tags, the existing tags of the person will be removed i.e adding of tags is not cumulative.
* You can remove all the person’s tags by typing `tag/` without
  specifying any tags after it.

Examples:
*  `edit_person s/1 p/91234567 e/johndoe@example.com` Edits the phone number and email address of the student with the ID of `s/1` to be `91234567` and `johndoe@example.com` respectively.
*  `edit_person s/2 n/Betsy Crower tag/` Edits the name of the student with the ID of `s/2` to be `Betsy Crower` and clears all existing tags.

### Editing a tutor : `edit_person`

Edits an existing tutor in the address book.

Format: `edit_person t/ID [n/NAME] [p/PHONE] [e/EMAIL] [a/ADDRESS] [tag/TAG]…​`

* Edits the tutor at the specified tutor ID (in the format `s/ID`). The tutor ID can be found from the displayed tutor list. 
* At least one of the optional fields must be provided.
* Existing values will be updated to the input values.
* When editing tags, the existing tags of the person will be removed i.e adding of tags is not cumulative.
* You can remove all the person’s tags by typing `tag/` without
  specifying any tags after it.

Examples:
*  `edit_person t/1 p/88888888 e/sarahwong@example.com` Edits the phone number and email address of the tutor with the ID of `t/1` to be `88888888` and `sarahwong@example.com` respectively.
*  `edit_person t/2 n/Oliver Tan tag/` Edits the name of the tutor with the ID of `t/2` to be `Oliver Tan` and clears all existing tags.

### Editing a session : `edit_session`

Edits an existing session in the address book.

Format: `edit_session c/ID [d/DAY] [ts/TIMESLOT] [s/SUBJECT] [tag/TAG]…​`

* Edits the session with the specified session ID. The session ID can be found from the displayed session list. 
* The session ID has to be a valid session ID i.e. the session has to exist in the Address Book.
* At least one of the optional fields must be provided.
* Existing values will be updated to the input values.
* DAY should match the format of a valid day in the week.
* TIMESLOT should be in the format `HH:MM to HH:MM` and the end time should only be after the start time.
* When editing tags, the existing tags of the session will be removed i.e adding of tags is not cumulative.
* A user can *ONLY* edit a session’s day and time slot if the session does not have any assigned tutor and assigned students, to avoid potential timeslot clashes when session is edited.
* Unassign students/tutor should be called before editing any session’s timeslot or day.

Examples:
*  `edit_session c/1 d/Monday s/Biology` Edits the day and subject of the session c/1 to be `Monday` and `Biology` respectively.
*  `edit_session c/2 ts/12:00 to 13:00 tag/haha` Edits the timeslot and tag of the session c/2 to be `12:00 to 13:00` and `haha` respectively.

### Locating persons by name: `find`

Finds persons whose names contain any of the given keywords.

Format: `find KEYWORD [MORE_KEYWORDS]`

* The search is case-insensitive. e.g `hans` will match `Hans`
* The order of the keywords does not matter. e.g. `Hans Bo` will match `Bo Hans`
* Only the name is searched.
* Only full words will be matched e.g. `Han` will not match `Hans`
* Persons matching at least one keyword will be returned (i.e. `OR` search).
  e.g. `Hans Bo` will return `Hans Gruber`, `Bo Yang`

Examples:
* `find John` returns `john` and `John Doe`
* `find alex david` returns `Alex Yeoh`, `David Li`<br>
  ![result for 'find alex david'](images/findAlexDavidResult.png)

### Deleting a student : `delete_person`

Deletes the specified student from the address book.

Format: `delete_person s/ID`

* Deletes the student with the specified `s/ID`.
* The s/ID refers to the student ID shown in the displayed person list.

Examples:
* `delete_person s/2` deletes the student with student ID s/2 in the address book.

### Deleting a tutor : `delete_person`

Deletes the specified tutor from the address book.

Format: `delete_person t/ID`

* Deletes the tutor with the specified `t/ID`.
* The t/ID refers to the tutor ID shown in the displayed person list.

Examples:
* `delete_person t/1` deletes the tutor with tutor ID t/1 in the address book.

### Deleting a session : `delete_session`

Deletes the specified session from the address book.

Format: `delete_session c/ID`

* Deletes the session with the specified `c/ID`.
* The c/ID refers to the session ID shown in the displayed session list.

Examples:
* `delete_session c/2` deletes the session with session ID c/2 in the address book.

### Assigning student(s)/tutor to session:`assign`

Assigns a student or multiple student and/or a tutor to a specific class

3 Formats : 

1) `assign [s/ID]…​ [c/ID]`

    * This assigns a student of `s/ID` or multiple students to a class of `c/ID`
    
    * Example : `assign s/2 s/1 c/1` This assigns students of `s/2` and `s/1` to class `c/1`


2) `assign [t/ID] [c/ID]`
    * This assign a tutor of `t/ID` to a class of `c/ID`
    * Example:  `assign t/1 c/1` This assign a tutor of `t/1` to class of `c/1`
    

3) `assign [s/ID]…​ [t/ID] [c/ID]`
    * This assigns a student of `s/ID` or multiple students and a tutor of `t/ID` to a class of `c/ID` 
    

A class must always be provided, either student or tutor can be optional.

### Unassigning people from a session : `assign`

Unassigns the specified people from a session.

Format: `unassign [s/ID]… [t/ID] c/ID`

* Unassigns students with the specified `s/ID` from the session with the specified `c/ID`
* Unassigns the tutor with the specified `t/ID` from the session with the specified `c/ID`
* At least one of the optional fields must be provided.
* Any number of students can be unassigned at the same time (including 0)

Examples:
* `unassign s/1 c/1` unassigns the student with student ID s/1 from the session with session ID c/1.
* `unassign c/1 t/1` unassigns the tutor with tutor ID t/1 from the session with session ID c/1.
* `unassign s/1 s/2 t/1 c/1` unassigns students with student IDs s/1 and s/2, and the tutor with tutor ID t/1 from the session with session ID c/1.

### Clearing all entries : `clear`

Clears all entries from the list of students, tutors and classes.

Format: `clear`

### Exiting the program : `exit`

Exits the program.

Format: `exit`

### Saving the data

EzManage data are saved in the hard disk automatically after any command that changes the data. There is no need to save manually.

### Editing the data file

EzManage data are saved as a JSON file `[JAR file location]/data/addressbook.json`. Advanced users are welcome to update data directly by editing that data file.

<div markdown="span" class="alert alert-warning">:exclamation: **Caution:**
If your changes to the data file makes its format invalid, AddressBook will discard all data and start with an empty data file at the next run.
</div>

### Archiving data files `[coming in v2.0]`

_Details coming soon ..._

--------------------------------------------------------------------------------------------------------------------

## FAQ

**Q**: How do I transfer my data to another Computer?<br>
**A**: Install the app in the other computer and overwrite the empty data file it creates with the file that contains the data of your previous EzManage home folder.

--------------------------------------------------------------------------------------------------------------------

## Command summary

Action | Format, Examples
--------|------------------
**Add** | For Person:`add_person tp/ROLE n/NAME p/PHONE_NUMBER e/EMAIL a/ADDRESS [tag/TAG]…​` <br> e.g., `add_person tp/student n/James Ho p/22224444 e/jamesho@example.com a/123, Clementi Rd, 1234665`<br><br> For Session: `add_session d/DAY ts/TIMESLOT s/SUBJECT [tag/TAG]…​` <br> e.g. `add_session d/Saturday ts/13:00 to 15:00 s/Math` 
**Clear** | `clear`
**Delete** | For Student: <br> `delete_person s/ID`<br> e.g., `delete_person s/22` <br><br> For Tutor: <br> `delete_person t/ID`<br> e.g., `delete_person t/8`<br><br> For Session:<br>`delete_session c/ID` <br> e.g., `delete_session c/9`
**Edit** | For Student: <br> `edit_person s/ID [n/NAME] [p/PHONE] [e/EMAIL] [a/ADDRESS] [tag/TAG]…​` <br> e.g., `edit_person s/2 n/Betsy Crower tag/` <br><br> For Tutor: <br> `edit_person t/ID [n/NAME] [p/PHONE] [e/EMAIL] [a/ADDRESS] [tag/TAG]…​` <br> e.g., `edit_person t/1 p/88888888 e/sarahwong@example.com` <br><br> For Session: <br> `edit_session c/ID [d/DAY] [ts/TIMESLOT] [s/SUBJECT] [tag/TAG]…​`<br> e.g.,`edit_session c/1 d/Monday s/Biology` <br> e.g. `edit_session c/2 d/Saturday ts/13:00 to 15:00 tag/Hard` 
**Assign** | `assign [s/ID]… [t/ID] c/ID`<br> e.g., `assign s/1 s/2 t/1 c/1`
**Unassign** | `unassign [s/ID]… [t/ID] c/ID`<br> e.g., `unassign s/1 s/2 t/1 c/1`
**Find** | `find KEYWORD [MORE_KEYWORDS]`<br> e.g., `find James Jake`
**List** | For All Persons: <br>`list persons` <br><br> For All Students: <br>`list students` <br><br> For All Tutors: <br>`list tutors` <br><br> For All Sessions: <br>`list sessions`
**View** | For Person: <br><br> For Session: <br> `view_session c/ID` <br> e.g., `view_session c/5`
**Help** | `help`
