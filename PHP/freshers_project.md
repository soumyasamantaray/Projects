# Simple To-Do List Application

## Project Description

This is a basic web-based To-Do List application developed using PHP, HTML, CSS, and a database (initially file-based, then MySQL/SQLite). The primary goal of this project is to provide a hands-on daily practice exercise for beginners and freshers in PHP development, covering fundamental concepts from form handling to database interaction.

Users can add new tasks, view existing tasks, mark tasks as complete or incomplete, and delete tasks. The application demonstrates core web development patterns and data persistence techniques.

## Features

The application will progressively implement the following features:

*   **Add New Tasks:** A simple form to input and submit new task descriptions.
*   **View All Tasks:** Display a list of all tasks.
*   **Mark Tasks as Complete/Incomplete:** Functionality to toggle the status of a task.
*   **Delete Tasks:** Ability to remove individual tasks from the list.
*   **Data Persistence:**
    *   Initially, tasks will be stored in a flat file (e.g., JSON or plain text).
    *   Later, tasks will be stored in a relational database (MySQL or SQLite).
*   **Basic User Interface:** A clean and functional interface using HTML and minimal CSS.

## Technologies Used

*   **Backend:** PHP
*   **Frontend:** HTML, CSS
*   **Database:**
    *   File-based (e.g., `.txt`, `.json`) for initial persistence.
    *   MySQL or SQLite for robust data storage.
*   **Server (for local development):** Apache or Nginx (typically provided by XAMPP/WAMP/MAMP).

## Setup and Installation (Local Development)

To get this project running on your local machine, follow these steps:

1.  **Install a Local Server Environment:**
    If you don't have one, install a local server package like [XAMPP](https://www.apachefriends.org/index.html), [WAMP](https://www.wampserver.com/en/), or [MAMP](https://www.mamp.info/en/mamp/mac/). These packages provide Apache, MySQL, and PHP.

2.  **Clone the Repository (or create project folder):**
    ```bash
    git clone https://github.com/your-username/simple-todo-list-php.git
    # OR
    mkdir simple-todo-list-php
    cd simple-todo-list-php
    ```
    Place this folder inside your web server's document root (e.g., `htdocs` for XAMPP).

3.  **Database Setup (for Day 3 onwards):**
    *   **For MySQL:**
        *   Start your MySQL server (via XAMPP/WAMP/MAMP control panel).
        *   Open phpMyAdmin (usually accessible at `http://localhost/phpmyadmin`).
        *   Create a new database named `todo_app`.
        *   Execute the following SQL query to create the `tasks` table:
            ```sql
            CREATE TABLE tasks (
                id INT AUTO_INCREMENT PRIMARY KEY,
                description VARCHAR(255) NOT NULL,
                status TINYINT(1) DEFAULT 0, -- 0 for incomplete, 1 for complete
                created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
            );
            ```
    *   **For SQLite:**
        *   You'll need to ensure the `pdo_sqlite` extension is enabled in your `php.ini`.
        *   The database file (`todo.sqlite`) will be created programmatically by PHP if it doesn't exist.

4.  **Configuration (if applicable):**
    *   If you're using a database, you might need to create a `config.php` file (or similar) to store your database credentials. For example:
        ```php
        <?php
        // config.php
        define('DB_HOST', 'localhost');
        define('DB_USER', 'root'); // Default for XAMPP/WAMP
        define('DB_PASS', '');     // Default for XAMPP/WAMP
        define('DB_NAME', 'todo_app');

        // For SQLite
        define('SQLITE_DB_PATH', __DIR__ . '/todo.sqlite');
        ?>
        ```

5.  **Access the Application:**
    Open your web browser and navigate to `http://localhost/simple-todo-list-php/index.php` (or whatever your project's main file is named).

## Daily Practice Breakdown

This project is designed to be built incrementally. Here's a suggested daily breakdown:

### Day 1: Basic Form Handling & Display

*   **Goal:** Create an HTML form to input tasks and display them immediately on the page.
*   **Focus:** HTML forms, PHP `$_POST` (or `$_GET`), `if (isset())`, `echo`, basic arrays.
*   **Outcome:** Tasks are displayed but disappear on page refresh.

### Day 2: File-Based Persistence

*   **Goal:** Store tasks in a file (e.g., `tasks.json`) to make them persist across page loads.
*   **Focus:** PHP file I/O (`file_put_contents()`, `file_get_contents()`), `json_encode()`, `json_decode()`, array manipulation.
*   **Outcome:** Tasks remain after refreshing the browser.

### Day 3: Database Persistence (MySQL or SQLite)

*   **Goal:** Migrate data storage from a file to a relational database.
*   **Focus:** Database connection (PDO or MySQLi), SQL `CREATE TABLE`, `INSERT`, `SELECT` queries, prepared statements.
*   **Outcome:** Tasks are managed in a structured database.

### Day 4: Implement Mark Complete & Delete Functionality

*   **Goal:** Add interactive elements to change task status and remove tasks.
*   **Focus:** Passing data via URL parameters (`$_GET`), SQL `UPDATE` and `DELETE` queries, HTML links/buttons.
*   **Outcome:** Users can fully manage tasks (add, view, mark, delete).

### Day 5 (and Beyond): Enhancements & Refinements

*   **Goal:** Improve user experience, add validation, error handling, and styling.
*   **Focus:** CSS styling, input validation, PHP error handling (`try-catch`), filtering/sorting tasks, displaying feedback messages.
*   **Outcome:** A more robust, user-friendly, and polished To-Do List application.

## Usage

1.  Open the application in your web browser.
2.  Use the input field to type a new task and click "Add Task".
3.  Existing tasks will be listed below.
4.  Click the "Complete" checkbox (or similar UI) to mark a task as done.
5.  Click the "Delete" button to remove a task.

## Contributing

Feel free to fork this repository and add your own improvements! Suggestions for contributions include:

*   Adding more advanced CSS for a better UI.
*   Implementing user authentication.
*   Adding task categories or due dates.
*   Improving error handling and validation.
*   Converting to an MVC pattern (for more advanced practice).

## License

This project is open-source and available under the [MIT License](LICENSE).
