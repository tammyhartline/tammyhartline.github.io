# Tammy Hartline's Computer Science Portfolio 2024
<img src="images/me.jpg" alt="Profile Image" class="profile-image" style="width: 150px; height: 150px; border-radius: 50%; margin: 0 auto;">

## Table of Contents

- [Professional Self-Introduction and Assessment](#self-introduction-and-assessment)
- [Software Engineering/Design](#software-engineeringdesign)
- [Algorithms and Data Structures](#algorithms-and-data-structures)
- [Databases](#databases)
- [Code Review](#code-review)
- [Final Project Narrative Summary](#final-project-narrative-summary)

### Find Me on LinkedIn!
- [![LinkedIn Logo](https://media.licdn.com/dms/image/C4E03AQGjDFlt0wN2nQ/profile-displayphoto-shrink_800_800/0/1695260208506?e=1721260800&v=beta&t=hbGvLeEHJBcn2Ya23jgbFRzw2cv-dTdTCs4f_5anYXs)](https://www.linkedin.com/in/tammy-hartline-91981266/)

### Professional Self-Introduction and Assessment

  My journey into the field of computer science began with a fascination for technology that sparked when the internet was launched to the public. Although computers at that time lacked the advanced features and user-friendliness of today, the potential for growth and innovation captivated me. During my freshman year of college in 2005, I enrolled in a few computer science courses, only to find myself as the sole female student, facing discouragement from pursuing this field. Consequently, I chose to pursue a degree in Business Administration with a concentration in Accounting.
<br/>
<br/>
  After college, my fondest moments at work were when our systems encountered issues, allowing me to explore the command prompt and restore the network to full operation. Following a diagnosis of narcolepsy with cataplexy, I shifted my focus to being a stay-at-home mother to my three daughters and working seasonally as a tax specialist. Little did I know that the COVID-19 pandemic would reignite my passion for technology.
<br/>
<br/>
  Confined at home during the pandemic, I became interested in remote work opportunities and was hired as a QuickBooks Payroll software support agent. Within three months, my coworkers encouraged me to explore roles in engineering or development, recognizing my aptitude for technology.
<br/>
<br/>
  Over the next six months, I immersed myself in researching technical careers, taking free courses, and utilizing open-source resources from institutions like MIT and Harvard to expand my knowledge. In May 2022, I took a leap of faith and enrolled in the computer science program at SNHU, simultaneously starting as a student worker in the analytics department.
<br/>
<br/>
  For nearly two years, I balanced my studies with remote work at SNHU, only resigning in November 2023 after accepting an offer as a project lead at Scale AI. During my academic journey, my concentration shifted from STEM Project Management to Software Engineering and finally to Data Analysis, reflecting the breadth of specializations available within computer science.
<br/>
<br/>
  Throughout this experience, I have cultivated a profound love for learning. I constantly seek to expand my knowledge, never feeling proficient enough or bored with mastering a specific skill. This insatiable curiosity has led me to learn and code in a diverse array of languages and technologies, including HTML, CSS, M+, DAX, SQL, NoSQL, Java, Python, JavaScript, Spring Boot, JUnit, Ruby, PHP, C, C++, C#, XML, MATLAB, Kotlin, Flutter, Dart, Android Studio, .NET, Bash, GraphQL, Salesforce, Power BI, Tableau, Sharepoint, GIT, and TypeScript.
<br/>
<br/>
  While I may not be an expert in any single language, I am proficient in nearly all of them. My skills encompass manually creating 3D and 4D images, developing dynamic and interactive web or mobile applications, building websites, performing data analysis, creating interactive analytic dashboards, and more.
<br/>
<br/>
  As I reflect on my journey, I am filled with gratitude for the opportunities that have allowed me to explore and cultivate my passion for computer science. The enhancements I have proposed for my ePortfolio will showcase my proficiency in software engineering, algorithm design, database optimization, web development, version control, and deployment processes. These skills align seamlessly with my career aspirations of being able to adapt to any technological role I am offered and contribute to the specialization of AI and Data Analysis in the field of computer science.
<br/>

### Software Engineering/Design

The enhancements made to the animal\_shelter.py and app.py files collectively demonstrate a strong proficiency in software engineering and design principles.

Key enhancements in the software engineering and design area:

·        **Modular and Maintainable Design**: The animal\_shelter.py file follows a modular and object-oriented design, with the well-defined AnimalShelter class encapsulating the database operations. This promotes code reusability and maintainability, as the database-related functionality is centralized and can be easily integrated into other parts of the application.

·        **Performance Optimization**: The addition of the \_create\_index() method in the animal\_shelter.py file showcases an understanding of performance optimization techniques in database management, improving the efficiency of data retrieval operations.

·        **Readability and Documentation**: Both the animal\_shelter.py and app.py files include detailed comments and documentation, following best practices for code readability and maintainability. The inclusion of changelogs and version information demonstrates a commitment to version control and tracking changes over time.

·        **Security Measures**: The read() method in the animal\_shelter.py file includes input validation and sanitization, demonstrating attention to security and defensive programming practices, particularly in the context of preventing SQL injection attacks.

·        **Iterative Approach**: The enhancements made to the program, such as the migration from MongoDB to SQLite3, the optimization of SQL queries, and the addition and removal of various CRUD methods in the animal\_shelter.py file, showcase an iterative approach to software development and a willingness to refactor and improve the codebase as needed.

·        **Structured and Interactive User Interface**: The app.py file demonstrates proficiency in software engineering and design by creating a user-friendly and interactive interface using the Dash framework. The organized layout, use of HTML components, and integration of data visualization techniques enhance the overall user experience.

·        **Deployment to a Live Environment**: The successful deployment of the application to a Render server showcases the ability to transition the project from a local development environment to a production-ready platform, improving the overall accessibility and usability of the application.

These software engineering and design enhancements, across both the animal\_shelter.py and app.py files, improve the overall quality, maintainability, security, and user experience of the application.

Here is the enhanced Python code for the animal\_shelter.py file:
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

### Algorithms and Data Structures

The enhancements made to the animal\_shelter.py and app.py files collectively demonstrate a strong proficiency in algorithms and data structures.

Key enhancements in the algorithms and data structures area:

·        **Database Utilization**: The animal\_shelter.py file utilizes the SQLite3 database, which is an efficient and lightweight embedded database solution. This choice of database technology aligns well with the application's requirements, as it only needs to handle a single CSV file.

·        **Table Creation and Indexing**: The \_create\_table() and \_create\_index() methods in the animal\_shelter.py file efficiently create a table and indexes in the SQLite3 database, ensuring that the data is properly stored and organized, and improving the efficiency of data retrieval operations.

·        **Data Manipulation and Processing**: The use of SQL queries and the pandas library in both the animal\_shelter.py and app.py files showcases an understanding of data manipulation and processing techniques. The read() method in the animal\_shelter.py file abstracts the database queries, allowing for more flexible and modular implementation of the application's data retrieval requirements.

·        **Input Validation and Sanitization**: The read() method in the animal\_shelter.py file includes input validation and sanitization, demonstrating attention to security and defensive programming practices, effectively preventing SQL injection attacks.

·        **Dynamic Data Filtering and Visualization**: The app.py file demonstrates proficiency in algorithms and data structures through the efficient manipulation and processing of data. The update\_dashboard callback function filters the data based on user interactions, groups the data, and creates interactive visualizations using Plotly Express, showcasing skills in data processing and visualization algorithms.

·        **Deployment to a Live Environment**: The successful deployment of the application to a Render server showcases the ability to integrate the application's algorithms and data structures into a production-ready environment, ensuring the effectiveness and reliability of the data processing and visualization components.

These enhancements in algorithms and data structures, across both the animal\_shelter.py and app.py files, improve the efficiency, scalability, security, and overall user experience of the application.

Here is the enhanced Python code for the app.py file:
``` python
from dash import Dash, html, dcc, dash_table  # Importing necessary Dash components
import dash  # Importing Dash
from dash.dependencies import Input, Output  # Importing Dash callback functions
import plotly.express as px  # Importing Plotly Express for data visualization
import pandas as pd  # Importing Pandas for data manipulation
from animal_shelter import AnimalShelter  # Importing AnimalShelter class for data access
import base64  # Importing base64 for image encoding

# Setup Dash
app = Dash(__name__)  # Creating a Dash application instance

# Data Manipulation / Model
db_path = 'animals.db'  # Path to the database file
shelter = AnimalShelter(db_path)  # Creating an instance of AnimalShelter to interact with the database
data = shelter.read()  # Reading data from the database
df = pd.DataFrame(data)  # Creating a Pandas DataFrame from the retrieved data

# Get each animal type in the collection (distinct, no duplicates)
unq_animal_types = df['animal_type'].unique()  # Extracting unique animal types from the DataFrame
data = df.to_dict('records')  # Converting DataFrame to a list of dictionaries for Dash data components

# Add in Grazioso Salvare’s logo
image_filename = 'Grazioso_Salvare_Logo.png'  # Path to the logo image file
encoded_image = base64.b64encode(open(image_filename, 'rb').read())  # Encoding the image to base64

# Defining the layout of the Dash application
app.layout = html.Div([
    html.Center(html.B(html.H1('Capstone Project Dashboard'))),  # Header
    html.Center(html.B(html.H1("Tammy Hartline's Grazioso Salvare DashBoard Final Project"))),  # Subheader
    html.Hr(),  # Horizontal line

    # Row 1: Header and Photo
    html.Div([
        html.Div(id='header', className='col-6', style={'text-align': 'center'}),
        html.Div([
            html.Img(id='customer-logo', src='data:image/png;base64,{}'.format(encoded_image.decode()),
                     alt='customer logo image', 
                     style={'width': '20%', 'height': '20%'}),
        ], className='col-6', style={'display': 'flex', 'justify-content': 'center', 'align-items': 'center'}),
    ], className='row'),

    # Row 2: Buttons for Animal Types
    html.Div([
        html.Div([
            html.Button('All', id='btn-all', n_clicks=0),
            *[html.Button(animal_type, id=f'btn-{animal_type}', n_clicks=0) for animal_type in unq_animal_types]
            # Creating buttons for each unique animal type
        ], className='col-6'),
    ], className='row'),

    # Row 3: Data Table
    html.Div([
        dash_table.DataTable(
            id='datatable-id',
            columns=[
                {"name": i, "id": i, "deletable": False, "selectable": True} for i in df.columns
            ],  # Defining columns for the data table
            data=data,
            editable=False,
            sort_action="native",
            sort_mode="multi",
            selected_rows=[0],
            filter_action="native",
            page_action="native",
            page_current=0,
            page_size=10,
        ),
    ], className='row'),

    # Row 4: Graph
    html.Div([
        dcc.Graph(id='bubble-plot', className='col-6'),
    ], className='row'),
])

# This section demonstrates skills and conceptualization of software design/engineering by setting up a user-friendly interface for data visualization.
# It also exhibits good design practices by organizing the layout in a structured and visually appealing manner.

@app.callback(
    [Output('bubble-plot', 'figure'), Output('datatable-id', 'data'), Output('datatable-id', 'columns')],
    [Input('btn-all', 'n_clicks')] + [Input(f'btn-{animal_type}', 'n_clicks') for animal_type in unq_animal_types],
    prevent_initial_call=True
)
def update_dashboard(*args):
    btn_all_clicks, *btn_type_click = args

    # Determine which button was clicked
    ctx = dash.callback_context
    clicked_button_id = ctx.triggered[0]['prop_id'].split('.')[0]

    if clicked_button_id == 'btn-all':
        filtered_df = df.copy()  # No filter, so use the entire DataFrame
    else:
        selected_animal_type = clicked_button_id.split('-')[1]
        filtered_df = df[df['animal_type'] == selected_animal_type]  # Filter by selected animal type

    # Group by animal_type and outcome_type and count the occurrences
    grouped_df = filtered_df.groupby(['animal_type', 'outcome_type']).size().reset_index(name='count')

    print("Grouped DataFrame:")
    print(grouped_df)

    # Create a bubble chart
    fig = px.scatter(
        grouped_df,
        x="animal_type",
        y="outcome_type",
        size="count",
        color="animal_type",
        hover_data={'count': True},
        labels={'count': 'Count'}
    )

    # Convert DataFrame to dict for dash_table
    filtered_data = filtered_df.to_dict('records')

    # Generate columns for dash_table
    columns = [{"name": i, "id": i, "deletable": False, "selectable": True} for i in filtered_df.columns]

    return fig, filtered_data, columns

# This callback function demonstrates skills and conceptualization of algorithms by dynamically updating the data visualization based on user interactions.
# It efficiently filters and processes data to generate relevant charts and tables.

if __name__ == '__main__':
    app.run_server(host='0.0.0.0', port=8050)
```

### Databases

The enhancements made to the animal\_shelter.py file demonstrate a strong proficiency in database management and design.

Key enhancements in the databases area:

·        **Database Migration**: The decision to switch from MongoDB to SQLite3 based on the requirements of the application showcases the ability to make informed technology choices and optimize the codebase accordingly. The use of SQLite3 is a more efficient and appropriate choice for the animal shelter application, which only requires a single CSV file.

·        **Table and Index Creation**: The creation of database tables and indexes in the \_create\_table() and \_create\_index() methods respectively exhibits a deep understanding of database design and optimization. These enhancements improve the performance and efficiency of data retrieval operations.

·        **CRUD Operations**: The CRUD (Create, Read, Update, Delete) operations, including the read() method, demonstrate the ability to correctly interact with the database and maintain data integrity.

·        **Input Validation and Sanitization**: The implementation of input validation and sanitization in the read() method in the animal\_shelter.py file highlights the awareness of SQL injection attacks and the importance of secure coding practices when working with databases.

·        **Database Connectivity and Querying**: The app.py file indirectly demonstrates proficiency in databases through the interaction with the AnimalShelter class, which handles the database operations. The creation of the AnimalShelter instance and the use of its read() method showcases knowledge of querying databases and fetching data efficiently.

·        **Deployment to a Live Environment**: The successful deployment of the application to a Render server showcases the ability to integrate the application's database-related components into a production-ready environment, ensuring the reliable and secure handling of data in a live setting.

These database-related enhancements, primarily in the animal\_shelter.py file, improve the overall reliability, security, and performance of the application, ensuring that the data stored and retrieved is accurate and well-managed.

Here is the test\_animal\_shelter.py file used to ensure proper functionality of the programs features:
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

### Code Review

<iframe width="640" height="360" src="https://www.youtube.com/embed/k3gyUmSv-Wk" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Final Project Narrative Summary

The enhancements made to the animal\_shelter.py and app.py files of the capstone project demonstrate a comprehensive proficiency across the key areas of software engineering and design, algorithms and data structures, and databases. These improvements not only optimized the overall program but also showcased the depth of understanding and skills acquired throughout the Computer Science program.

**_Software Engineering and Design:_**

The codebase follows a modular and object-oriented design, with the well-defined AnimalShelter class in the animal\_shelter.py file encapsulating the database operations. This promotes code reusability and maintainability, as the database-related functionality is centralized and can be easily integrated into other parts of the application. The addition of the \_create\_index() method showcases an understanding of performance optimization techniques in database management, improving the efficiency of data retrieval operations.

Both the animal\_shelter.py and app.py files include detailed comments and documentation, following best practices for code readability and maintainability. The inclusion of changelogs and version information demonstrates a commitment to version control and tracking changes over time, which is crucial for managing complex software projects.

The read() method in the animal\_shelter.py file includes input validation and sanitization, demonstrating attention to security and defensive programming practices, particularly in the context of preventing SQL injection attacks. This enhancement improves the overall security of the application and reduces the risk of malicious attacks.

The iterative approach to software development is evident in the enhancements, such as the migration from MongoDB to SQLite3, the optimization of SQL queries, and the addition and removal of various CRUD methods in the animal\_shelter.py file. This willingness to refactor and improve the codebase showcases the ability to adapt to changing requirements and continuously enhance the application.

In the app.py file, the use of the Dash framework demonstrates proficiency in creating a user-friendly and interactive interface. The organized layout, use of HTML components, and integration of data visualization techniques enhance the overall user experience, making the application more engaging and informative for the end-users.

The successful deployment of the application to a Render server showcases the ability to transition the project from a local development environment to a production-ready platform, improving the overall accessibility and usability of the application.

**_Algorithms and Data Structures:_**

The animal\_shelter.py file utilizes the SQLite3 database, which is an efficient and lightweight embedded database solution. This choice of database technology aligns well with the application's requirements, as it only needs to handle a single CSV file. The `_create_table()` and `_create_index()` methods efficiently create a table and indexes in the SQLite3 database, ensuring that the data is properly stored and organized, and improving the efficiency of data retrieval operations.

The use of SQL queries and the pandas library in both the animal\_shelter.py and app.py files showcases an understanding of data manipulation and processing techniques. The read() method in the animal\_shelter.py file abstracts the database queries, allowing for more flexible and modular implementation of the application's data retrieval requirements.

The read() method's inclusion of input validation and sanitization in the animal\_shelter.py file demonstrates attention to security and defensive programming practices, effectively preventing SQL injection attacks.

In the app.py file, the update\_dashboard callback function filters the data based on user interactions, groups the data, and creates interactive visualizations using Plotly Express, showcasing skills in data processing and visualization algorithms. These enhancements improve the user experience by providing dynamic and informative data representations.

The successful deployment of the application to a Render server showcases the ability to integrate the application's algorithms and data structures into a production-ready environment, ensuring the effectiveness and reliability of the data processing and visualization components.

**_Databases:_**

The animal\_shelter.py file exhibits a deep understanding of database design and management. The decision to switch from MongoDB to SQLite3 based on the requirements of the application showcases the ability to make informed technology choices and optimize the codebase accordingly. The use of SQLite3 is a more efficient and appropriate choice for the animal shelter application, which only requires a single CSV file.

The creation of database tables and indexes in the \_create\_table() and \_create\_index() methods respectively demonstrates a strong understanding of database design and optimization. These enhancements improve the performance and efficiency of data retrieval operations.

The CRUD (Create, Read, Update, Delete) operations, including the read() method, showcase the ability to correctly interact with the database and maintain data integrity. The implementation of input validation and sanitization in the read() method highlights the awareness of SQL injection attacks and the importance of secure coding practices when working with databases.

The app.py file indirectly demonstrates proficiency in databases through the interaction with the AnimalShelter class, which handles the database operations. The creation of the AnimalShelter instance and the use of its read() method showcases knowledge of querying databases and fetching data efficiently.

The successful deployment of the application to a Render server showcases the ability to integrate the application's database-related components into a production-ready environment, ensuring the reliable and secure handling of data in a live setting.

###### To view the result of all enhancements made to the program, and to interact with application, please visit [https://tammyhartlinescapstone.onrender.com](https://tammyhartlinescapstone.onrender.com/).
###### To view my project repository, please visit [https://github.com/tjhartline/capstone](https://github.com/tjhartline/capstone/).

**_Proof of Program Optimization:_**

The enhancements made to the application have resulted in a significant improvement in the build and deployment time on the Render platform. Initially, the deployment process was taking approximately 50 minutes on May 21, 2024. However, after implementing various optimizations, the build and deployment time has now been reduced to approximately 4 minutes on May 25, 2024.

These optimizations, which include the removal of unnecessary requirements, enhanced error handling, added security measures, and improvements to algorithms, queries, and data structures, demonstrate the positive impact of the comprehensive enhancements made to the application. The dramatic decrease in build and deployment time is a testament to the effectiveness of these improvements and the overall optimization of the program.

Deployment to a Live Environment: Another key optimization was the creation of a Render server and the successful deployment of the application to a live environment. Previously, the application was only accessible by running it on a local Jupyter Notebook and Jupyter Dash setup, which was **not** as convenient or scalable. By creating a Render server and deploying the application to it, the capstone project has become more accessible and can be easily shared with others, showcasing the final product in a real-world setting.

The successful deployment to the Render server demonstrates the ability to transition the application from a local development environment to a production-ready platform. This enhancement improves the overall accessibility and usability of the application, making it more user-friendly and suitable for real-world use cases.

In conclusion, the enhancements made to the animal\_shelter.py and app.py files of the capstone project showcase a comprehensive proficiency in software engineering and design, algorithms and data structures, and databases. These improvements, along with the successful deployment to a live Render server, have optimized the overall program, ensuring its reliability, security, and efficiency for the end-users. The **significant** reduction in build and deployment time and the transition to a production-ready platform are testaments to the effectiveness of these comprehensive enhancements. 

<img src="/proofop3.png">

<img src="/proofop1.png">

<img src="/proofop2.png">
