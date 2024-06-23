<!-- databases.md -->

<style>
    .content-wrapper {
        display: flex;
        justify-content: space-between;
        align-items: flex-start;
    }
    .main-content {
        flex: 1;
        padding-right: 20px;
    }
    .nav-menu {
        width: 200px;
        display: flex;
        flex-direction: column;
        gap: 10px;
        background-color: rgba(255, 255, 255, 0.8);
        padding: 15px;
        border-radius: 10px;
        box-shadow: 0 0 10px rgba(0,0,0,0.1);
        margin-left: 25px;
        position: sticky;
        top: 20px;
    }
    .nav-menu a {
        background-color: #8B0000;
        color: white;
        padding: 10px 10px;
        text-decoration: none;
        border-radius: 5px;
        text-align: center;
        font-size: 14px;
        white-space: nowrap;
    }
    .nav-menu a:hover {
        background-color: #660000;
    }
</style>

<div class="content-wrapper">
    <div class="main-content">
        <h1 style="text-align: center;">Tammy Hartline's E-Portfolio</h1>
    <div style="text-align: center;">
        <img src="images/me.jpg" alt="Profile Image" class="profile-image" style="width: 350px; height: 350px; border-radius: 50%; margin: 0 auto;">
        <h3 class="centered">Follow Me on LinkedIn!</h3>
<a href="https://www.linkedin.com/in/tammy-hartline-91981266/"><img class="centered" src="linkedin.jpg" width="100" height="100" alt="LinkedIn Logo"></a>
    </div>
    </div>

    <div class="nav-menu" style="text-align: right;">
        <a href="/">Home</a>
        <a href="/intro">About Me</a>
        <a href="/original-artifact-functionality">Original Artifacts</a>
        <a href="/enhancement-plan">Enhancement Plan</a>
        <a href="/software-engineering-and-design">Software Engineering</a>
        <a href="/algorithms-and-data-structures">Algorithms & Data Structures</a>
        <a href="/databases">Databases</a>
        <a href="/code-review">Code Review</a>
        <a href="/final-enhancements-review-summary">Enhancements Summary</a>
        <a href="/program_instructions">Run Instructions</a>
        <a href="/career-objective">Career Objective</a>
        <a href="/site-and-repo-links">Site & Repo Links</a>
    </div>
</div>
# Databases

The enhancements made to the `animal_shelter.py` file demonstrate a strong proficiency in database management and design.

Key enhancements in the databases area:

·        **Database Migration**: The decision to switch from `MongoDB` to `SQLite3` based on the requirements of the application showcases the ability to make informed technology choices and optimize the codebase accordingly. The use of `SQLite3` is a more efficient and appropriate choice for the animal shelter application, which only requires a single `CSV` file.

·        **Table and Index Creation**: The creation of database tables and indexes in the `_create_table()` and `_create_index()` methods respectively exhibits a deep understanding of database design and optimization. These enhancements improve the performance and efficiency of data retrieval operations.

·        **CRUD Operations**: The `CRUD` (Create, Read, Update, Delete) operations, including the `read()` method, demonstrate the ability to correctly interact with the database and maintain data integrity.

·        **Input Validation and Sanitization**: The implementation of input validation and sanitization in the `read()` method in the `animal_shelter.py` file highlights the awareness of `SQL` injection attacks and the importance of secure coding practices when working with databases.

·        **Database Connectivity and Querying**: The `app.py` file indirectly demonstrates proficiency in databases through the interaction with the `AnimalShelter` class, which handles the database operations. The creation of the `AnimalShelter` instance and the use of its `read()` method showcases knowledge of querying databases and fetching data efficiently.

·        **Deployment to a Live Environment**: The successful deployment of the application to a Render server showcases the ability to integrate the application's database-related components into a production-ready environment, ensuring the reliable and secure handling of data in a live setting.

These database-related enhancements, primarily in the `animal_shelter.py` file, improve the overall reliability, security, and performance of the application, ensuring that the data stored and retrieved is accurate and well-managed.

---

**How to Run the Code:**

1. Ensure you have Python installed on your system (version 3.7 or higher recommended).

2. Install the required dependencies by running the following command in your terminal/shell:

   `pip install pandas sqlite3`

3. Make sure you have the `animal_shelter.py` file in the same directory as the `test_animal_shelter.py` file.

4. Save the `test_animal_shelter.py` file with the provided code in your project directory.

5. To run the unit tests, execute the following command in your terminal:

   `python -m unittest test_animal_shelter.py`

6. The test results will be displayed in the terminal, showing which tests passed or failed.

Note: These tests are designed to run **independently** of your main database, using a separate test database file. The test database will be created and deleted automatically during the testing process.

Running these tests demonstrates the robustness of my database implementation, showcasing an ability to handle various scenarios including data creation, reading, updating, and deleting, as well as error handling and SQL injection prevention. This comprehensive test suite underlines my proficiency in database management and secure coding practices.

---

Here is the `test_animal_shelter.py` file used to ensure proper functionality of the program's features:

``` python
import unittest
import sqlite3
import os
import pandas as pd
from animal_shelter import AnimalShelter

class TestAnimalShelter(unittest.TestCase):
    def setUp(self):
        self.db_path = 'test_animals.db'
        self.shelter = AnimalShelter(self.db_path)

    def tearDown(self):
        os.remove(self.db_path)

    def test_create_table(self):
        with sqlite3.connect(self.db_path) as conn:
            cursor = conn.cursor()
            cursor.execute("SELECT name FROM sqlite_master WHERE type='table' AND name='animals'")
            table_exists = cursor.fetchone() is not None
            self.assertTrue(table_exists)

    def test_create_index(self):
        with sqlite3.connect(self.db_path) as conn:
            cursor = conn.cursor()
            cursor.execute("SELECT name FROM sqlite_master WHERE type='index' AND name='idx_animal_type'")
            index_exists = cursor.fetchone() is not None
            self.assertTrue(index_exists)

    def test_create_record(self):
        data = {
            'name': 'Max',
            'animal_type': 'Dog',
            'breed': 'Labrador',
            'age': 3,
            'outcome_type': 'Adoption',
            'outcome_subtype': 'Foster',
            'sex_upon_outcome': 'Neutered Male',
        }
        self.shelter.create(data)
        result = self.shelter.read(("name = ?", ('Max',)))
        self.assertEqual(len(result), 1)
        self.assertEqual(result.iloc[0]['name'], 'Max')

    def test_read_all_data(self):
        data = self.shelter.read()
        self.assertIsInstance(data, pd.DataFrame)
        self.assertGreater(len(data), 0)

    def test_read_with_valid_query(self):
        query = ("animal_type = ?", ("Dog",))
        data = self.shelter.read(query)
        self.assertIsInstance(data, pd.DataFrame)
        self.assertTrue(all(data['animal_type'] == 'Dog'))

    def test_read_with_invalid_query_format(self):
        query = "invalid query"
        with self.assertRaises(ValueError):
            self.shelter.read(query)

    def test_read_with_invalid_query_condition(self):
        query = ("", ("Dog",))
        with self.assertRaises(ValueError):
            self.shelter.read(query)

    def test_read_with_invalid_query_parameters(self):
        query = ("animal_type = ?", "Dog")
        with self.assertRaises(ValueError):
            self.shelter.read(query)

    def test_read_with_sql_injection_attempt(self):
        query = ("animal_type = ?; DROP TABLE animals; --", ("Dog",))
        data = self.shelter.read(query)
        self.assertIsInstance(data, pd.DataFrame)
        self.assertTrue(all(data['animal_type'] == 'Dog'))
        with sqlite3.connect(self.db_path) as conn:
            cursor = conn.cursor()
            cursor.execute("SELECT name FROM sqlite_master WHERE type='table' AND name='animals'")
            table_exists = cursor.fetchone() is not None
            self.assertTrue(table_exists)

    def test_update_record(self):
        data = {
            'name': 'Max',
            'animal_type': 'Dog',
            'breed': 'Labrador',
            'age': 3,
            'outcome_type': 'Adoption',
            'outcome_subtype': 'Foster',
            'sex_upon_outcome': 'Neutered Male',
        }
        self.shelter.create(data)
        updated_data = {'age': 4}
        self.shelter.update(("name = ?", ('Max',)), updated_data)
        result = self.shelter.read(("name = ?", ('Max',)))
        self.assertEqual(result.iloc[0]['age'], 4)

    def test_delete_record(self):
        data = {
            'name': 'Max',
            'animal_type': 'Dog',
            'breed': 'Labrador',
            'age': 3,
            'outcome_type': 'Adoption',
            'outcome_subtype': 'Foster',
            'sex_upon_outcome': 'Neutered Male',
        }
        self.shelter.create(data)
        self.shelter.delete(("name = ?", ('Max',)))
        result = self.shelter.read(("name = ?", ('Max',)))
        self.assertEqual(len(result), 0)

if __name__ == '__main__':
    unittest.main()
```
