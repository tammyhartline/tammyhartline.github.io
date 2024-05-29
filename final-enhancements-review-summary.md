<!-- final-enhancements-review-summary.md -->

# Tammy Hartline's Computer Science E-Portfolio

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

# Final Enhancements Review Summary

The enhancements made to the `animal_shelter.py` and `app.py` files of the capstone project demonstrate a comprehensive proficiency across the key areas of software engineering and design, algorithms and data structures, and databases. These improvements not only optimized the overall program but also showcased the depth of understanding and skills acquired throughout the Computer Science program.

**_Software Engineering and Design:_**

The codebase follows a modular and object-oriented design, with the well-defined `AnimalShelter` class in the `animal_shelter.py` file encapsulating the database operations. This promotes code reusability and maintainability, as the database-related functionality is centralized and can be easily integrated into other parts of the application. The addition of the `_create_index()` method showcases an understanding of performance optimization techniques in database management, improving the efficiency of data retrieval operations.

Both the `animal_shelter.py` and `app.py` files include detailed comments and documentation, following best practices for code readability and maintainability. The inclusion of changelogs and version information demonstrates a commitment to version control and tracking changes over time, which is crucial for managing complex software projects.

The `read()` method in the `animal_shelter.py` file includes input validation and sanitization, demonstrating attention to security and defensive programming practices, particularly in the context of preventing `SQL` injection attacks. This enhancement improves the overall security of the application and reduces the risk of malicious attacks.

The iterative approach to software development is evident in the enhancements, such as the migration from `MongoDB` to `SQLite3`, the optimization of `SQL` queries, and the addition and removal of various `CRUD` methods in the `animal_shelter.py` file. This willingness to refactor and improve the codebase showcases the ability to adapt to changing requirements and continuously enhance the application.

In the `app.py` file, the use of the Dash framework demonstrates proficiency in creating a user-friendly and interactive interface. The organized layout, use of `HTML` components, and integration of data visualization techniques enhance the overall user experience, making the application more engaging and informative for the end-users.

The successful deployment of the application to a `Render` server showcases the ability to transition the project from a local development environment to a production-ready platform, improving the overall accessibility and usability of the application.

**_Algorithms and Data Structures:_**

The `animal_shelter.py` file utilizes the `SQLite3` database, which is an efficient and lightweight embedded database solution. This choice of database technology aligns well with the application's requirements, as it only needs to handle a single `CSV` file. The `_create_table()` and `_create_index()` methods efficiently create a table and indexes in the `SQLite3` database, ensuring that the data is properly stored and organized, and improving the efficiency of data retrieval operations.

The use of `SQL` queries and the `pandas` library in both the `animal_shelter.py` and `app.py` files showcases an understanding of data manipulation and processing techniques. The `read()` method in the `animal_shelter.py` file abstracts the database queries, allowing for a more flexible and modular implementation of the application's data retrieval requirements.

The `read()` method's inclusion of input validation and sanitization in the `animal_shelter.py` file demonstrates attention to security and defensive programming practices, effectively preventing `SQL` injection attacks.

In the `app.py` file, the `update_dashboard` callback function filters the data based on user interactions, groups the data, and creates interactive visualizations using `Plotly Express`, showcasing skills in data processing and visualization algorithms. These enhancements improve the user experience by providing dynamic and informative data representations.

The successful deployment of the application to a Render server showcases the ability to integrate the application's algorithms and data structures into a production-ready environment, ensuring the effectiveness and reliability of the data processing and visualization components.

**_Databases:_**

The `animal_shelter.py` file exhibits a deep understanding of database design and management. The decision to switch from `MongoDB` to `SQLite3` based on the requirements of the application showcases the ability to make informed technology choices and optimize the codebase accordingly. The use of `SQLite3` is a more efficient and appropriate choice for the animal shelter application, which only requires a single `CSV` file.

The creation of database tables and indexes in the `_create_table()` and `_create_index()` methods respectively demonstrates a strong understanding of database design and optimization. These enhancements improve the performance and efficiency of data retrieval operations.

The `CRUD` (Create, Read, Update, Delete) operations, including the `read()` method, showcase the ability to correctly interact with the database and maintain data integrity. The implementation of input validation and sanitization in the `read()` method highlights the awareness of `SQL` injection attacks and the importance of secure coding practices when working with databases.

The `app.py` file indirectly demonstrates proficiency in databases through the interaction with the `AnimalShelter` class, which handles the database operations. The creation of the `AnimalShelter` instance and the use of its `read()` method showcases knowledge of querying databases and fetching data efficiently.

The successful deployment of the application to a Render server showcases the ability to integrate the application's database-related components into a production-ready environment, ensuring the reliable and secure handling of data in a live setting.

## To view and interact with the final application, please visit [https://tammyhartlinescapstone.onrender.com](https://tammyhartlinescapstone.onrender.com/).
## To view my project repository, please visit [https://github.com/tjhartline/capstone](https://github.com/tjhartline/capstone/).

**_Proof of Program Optimization:_**

The enhancements made to the application have resulted in a significant improvement in the build and deployment time on the `Render` platform. Initially, the deployment process was taking approximately 50 minutes on May 21, 2024. However, after implementing various optimizations, the build and deployment time has now been reduced to approximately 4 minutes on May 25, 2024.

These optimizations, which include the removal of unnecessary requirements, enhanced error handling, added security measures, and improvements to algorithms, queries, and data structures, demonstrate the positive impact of the comprehensive enhancements made to the application. The dramatic decrease in build and deployment time is a testament to the effectiveness of these improvements and the overall optimization of the program.

**Deployment to a Live Environment:** Another key optimization was the creation of a 'Render' server and the successful deployment of the application to a live environment. Previously, the application was only accessible by running it on a local `Jupyter Notebook` and `Jupyter Dash` setup, which was **not** as convenient or scalable. By creating a `Render` server and deploying the application to it, the capstone project has become more accessible and can be easily shared with others, showcasing the final product in a real-world setting.

The successful deployment to the `Render` server demonstrates the ability to transition the application from a local development environment to a production-ready platform. This enhancement improves the overall accessibility and usability of the application, making it more user-friendly and suitable for real-world use cases.

In conclusion, the enhancements made to the `animal_shelter.py` and `app.py` files of the capstone project showcase a comprehensive proficiency in software engineering and design, algorithms and data structures, and databases. These improvements, along with the successful deployment to a live `Render` server, have optimized the overall program, ensuring its reliability, security, and efficiency for the end-users. The **significant** reduction in build and deployment time and the transition to a production-ready platform are testaments to the effectiveness of these comprehensive enhancements. 

<img src="/proofop3.png">

<img src="/proofop1.png">

<img src="/proofop2.png">
