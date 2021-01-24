---
title: 29. Hands-on Lab Creating Custom Python Exception Types
tags: [handson]
keywords: sample
#summary: "This is just a sample topic..."
sidebar: python_sidebar
permalink: Lab_29.html
folder: handson
---


## Introduction

When building a larger system with custom classes, we will likely have different situations come up that wouldn't be encompassed by existing exceptions. In this hands-on lab, we'll create a few custom exception types that will fit into our employee management class hierarchy. To feel comfortable completing this lab, you'll want to know how to create custom exception types (watch the "Creating Custom Exception Types" video from the Certified Associate in Python Programming Certification course).

## Solution

To work through the lab, you can either log in via a terminal on your local machine and use a text editor in the terminal, or you can use VS Code in the browser. This lab guide will go through the steps using VS Code in the browser.

In order to use VS Code in the browser, navigate to the public IP address of the workstation server (provided on the lab page) on port 8080 (e.g., http://<PUBLIC_IP>:8080).

## Create MissingEmployeeError and DatabaseError in employee.py

1. In the menu at the top, click **Terminal** > **New Terminal**.

2. Run **test_custom_exceptions.py**:

```
python3.7 test_custom_exceptions.py
```

We'll get a couple errors.

3. In the menu at the top, click **File** > **Open**.

4. Select **employee.py**.

5. Add the following to the top of the file:

```
class MissingEmployeeError(Exception):
    pass

class DatabaseError(Exception):
    pass
    # Rest of file unchanged and omitted
```

6. Run `test_custom_exceptions.py`:

```
python3.7 test_custom_exceptions.py
```

This time, we'll get an error saying it expected a `DatabaseError` but instead got `FileNotFoundError`.

## Raise DatabaseError Anywhere We Fail to Open the Database File

1. Everywhere we use `open` in the `Employee` class, we need to catch these exceptions and instead raise a `DatabaseError`. To do so, edit the `class Employee` section to match the following:

```
class Employee:
    default_db_file = "employee_file.txt"

    @classmethod
    def get_all(cls, file_name=None):
        results = []

        if not file_name:
            file_name = cls.default_db_file

        try:
            with open(file_name, "r") as f:
                lines = [
                    line.strip("\n").split(",") + [index + 1]
                    for index, line in enumerate(f.readlines())
                ]
        except (FileNotFoundError, PermissionError) as err:
            raise DatabaseError(str(err))

        for line in lines:
            results.append(cls(*line))

        return results

    @classmethod
    def get_at_line(cls, line_number, file_name=None):
        if not file_name:
            file_name = cls.default_db_file

        try:
            with open(file_name, "r") as f:
                line = [
                    line.strip("\n").split(",") + [index + 1]
                    for index, line in enumerate(f.readlines())
                ][line_number - 1]
                return cls(*line)
        except (FileNotFoundError, PermissionError) as err:
            raise DatabaseError(str(err))

    def __init__(self, name, email_address, title, phone_number=None, identifier=None):
        self.name = name
        self.email_address = email_address
        self.title = title
        self.phone_number = phone_number
        self.identifier = identifier

    def email_signature(self, include_phone=False):
        signature = f"{self.name} - {self.title}\n{self.email_address}"
        if include_phone and self.phone_number:
            signature += f" ({self.phone_number})"
        return signature

    def save(self, file_name=None):
        if not file_name:
            file_name = self.default_db_file

        try:
            with open(file_name, "r+") as f:
                lines = f.readlines()
                if self.identifier:
                    lines[self.identifier - 1] = self._database_line()
                else:
                    lines.append(self._database_line())
                f.seek(0)
                f.writelines(lines)
        except (FileNotFoundError, PermissionError) as err:
            raise DatabaseError(str(err))

    def _database_line(self):
        return (
            ",".join(
                [self.name, self.email_address, self.title, self.phone_number or ""]
            )
            + "\n"
        )
```

## Raise MissingEmployeeError in get_at_line and save if IndexError Occurs

1. At the bottom of the `get_at_line` section, add the following:

```
except IndexError:
    raise MissingEmployeeError(f"no employee at line {line_number}")
At the bottom of the save section, add the following:

except IndexError:
    raise MissingEmployeeError(f"no employee at line {self.identifier}")
For clarity's sake, this is what the class Employee section should now look like:

class Employee:
    default_db_file = "employee_file.txt"

    @classmethod
    def get_all(cls, file_name=None):
        results = []

        if not file_name:
            file_name = cls.default_db_file

        try:
            with open(file_name, "r") as f:
                lines = [
                    line.strip("\n").split(",") + [index + 1]
                    for index, line in enumerate(f.readlines())
                ]
        except (FileNotFoundError, PermissionError) as err:
            raise DatabaseError(str(err))

        for line in lines:
            results.append(cls(*line))

        return results

    @classmethod
    def get_at_line(cls, line_number, file_name=None):
        if not file_name:
            file_name = cls.default_db_file

        try:
            with open(file_name, "r") as f:
                line = [
                    line.strip("\n").split(",") + [index + 1]
                    for index, line in enumerate(f.readlines())
                ][line_number - 1]
                return cls(*line)
        except (FileNotFoundError, PermissionError) as err:
            raise DatabaseError(str(err))
        except IndexError:
            raise MissingEmployeeError(f"no employee at line {line_number}")

    def __init__(self, name, email_address, title, phone_number=None, identifier=None):
        self.name = name
        self.email_address = email_address
        self.title = title
        self.phone_number = phone_number
        self.identifier = identifier

    def email_signature(self, include_phone=False):
        signature = f"{self.name} - {self.title}\n{self.email_address}"
        if include_phone and self.phone_number:
            signature += f" ({self.phone_number})"
        return signature

    def save(self, file_name=None):
        if not file_name:
            file_name = self.default_db_file

        try:
            with open(file_name, "r+") as f:
                lines = f.readlines()
                if self.identifier:
                    lines[self.identifier - 1] = self._database_line()
                else:
                    lines.append(self._database_line())
                f.seek(0)
                f.writelines(lines)
        except (FileNotFoundError, PermissionError) as err:
            raise DatabaseError(str(err))
        except IndexError:
            raise MissingEmployeeError(f"no employee at line {self.identifier}")

    def _database_line(self):
        return (
            ",".join(
                [self.name, self.email_address, self.title, self.phone_number or ""]
            )
            + "\n"
        )
```

4. Run the `test_custom_exceptions.py` script:

```
python3.7 test_custom_exceptions.py
```

We shouldn't see any issues.
