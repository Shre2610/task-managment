# TaskFlow – Task Management System

A modern, responsive, and lightweight Task Management System web application built with Python, Flask, SQLite, Jinja2, and Vanilla JavaScript/CSS. Designed as a complete, academic-grade project for task tracking, team workload management, deadline monitoring, and project deliverable reporting.

---

## 🚀 Key Features

* **Real-time Task Dashboard**: High-level live stats tracking *Total Tasks*, *To Do*, *In Progress*, *Completed*, and *Overdue Tasks*, paired with a project deliverables completion rate bar and an overdue alert counter.
* **Full Database-Backed CRUD Operations**: Seamless creation, viewing, editing, and deletion of tasks with comprehensive server-side input validation and flash alerts.
* **Task Attributes**:
  * Auto-generated Primary Key (`Task ID`)
  * Task Title (required, validated)
  * Task Description (multiline text)
  * Assignee Name & ID with auto-suggestions
  * Category (Development, Design, Research, Testing, Documentation)
  * Priority (Low, Medium, High, Urgent) with color-coded pill badges
  * Status (To Do, In Progress, Completed) with inline quick-change controls
  * Start Date (optional) & Due Date (required)
  * Automatic timestamps (`created_at`, `updated_at`)
* **Overdue Deadline Monitoring**: Automatically flags tasks whose due date is in the past and whose status is not `Completed`.
* **Instant Quick-Status Toggle**: Update a task's status directly from dashboard and master tables with a single click without opening the edit form.
* **Multi-Factor Search & Filtering**:
  * Keyword search across Title, Description, Assignee, and Category.
  * Filter by Status (`To Do`, `In Progress`, `Completed`).
  * Filter by Priority (`Urgent`, `High`, `Medium`, `Low`).
  * Filter by Assignee.
  * Filter by Deadline range (Overdue, Due Today, Due This Week, Due This Month).
  * Sort by Due Date (Soonest/Latest), Priority (Urgent first), Title (A-Z), or Recently Added.
* **Zero-Reload AJAX Interactivity**: Master task table filters and paginates smoothly via asynchronous `fetch()` and `DOMParser` without full page refreshes, synchronizing URL parameters with `window.history.pushState()`.
* **Smooth Filter Reset**: Restores the unfiltered dataset and clears all dropdowns client-side without page reloads.
* **Excel Report Export Engine**: Generates and downloads styled Microsoft Excel (`.xlsx`) workbooks matching active search parameters with OpenPyXL.
* **Team Workload View (`/assignee`)**: Dedicated profiles for individual team members displaying assigned deliverables, workload statistics, and contact info.
* **Deliverables Timeline View (`/timeline`)**: Monthly schedule overview grouping deadlines and metrics by month.
* **Dark / Light Mode**: Theme toggle in header bar with smooth CSS transitions and `localStorage` persistence with zero page flash.
* **Self-Healing SQLite Database**: Initializes tables, constraints, indexes, and seeds realistic initial mock tasks upon startup.

---

## 🛠️ Tech Stack

* **Frontend**: HTML5, Vanilla CSS3 (custom CSS variables, flexbox, grid, and dark mode variants), Vanilla JavaScript (ES6+ DOM APIs, no heavy frameworks).
* **Backend**: Python 3.8+, Flask 3.0.3.
* **Database**: SQLite3 (relational schema with `CHECK` constraints, indexes, and parameterized queries).
* **Export Engine**: OpenPyXL 3.1.2.
* **WSGI Production Server**: Gunicorn 22.0.0.

---

## 📁 Project Folder Structure

```text
task-management/
│
├── main.py                 # Core Flask entrypoint containing routes, DB queries & Excel export
├── requirements.txt         # Production and development Python dependencies
├── README.md               # Project documentation & architectural overview
├── deployment_guide.md     # Deployment guide for Render with persistent SQLite volumes
├── database.db             # SQLite database file (auto-initialized upon first launch)
│
├── static/
│   ├── app.js              # Theme switcher, custom select components, AJAX filtering & reset
│   └── style.css           # Vanilla CSS layout, dark mode tokens, priority/status badges
│
└── templates/              # HTML layout templates using Jinja2 inheritance
    ├── base.html           # Main shell wrapper (sidebar, header, theme toggle, flash alerts)
    ├── dashboard.html      # Metrics cards, completion bar, search bar, recent tasks table
    ├── allocations.html    # Master tasks directory with AJAX, sort, filter, and pagination
    ├── add_assignment.html # Dual-purpose form for creating and editing tasks
    ├── employee.html       # Team member profile and assigned workload overview
    └── month.html          # Monthly deliverables schedule and timeline overview
```

---

## 💾 Database Schema

The system uses an engineered SQLite table `tasks` with strict constraints and indexes:

```sql
CREATE TABLE tasks (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    title TEXT NOT NULL,
    description TEXT,
    assignee TEXT NOT NULL,
    assignee_id TEXT,
    category TEXT NOT NULL DEFAULT 'Development',
    priority TEXT NOT NULL DEFAULT 'Medium' CHECK(priority IN ('Low', 'Medium', 'High', 'Urgent')),
    status TEXT NOT NULL DEFAULT 'To Do' CHECK(status IN ('To Do', 'In Progress', 'Completed')),
    start_date TEXT,
    due_date TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_tasks_status ON tasks(status);
CREATE INDEX idx_tasks_priority ON tasks(priority);
CREATE INDEX idx_tasks_due_date ON tasks(due_date);
CREATE INDEX idx_tasks_assignee ON tasks(assignee);
```

---

## 💻 Installation & How to Run

### 1. Prerequisites
Ensure you have **Python 3.8+** installed:
```bash
python --version
```

### 2. Install Dependencies
```bash
pip install -r requirements.txt
```

### 3. Run the Server
```bash
python main.py
```

### 4. Access the Application
Open your web browser and navigate to:
👉 **[http://localhost:5000](http://localhost:5000)**
