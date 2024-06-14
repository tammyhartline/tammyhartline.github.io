<!-- original-artifact-functionality.md -->

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

# Original Artifacts Functionality

## Course: SNHU CS-340 Client/Server Developement

*Note: I chose the same artifact for all three of proficiencies, Software Design & Engineering, Algorithms & Data Structures, and Databases. I will explain the functionality of that artifact below.*

---

Originally my project consisted of Python, Jupyter Notebook, MongoDB, and Mongosh which were leveraged to create a dash application that could be launched on the local virtual desktop environment. The previous codebase environment was fully set and consisted of all the dependencies, utilities, and step-by-step instructions for building the application.

---

### Algorithms & Data Structures & Databases
**Python-** Python was used for the CRUD methods that set the ability to interact with the database records from the database application and were a critical part of the Algorithms & Data-Structures, as I was able to write simple queries, create, read, update, and delete data records, therefore altering its structure.

```python
from pymongo import MongoClient

class AnimalShelter(object):
    '''CRUD operations for animals collection in MongoDB'''

    def __init__(self, user, password, host, port, db, col):
        '''
        Initialize Connection.
        Parameters should be read from the environment or configuration, not hardcoded.
        '''
        self.client = MongoClient(f'mongodb://{user}:{password}@{host}:{port}')
        self.database = self.client[db]
        self.collection = self.database[col]

    def createOne(self, data):
        '''
        Implement the C in CRUD.
        Insert document into the specified MongoDB collection.
        '''
        if data:
            result = self.collection.insert_one(data)
            return True if result.inserted_id else False
        else:
            print('\nNothing to save, data parameter is empty.')
            return False

    def createMany(self, datas):
        '''
        Implement C but for more than 1 insertion
        '''
        if datas:
            result = self.collection.insert_many(datas)
            return True if result.inserted_ids else False
        else:
            print('\nNothing to save, data parameter is empty.')
            return False

    def read(self, query):
        print(f'\nQuery received: {query}, type: {type(query)}')  # Debugging line
        '''
        Implement the R in CRUD.
        Query documents from the specified MongoDB collection.
        '''

        if query is not None:  # This will be True for an empty dictionary
            result = list(self.collection.find(query))

            # Iterate through the results and categorize breeds
            categorized_results = []
            for doc in result:
                # Add breed categorization logic here based on your criteria
                breed = doc.get('breed', 'N/A')
                if breed in ['Labrador Retriever Mix', 'Chesapeake Bay Retriever', 'Newfoundland']:
                    doc['rescue_type'] = 'water'
                elif breed in ['German Shepard', 'Alaskan Malamute', 'Old English Sheepdog', 'Siberian Husky', 'Rottweiler']:
                    doc['rescue_type'] = 'mountain'
                elif breed in ['Doberman Pinscher', 'German Shepard', 'Golden Retriever', 'Bloodhound', 'Rottweiler']:
                    doc['rescue_type'] = 'disaster'
                else:
                    doc['rescue_type'] = 'unknown'  # Handle other breeds

                categorized_results.append(doc)

            print('\n')  # Add a newline before printing the results
            for doc in categorized_results:
                print(doc)
            print('\n')  # Add a newline after printing the results

            return categorized_results if categorized_results else []
        else:
            print('\nQuery parameter is empty. Nothing read. Test Failed.')
            return []

    def update(self, query, update_data, multi=False):
        '''
        Implement the U in CRUD
        Update option
        '''
        if query:
            if multi:
                result = self.collection.update_many(query, {"$set": update_data})
                print('\n\n')
            else:
                result = self.collection.update_one(query, {"$set": update_data})
                print('\n\n')
            return result.modified_count
        else:
            print('\nQuery parameter is empty')
            return 0

    def delete(self, query, multi=False):
        '''
        Implement the D in CRUD.
        Options should be to delete one or delete many.
        '''
        if query:
            if multi:
                result = self.collection.delete_many(query)
                print('\n\n')
            else:
                result = self.collection.delete_one(query)
                print('\n\n')
            return result.deleted_count
        else:
            print('\nQuery parameter is empty')
            return 0
```
You can also view all code found here in the Github Repository: [Click here to view the code file pictured above.](https://github.com/tjhartline/SNHU-CS340/blob/main/module.py)


For the original program, I read a .csv file and then added it manually to the MongoDB. I was required to create the database and collection, then load the records by scripting in the terminal. Here is an image taken as proof of the database creation.
[![Github screenshot of loaded database with my visible user name](https://github.com/tjhartline/SNHU-CS340/blob/main/dbLoadSS.png?raw=true)](https://github.com/tjhartline/SNHU-CS340/tree/main)
*Screenshot of successfully loaded database, documents, and collections.*

---

### Proficiencies and Concepts Learned from Courses

The setup, design, and implementation of the dashboard, its features, security, and functionality demonstrate the concepts learned throughout many courses I have completed here at SNHU. While I did not struggle with the original version, that is likely due to the pre-setup environment, with all that was needed to code and run the program sufficiently. The enhancements proved to be much more challenging. The dashboard application meets the software design and engineering criteria as it was originally structured using Pseudocode, and flowcharts, and created in steps based on the desired functionality. It also required a test environment, which in this scenario was using Jupyter Notebook to run the application via a local host from a Firefox browser. It also required extensive use of scripting in the terminal, communicating with the terminal to engineer what we wanted the dashboard to do.

Calling queries, CRUD methods, and creating visuals based on our created database and table data, shows my proficiency in all needed areas of computer science for this project. To view the original functionality of this dashboard, please watch the [Code Review](/layouts/code-review.md) video, as I demonstrate the original functionality of this dash app. Below is the Jupyter Notebook code for creating the dashboard.

```python
# Tammy Hartline
# CS-340
# Final Project
# Interactive Dashboard coded with Python/Uses MongoDB integration
# October 2023

# Setup the Jupyter version of Dash
from jupyter_dash import JupyterDash

# Configure the necessary Python module imports for dashboard components
import dash
import dash_leaflet as dl
from dash import dcc
from dash import html
from dash.dependencies import Input, Output, State
import plotly.express as px  # For heatmap
from dash import dash_table
import base64
import pymongo
# Configure OS routines
import os

# Configure the plotting routines
import pandas as pd

# Change 'animal_shelter' and 'AnimalShelter' to match your CRUD Python module file name and class name
from module import AnimalShelter

# Data Manipulation / Model
# Update with your username and password and CRUD Python module name
username = "aacuser"
pwd = "myPassword"

# Set the default host to '127.0.0.1:27017'
default_host = 'mongodb://aacuser:myPassword@127.0.0.1:27017/aac'
host = os.getenv('MONGO_HOST', default_host)

# Create a MongoClient using the determined host
client = pymongo.MongoClient(host)
port = int(os.getenv('MONGO_PORT', 27017))  # Default to set port

db = 'AAC'
col = 'animals'
shelter = AnimalShelter(username, pwd, host, port, db, col)

# Class read method must support return of a list object and accept projection JSON input.
# Sending the read method an empty document requests all documents be returned.
df = pd.DataFrame.from_records(shelter.read({}))

# MongoDB v5+ is going to return the '_id' column, which will cause the data_table to crash. So, we remove it here.
# The df.drop command allows us to drop the column. If we do not set inplace=True, it will return a new dataframe
# that does not contain the dropped column(s).
df.drop(columns=['_id'], inplace=True)

# Dashboard Layout / View
app = JupyterDash(__name__)

# Add in Grazioso Salvare’s logo
image_filename = 'Grazioso_Salvare_Logo.png'
encoded_image = base64.b64encode(open(image_filename, 'rb').read())

# Place the HTML image tag in the line below into the app.layout code according to your design.
# Also, remember to include a unique identifier such as your name or date.
# html.Img(src='data:image/png;base64,{}'.format(encoded_image.decode()))

# Create global variables to populate filtered data

# Get each animal type in the collection (distinct, no duplicates)
unq_animal_types = df['animal_type'].unique()
data = df.to_dict('records')
app.layout = html.Div([
    html.Center(html.B(html.H1('SNHU CS-340 Dashboard'))),
    html.Center(html.B(html.H1("Tammy Hartline's Grazioso Salvare DashBoard Final Project"))),
    html.Hr(),

    # Row 1: Header and Photo
    html.Div([
        html.Div(id='header', className='col-6', style={'text-align': 'center'}),
        html.Div([
            html.Img(id='customer-logo', src='data:image/png;base64,{}'.format(encoded_image.decode()),
                     alt='customer logo image'),
        ], className='col-6', style={'display': 'flex', 'justify-content': 'center', 'align-items': 'center'}),
    ], className='row'),

    # Row 2: Buttons for Animal Types and Radio Buttons
    html.Div([
        html.Div([
            html.Button('All', id='btn-all', n_clicks=0),
            *[html.Button(animal_type, id=f'btn-{animal_type}', n_clicks=0) for animal_type in unq_animal_types]
        ], className='col-6'),
        html.Div([
            dcc.RadioItems(
                id='rescue-filter',
                options=[
                    {'label': 'Water Rescue', 'value': 'water'},
                    {'label': 'Mountain and Wilderness Rescue', 'value': 'mount'},
                    {'label': 'Disaster and Individual Tracking', 'value': 'disaster'},
                    {'label': 'Reset', 'value': 'reset'}
                ],
                value='reset',
            ),
        ], className='col-6', id='radio-buttons'),  # Give it an ID for callback
    ], className='row'),

    # Row 3: Data Table and Breed Count
    html.Div([
        dash_table.DataTable(
            id='datatable-id',
            columns=[
                {"name": i, "id": i, "deletable": False, "selectable": True} for i in df.columns
            ],
            data=data,
            # Set up the features for your interactive data table to make it user-friendly for your client.
            # If you completed the Module Six Assignment, you can copy in the code you created here.
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

    # Row 4: Graph and Map
    html.Div([
        dcc.Graph(id='bubble-plot', className='col-6'),  # Use dcc.Graph for bubble-plot
        html.Div([
            html.Div(id='graph-id', className='col-12'),  # Update the size to col-12
            html.Div(id='map-id', className='col-12'),  # Update the size to col-12
        ], className='col-6'),
    ], className='row'),

    # Row 5: Breed Count
    html.Div(id='breed-count'),

], style={'display': 'flex', 'flex-direction': 'column'})


# In[ ]:


@app.callback(
    Output('breed-count', 'children'),
    Input('rescue-filter', 'value')
)
def update_breed_count(selected_rescue_type):
    if selected_rescue_type == 'reset':
        return f'Total Breeds: {len(df)}'
    
    # Initialize a count variable
    count = 0
    
    # Iterate through the DataFrame and count breeds based on selected rescue type
    for index, row in df.iterrows():
        breed = row['breed']
        rescue_types = row['rescue_type']
        
        # Check if the selected rescue type matches any of the breed's rescue types
        if selected_rescue_type in rescue_types:
            count += 1
    
    return f'Breeds with {selected_rescue_type} Rescue: {count}'


# In[ ]:


@app.callback(
    [Output('datatable-id', 'data'), Output('datatable-id', 'columns')],
    [Input('btn-all', 'n_clicks')] + [Input(f'btn-{animal_type}', 'n_clicks') for animal_type in unq_animal_types] + [Input('rescue-filter', 'value')],
    prevent_initial_call=True
)
def update_dashboard(*args):
    # Extract the values from the *args list
    btn_all_clicks, *btn_type_click, rescue_filter = args

    context = dash.callback_context
    button_id = context.triggered[0]['prop_id'].split('.')[0]
    
    # Determine the selected animal type
    if button_id == 'btn-all':
        selected_animal_type = None
    else:
        selected_animal_type = button_id.split('-')[1]

    # Filter the data based on the selected animal type
    if selected_animal_type:
        filtered_data = [record for record in data if record['animal_type'] == selected_animal_type]
    else:
        filtered_data = data

    # Show or hide the rescue filter based on the selected animal type
    rescue_filter_style = {'display': 'block' if selected_animal_type == 'dog' else 'none'}

    # Filter the data based on the selected rescue type
    if rescue_filter != 'reset':
        filtered_data = [record for record in filtered_data if record['rescue_type'] == rescue_filter]

    # Define the columns for the datatable
    columns = [{"name": i, "id": i, "deletable": False, "selectable": True} for i in df.columns]

    return filtered_data, columns


# In[ ]:


@app.callback(
    Output('bubble-plot', 'figure'),
    Output('datatable-id', 'derived_viewport_data'),
    Output('graph-id', "children"),
    Input('rescue-filter', 'value'),
    [Input(f'btn-{animal_type}', 'n_clicks') for animal_type in unq_animal_types],
    prevent_initial_call=True
)
def update_plot(rescue_filter, *btn_clicks):
    dff = df.copy()

    # Calculate total counts of each rescue type for dogs
    if rescue_filter == 'reset':
        dff_dogs = dff[dff['animal_type'] == 'Dog']
        rescue_counts = dff_dogs['rescue_type'].value_counts()
    else:
        dff_dogs = dff[(dff['animal_type'] == 'Dog') & (dff['rescue_type'] == rescue_filter)]
        rescue_counts = dff_dogs['rescue_type'].value_counts()        

    # Calculate the total count of all rescue dogs
    total_rescue_dogs = len(dff_dogs)

    # Create a size column based on rescue counts for each data point
    dff_dogs['size'] = dff_dogs['rescue_type'].map(rescue_counts)

    # Create the bubble plot
    fig = px.scatter(
        dff_dogs,
        x='age_upon_outcome_in_weeks',
        y='outcome_type',
        size='size',  # Use the 'size' column for sizing
        color='breed',
        hover_name='animal_type'
    )

    return fig, dff_dogs.to_dict('records'), total_rescue_dogs


# In[ ]:


# Map
@app.callback(
    Output('map-id', "children"),
    Input('datatable-id', "derived_viewport_data"),
    Input('datatable-id', 'selected_rows'),
    prevent_initial_call = True
)
def update_map(viewData, selected_rows):
    dff = pd.DataFrame.from_dict(viewData)
    
    if selected_rows is not None and len(selected_rows) > 0:
        selected_row_index = selected_rows[0]

        if selected_row_index >= 0 and selected_row_index < len(dff):
            selected_row = dff.iloc[selected_row_index]

            latitude = selected_row['location_lat']
            longitude = selected_row['location_long']

            return [
                dl.Map(
                    style={'width': '1000px', 'height': '500px'},
                    center=[30.75, -97.48],
                    zoom=10,
                    children=[
                        dl.TileLayer(id="base-layer-id"),
                        dl.Marker(
                            position=(latitude, longitude),
                            children=[
                                dl.Tooltip('Austin Animal Shelter'),  # Replace with relevant tooltip data
                                dl.Popup([
                                    html.H1(selected_row["animal_type"]),
                                    html.P(selected_row["breed"])  # Replace with relevant popup content
                                ])
                            ]
                        )
                    ]
                )
            ]

    # Return an empty list when no row is selected or the selected index is out of bounds
    return []



app.run_server(debug=True)


# In[ ]:


#display all column names of DataFrame
print(dff.columns.tolist())
df.dtypes
print(df.head())


# In[ ]:
```
