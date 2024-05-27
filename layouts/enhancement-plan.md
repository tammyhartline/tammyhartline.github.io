# Tammy Hartline's Computer Science E-Portfolio

## Table of Contents

- [Home](/index.md/)
- [Professional Self-Introduction and Assessment](/layouts/assessment-and-intro.md/)
- [Original Artifact Functionality](/layouts/original-artifact-functionality.md/)
- [Enhancement Plan](/layouts/enhancement-plan.md/)
- [Software Engineering/Design](/layouts/software-engineering-and-design.md/)
- [Algorithms and Data Structures](/layouts/algorithms-and-data-structures.md/)
- [Databases](/layouts/databases.md/)
- [Code Review](/layouts/code-review.md/)
- [Final Enhancements Review Summary](/layouts/final-enhancements-review-summary.md/)

### Follow Me on LinkedIn!
<a href="https://www.linkedin.com/in/tammy-hartline-91981266/"><img src="linkedin.jpg" width="100" height="100" alt="LinkedIn Logo"></a>

# Artifact Enhancement Plan

### Category One: Software Engineering/Design
•	Artifact: Grazioso Animal Shelter CRM Dashboard
•	Origin: SNHU Course CS-340 [Original Artifact Repository](https://github.com/tjhartline/SNHU-CS340) – Completed October 2023
•	Category: Software Engineering/Design

**Enhancement Plan:**
1.	Convert the existing Jupyter Notebook file (.ipynb) to an HTML formatted file (.html).
2.	Create a server directory and copy the converted HTML file into it.
3.	Initialize a Git repository and commit the changes, including the converted HTML file.
4.	Push the Git repository to a remote hosting platform (e.g., GitHub).
5.	Create and configure a server using a platform like Render.
6.	Deploy the HTML file and the CRM Dashboard to the configured server.

**Skills Demonstrated:**
•	Proficiency in multiple programming languages (Python, HTML)
•	File manipulation and conversion
•	Web development concepts (HTML, server deployment)
•	Version control using Git
•	Documentation and commenting skills
•	Problem-solving and critical thinking
•	Understanding of server configurations and deployment processes
•	User Interface (UI) design principles
•	Continuous learning and adaptability

```
# Pseudocode for file conversion and deployment – enhancement plan
# Convert .ipynb file to html
Jupyter nbconvert – to html csDashboard.ipynb
# Copy HTML file to server directory
cp csDashboard.html /enter path to server/directory
# Following creation of git repository, commit the changes to the repository.
Git add.
Git commit -m “Add the converted HTML formatted file here”
Git push origin master
# Deploy enhancement on render server
Git push render master
```
### Category Two: Algorithms and Data Structures
•	Artifact: Grazioso Animal Shelter CRM Dashboard
•	Origin: SNHU Course CS-340 [Original Artifact Repository](https://github.com/tjhartline/SNHU-CS340) – Completed October 2023
•	Category: Algorithms and Data Structures

**Enhancement Plan:**
1.	Implement a new data structure (e.g., linked list, tree, or graph) to store and manage the animal shelter data.
2.	Develop algorithms for efficient searching, sorting, and retrieval of data within the chosen data structure.
3.	Analyze the time and space complexity of the implemented algorithms.
4.	Optimize the algorithms for better performance, considering factors like memory usage and execution time.
5.	Integrate the optimized algorithms and data structures into the CRM Dashboard application.
   
**Skills Demonstrated:**
•	Understanding of data structures and their applications
•	Algorithm design and implementation
•	Time and space complexity analysis
•	Performance optimization techniques
•	Integration of data structures and algorithms into practical applications
•	Problem-solving and critical thinking

```
# Pseudocode for implementing data storage with SQLite instead of Mongo DB.
# Step 1. Create SQLite3 database file
	CREATE DATABASE IF NOT EXISTS animal_shelter_db;
# Step 2: Connect to the SQLite3 database
	Connection = sqlite3.connect(‘animal_shelter_db’)
# Step 3: Create a tale to store the CSV data
CREATE TABLE IF NOT EXISTS animals (
		id INTEGER PRIMARY KEY, name TEXT, species TEXT, breed TEXT,
		age INTEGER, type TEXT, status TEXT
);
# Step 4: Import the CSV data into the new SQLite3 table
Import csv
With open (‘animals.csv’, ‘r’) as file:
	Reader = csv.DictReader(file)
	For row in reader:
		Cursor.execute (‘INSERT INTO animals (name, species, breed, age, type, status) 			VALUES (‘..’, ‘..’, ‘..’, ‘..’)’,
Row[‘name’], row[‘species’], row[‘breed’], row[‘age’], row[‘type’], row[‘status’]))
# Step 5: Implement functions for CRUD operations
# C in CRUD – Create
Def create_record (name, species, breed, age, type, status):
	Cursor.execute (‘INSERT INTO animals (name, species, breed, age, type, status) 
	VALUES (‘..’, ‘..’, ‘..’, ‘..’, ‘..’)’,
			(name, species, breed, age, status))
	Connection.commit()
# R in CRUD – Read
Def read_records (species = None, status = None):
	Query = ‘SELECT * FROM animals’
	If species:
		Query += f” WHERE species = ‘{species}’”
	If status:
		If ‘WHERE’ in query:
			Query += f” AND status = ‘{status}’”
		Else:
			Query += f” WHERE status = ‘{status}’”
	Cursor.execute(query)
	Return cursor.fetchall()
# U in CRUD – Update
def update_record (animal_id, new_status):
    cursor.execute ("UPDATE animals SET status = ? WHERE id = ?", (new_status, animal_id))
    connection.commit()
# D in CRUD - Delete
def delete_record (animal_id):
    cursor.execute ("DELETE FROM animals WHERE id = ?", (animal_id,))
    connection.commit()
# Close connection after use
connection.close()
```
### Category Three: Databases
•	Artifact: Grazioso Animal Shelter CRM Dashboard
•	Origin: SNHU Course CS-340 [Original Artifact Repository](https://github.com/tjhartline/SNHU-CS340) – Completed October 2023
•	Category: Databases

**Enhancement Plan:**
1.	Review and analyze the existing database queries for potential optimization opportunities.
2.	Implement indexing on relevant columns to improve query performance.
3.	Restructure and refine queries based on best practices (e.g., query structure, data filtering, and joins).
4.	Measure and compare the execution times of optimized queries against the original queries.
5.	Document and explain the optimization techniques applied and their impact on query performance.
   
**Skills Demonstrated:**
•	Database query optimization techniques
•	Indexing strategies for performance improvements
•	Query restructuring and refinement
•	Performance analysis and benchmarking
•	Documentation and reporting skills
•	Attention to detail and critical thinking

```
# Pseudocode for Database Interaction – Enhancement Plan
# Existing query example
result = db.collection.find ({"status": "adoptable", "breed": "Labrador- Retriever"})
# Optimized query with indexing example
db.collection.create_index ([("status", pymongo.ASCENDING), ("breed", pymongo.ASCENDING)])
# Optimized query usage example
result = db.collection.find ({"status": "adoptable", "breed": "Labrador Retriever"}).hint([("status", 1), ("breed", 1)])
```
### Skills Shown with Proposed Enhancements
•	Skills/Outcomes Planned to be Illustrated in the Code Review: Technical proficiency, addressing previous grading experiences.
•	Skills/Outcomes Planned to be Illustrated in the Narratives: Insights into the decision-making process, lessons learned, and continuous improvement.
•	Skills/Outcomes Planned to be Illustrated in the Professional Self-Assessment: Holistic understanding of software engineering principles, effective problem-solving, and commitment to ongoing improvement.

This plan outlines the artifacts selected for my ePortfolio, the enhancements planned, and the skills/outcomes planned to be illustrated. It provides a detailed overview of the project's scope and objectives, demonstrating a well-rounded approach to showcasing proficiency in various aspects of computer science.

## To view and interact with the final application, please visit [https://tammyhartlinescapstone.onrender.com](https://tammyhartlinescapstone.onrender.com/).
## To view my project repository, please visit [https://github.com/tjhartline/capstone](https://github.com/tjhartline/capstone/).

