# Requirements

## User Needs

### User stories
TODO: Write brief user stories to explain how various actors would interact with the system to accomplish a goal.
    Express these in the form from agile development:- As a (role) I want (goal) so that (benefit).

US1: As a member of the public, I want to search for food businesses by name, postcode, or address so that I can quickly find hygiene ratings for places I am interested in visiting.

US2: As a health-conscious consumer, I want to filter food businesses by their hygiene rating score (0 to 5) so that I can easily identify establishments with high hygiene standards.

US3: As a concerned diner, I want to view detailed information about a food business including its rating date and whether a new rating is pending so that I can judge how current and reliable the displayed rating is.

US4: As a parent, I want to filter businesses by their type (for example, restaurants, takeaways, schools, pubs) so that I can find appropriate and safe dining options for my family.

US5: As a public user, I want to access and view all hygiene ratings without needing to create an account or log in so that I can get important health information immediately with no barriers.

US6: As a first-time visitor to Bristol, I want to browse food businesses in a specific area by entering a postcode so that I can find hygienic places to eat near where I am staying.

US7: As a consumer unfamiliar with food hygiene ratings, I want to understand what each rating score from 0 to 5 means so that I can properly interpret the information and make informed choices about where to eat.

US8: As a user on my mobile phone, I want the web application to display properly on smaller screens so that I can check hygiene ratings while I am out and about.

US9: As a member of the public, I want to see whether a business is awaiting inspection or has a new rating pending so that I know if the displayed rating might not reflect the current state of the business.

US10: As a regular user, I want to see the official food hygiene rating graphic for each business so that I can recognise the same rating format that is displayed on the doors of food establishments.

### Actors
TODO: List and describe the actors/users for this product.

1. General Public User Any member of the public who visits the web application to look up food hygiene ratings for businesses in Bristol. This is the primary actor and represents the widest audience. It includes local residents, tourists, students, and anyone who wants to make a more informed choice about where to eat. The general public user does not need to create an account or log in. They have full access to all search, filter, and viewing features provided by the application.

2. Parent or Guardian A specific type of general public user who is particularly focused on finding safe and hygienic food options suitable for children and families. This actor places importance on being able to filter by business categories such as schools, cafes, and restaurants, and tends to look for establishments with the highest hygiene ratings. While they use the same features as the general public user, their goals and priorities are distinct enough to be considered separately.

3. System (Web Application) The Bristol Food Hygiene Ratings web application itself. This is not a human actor, but it plays an active role in the use cases by retrieving data from the Open Bristol dataset, processing search queries and filters, and presenting the results to the user. The system fetches data that includes business name, address, business type, rating, rating status, new rating pending, rating date, postcode, and rating graphic URL.

4. Open Bristol Data API (External System) The external data source that supplies all food hygiene rating information used by the application. This is an external actor that the system depends on. It provides a publicly accessible API through which the application retrieves up-to-date records about food businesses in Bristol. The data fields provided include: business name, address, business type, rating, rating status, new rating pending, rating date, postcode, and rating graphic URL.

### Use Cases

| USE CASE 1|   View Food Hygiene Rating Details | 
| -------------------------------------- | ------------------- |
| **Description** | The application is a web-based system that allows users to search and view food hygiene ratings for businesses in Bristol. Users can search by business name, postcode, or address and filter results by hygiene rating or business type. The system retrieves data from the Open Bristol Data API and displays information such as the business name, address, hygiene rating, rating date, and rating status. The application is designed to help members of the public quickly find and understand hygiene ratings so they can make informed decisions about where to eat. Some key benefits of this web app is providing a user-friendly interface and real-time access to data. Sources: US1, US2, US4, US5, US6, US8 |
| **Actors** | Primary: General Public User, Parent or Guardian. Secondary: System, Open Bristol Data API.|
| **Assumptions** |  Pre condition The Open Bristol Data API is available and returns data in the expected format. The user has access to a modern web browser on a desktop, tablet, or mobile device. The dataset contains records for food businesses in Bristol with the relevant data fields (business name, address, business type, rating, rating status, new rating pending, rating date, postcode, rating graphic URL). Post condition - The requested food hygiene rating data is successfully displayed to the user in the application.
| **Steps** | 1. The user opens the web application in their browser and arrives at the homepage. 2. The user enters a search term into the search bar. This could be a business name, a postcode, or part of an address. 3. The system validates the input to check it is not empty or invalid. 4. The system queries the Open Bristol dataset using the search term. 5. The system retrieves matching food businesses and displays them in a results list. Each result shows the business name, address, business type, hygiene rating (displayed as a number from 0 to 5, or as "Awaiting Inspection" if no rating exists), and the rating date. 6. The user optionally applies one or more filters to narrow the results. Available filters include hygiene rating score (0 to 5) and business type category (for example, restaurant, takeaway, cafe, pub or bar, school, hotel). 7. The system updates the displayed results to show only the businesses that match all active filters. 8. The user browses the filtered results and selects a business to view in more detail (this leads to UC2). |
| **Variations** |  1- If the user submits an empty or clearly invalid search term, the system displays a prompt asking them to enter a valid search. 2- If no businesses match the search term, the system displays a message saying no results were found and suggests the user try a different or broader search. 6a. The user may choose to use filters without first performing a text search, in which case the system displays all businesses in the dataset that match the selected filter criteria.|
| **Non-functional** | NFR1 – Usability: The system must allow users to search for and view food hygiene ratings within three clicks or taps from the homepage, ensuring the interface is simple and easy to use. NFR2 – Responsive Design: The web application must function correctly on desktop, tablet, and mobile devices, adapting the layout to different screen sizes. NFR4 – Performance: The system must return search results within two seconds for at least 95% of queries under normal network conditions. NFR5 – Capacity: The system must support at least 100 concurrent users without noticeable slowdown. NFR8 – Security: The system shall validate all user input, such as search terms and filter selections, to ensure that no harmful or malicious code can be entered into the application. This helps protect the system from security risks such  and ensures the application remains safe for all users. |
| **Issues** | The "rating status" field in the Open Bristol dataset can contain several different values ie “Awaiting Inspection, rated, exempt,” or may not yet have a hygiene rating. The application needs to ensure these cases are clearly explained to users so they are not confused by missing ratings. |



<img width="1408" height="768" alt="use case diagram " src="https://github.com/user-attachments/assets/9ac5f54b-0d1b-4fc2-9011-6cded2df6ee7" />

## Software Requirements Specification
### Functional requirements

**UC1: Search and Filter Food Hygiene Ratings**

- FR1: The system shall provide a search bar on the homepage that allows users to enter a business name, postcode, or address to search for food businesses. Source: UC1, US1, US6

- FR2: The system shall query the Open Bristol Data API using the user's search term and retrieve matching food business records. Source: UC1

- FR3: The system shall display search results in a list format, with each result showing the business name, address, business type, hygiene rating (0 to 5), and rating date. Source: UC1, US1

- FR4: The system shall display "Awaiting Inspection" in place of a numeric rating for any business that has not yet been inspected. Source: UC1, US9

- FR5: The system shall allow users to filter the displayed results by hygiene rating score, enabling the user to select one or more values from 0 to 5. Source: UC1, US2

- FR6: The system shall allow users to filter the displayed results by business type category (for example, restaurant, takeaway, cafe, pub or bar, school, hotel). Source: UC1, US4

- FR7: The system shall allow users to apply both a rating filter and a business type filter at the same time, with the results updating to reflect all active filters. Source: UC1, US2, US4

- FR8: The system shall display a clear message when no results match the user's search or filter criteria, suggesting the user broadens their search. Source: UC1

- FR9: The system shall validate the search input and display a prompt if the user submits an empty or invalid search term. Source: UC1

- FR10: The system shall allow all users to access the search, filter, and viewing features without requiring any form of login, registration, or account creation. Source: UC1, UC2, US5


**UC2: View Detailed Business Information and Understand Ratings**

- FR11: The system shall display a detailed information page when the user selects a business from the search results, showing the following fields from the dataset: business name, full address, postcode, business type, hygiene rating, rating date, rating status, and new rating pending indicator. Source: UC2, US3, US9

- FR12: The system shall load and display the official food hygiene rating graphic for each business using the rating graphic URL provided by the Open Bristol dataset. Source: UC2, US10

- FR13: The system shall display the numeric rating value as a fallback if the rating graphic URL is missing or the image fails to load. Source: UC2, US10

- FR14: The system shall display a clear notice when a business is marked as "Awaiting Inspection", explaining that no rating is available because the business has not yet been inspected. Source: UC2, US9

- FR15: The system shall display a notice when the new rating pending field indicates that a new rating is pending, informing the user that the currently displayed rating may change soon. Source: UC2, US9

- FR16: The system shall display the rating status for each business (for example, rated, exempt, or awaiting inspection) in plain language that is easy for any user to understand. Source: UC2, US3

- FR17: The system shall include an information section (either on the detail page or accessible from it) that explains what each hygiene rating score from 0 to 5 means in practice, so that users can interpret the ratings correctly. Source: UC2, US7


### Non-Functional Requirements 

**Usability**

- NFR1: The system shall provide a clear and intuitive layout that allows users to complete a search and view a business's rating within three clicks or taps from the homepage. Source: UC1, UC2

- NFR2: The system shall be fully responsive and work correctly on mobile phones, tablets, and desktop computers, using responsive design techniques (such as CSS media queries or a flexible grid layout) to adapt to different screen sizes. Source: UC1, UC2, US8

- NFR3: The system shall meet WCAG 2.1 Level AA accessibility standards. This includes ensuring all text has sufficient colour contrast, all images have descriptive alternative text, and all interactive elements can be operated using a keyboard. Source: UC2, US5

**Performance**

- NFR4: The system shall return search results within two seconds for at least 95 percent of queries under normal network conditions. Source: UC1

- NFR5: The system shall be capable of supporting at least 100 concurrent users without any noticeable slowdown or loss of functionality. Source: UC1

**Reliability**

- NFR6: The system shall remain available and functional at least 99 percent of the time during normal operating hours (06:00 to 23:00 GMT). Source: UC1, UC2

- NFR7: The system shall handle failures from the Open Bristol Data API gracefully. If data cannot be retrieved, the system shall display a user-friendly error message rather than showing a blank page, broken layout, or technical error details. Source: UC1, UC2

**Security**

- NFR8: The system shall validate and sanitise all user inputs (including search terms and filter selections) to prevent cross-site scripting (XSS) attacks and other injection vulnerabilities. Source: UC1

- NFR9: The system shall serve all pages over HTTPS to make sure that data transmitted between the user's browser and the server is encrypted. Source: UC1, UC2

**Maintainability**

- NFR10: The system shall be built using modular, well-organised, and clearly commented HTML, CSS, and JavaScript code, so that future developers can understand and extend the application without difficulty. Source: UC1,
  UC2
