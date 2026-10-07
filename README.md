# INFO 5100 Application Engineering and Development

A Java Swing desktop application built across the labs of INFO 5100 at Northeastern University. Each lab adds features to the same idea: collect a user's details, validate them, and display them back.

**Author:** Girish Raja Thiyagarajan

## Labs

| Lab | What was built | Where |
|---|---|---|
| Lab 3 | Single-window user input form with validation, photo upload, and a profile dialog | [`girishraja71/lab-3`](https://github.com/girishraja71/lab-3) |
| Lab 4 | Split-pane navigation with CardLayout, separate registration and view panels, and a date picker | This repository, tag `lab4` |

To see the code exactly as it was for Lab 4:

```bash
git checkout lab4
git checkout main    # return to the latest version
```

## Requirements

- JDK 24 or newer and Apache NetBeans (developed with NetBeans 31)
- No other setup. The date picker library is bundled in `lib/` and referenced by a relative path.

## How to run

1. Clone the repository.
2. In NetBeans, choose **File > Open Project** and select the cloned folder.
3. Right-click the project and choose **Clean and Build**, then **Run** (F6). The main class is `ui.MainJFrame`.

## Project structure

```
|-- lib/
|   `-- jcalendar-0.8.jar            Date picker library
|-- nbproject/                       NetBeans project configuration
|-- lab 4 screenshots/              Lab 4 screenshots, Step 1 to Step 3
|-- src/
|   |-- model/
|   |   `-- User.java                Data model
|   `-- ui/
|       |-- MainJFrame.java          Main window: split pane and navigation
|       |-- RegistrationJPanel.java  Registration form and validation
|       `-- ViewJPanel.java          Read-only details screen
|-- build.xml
`-- README.md
```

## Lab 4: Registration and view panels

### How it works

- `MainJFrame` contains a `JSplitPane`. The top section holds the **Form** and **View** navigation buttons. The bottom section is a panel using `CardLayout` that holds the two screens.
- `RegistrationJPanel` collects the user's details and validates them. On a valid submission it builds a `User` object, shows a **Success** dialog, passes the user to `ViewJPanel.displayUser(...)`, and switches the card to the view screen.
- `ViewJPanel` displays the `User` with every input locked, including the uploaded photo. Its Submit and Upload buttons are hidden.
- `User` is the model that carries the data between the two panels.

### Fields and validation

| Field | Rule |
|---|---|
| First name, last name | Required |
| Age | Chosen with a number spinner |
| Date | Chosen with the calendar picker |
| Gender | Male or Female radio buttons. Only one can be selected |
| Phone number | Required. Format `123-456-7890`, enforced by an input mask |
| Continent | Dropdown |
| Experience | Optional |
| Photo | Optional. Chosen with a file chooser and shown as a preview |

Each failed check shows an error message describing the problem, and the form stays open until the input is valid.

### Screenshots

**Step 1. View screen.** Clicking **View** shows the submitted details with all inputs locked, plus the photo.

![Step 1](lab%204%20screenshots/Screenshot%202026-10-06%20220808.png)

**Step 2. Success dialog.** Shown after a valid submission, with every input and the uploaded photo.

![Step 2](lab%204%20screenshots/Screenshot%202026-10-06%20220725.png)

**Step 3. Project structure.** The `model` package holds `User.java`, and the `ui` package holds the main frame and the two panels.

![Step 3](lab%204%20screenshots/Screenshot%202026-10-06%20214300.png)

## Lab 3: User input form

The first version was a single-window form (`UserJFrame`) with validation, a photo upload, and a **Profile** dialog that displayed the submitted details using `User.toString()`. That version is in its own repository: [girishraja71/lab-3](https://github.com/girishraja71/lab-3).

## Design notes and assumptions

- The view screen is read-only. It reflects the most recent valid submission.
- Before the first submission, the view screen is empty.
- Photos are scaled to 60 by 60 pixels on the view screen and 150 by 150 pixels in the success dialog.
- The `User` model also has `email` and `hobbies` fields, kept from Lab 3. The Lab 4 form does not collect them yet.
