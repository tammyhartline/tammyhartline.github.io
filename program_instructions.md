# How to Run the Enhanced Animal Shelter Program

This guide provides step-by-step instructions to set up and run the enhanced Animal Shelter program, including the database operations, Dash application, and unit tests.

## Prerequisites

1. Ensure you have Python installed on your system (version 3.7 or higher recommended).

2. Install the required dependencies by running the following command in your terminal:
   pip install pandas sqlite3 dash plotly

## File Structure

Ensure you have downloaded the following files, creating a project directory from this repository:
- animal_shelter.py: Contains the AnimalShelter class for database operations
- app.py: Contains the Dash application for the interactive dashboard
- test_animal_shelter.py: Contains unit tests for the AnimalShelter class
- animals.db: SQLite database file (will be created if it doesn't exist)
- aac_shelter_outcomes.csv: CSV file containing the animal shelter data
- Grazioso_Salvare_Logo.png: Logo image file for the dashboard

## Running the Program

1. Database Setup and Operations:
   - The database will be automatically set up when you run either the Dash application or the unit tests.
   - To use the AnimalShelter class directly in your own Python script:
     from animal_shelter import AnimalShelter
     shelter = AnimalShelter("animals.db")
     all_animals = shelter.read()
     dogs = shelter.read(("animal_type = ?", ("Dog",)))

2. Running the Dash Application:
   - Open a terminal and navigate to your project directory.
   - Run the following command:
     python app.py
   - Open a web browser and navigate to http://localhost:8050 to view and interact with the dashboard.

3. Running the Unit Tests:
   - Open a terminal and navigate to your project directory.
   - Run the following command:
     python -m unittest test_animal_shelter.py
   - The test results will be displayed in the terminal, showing which tests passed or failed.

## Notes

- The Dash application will automatically use the animals.db database file. If it doesn't exist, it will be created and populated with data from the aac_shelter_outcomes.csv file.
- The unit tests use a separate test database that is created and deleted during the testing process.
- Ensure all files are in the same directory unless you modify the file paths in the code.

By following these instructions, you can run and test all components of the enhanced Animal Shelter program, demonstrating the improvements in database management, data visualization, and overall software design.
