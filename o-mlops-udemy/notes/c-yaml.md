## YAML Complete

* YAML --> YAML Ain't Markup Language

## Usage
* Used for Data Serialization
* Better than JSON or XML for readability
* Uses Python style Indentation
* Both .yml or .yaml work

## Structure
* Map or a  List
* Key Value Pairs
* keys have to be unique

## Data Types
* Strings, Integers, dates, numbers or booleans
* List (starts with a dash)
* New map can be creating by increasing indentation level or resolving previous map


```sh

# Hey This is a yaml
my-course: AWS AI 
version: 1.0
price: 299
is_public: true
release-date: 2024-01-19
pre_enroll: null
category:
 - AWS
 - AI
course_dev: [Ravi, Sourav, Shalu]
dev_details:
 - name: Ravi
   email: ravi.31@gmail.com
 - name: Sourav
   email: sourav@gmail.com
short_description: >
 This is a course for 
 AWS AI Professionsals.

detailed_description: |
 This is a multiline string which 
 will be treated like a multiline string, 
 unlike previous examples.


```