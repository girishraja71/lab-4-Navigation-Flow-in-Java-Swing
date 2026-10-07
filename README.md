# INFO 5100 Labs

A Java Swing desktop application for INFO 5100 (Application Engineering and Development) at Northeastern University. Each lab builds on the same NetBeans project, and each finished lab is tagged in Git.

**Author:** Girish Raja Thiyagarajan

## Labs

| Lab | What was built | Git tag |
|---|---|---|
| Lab 4 | Split-pane navigation with CardLayout, a registration panel and a read-only view panel | `lab4` |

To see the code as it was for a lab:

```bash
git checkout lab4
git checkout main    # back to the latest version
```

## Requirements

- JDK 24 or newer
- Apache NetBeans
- The date picker library (`jcalendar-0.8.jar`) is included in `lib/`, so no extra setup is needed.

## How to run

1. Clone the repository.
2. In NetBeans, choose **File > Open Project** and select the cloned folder.
3. Right-click the project and choose **Run** (F6). The main class is `ui.MainJFrame`.

## Project structure

```
|-- lib/
|   `-- jcalendar-0.8.jar            Date picker library
|-- nbproject/                       NetBeans project configuration
|-- Screenshots/                     Application screenshots
|-- src/
|   |-- model/
|   |   `-- User.java                Data model passed between panels
|   `-- ui/
|       |-- MainJFrame.java          Main window: split pane and Form/View buttons
|       |-- RegistrationJPanel.java  Registration form and validation
|       `-- ViewJPanel.java          Read-only view of the submitted user
|-- build.xml
`-- README.md
```

## Lab 4: How it works

- `MainJFrame` contains a `JSplitPane`. The top holds the **Form** and **View** buttons. The bottom is a `CardLayout` panel holding the two screens.
- `RegistrationJPanel` collects the user's details and validates them. On a valid submit it builds a `User`, passes it to `ViewJPanel.displayUser(...)`, and switches to the view screen.
- `ViewJPanel` shows the submitted user with every field read-only, including the uploaded photo.

### Fields and validation

| Field | Rule |
|---|---|
| First name, last name | Required |
| Age | Number spinner |
| Gender | Male or Female (only one can be selected) |
| Phone number | Required, format `123-456-7890` (input mask) |
| Continent | Dropdown |
| Experience | Optional |
| Photo | Optional image upload |
