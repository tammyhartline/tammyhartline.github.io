<!-- algorithms-and-data-structures.md -->
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
- [Site & Repository Links](/site-and-repo-links.md/)

###### Follow Me on LinkedIn!
<a href="https://www.linkedin.com/in/tammy-hartline-91981266/"><img src="linkedin.jpg" width="50" height="50" alt="LinkedIn Logo"></a>

# Algorithms and Data Structures

The enhancements made to the `animal_shelter.py` and `app.py` files collectively demonstrate a strong proficiency in algorithms and data structures.

Key enhancements in the algorithms and data structures area:

·        **Database Utilization**: The `animal_shelter.py` file utilizes the `SQLite3` database, which is an efficient and lightweight embedded database solution. This choice of database technology aligns well with the application's requirements, as it only needs to handle a single `CSV` file.

·        **Table Creation and Indexing**: The `_create_table()` and `_create_index()` methods in the `animal_shelter.py` file efficiently create a table and indexes in the `SQLite3` database, ensuring that the data is properly stored and organized, and improving the efficiency of data retrieval operations.

·        **Data Manipulation and Processing**: The use of `SQL` queries and the `pandas` library in both the `animal_shelter.py` and `app.py` files showcase an understanding of data manipulation and processing techniques. The `read()` method in the `animal_shelter.py` file abstracts the database queries, allowing for a more flexible and modular implementation of the application's data retrieval requirements.

·        **Input Validation and Sanitization**: The `read()` method in the `animal_shelter.py` file includes input validation and sanitization, demonstrating attention to security and defensive programming practices, effectively preventing `SQL` injection attacks.

·        **Dynamic Data Filtering and Visualization**: The `app.py` file demonstrates proficiency in algorithms and data structures through the efficient manipulation and processing of data. The `update_dashboard` callback function filters the data based on user interactions, groups the data, and creates interactive visualizations using Plotly Express, showcasing skills in data processing and visualization algorithms.

·        **Deployment to a Live Environment**: The successful deployment of the application to a `Render` server showcases the ability to integrate the application's algorithms and data structures into a production-ready environment, ensuring the effectiveness and reliability of the data processing and visualization components.

These enhancements in algorithms and data structures, across both the `animal_shelter.py` and `app.py` files, improve the efficiency, scalability, security, and overall user experience of the application.

Here is the enhanced `Python` code for the `app.py` file:
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
