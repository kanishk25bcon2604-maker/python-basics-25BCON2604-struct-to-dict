# Struct to Dictionary Converter

A simple Python program that collects student details from the user and converts them into a dictionary.

## Description

This project shows how to store related data in a struct-like record and convert it to a dictionary. It uses `namedtuple` from Python's standard library to define a `Student` record with three fields (`name`, `roll_number`, and `course`), fills it with user input, and converts it to a dictionary with the `_asdict()` method.

The whole program is in a single file, `struct_to_dict.py`.

## Features

- Defines a struct-like `Student` record using `namedtuple`
- Collects the name, roll number, and course interactively from the user
- Converts the record to a dictionary using `_asdict()`
- Prints the resulting dictionary
- No external dependencies

## Requirements

- Python 3.8 or higher (earlier versions return an `OrderedDict` from `_asdict()` instead of a regular `dict`)
- No third-party packages

## Installation

Clone the repository and move into the project folder:

```bash
git clone https://github.com/<your-username>/<your-repository>.git
cd <your-repository>
```

## Usage

Run the script from the command line:

```bash
python struct_to_dict.py
```

The program asks for three inputs, one after another: your name, your roll number, and your course. It then prints the dictionary form of the details you entered.

## Example

```text
Enter your name: Asha
Enter your roll number: 42
Enter your course: CSE
Dictionary form:
{'name': 'Asha', 'roll_number': '42', 'course': 'CSE'}
```

Note that every value is stored as a string, including the roll number, because the program uses `input()` and does not convert the values.
