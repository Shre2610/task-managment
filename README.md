# TaskFlow – Task Management System

TaskFlow is a web-based task management application designed to help users create, organize, assign, and track tasks through a simple dashboard.

## Features

- **Dashboard:** View task statistics and task progress.
- **Task Management:** Create, view, edit, and delete tasks.
- **Task Details:** Manage task titles, descriptions, assignees, priorities, statuses, and due dates.
- **Search and Filters:** Find tasks and filter them by status, priority, or assignee.
- **Task Tracking:** Monitor pending, in-progress, completed, and overdue tasks.
- **Responsive UI:** A clean interface designed for desktop and smaller screens.
- **Dark and Light Mode:** Switch between themes.

## Technology Stack

- **Backend:** Python, Flask
- **Frontend:** HTML5, CSS3, JavaScript
- **Templating Engine:** Jinja2
- **Database:** SQLite
- **Excel Export:** OpenPyXL, if enabled in the current build
- **Production Server:** Gunicorn

## Project Structure

```text
task-managment/
├── main.py
├── requirements.txt
├── README.md
├── deployment_guide.md
├── static/
│   ├── app.js
│   └── style.css
└── templates/
    ├── base.html
    ├── dashboard.html
    ├── allocations.html
    ├── add_assignment.html
    └── ...
```

## Installation and Setup

### 1. Clone the Repository

```bash
git clone https://github.com/Shre2610/task-managment.git
cd task-managment
```

### 2. Create a Virtual Environment (Recommended)

**Windows:**

```bash
python -m venv .venv
.venv\Scripts\activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Run the Application

```bash
python main.py
```

### 5. Open in Your Browser

Visit:

http://127.0.0.1:5000

## Database

TaskFlow uses SQLite for data storage. The database initialization and schema are managed by the application.

Avoid committing sensitive data, credentials, secret keys, or private database records.

## Future Improvements

- User authentication and role-based access control
- Task comments and activity history
- Email notifications for upcoming deadlines
- Advanced reporting and analytics

## Repository

GitHub: https://github.com/Shre2610/task-managment

## Project Purpose

This project demonstrates the development of a database-backed web application using Flask, SQLite, and frontend web technologies for task management.
