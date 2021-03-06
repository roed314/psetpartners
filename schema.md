# Schema

This file provides documentation on the underlying schema; try to keep it up to date if you make changes.

## classes	

Column                | Type        |  Notes
----------------------|-------------|-------
id                    | bigint      | unique identifier automatically assigned by postgres
name                  | text        | Course name, e.g. Algebra I
number                | text        | Course number, e.g. 18.701
year                  | smallint    | Calendar year
term                  | smallint    | Encoding of semester 0=IAP, 1=spring, 2=summer, 3=fall
homepage              | text        | course homepage

## students
			
Column                | Type        |  Notes
----------------------|-------------|-------
id                    |	bigint      | unique identifier automatically assigned by postgres (not MIT id)
name                  |	text        | e.g. Johnathan Smith
year	              | smallint    | 1, 2, 3, 4, etc
identifier            |	text	    | kerb id
email	              | text	    | smith@gmail.com
preferred_name        | text        | e.g. John Smith
preferred_pronouns    | text	    | e.g. they/them
preferences           |	jsonb	    | dictionary of preferences (see Preferences tab)
preferences_strength  | jsonb       | dictionary of preference strength (values are integers from 0 to 10)
timezone              |	text	    | e.g. US/Eastern
description           |	text	    | Student's public description of themself
blocked_student_ids   | bigint[]    | list of student ids this student will never be put in a group with
rejected_group_ids    | bigint[]    | list of group ids theis student has rejectd
			
## groups

Column                | Type        |  Notes
----------------------|-------------|-------
id                    |	bigint      | unique identifier automatically assigned by postgres (not MIT id)
class_id	      | bigint	    | id in classes table
group_name            | text	    | custom name, editable by anyone in group
visibility            | smalling    | 0=closed, 1=open, 2=public  (closed+open are system created)
preferences	      | jsonb       | optional group preferences; if unspecified, system constructs something from member preferences
preferences_strength  | jsonb       | preference strengths

## classlist

Column                | Type        |  Notes
----------------------|-------------|-------
id                    |	bigint      | unique identifier automatically assigned by postgres (not MIT id)
class_id	      | bigint	    | id in classes table
student_id            | bigint	    | id in students table
preferences           |	jsonb       | overrides students preferences
preferences_strength    jsonb       | overrides students preferences
			
## grouplist

Column                | Type        |  Notes
----------------------|-------------|-------
id                    |	bigint      |	unique identifier automatically assigned by postgres (not MIT id)
group_id	            | bigint	id  | id in groups table
student_id            | bigint	id  | id in students table
