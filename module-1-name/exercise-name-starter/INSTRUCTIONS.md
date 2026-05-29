# Exercise: JSON Data Contracts
## Overview
A data contract is a formal agreement that defines the structure, rules, and expectations for a dataset. In this exercise you will write a JSON data contract for a provided student grades dataset, then validate the dataset against your contract using Python.
Data contracts are used in data engineering and analytics pipelines to ensure data quality, catch errors early, and create a shared understanding between data producers and consumers.

## The Dataset
You have been provided with student_grades.csv. Open the file and examine its contents before writing your contract. The dataset has four columns, all of which are required - no row should have a missing value in any column.
Student Name - full name of the student (text)
Class - the course the student is enrolled in (text, restricted values)
Semester - the semester in which the class was taken (text, restricted values)
Grade - the student's numeric grade (integer, restricted range)
Approved values for Class:
Calculus 1
English 101
Python 101
Intro to Databases
Approved values for Semester:
Fall
Spring
Approved range for Grade: 60 to 100 (inclusive)

Part 1 — Write the JSON Data Contract
Create a file named student_grades_contract.json. Your contract must include the following four sections.
1a. Contract Metadata
Include a top-level contract section with:
name — the name of the dataset
version — use "1.0.0"
description — one sentence describing the dataset
1b. Source Definition
Include a source section that describes the file:
format — the file type
delimiter — the character separating values
has_header — whether the first row is a header (true or false)
1c. Schema Definition
Include a schema section with a fields object. For each of the four columns define:
type — the data type (string or integer)
nullable — whether empty values are allowed (all columns are required)
allowed_values — for Class and Semester, list the only accepted values
min_value and max_value — for Grade, define the acceptable numeric range
1d. Quality Rules
Include a quality_rules section with:
no_duplicate_rows — set to true
min_row_count — the minimum number of rows the file must contain (use 1)
Contract Skeleton
Use this structure as your starting point and fill in all the values:
json
{
  "contract": {
    "name": "...",
    "version": "...",
    "description": "..."
  },
  "source": {
    "format": "...",
    "delimiter": "...",
    "has_header": ...
  },
  "schema": {
    "fields": {
      "Student Name": {
        "type": "...",
        "nullable": ...
      },
      "Class": {
        "type": "...",
        "nullable": ...,
        "allowed_values": [...]
      },
      "Semester": {
        "type": "...",
        "nullable": ...,
        "allowed_values": [...]
      },
      "Grade": {
        "type": "...",
        "nullable": ...,
        "min_value": ...,
        "max_value": ...
      }
    }
  },
  "quality_rules": {
    "no_duplicate_rows": ...,
    "min_row_count": ...
  }
}

Part 2 — Validate the Dataset in Python
Write a Python script or Jupyter notebook that loads your contract and validates the dataset against it. Your code must perform the following checks in order:
Load the CSV using pandas
Load the JSON contract using the json library
Check that all required columns are present
Check that no column contains null or empty values
Check that all Class values match the allowed list in your contract
Check that all Semester values match the allowed list in your contract
Check that all Grade values are integers within the min/max range defined in your contract
Check for duplicate rows
For each check, print a clear PASS or FAIL result. If a check fails, print the rows that caused the failure.

## Deliverables
Submit the following file:
student_grades_contract.json - your completed data contract
Ensure you use this naming convention or validation script may not work



## Tips
Read the entire dataset before writing your contract - look at the actual values in each column.
Your contract is just a structured JSON file. There is no single correct format, but it must contain all the required fields listed above.

Test your validation script on the provided dataset - there should be 4 failed rows if done correctly.


