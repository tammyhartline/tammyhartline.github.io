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
# Enhanced Program - Run Instructions 📄
---
## How to Access the Live Enhanced Animal Shelter Dashboard Application 🔗

Visit [https://tammyhartlinescapstone.onrender.com](https://tammyhartlinescapstone.onrender.com)

---
## How to Run the Enhanced Animal Shelter Dashboard on Your Local Machine 💻

This guide provides step-by-step instructions to set up and run the enhanced Animal Shelter program directly from the GitHub repository.

### Prerequisites

1. Ensure you have `Python` installed on your system (`version 3.7` or higher recommended).

2. Install `Git` on your system if it's not already installed.

### Setup and Installation

1. Clone the repository:
   Open a terminal and run the following command:
   `git clone https://github.com/tjhartline/capstone.git`

2. Navigate to the project directory:
   `cd capstone`

3. Install the required dependencies:
   `pip install -r requirements.txt`

### Running the Program

1. Running the `Dash` Application:
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
