# Multi-User Task Manager with Categories and Due Dates

## Project Description

This project is an evolution of the "Simple To-Do List Application," transforming it into a more robust **Multi-User Task Manager**. The primary goal is to introduce and practice advanced PHP concepts such as user authentication, session management, relational database design, more complex data handling (categories, due dates, priorities), and basic AJAX for a smoother user experience.

Each registered user will have their own private task list, which they can organize, filter, and manage. This project provides a practical scenario to solidify your understanding of building secure and interactive web applications with PHP.

## Features

This application will progressively implement the following advanced features:

*   **User Authentication:**
    *   User Registration (with password hashing).
    *   User Login and Logout.
    *   Session management to keep users logged in.
*   **Personalized Task Lists:** Each user has their own tasks, separate from other users.
*   **Enhanced Task Attributes:** Tasks can have:
    *   Description (text)
    *   Category (e.g., Work, Personal, Shopping, dynamically managed)
    *   Due Date
    *   Priority (e.g., High, Medium, Low)
    *   Status (Complete/Incomplete)
*   **Advanced Task Management:**
    *   Create, Read, Update (edit description, category, due date, priority, status), Delete tasks.
    *   Mark tasks as complete/incomplete.
*   **Filtering and Sorting:**
    *   Filter tasks by status (all, active, completed).
    *   Filter tasks by category.
    *   Filter tasks by due date (e.g., today, upcoming).
    *   Sort tasks by due date, priority, or creation date.
*   **Basic AJAX for Status Updates:** Update task status (complete/incomplete) without a full page reload.
*   **Robust Input Validation and Error Handling:** Server-side validation for all user inputs.

## Technologies Used

*   **Backend:** PHP (with emphasis on PDO for database interaction)
*   **Frontend:** HTML, CSS, JavaScript (for AJAX)
*   **Database:** MySQL (recommended) or PostgreSQL
*   **Server (for local development):** Apache or Nginx (typically XAMPP/WAMP/MAMP)

## Setup and Installation (Local Development)

1.  **Prerequisites:**
    *   A local server environment (XAMPP, WAMP, MAMP, or similar) with PHP, Apache/Nginx, and MySQL/MariaDB installed and running.
    *   Ensure PHP's `pdo_mysql` (or `pdo_pgsql`) and `mbstring` extensions are enabled in your `php.ini`.

2.  **Clone the Repository (or create project folder):**
    ```bash
    git clone https://github.com/your-username/multi-user-task-manager-php.git
    cd multi-user-task-manager-php
    ```
    Place this folder inside your web server's document root (e.g., `htdocs` for XAMPP).

3.  **Database Setup:**
    *   Start your MySQL/MariaDB server.
    *   Open your database management tool (e.g., phpMyAdmin, Adminer, MySQL Workbench).
    *   Create a new database, for example, `task_manager_db`.
    *   Execute the following SQL queries to create the necessary tables:

    ```sql
    -- users table
    CREATE TABLE users (
        id INT AUTO_INCREMENT PRIMARY KEY,
        username VARCHAR(50) NOT NULL UNIQUE,
        password VARCHAR(255) NOT NULL, -- Store hashed passwords
        created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
    );

    -- categories table
    CREATE TABLE categories (
        id INT AUTO_INCREMENT PRIMARY KEY,
        user_id INT NOT NULL, -- Link categories to specific users
        name VARCHAR(100) NOT NULL,
        created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
        FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE,
        UNIQUE (user_id, name) -- A user cannot have two categories with the same name
    );

    -- tasks table
    CREATE TABLE tasks (
        id INT AUTO_INCREMENT PRIMARY KEY,
        user_id INT NOT NULL,
        category_id INT, -- Optional: link to a category
        description TEXT NOT NULL,
        due_date DATE,
        priority ENUM('Low', 'Medium', 'High') DEFAULT 'Medium',
        status TINYINT(1) DEFAULT 0, -- 0 for incomplete, 1 for complete
        created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
        updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
        FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE,
        FOREIGN KEY (category_id) REFERENCES categories(id) ON DELETE SET NULL
    );
    ```

4.  **Configuration:**
    Create a `config.php` file (or similar, e.g., `.env` file if you want to get fancy with `dotenv` package) in your project root to store database credentials and other configuration:

    ```php
    <?php
    // config.php
    define('DB_HOST', 'localhost');
    define('DB_NAME', 'task_manager_db');
    define('DB_USER', 'root'); // Default for XAMPP/WAMP
    define('DB_PASS', '');     // Default for XAMPP/WAMP

    // Optional: Define base URL for consistent links
    define('BASE_URL', 'http://localhost/multi-user-task-manager-php');

    // Start session
    session_start();
    ?>
    ```
    *Remember to never hardcode sensitive credentials directly into version control in a real-world project. Use environment variables or a `.env` file.*

5.  **Access the Application:**
    Open your web browser and navigate to `http://localhost/multi-user-task-manager-php/index.php` (or your chosen entry point).

## Advanced Practice Breakdown

This project is structured for incremental learning, building complexity day by day.

### Day 1: User Registration & Login

*   **Goal:** Implement a basic user authentication system.
*   **Focus:**
    *   Database connection (PDO).
    *   HTML forms for registration and login.
    *   Server-side input validation for username/password.
    *   Password hashing (`password_hash()`, `password_verify()`).
    *   PHP Sessions (`session_start()`, `$_SESSION`) for user state management.
    *   Basic routing (e.g., `index.php` for login, `register.php`, `dashboard.php`).
*   **Outcome:** Users can register, log in, and log out. Logged-in users are redirected to a dashboard, while unauthenticated users are redirected to the login page.

### Day 2: Personalized Task Management (CRUD)

*   **Goal:** Allow logged-in users to create, view, edit, and delete their *own* tasks.
*   **Focus:**
    *   Relating tasks to users (foreign key `user_id` in `tasks` table).
    *   CRUD operations for tasks using PDO prepared statements.
    *   Displaying tasks specific to the logged-in user.
    *   Form for adding new tasks, and forms/links for editing/deleting existing tasks.
*   **Outcome:** Each user has a functional task list that only they can access and modify.

### Day 3: Categories, Due Dates, and Priorities

*   **Goal:** Enhance task attributes by adding categories, due dates, and priorities.
*   **Focus:**
    *   Updating database schema (`categories` table, `category_id`, `due_date`, `priority` columns in `tasks`).
    *   Forms for adding/editing tasks to include new fields (dropdown for categories, date input for due date, radio/dropdown for priority).
    *   Managing categories (add/edit/delete categories for a user).
    *   Displaying these new attributes with tasks.
*   **Outcome:** Tasks are more organized with additional metadata.

### Day 4: Advanced Filtering and Sorting

*   **Goal:** Implement robust filtering and sorting options for the task list.
*   **Focus:**
    *   Building dynamic SQL queries based on user selections (e.g., `WHERE status = ?`, `WHERE category_id = ?`, `ORDER BY due_date`).
    *   HTML forms with dropdowns/checkboxes for filter and sort options.
    *   Handling `$_GET` parameters for filtering and sorting states.
*   **Outcome:** Users can easily find specific tasks by filtering and sorting their list.

### Day 5: Basic AJAX for Status Updates

*   **Goal:** Improve user experience by updating task status (complete/incomplete) without a full page reload.
*   **Focus:**
    *   JavaScript (Fetch API or XMLHttpRequest) for asynchronous requests.
    *   Creating a dedicated PHP endpoint (e.g., `api/update_task_status.php`) to handle AJAX requests.
    *   Updating the database and returning a JSON response.
    *   Manipulating the DOM with JavaScript to reflect the status change.
*   **Outcome:** Marking tasks as complete/incomplete is instant and seamless.

### Day 6 (and Beyond): Refinements and Further Enhancements

*   **Goal:** Polish the application, add more advanced features, and improve code structure.
*   **Focus:**
    *   **MVC Pattern:** Refactor code into Model-View-Controller structure for better organization and maintainability.
    *   **Better UI/UX:** More extensive CSS, responsive design.
    *   **Flash Messages:** Display temporary success/error messages after actions.
    *   **Password Reset:** Implement a "forgot password" feature.
    *   **Task Archiving:** Instead of deleting, allow archiving tasks.
    *   **User Profiles:** Allow users to update their profile information.
    *   **Client-side Validation:** Add JavaScript validation to forms for immediate feedback.
    *   **Error Logging:** Implement a basic error logging mechanism.
*   **Outcome:** A more professional, maintainable, and feature-rich web application.

## Usage

1.  Navigate to the application in your browser.
2.  **Register** a new user account.
3.  **Log in** with your credentials.
4.  You will be redirected to your personal dashboard where you can:
    *   Add new tasks with descriptions, categories, due dates, and priorities.
    *   View your task list.
    *   Edit existing task details.
    *   Mark tasks as complete or incomplete (via AJAX).
    *   Delete tasks.
    *   Filter and sort your tasks using the provided options.

## Contributing

This project is a learning exercise. Feel free to fork it, implement the suggested features, or add your own creative enhancements!

## License

This project is open-source and available under the [MIT License](LICENSE).
