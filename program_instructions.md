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
- [Enhanced Program - Run Instructions](/program_instructions.md/)
- [Career Objective: Machine Learning Architect](/career-objective.md)
- [Site & Repository Links](/site-and-repo-links.md/)

###### Follow Me on LinkedIn!
<a href="https://www.linkedin.com/in/tammy-hartline-91981266/"><img src="linkedin.jpg" width="50" height="50" alt="LinkedIn Logo"></a>

# Enhanced Program - Run Instructions 📄
---
## How to Access the Live Enhanced Animal Shelter Dashboard Application 🔗

Visit [https://tammyhartlinescapstone.onrender.com](https://tammyhartlinescapstone.onrender.com)

---
## How to Run the Enhanced Animal Shelter Dashboard on Your Local Machine 💻

This guide provides step-by-step instructions to set up and run the enhanced Animal Shelter program directly from the GitHub repository.

### Prerequisites

1. Ensure you have Python installed on your system (version 3.7 or higher recommended).

2. Install Git on your system if it's not already installed.

### Setup and Installation

1. Clone the repository:
   Open a terminal and run the following command:
   `git clone https://github.com/tjhartline/capstone.git`

2. Navigate to the project directory:
   `cd capstone`

3. Install the required dependencies:
   `pip install -r requirements.txt`

### Running the Program

1. Running the Dash Application:
   - In the terminal, ensure you're in the project directory.
   - Run the following command:

     `python app.py`
     
   - Open a web browser and navigate to `http://localhost:8050` to view and interact with the dashboard.

2. Running the Unit Tests:
   - In the terminal, ensure you're in the project directory.
   - Run the following command:

     `python -m unittest test_animal_shelter.py`
     
   - The test results will be displayed in the terminal, showing which tests passed or failed.

### Notes

- The Dash application will automatically use the `animals.db` database file. If it doesn't exist, it will be created and populated with data from the `aac_shelter_outcomes.csv` file included in the repository.
- The unit tests use a separate test database that is created and deleted during the testing process.
- All necessary files, including the Grazioso Salvare logo, are included in the cloned repository.

By following these instructions, you can run and test all components of the enhanced Animal Shelter program, demonstrating the improvements in database management, data visualization, and overall software design.

For any issues or questions, please refer to the repository's README or open an issue on the GitHub page.
