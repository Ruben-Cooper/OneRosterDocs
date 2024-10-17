## Error Messages Guide

### About

The OneRoster Plug-in Error Messages section serves as a crucial part of understanding potential issues during the integration process. These error messages help developers identify and troubleshoot common problems that arise when importing CSV data into the backend system. By providing detailed error messages, this aims to aid in diagnosing and resolving these challenges efficiently, ensuring that the CSV data is correctly converted.

## Errors Messages
<b> Error 1.  Failed to Upload ZIP File </b>
```
Failed to move the uploaded ZIP file.
```
<b>Solution </b>
* Ensure that the ZIP file is properly formatted and that you have sufficient permissions to upload files. Verify that the upload directory has the correct write permissions and that there are no issues with file paths or server storage limits. 
<br>

<b> Error 2.  Failed to Open the ZIP File </b>
```
Failed to open the ZIP file.
```
<b>Solution </b>
* Verify that the ZIP file is not corrupted and follows the proper compression format. Ensure that the ZIP file is complete and not password-protected, as these issues can prevent the system from opening it. 
<br>

<b> Error 3.  Missing CSV Manifest File </b>
```
The manifest.csv file is missing.
 or 
The classes.csv file is missing.
```
<b>Solution </b>
* Make sure to include the manifest.csv file in the ZIP folder, as it is required for the system to recognize and process the CSV data files according to the OneRoster v1.1 specification.
<br>

<b> Error 4. Unnecessary CSV File Detected</b>
```
courses.csv is not needed. Update its value to "absent" in the manifest file
```
<b>Solution </b>
* The following file is not required for this process. Update the manifest.csv file to set the value for file to "absent." This will inform the system that the file is intentionally omitted, ensuring that processing continues smoothly without expecting file.
<br>

<b> Error 5.  Missing Required CSV File</b>
```
The following required files are missing: users.csv, classes.csv
```
<b>Solution </b>
* The required files are missing from the ZIP folder. Ensure these files are included in the ZIP archive before proceeding, as they are essential for proper data integration according to the OneRoster v1.1 specification.
<br>

<b> Error 6. Invalid Headers in the CSV File</b>
```
The following files have invalid or missing headers: enrollments.csv
```
<b>Solution </b>
* Ensure that the headers in the CSV file match the required format as per the OneRoster v1.1 specification. Verify the spelling, capitalization, and ordering of headers to ensure compatibility with the system requirements.
<br>

<b> Error 7. Invalid Headers in the CSV File</b>
``` 
Data Type Errors Messages 

Validation failed for header 'startDate' in file 'academicSessions.csv'.
Validation failed for header 'endDate' in file 'academicSessions.csv'.
Validation failed for header 'dateLastModified' in file 'enrollments.csv'.
Validation failed for header 'classSourcedId' in file 'enrollments.csv'.
Validation failed for header 'role' in file 'enrollments.csv'.
Validation failed for header 'primary' in file 'enrollments.csv'.
Validation failed for header 'dateLastModified' in file 'users.csv'.
Validation failed for header 'username' in file 'users.csv'.
Validation failed for header 'password' in file 'users.csv'.

For more details, please refer to the specification: OneRoster CSV Table Specifications.
```
<b>Solution </b>
* Ensure that the data under each header in the CSV file adheres to the correct data types as specified in the OneRoster v1.1 specification. For instance, dates should be in the proper format (e.g., YYYY-MM-DD), and fields like primary should have the correct values (e.g., boolean values true or false). Verify each field's data type to ensure compatibility and avoid validation issues. Use the reference specification to check the expected format for each header and adjust the data accordingly.
<br>

<b> Error 8. Invalid Selection of Org ID</b>
``` 
Invalid form submission.
```
<b>Solution </b>
* Make sure the organisation ID (org_sourcedId) selected in the form is valid. Double-check that organization ID has data that populates the users, schools and classes and enrollments.
<br>

<b> Error 9. Invalid User in users.csv </b>
``` 
The returned data is missing the 'user' property
```
<b>Solution</b>
1. Ensure that all users referenced in classes.csv, enrollments.csv, or academicSessions.csv are also present in users.csv. Missing user records can cause inconsistencies in the data, resulting in this error.
2. Add the missing user information to users.csv to maintain consistency across all related CSV files. Verify that all user records are complete and properly formatted as per the OneRoster v1.1 specification.
<br>

<b> Error 10. Invalid organisation in orgs.csv </b>
``` 
The returned data is missing the 'org' property
```
<b>One of the Two Solution</b>
1. Ensure that at least one organization is present in orgs.csv. An organization is required for the OneRoster system to function correctly, so make sure to add an appropriate record to proceed.
2. Verify that the organisation is listed in classes.csv, enrollments.csv, or academicSessions.csv.
<br>

<b> Error 11. Invalid academicSession in academicSessions.csv </b>
``` 
The returned data is missing the 'academicSession' property
```
<b>Solution</b>
1. Ensure that at least one academic session is present in academicSessions.csv. An academic session is required for the OneRoster system to function properly, so add a relevant record to proceed.
2. Verify that the academic sessions referenced in classes.csv and enrollments.csv are properly listed in academicSessions.csv. All academic sessions used across related files must have corresponding entries in academicSessions.csv to avoid missing data and maintain consistency.
<br>

<b> Error 12. Invalid class in classes.csv </b>
``` 
The returned data is missing the 'class' property
```
<b>Solution</b>
1. Ensure that at least one class is present in classes.csv. A class is required for the OneRoster system to function properly, so add an appropriate record to proceed.
2. Verify that all classes referenced in enrollments.csv or academicSessions.csv are properly listed in classes.csv. Every class used across related files must have a corresponding entry in classes.csv to maintain data consistency and prevent errors.
<br>

<b> Error 13. Invalid course in classes.csv </b>
``` 
The returned data is missing the 'course' property
```
<b>Solution</b>
1. Ensure that at least one course is present in classes.csv. A course is required for defining classes in the OneRoster system, so add a relevant course record to proceed.
2. Verify that all courses referenced in classes.csv are unique to one another.
<br>
