# Criterion A: Planning
## Problem Definition

My client is **Mr. X**, the Director of IT Security at a large financial institution. The bank’s employees frequently handle sensitive information, and the client is concerned about secure password management. With many employees working remotely and in shared workspaces, traditional password managers could attract attention or be targeted by cyber threats. Mr. X is seeking a **secure, covert solution** for storing passwords that integrate seamlessly into the daily workflow of bank employees without raising suspicion.

(See the evidence of Consultation in the Appendix)

## Proposed Solution

I propose to develop **Schedulix**, a disguised password manager in Python, which functions as a simple calendar application. This calendar will allow users to add and manage events while hiding its true purpose—storing and retrieving passwords securely—activated only by a secret code. A login and signup system will add an extra layer of security, ensuring only authorized users have access.
### Why Python?

I proposed Python as it is the ideal choice for this project for several reasons:

- **Cross-platform Compatibility**: Python can run on various operating systems used by employees (Windows, MacOS, Linux), ensuring the tool is widely accessible across different work environments.
- **Readability and Maintenance**: Python’s clean syntax makes the program easy to maintain and extend, which is essential for a growing financial institution where the system may need to be updated or modified in the future.
- **Security Libraries**: Python has strong support for cryptographic libraries such as `cryptography` or `hashlib`, allowing the tool to implement robust encryption for password storage, which is a core requirement of the project.
- **Rapid Prototyping**: Python allows for fast development cycles, meaning that we can iterate quickly on the design and incorporate feedback from the client to meet their exact needs in a shorter timeframe.

### Why Use a CSV File?

I proposed using a **CSV file** to store the calendar events and encrypted passwords for the following reasons:

- **Simplicity and Transparency**: CSV files are simple to manage, and they integrate well with Python’s native libraries. This makes the tool efficient to run without complex database setups that may be unnecessary for the client’s needs.
- **Low Resource Consumption**: For a financial institution, performance matters, and CSV files provide a lightweight, low-resource option.
- **Data Encryption**: Even though the data is stored in CSV, passwords will be encrypted using basic cryptographic techniques like character shifting or hashing. This ensures that sensitive information remains protected, even if the file is accessed without permission.

## Requirements

### Basic Calendar Functionality

- The application should operate as a basic calendar where users can **add, view, and edit events**.

### Hidden Functionality

- The program should include a hidden password manager mode that is only activated when a **secret code** (e.g., "open123") is entered.
- Once in password manager mode, users should be able to:
  - **Add a password** for specific purposes, such as logging into websites or accounts.
  - **View the stored passwords**, which are masked initially and revealed only if the user re-enters the secret code.
  - Optionally, the application can display passwords in a **partially masked form** (e.g., showing only the first and last characters for security).

### Basic Security Features

- Passwords should be stored in an **external text file**, allowing the program to persistently save user data.
- To ensure security, passwords should be stored using a basic **encryption or obfuscation technique**. This could include reversing the password string, character shifting, or more advanced methods like hashing or encryption algorithms.

### Login and Signup System

- The tool should include a **login and signup system** to restrict access to the password manager.
- Only registered users can access the application, ensuring protection and preventing unauthorized access to both calendar functions and the hidden password manager.
- The login system should prompt for a **username and password**, securing the application from the start.

### User Interaction

- The tool will be operated through a **simple terminal-based interface**.


# Criterion  B: Design
## System diagram
![project1](https://github.com/user-attachments/assets/5b611962-edef-4d84-a1e5-b92cd93a39db)
This diagram shows the solution's hardware and software components.

## Flow diagrams for algorithms
![Algorithm flowchart example (2)](https://github.com/user-attachments/assets/d5bc9276-90e7-42ef-9918-dc9beb691386)
**fig. 1** This is the flow diagram for the algorithm used to sign users up while validating information and checking uniqueness, and save the information to the database.

![Algorithm flowchart example (1)](https://github.com/user-attachments/assets/35a2d944-3ef4-410d-94da-83ded31e0bd6)
**fig. 2** This is the flow diagram for the algorithm used to evaluate the strength of a password, both user inputted and generated ones.

![Algorithm flowchart example](https://github.com/user-attachments/assets/9d1c454b-17cc-4c36-83b6-4399a8dd5381)
**fig. 3**This is the flow diagram for the algorithm used to generate a secure password when the user needs it.

## Data storage

I use CSV files to store data in this product because they allow for easy and convenient access to the information. However, recognizing that CSV files are not inherently secure due to their simplicity and accessibility, I take additional steps to protect sensitive data. The saved passwords are encrypted. I use three CSV files within this product: user.csv, which stores user information, cal.csv which stores calendar events and passwords.csv, which holds saved passwords. 



## Test plan

| Description                                    | Test Type       | Input                                                                                                                                                      | Expected Outcome                                                                                                                                                                        |
|------------------------------------------------|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Test for Signup System**                     | Unit test       | 1. Run the script 2. Click the Signup button 3. Input the username and password 4. Click Signup                                                             | A popup should show if the username exists or passwords don’t match; otherwise, user should be redirected to login screen.                                                               |
| **Test for Login System**                      | Unit test       | 1. Run the script 2. Input correct username and password 3. Click Login                                                                                     | Successful login should take user to the User Menu. If credentials are incorrect or file is missing, an error message should appear.                                                     |
| **Test for Add Event System**                  | Unit test       | 1. Login 2. Select "Add Event" from the menu 3. Input event date and description 4. Press Add Event                                                         | If input is correct, a success message should appear. If the date format is wrong, or the event is empty, an error message should appear.                                                |
| **Test for View Events System**                | Unit test       | 1. Login 2. Select "View Events" from the menu                                                                                                              | The list of events should be displayed with date and description. If there are no events, a message indicating "No events found" should be shown.                                        |
| **Test for Edit Event System**                 | Unit test       | 1. Login 2. Select "Edit Event" 3. Input the number corresponding to the event to edit 4. Input new date and description                                    | The event should be updated successfully, and a confirmation message should be displayed. If the event number is invalid or date format is wrong, an error message should appear.        |
| **Test for Delete Event System**               | Unit test       | 1. Login 2. Select "Delete Event" 3. Input the number corresponding to the event to delete                                                                  | The event should be removed, and the list should be updated with a success message. If an invalid event number is entered, an error message should be shown.                             |
| **Test for Password Manager - Add Password**   | Integration test | 1. Login 2. Open Password Manager using current date and time 3. Select "Add Password" 4. Enter website, account name, and password or leave blank to auto-generate                     | If inputs are valid, a success message should be shown, and the password should be saved. A generated password should appear if left blank.                                               |
| **Test for Password Manager - View Passwords** | Integration test | 1. Login 2. Open Password Manager using current date and time 3. Select "View Passwords" 4. Select a website to view its stored password                                                | The list of saved passwords should be displayed. When selecting a website, the corresponding decrypted password should be shown.                                                         |
| **Test for Password Manager - Delete Password**| Integration test | 1. Login 2. Open Password Manager using current date and time 3. Select "Delete Password" 4. Input the number corresponding to the password entry to delete                             | The password entry should be deleted, and a success message should be displayed. If an invalid number is selected, an error message should be shown.                                      |
| **Test for Logout System**                     | Unit test       | 1. Login 2. Perform any action 3. Select "Logout"                                                                                                           | Upon selecting logout, the user should be returned to the login screen, ending the session.                                                                                               |

## Record of tasks

| Task Number | Planned Action                   | Planned Outcome                                                                                          | Time Estimated | Target Completion Date | Criterion |
|-------------|----------------------------------|----------------------------------------------------------------------------------------------------------|----------------|------------------------|-----------|
| 1           | First meeting with the client    | Obtain a problem definition, understand the situation to propose a solution.                              | 10 min         | Sep 10th               | A         |
| 2           | Set criteria                     | Develop detailed criteria for the solution that the program will follow to perform all tasks.             | 20 min         | Sep 10th               | A         |
| 3           | Complete system diagram          | Create a diagram representing the hardware and software components of the calendar-based password manager. | 20 min         | Sep 16th               | B         |
| 4           | Complete test plan               | Create a table specifying the process for testing the solution with inputs and expected outputs.           | 45 min         | Sep 20th               | B         |
| 5           | Complete calendar function       | Develop a disguised calendar interface with interactive event features, running on the terminal.           | 150 min        | Sep 24th               | C         |
| 6           | Complete password manager function | Implement a hidden password manager activated by a secret code, ensuring it follows criteria and passes tests. | 90 min         | Sep 25th               | C         |
| 7           | Complete 3 flow diagrams         | Diagrams that visually represent how key functions in the calendar and password manager work.              | 45 min         | Sep 26th               | B         |
| 8           | Record a demonstration           | Provide the client a preview of the product for feedback and adjustments if needed.                       | 20 min         | Sep 26th               | D         |
| 9           | Finalize record of tasks         | Review and finalize the record of tasks to ensure everything is documented and completed.                  | 10 min         | Sep 27th               | B         |

