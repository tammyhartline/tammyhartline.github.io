<!-- software-engineering-and-design.md -->

# Tammy Hartline's E-Portfolio

#### Table of Contents

- [Home](/index.md/)
- [Introduction/About Me](/intro.md/)
- [Original Artifacts Functionality](/original-artifact-functionality.md/)
- [Enhancement Plan](/enhancement-plan.md/)
- [Software Engineering/Design](/software-engineering-and-design.md/)
- [Algorithms and Data Structures](/algorithms-and-data-structures.md/)
- [Databases](/databases.md/)
- [Code Review](/code-review.md/)
- [Final Enhancements Review Summary](/final-enhancements-review-summary.md/)
- [Career Objective: Machine Learning Architect](/career-objective.md)
- [Site & Repository Links](/site-and-repo-links.md/)

###### Follow Me on LinkedIn!
<a href="https://www.linkedin.com/in/tammy-hartline-91981266/"><img src="linkedin.jpg" width="50" height="50" alt="LinkedIn Logo"></a>

# Software Engineering/Design

The enhancements made to the `animal_shelter.py` and `app.py` files collectively demonstrate a strong proficiency in software engineering and design principles.

Key enhancements in the software engineering and design area:

·        **Modular and Maintainable Design**: The `animal_shelter.py` file follows a modular and object-oriented design, with the well-defined `AnimalShelter` class encapsulating the database operations. This promotes code reusability and maintainability, as the database-related functionality is centralized and can be easily integrated into other parts of the application.

·        **Performance Optimization**: The addition of the `_create_index()` method in the `animal_shelter.py` file showcases an understanding of performance optimization techniques in database management, improving the efficiency of data retrieval operations.

·        **Readability and Documentation**: Both the `animal_shelter.py` and `app.py` files include detailed comments and documentation, following best practices for code readability and maintainability. The inclusion of changelogs and version information demonstrates a commitment to version control and tracking changes over time.

·        **Security Measures**: The `read()` method in the `animal_shelter.py` file includes input validation and sanitization, demonstrating attention to security and defensive programming practices, particularly in the context of preventing `SQL` injection attacks.

·        **Iterative Approach**: The enhancements made to the program, such as the migration from `MongoDB` to `SQLite3`, the optimization of `SQL` queries, and the addition and removal of various `CRUD` methods in the `animal_shelter.py` file, showcase an iterative approach to software development and a willingness to refactor and improve the codebase as needed.

·        **Structured and Interactive User Interface**: The `app.py` file demonstrates proficiency in software engineering and design by creating a user-friendly and interactive interface using the `Dash` framework. The organized layout, use of `HTML` components, and integration of data visualization techniques enhance the overall user experience.

·        **Deployment to a Live Environment**: The successful deployment of the application to a Render server showcases the ability to transition the project from a local development environment to a production-ready platform, improving the overall accessibility and usability of the application.

These software engineering and design enhancements, across both the `animal_shelter.py` and `app.py` files, improve the overall quality, maintainability, security, and user experience of the application.

---
How to Run the Code:

1. Ensure you have Python installed on your system (version 3.7 or higher recommended).

2. Install the required dependencies by running the following command in your terminal:
   pip install pandas sqlite3

3. Save the animal_shelter.py file in your project directory.

4. To use the AnimalShelter class in your main application:
- Import the class: `from animal_shelter import AnimalShelter`
- Create an instance: `shelter = AnimalShelter("animals.db")`
- Use the methods as needed, for example:
  ```python
  # Read all records
  all_animals = shelter.read()
  
  # Read with a specific query
  dogs = shelter.read(("animal_type = ?", ("Dog",)))
  ```

5. To run the Dash application (app.py file):
- Install Dash: `pip install dash`
- Run the application: `python app.py`
- Open a web browser and navigate to `http://localhost:8050` (or the port specified in the app file)

Note: Ensure that your CSV file (aac_shelter_outcomes.csv) is in the same directory as your Python scripts.

These instructions provide a step-by-step guide for setting up and running my enhanced animal shelter application, showcasing the improved accessibility and ease of use resulting from my software engineering and design enhancements.

---

Here is the enhanced `Python` code for the `animal_shelter.py` file:

---
``` python
# Import required libraries
import sqlite3
import pandas as pd
import os

class AnimalShelter(object):
    def __init__(self, db_path=':memory:'):
        self.db_path = db_path
        self._create_table()
        self._create_index()

    def _create_table(self):
        if self.db_path == ':memory:':
            db_file = "animals.db"
            if os.path.exists(db_file):
                return

        query_str = '''
            CREATE TABLE IF NOT EXISTS animals (
                animal_id INTEGER PRIMARY KEY,
                age_upon_outcome TEXT,
                animal_type TEXT,
                breed TEXT,
                color TEXT,
                date_of_birth TEXT,
                datetime TEXT,
                monthyear TEXT,
                name TEXT,
                outcome_subtype TEXT,
                outcome_type TEXT,
                sex_upon_outcome TEXT,
                location_lat REAL,
                location_long REAL,
                age_upon_outcome_in_weeks REAL
            )
        '''
        with sqlite3.connect(self.db_path) as conn:
            cursor = conn.cursor()
            cursor.execute(query_str)
            df = pd.read_csv("./aac_shelter_outcomes.csv")
            df.to_sql('animals', conn, if_exists='replace', index=False)

    def _create_index(self):
        with sqlite3.connect(self.db_path) as conn:
            cursor = conn.cursor()
            cursor.execute('CREATE INDEX IF NOT EXISTS idx_animal_type ON animals (animal_type)')
            cursor.execute('CREATE INDEX IF NOT EXISTS idx_outcome_type ON animals (outcome_type)')

    def read(self, query=None):
        query_str = 'SELECT * FROM animals'
        params = None

        if query is not None:
            # Input validation and sanitization
            if not isinstance(query, tuple) or len(query) != 2:
                raise ValueError("Invalid query format. Expected a tuple of length 2.")
            
            query_condition, query_params = query
            if not isinstance(query_condition, str) or not query_condition.strip():
                raise ValueError("Invalid query condition. Expected a non-empty string.")
            
            if not isinstance(query_params, tuple):
                raise ValueError("Invalid query parameters. Expected a tuple.")
            
            # Sanitize the query condition to prevent SQL injection
            query_condition = query_condition.replace(';', '').replace('--', '')
            
            query_str += f" WHERE {query_condition}"
            params = query_params

        try:
            with sqlite3.connect(self.db_path) as conn:
                cursor = conn.cursor()

                if params is not None:
                    df = pd.read_sql_query(query_str, conn, params=params)
                else:
                    df = pd.read_sql_query(query_str, conn)
                return df
        except sqlite3.Error as e:
            # Proper error handling
            print(f"An error occurred while executing the query: {e}")
            return None
```
