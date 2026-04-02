# Project Proposal

## Business Case

### Problem statement
The current sources for viewing food hygiene ratings in Bristol are often outdated, difficult to navigate, or require downloading large datasets. Local food‑business owners receive inspection results that are published days or even weeks after the actual visit, creating a delay between when businesses make necessary improvements and when the public is informed. Members of the public often struggle to find easy‑to‑understand food hygiene ratings for restaurants and takeaways in Bristol. While the data exists in the Open Bristol datasets, it is not presented in a simple or accessible format, making it difficult for users to quickly check whether a food business is safe and hygienic. Many people are unaware of where to look for this information, which increases the risk of choosing unsafe establishments. High volume of unrated new businesses – Over 42 000 newly registered food premises have not yet received their first inspection, meaning a large segment of the market operates without any publicly available hygiene information. A modern, user‑friendly web application is needed to simplify access to food hygiene ratings, providing a seamless and accessible platform where the public can easily explore, view, and understand this important information, ensuring that everyone can make safer, more informed choices when dining out.


### Business benefits
1) User-Friendly Interface (The app offers an easy-to-navigate interface that makes it simple for users to search, filter, and view hygiene ratings,ensuring accessibility for all.)
2) Improved Public Health (This app aims to helps consumers make safer decisions when choosing where to eat, reducing the risk of foodborne illnesses.)
3) Competitive Advantage for Businesses (Food businesses with high hygiene ratings can use the platform as a marketing tool to attract health-conscious customers.
4) Encourages Hygiene Improvements (With ratings visible to the public, businesses are motivated to improve their hygiene standards to stay competitive. This encourages them to keep up with or surpass others in order to attract more customers who care about hygiene.)
5) User Engagement and Feedback (Allows consumers to report hygiene issues or provide feedback on their dining experiences, creating an interactive environment for accountability.)
6) Real-Time Data Access (The application ensures that users have immediate access to the latest food hygiene ratings)
7) Data Transparency ( The app provides full transparency by showing food hygiene ratings exactly as they are, with no changes or adjustments. This allows the public to view the ratings clearly and holds businesses accountable for their hygiene practices)

### Systems Development Approach
The project will follow an iterative Systems Development Life Cycle (SDLC) model. Development will start with a basic version that connects to the Open Bristol API to display hygiene ratings, then new features such as filtering and accessibility improvements will be added in later iterations. This approach supports continuous testing and feedback, ensuring that quality and functionality improve with each stage.

### Options Considered
1) Government Websites (FSA or Local Council)  - These sites have the data, but they’re hard to navigate, not mobile-friendly, and users can’t easily filter results. They often have to search or download large files.
2) Open Data Platforms (e.g., Open Bristol) -  Just like the goverment webs, open data has the ratings, but it’s in a format that's hard for most people to understand. Users would need to download big files and figure out how to use the data, which isn’t quick or easy.
3) Third-Party Review Apps  - These platforms sometimes include hygiene ratings, but the main focus is on user reviews. This means hygiene ratings can be mixed in with other types of feedback, not up to date, making it unclear for users who are specifically looking for hygiene information. 
4) Creating a New App  - Building an app gives me full control to design a simple straighforward user-friendly platform, that shows up-to-date hygiene ratings and makes it easy for people to find the info they need.


### Expected Risks
1) Privacy and Security Concerns
 If the app allows users to report hygiene issues or leave feedback, it’s essential to ensure both user and business information is kept confidential. Without proper security measures, there’s a risk of breach of data, which could lead to violations of privacy laws.
Mitigation: Ths web app will use HTTPS to keep all communication between the app and users encrypted and secure. It will also limit data collection only gathering basic information that is essential for feedback and avoid storing names or contact details.
3) Maintenance and Scalability
The app may face challenges in scaling as the number of food premises grows. Continuous updates and maintenance may be needed to ensure the app remains reliable, especially as new hygiene inspection data is added regularly.
Mitigation: Schedule regular maintenance checks at intervals (e.g., every 2–4 weeks). This is to test functionality, verify data freshness, and check links or API responses. Developers can maintain a simple maintenance log documenting updates and fixes.
4) Incomplete Data / Data Accuracy
 There are thousands of new food businesses without hygiene ratings, so it may take time for the app to gather and display accurate information for all of them. This could result in incomplete data, which might frustrate users who expect to see ratings for every business. Also, since food hygiene ratings rely on inspections conducted by local authorities, there may be a delay in receiving and updating this data. Any inconsistency or delay of inspection results could affect the reliability of the app.
Mitigation: 1 - Use simple labels such as “Awaiting Inspection” or “No Rating Yet” instead of leaving blank spaces. This helps users understand that missing ratings are normal and not app errors.
2 - Refresh the data often using the Open Bristol API so users always see the latest version. The app will also stay in sync with Open Bristol data by connecting directly to the Open Data API. It will fetch information live or through a timed refresh, while regular maintenance checks will verify the API structure to ensure everything continues to work correctly. If the API fails or sends missing data, it will show an easy‑to‑read message such as “Data temporarily unavailable — please try again later.”



## Project Scope
## In scope
- Food Hygiene Ratings Display:
The web app will show up‑to‑date ratings for food businesses across Bristol using data from the Open Bristol API. Each listing will display the business name, address, rating score (0 – 5), and the inspection date.
- Search and Filter Features:
Users can search by business name, postcode, or area and use filters to view businesses by rating level or type (for example restaurant, café, takeaway, or school). The results will be shown in a clear, easy‑to‑read list.
- Food Hygiene Rating Guide:
A dedicated page will explain what each rating means, what “Awaiting Inspection” or “New Rating Pending” statuses show, and how the inspection process works. This helps users understand the meaning behind each score.
- Responsive and Accessible Design:
The layout will adjust automatically for desktop, tablet, and mobile screens, with strong colour contrast, readable text, alt‑text for icons, and keyboard navigation support.

## Out of scope 
- No Live Directions: The app will show you the address of the business, but it will not give you a "Sat-Nav" style map or live directions to get there.
- Push Notifications: The application will not send automated alerts to mobile devices regarding nearby rating changes; it functions as a pull-based search tool only.
- User-Generated Content: Users will not be able to post their own reviews, hygiene concerns/ complaints, photos of food, or personal star ratings. The app is strictly a data-mirror for official government ratings
- Creating or managing user accounts.
- Historical Data Tracking: The app will only show the most recent inspection result. It will not maintain a public archive of a business's previous scores from past years.

## Context Diagram 
<img width="1380" height="693" alt="contextdiagram" src="https://github.com/user-attachments/assets/1091a454-c36a-483a-848a-a0aece940848" />
