# README Audit: `struct_to_dict.py`

This audit checks each claim in the README for `struct_to_dict.py` against the actual code. Claims were verified by reading the code and by running it (Python 3.12.3) with sample and edge-case input.

## Summary

- **Claims checked:** 17
- **Supported:** 16
- **Not Supported:** 1 (the clone URL, which is a placeholder the code cannot confirm)

## Source Code Audited

```python
from collections import namedtuple

Student = namedtuple("Student", ["name", "roll_number", "course"])

student = Student(
    name=input("Enter your name: "),
    roll_number=input("Enter your roll number: "),
    course=input("Enter your course: ")
)

student_dict = student._asdict()

print("Dictionary form:")
print(student_dict)
```

## Claim-by-Claim Results

| # | Claim in README | Verdict | Evidence from the code |
|---|---|---|---|
| 1 | Collects student details from the user and converts them into a dictionary | Supported | Three `input()` calls fill the record, and `student._asdict()` converts it. Running with sample input printed a dictionary. |
| 2 | Uses `namedtuple` from Python's standard library | Supported | `from collections import namedtuple` is the only import in the file. |
| 3 | Defines a `Student` record with three fields: `name`, `roll_number`, `course` | Supported | `namedtuple("Student", ["name", "roll_number", "course"])`. Checked at runtime: `Student._fields` is `('name', 'roll_number', 'course')`. |
| 4 | Fills the record with user input | Supported | Each field is set from an `input(...)` call in the `Student(...)` constructor. |
| 5 | Converts it to a dictionary with the `_asdict()` method | Supported | `student_dict = student._asdict()`. The result's type is `dict`. |
| 6 | The whole program is in a single file, `struct_to_dict.py` | Supported | All logic is in one file. |
| 7 | Features: defines a struct-like `Student` record using `namedtuple` | Supported | Same evidence as #3. The `student` object is a tuple subclass with named fields. |
| 8 | Features: collects name, roll number, and course interactively | Supported | The prompts are `Enter your name: `, `Enter your roll number: `, and `Enter your course: `. |
| 9 | Features: prints the resulting dictionary | Supported | `print("Dictionary form:")` followed by `print(student_dict)`. |
| 10 | Features: no external dependencies | Supported | Only `collections`, which is part of the standard library, is imported. |
| 11 | Requires Python 3.8 or higher, because earlier versions return an `OrderedDict` from `_asdict()` | Supported, from documentation | This follows the Python documentation for `namedtuple._asdict()`: it returned an `OrderedDict` before 3.8 and a regular `dict` from 3.8. Only 3.12.3 was run, so older versions were not tested. |
| 12 | No third-party packages needed | Supported | Same evidence as #10. |
| 13 | `git clone https://github.com/<your-username>/<your-repository>.git` | Not Supported | The code cannot confirm any repository, URL, or folder name, and the URL is a placeholder. |
| 14 | `python struct_to_dict.py` runs the script | Supported | It ran successfully. On some systems the command is `python3`. |
| 15 | The program asks for name, roll number, and course one after another, then prints the dictionary | Supported | The three `input()` calls run in that order, and the prints come after them. |
| 16 | Example output is `{'name': 'Asha', 'roll_number': '42', 'course': 'CSE'}` after the `Dictionary form:` line | Supported | Tested with inputs `Asha`, `42`, `CSE`. The printed dictionary matched exactly. |
| 17 | Every value is stored as a string, including the roll number | Supported | `input()` returns strings and no conversion is done. Checked at runtime: the `roll_number` value was of type `str`. |

## Behaviors the README Does Not Mention

### No input validation

Empty answers are accepted. Pressing Enter at all three prompts printed `{'name': '', 'roll_number': '', 'course': ''}`. The roll number is not checked to be numeric.

### No input available

If the script runs with no standard input (for example, `python struct_to_dict.py < /dev/null`), it stops with `EOFError: EOF when reading a line`.

### Import side effect

Importing the file runs the prompts and prints the output, because the `input()` calls and `print(...)` lines sit at module level without an `if __name__ == "__main__":` guard. In testing, `import struct_to_dict` immediately asked for a name, roll number, and course.

## Test Environment

- Python 3.12.3
- Checks run: direct execution with sample input (`Kanishk` / `12345` / `B.Tech` and `Asha` / `42` / `CSE`), empty input at every prompt, no standard input, import of the module, runtime check of the field names and the types of `student`, `student_dict`, and the `roll_number` value, and a search of the file for imports.
