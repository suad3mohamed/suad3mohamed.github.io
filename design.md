# 03 Design
## Bristol Food Hygiene Ratings Web Application

---

## 3.1 Introduction to the Design Phase

The design phase of the Bristol Food Hygiene Ratings web application bridges the gap between the requirements specification produced in Phase 2 and the implementation work that follows in Phase 4. The purpose of this phase is to translate the functional and non-functional requirements into a clear, structured, and professionally presented visual blueprint for the application before any code is written.

This document presents three interconnected design artefacts. First, a wireflow diagram maps out every screen in the application alongside all navigation paths, user interactions, and edge-case states such as empty results and API errors. Second, high-fidelity desktop mockups present the final visual design including colour scheme, typography, grid layout, spacing, and all interface components. Third, the overall user interface architecture is described in terms of grid layout, component structure, and design rationale, with each decision traced back to the relevant requirement or use case.

The design process followed an iterative and user-centred approach. Low-fidelity wireframes were produced first to plan the structure and navigation of each page without the distraction of visual styling. These were then connected into a full wireflow diagram to validate every user journey before any visual or colour decisions were made. Once the structure and navigation were confirmed as complete and correct, high-fidelity mockups were produced by applying the full design system. This deliberate progression from structure to style reduced the risk of costly changes at the implementation stage and ensured that every visual decision could be justified against a validated structural foundation.

All design artefacts were produced in Figma. The complete wireflow diagram and all high-fidelity mockups are available at full resolution at the following links:

- **Wireflow Diagram:** https://www.figma.com/design/cDzHoE1BvKaEpMsooiBrOb/High-Fidelity-MockUp?node-id=2071-507&t=36W43D7d1QbB3XwJ-1
- **Wireframe (All Pages):** https://www.figma.com/design/0V6qioQcKcWNtVy9fG22DS/WireFrame-finished---Desktop?node-id=0-1&t=rGD7ReVYtfm3j7XF-1
- **High-Fidelity Mockup (All Pages):** https://www.figma.com/design/cDzHoE1BvKaEpMsooiBrOb/High-Fidelity-MockUp?t=rGD7ReVYtfm3j7XF-1

---

## 3.2 Wireflow Diagram

### 3.2.1 What is a Wireflow and Why Was One Produced?

A wireflow is a design technique that combines wireframes with a user flow diagram. A wireframe is a low-fidelity structural representation of a single screen, showing the position of interface elements without any visual styling. A user flow diagram shows how a user navigates between screens through their actions and decisions. By combining both into a single wireflow, it is possible to understand the entire application as a connected system rather than as a collection of isolated pages.

Unlike a standalone wireframe set, a wireflow makes it possible to see every navigation path, every error and edge-case state, and every same-page interaction in one unified view. This is particularly valuable for validating that the design fully addresses all of the use cases and functional requirements identified in the requirements specification before implementation begins. Identifying gaps in the navigation model at the wireflow stage is significantly less costly than discovering them during development.

The wireflow for this application was produced in Figma and covers all four pages: Homepage, Search Results Page, Business Details Page, and Rating Guide Page. Every connection between pages is annotated to explain what user action triggers it, ensuring that the diagram is self-explanatory and can be read without prior knowledge of the application.

---

### 3.2.2 Wireflow Legend and Visual Notation

The wireflow uses a consistent visual notation system to distinguish between different types of interactions and navigation paths. The table below defines every symbol used in the diagram.

| Arrow / Annotation Type | Colour | Meaning |
|---|---|---|
| Primary navigation arrow | Green solid | The user clicks an interactive element and moves to a new page |
| Navigation bar link arrow | Blue dashed | A navigation bar link available from every page at any time |
| Back / return arrow | Grey dashed | The user returns to the previous page without losing their current state |
| Validation or error arrow | Red solid | The user stays on the same page and a validation message or error notice is displayed |
| Same-page interaction arrow | Black solid | The user stays on the current page but the content updates without a full navigation |
| Annotation box | Yellow filled rectangle | Informational note highlighting conditional behaviour or design decisions not visible in the screen itself |

---

### 3.2.3 Wireflow Diagram Screenshots

The screenshots below present the complete wireflow diagram as captured from Figma. Together they cover every screen, every navigation connection, and every annotation in the diagram.

#### View 1 — Homepage and Search Results Page

This view shows the Homepage and Search Results Page positioned side by side, with all navigation connections between them annotated.

The green arrows trace the primary user journey: the user arrives on the Homepage, enters a search query, and arrives at the Search Results Page. A red arrow illustrates the validation path where the user submits an empty search field and remains on the Homepage with a validation message displayed beneath the input. Green arrows also show that clicking any category tile on the Homepage navigates to the Search Results Page with that business type filter pre-applied, providing an alternative entry point that does not require the user to type a query.

<img width="986" height="733" alt="Screenshot 2026-03-16 at 14 46 27" src="https://github.com/user-attachments/assets/f155d48f-cef6-4b41-a7c4-d94acb742e65" />


#### View 2 — Search Results Page and Business Details Page

This view focuses on the connection between the Search Results Page and the Business Details Page. A green arrow represents the primary action of clicking a result card to open the Business Details Page. A grey dashed arrow represents the Back to Results navigation, which returns the user to the results list without resetting their search query or applied filters, preserving the user's state across the navigation.

<img width="986" height="733" alt="Screenshot 2026-03-16 at 14 47 02" src="https://github.com/user-attachments/assets/72aa7cb3-313b-4b1a-8f5a-c6eab00c98ae" />


#### View 3 — Rating Guide Page and Wireflow Legend

This view shows the Rating Guide Page and the full wireflow legend. The Rating Guide is reachable from three entry points: the navigation bar on every page, the View Full Guide button on the Homepage, and the Full Guide link on the Business Details Page. The legend panel documents all arrow types and the annotation box convention used throughout the diagram.

<img width="986" height="733" alt="Screenshot 2026-03-16 at 14 48 07" src="https://github.com/user-attachments/assets/faf0f8d9-b3c1-490d-8d98-9951a249a562" />


#### View 4 — Rating Guide Detail and Full Legend (Close-up)

This view presents the Rating Guide Page content and the complete wireflow legend at greater detail. It also shows the footer structure including the certification logos, Quick Links column, and Legal column that are consistent across all pages.

<img width="665" height="733" alt="Screenshot 2026-03-16 at 14 49 01" src="https://github.com/user-attachments/assets/9095ca72-13eb-4921-82fa-77a87b0a6414" />

<img width="987" height="738" alt="Screenshot 2026-03-16 at 14 50 02" src="https://github.com/user-attachments/assets/8774058e-973e-4983-bd54-d41fcd441ee8" />

---

### 3.2.4 Complete Navigation Map

The table below documents every navigation path in the application as represented in the wireflow diagram.

| From Page | User Action | To Page / State |
|---|---|---|
| Homepage | Submits a valid search query | Search Results Page |
| Homepage | Submits an empty search field | Stays on Homepage, validation message shown |
| Homepage | Clicks a category tile | Search Results Page with that business type pre-filtered |
| Homepage | Clicks View Full Guide | Rating Guide Page |
| Homepage | Clicks Search in the navigation bar | Search Results Page |
| Homepage | Clicks Detail in the navigation bar | Business Details Page |
| Homepage | Clicks Rating Guide in the navigation bar | Rating Guide Page |
| Search Results | Clicks a result card | Business Details Page |
| Search Results | Applies or removes a filter checkbox | Results update in place, same page |
| Search Results | Submits a new search query | Results refresh on the same page |
| Search Results | Clicks Retry on the error panel | Data reload attempted, same page |
| Search Results | Clicks View Full Guide | Rating Guide Page |
| Search Results | Clicks Logo or Home in the navigation bar | Homepage |
| Business Details | Clicks Back to Results | Search Results Page with state preserved |
| Business Details | Clicks Full Guide link in the rating panel | Rating Guide Page |
| Rating Guide | Clicks any navigation bar link | Corresponding page |
| Any page | Clicks the application Logo | Homepage |

---

### 3.2.5 Wireflow to Use Case Mapping

The table below maps each section of the wireflow to the use cases and functional requirements it validates, demonstrating that the design provides complete coverage of the requirements specification.

| Use Case | Screens Involved | User Journey | Requirements Covered |
|---|---|---|---|
| UC1 — Search for a business | Homepage, Search Results | User enters query and arrives at results page | FR1, FR2, FR3, FR4 |
| UC1 — Filter results | Search Results | User applies checkboxes, results update in place | FR5, FR6, FR7 |
| UC1 — No results state | Search Results | No results message and guidance displayed | FR8 |
| UC1 — Error state | Search Results | Retry button reloads data without page refresh | NFR7 |
| UC2 — View business details | Search Results, Business Details | User clicks result card, full record displayed | FR11, FR12 |
| UC2 — Conditional status notices | Business Details | Relevant notice panel shown based on business data | FR14, FR15, FR16 |
| UC2 — Understand the rating | Business Details, Rating Guide | Full Guide link navigates to Rating Guide | FR17 |
| UC3 — Understand the rating system | Rating Guide | Full rating scale and special statuses explained | FR18 |

---

## 3.3 User Interface Architecture

### 3.3.1 Page Structure and Navigation Model

The application consists of four pages connected by a shared navigation bar and a consistent footer. Every page is accessible from every other page at any time via the navigation bar, which means no page is ever more than one click away from any other page in the application.

| Page | Route | Primary Purpose |
|---|---|---|
| Homepage | `/` | Entry point with hero search bar and category tiles |
| Search Results | `/search` | Displays businesses matching the user's query with filter controls |
| Business Details | `/detail/:id` | Presents the full inspection record for a selected business |
| Rating Guide | `/guide` | Explains the food hygiene rating system and all special statuses |

---

### 3.3.2 Grid Layout and Responsive Design

The application is built on a twelve-column CSS grid layout. This provides the flexibility to implement multi-column arrangements on desktop whilst gracefully collapsing to narrower layouts on smaller screens.

| Breakpoint | Grid Configuration | Content Behaviour |
|---|---|---|
| Desktop (1024px and above) | 12-column grid, maximum width 1200px | Multi-column layouts as shown in the mockups |
| Tablet (768px to 1023px) | 6-column grid | Filter panel and results stack vertically; category tiles wrap to two rows |
| Mobile (below 768px) | Single column | All content stacks vertically; filter panel accessible via a modal or drawer |

The homepage uses the twelve-column grid to place the category tiles in a single six-item row on desktop. The search results page uses a three-column and nine-column split for the filter panel and results list respectively. The business details page uses a seven-column and five-column split for the information and rating panels.

---

### 3.3.3 Shared Components

The following components appear on multiple pages and are defined once in the design system to ensure consistency across the application.

#### Navigation Bar

Present on all four pages. Contains the application logo on the left, four navigation links (Home, Search, Details, Rating Guide) in the centre-right area, and a highlighted active state on the link corresponding to the current page.

#### Footer

A three-column layout on a dark background containing Contact Us information in the left column, Quick Links in the centre column, and Legal links in the right column. Certification logos from CIEH, RoSPA, and ISO 22000 are displayed in the upper section of the footer above the three columns. A copyright and data attribution line is displayed at the base of the footer.

#### Hygiene Rating Badge

A colour-coded square badge displaying the numeric rating score. Used on result cards, the business details page, and the rating guide page.

| Rating | Colour |
|---|---|
| 5 — Very Good | Dark green |
| 4 — Good | Mid green |
| 3 — Generally Satisfactory | Yellow-green |
| 2 — Improvement Necessary | Amber |
| 1 — Major Improvement Necessary | Orange-red |
| 0 — Urgent Improvement Required | Dark red |

#### Status Badge

A small coloured label badge displayed on result cards and the business details page. Possible values: Rated (green), New Rating Pending (yellow), Awaiting Inspection (purple), Exempt (grey), and Improvement Necessary (orange).

---

## 3.4 Wireframes

Low-fidelity wireframes were produced for all four pages before any high-fidelity styling was applied. The wireframes establish the structural layout, the position of every interface element, and the hierarchy of content on each page. No colours, fonts, or visual styling are applied in the wireframe stage.

**Wireframe Figma Link:** https://www.figma.com/design/0V6qioQcKcWNtVy9fG22DS/WireFrame-finished---Desktop?node-id=0-1&t=rGD7ReVYtfm3j7XF-1

---

### 3.4.1 Homepage Wireframe

The homepage wireframe establishes a clear vertical hierarchy. The header navigation sits at the top. Below it, the hero section occupies the full width of the page and contains the primary heading, a short descriptive subtitle, and the main search input with its Search button. A validation message placeholder is shown beneath the input to indicate where the error message will appear when the form is submitted empty.

Below the hero, the Browse by Business Type section contains six icon-based category tiles arranged in a horizontal row. Below this sits the What Do the Ratings Mean section containing a horizontal row of rating badges from 5 to 0 with a View Full Guide link. The page ends with the consistent footer.

The wireframe deliberately omits all colour and iconography to focus the design review on structure and hierarchy alone.

<img width="400" height="715" alt="Screenshot 2026-03-16 at 14 51 51" src="https://github.com/user-attachments/assets/528a9377-d15c-4456-b4b7-2ae548844129" />


---

### 3.4.2 Search Results Wireframe

The search results wireframe uses a two-column layout. The left column contains the Filters panel with two groups of checkboxes: Hygiene Rating (values 5 to 0) and Business Type (Restaurant, Takeaway, Cafe, Pub/Bar, School, Hotel). The right column contains the search bar at the top followed by the results count label and the vertical list of result cards.

Each result card is a horizontal row showing a rating badge placeholder on the left, followed by the business name, business type label, address, and rating date. A right-pointing arrow indicates that the card is clickable.

Below the results list, two additional states are shown as separate panels: the No Results state with a message and the Error state with a Retry button. This ensures both states are documented within the wireframe rather than being left implicit.

<img width="323" height="732" alt="Screenshot 2026-03-16 at 14 52 39" src="https://github.com/user-attachments/assets/59c94d74-c479-44f3-8aa6-540776b26963" />

---

### 3.4.3 Business Details Wireframe

The business details wireframe uses a two-column layout. The Back to Results link is positioned above both columns. The left column contains the business information card at the top, showing the rating score box, business name, type badge, and status badge, followed by the full detail table listing every API data field. The right column contains the Official Rating Graphic placeholder at the top and the What Does This Rating Mean panel below it, listing all six rating levels.

Below the two-column grid, the wireframe documents three conditional status notices as separate labelled panels: A new rating is pending, Awaiting Inspection, and Exempt from Rating. The label "(shown conditionally)" confirms that these are not always displayed simultaneously.

<img width="372" height="732" alt="Screenshot 2026-03-16 at 14 53 23" src="https://github.com/user-attachments/assets/0a7bdb35-8be8-44d8-87a9-362d021434c4" />

---

### 3.4.4 Rating Guide Wireframe

The rating guide wireframe presents a single-column, scroll-based layout. A page heading and brief introduction paragraph are followed by six rating entry rows, each displaying a numeric score badge on the left and the rating label with description on the right. Below the six numeric ratings, a Special Statuses section presents three side-by-side cards for Awaiting Inspection, New Rating Pending, and Exempt.

<img width="304" height="732" alt="Screenshot 2026-03-16 at 14 55 06" src="https://github.com/user-attachments/assets/a2122fc8-235e-47cf-9a19-b96e82764119" />

---

## 3.5 High-Fidelity Mockups

High-fidelity desktop mockups were produced for all four pages after the wireframe structure and wireflow navigation were validated. The mockups apply the full design system to the validated wireframe layouts, adding colour, typography, iconography, spacing, and all interactive component styles.

**High-Fidelity Mockup Figma Link:** https://www.figma.com/design/cDzHoE1BvKaEpMsooiBrOb/High-Fidelity-MockUp?t=rGD7ReVYtfm3j7XF-1

---

### 3.5.1 Visual Design System

All four pages share a single design system defined below.

| Category | Value | Usage |
|---|---|---|
| Primary colour | `#1B5E20` and and `#1D8A4F` (dark green) | Hero section backgrounds, header |
| Secondary colour | `#2E7D32` | Buttons, active navigation states |
| Accent colour | `#81C784` | Highlights, hover states |
| Warning colour | `#F57F17` | Rating badge 2, New Rating Pending notice |
| Danger colour | `#B71C1C` | Rating badge 0 |
| Page background | `#FFFFFF` | Main page background |
| Surface background | `#F5F5F5` | Cards and filter panels |
| Body typography | Inter (sans-serif) | All body text |
| Border radius (cards) | 8px | Result cards, detail cards |
| Border radius (buttons) | 4px | Search button, Retry button |
| Border radius (badges) | 24px | Status badges |
| Card shadow | `0 2px 8px rgba(0,0,0,0.1)` | All cards |

---

### 3.5.2 Homepage High-Fidelity Mockup

The homepage mockup applies the full design system to the wireframe structure. The hero section uses the primary dark green (`#1B5E20`) as a background with decorative circular shapes in a slightly lighter green tone creating depth and visual interest. The heading "Find Food Hygiene Ratings in Bristol" is set in white bold text, centred within the hero. The search input uses a white background with a black Search button to create a strong contrast focal point that immediately draws the user's eye.

Below the hero, a statistics bar displays four icon-accompanied figures in a horizontal row: 3,268 Rated businesses, 443 Awaiting inspection, Open Data (powered by Open Bristol), and Free Access (no account required). This section builds immediate user confidence in the platform.

The six category tiles in the Browse by Business Type section each display a food-relevant illustration icon above a text label on a light grey card background. The rating summary badges in the What Do the Ratings Mean section are displayed in their full colour progression from dark green (5) to dark red (0) against white pill-shaped outlines. A View Full Guide button sits below the badges.

The footer uses a dark near-black background with white text, the CIEH, RoSPA, and ISO 22000 certification logos in the upper zone, and the three-column layout below.

<img width="425" height="732" alt="Screenshot 2026-03-16 at 14 56 31" src="https://github.com/user-attachments/assets/bf8dac3a-c32f-4794-b1bb-fa7b1e604abf" />


---

### 3.5.3 Search Results High-Fidelity Mockup

The search results mockup implements the two-column wireframe layout with the full design system applied. The filter panel on the left uses a white card on a light grey surface background with a thin border, presenting the Hygiene Rating and Business Type checkbox groups. Each checkbox option displays a result count to the right, helping users make informed filtering decisions. A green Clear All Filters button sits at the base of the panel.

Active filter selections are displayed as removable pill-shaped tags above the results list, labelled with the filter name and value (such as "Rating: 5" and "Type: Restaurant"). A cross icon on each tag allows individual filters to be removed without reopening the filter panel.

Each result card in the right column uses a prominent colour-coded rating badge on the left edge, followed by the business name in bold, a coloured business type label badge, the full address in grey body text, the rating date, and a status badge in the bottom right corner of the card.

The No Results state panel displays a magnifying glass icon, the message "No results found", and guidance to broaden the search or adjust the filters. The error state panel displays a warning triangle icon, the message "Unable to load data", a brief explanatory sentence, and a Retry button. Pagination controls at the bottom of the results list show page number buttons and forward and backward arrow buttons.

<img width="316" height="718" alt="Screenshot 2026-03-16 at 14 56 56" src="https://github.com/user-attachments/assets/aaa77179-62b1-4836-b804-e24658203aaf" />


---

### 3.5.4 Business Details High-Fidelity Mockup

The business details mockup implements the two-column wireframe layout. The Back to Results button with a left-pointing arrow icon is positioned above the two columns. The left column opens with a business information card displaying the numeric rating score in a large box, the business name in bold, a business type badge, a green Rated status badge, and the full address in grey body text. Below the card, a structured detail table presents every API data field as a labelled row.

The right column displays the official Food Hygiene Rating sticker graphic, which uses the nationally recognised green and black design with the score badge and star rating. A fallback numeric box is shown below it in case the graphic fails to load. Below the graphic, the "What Does This Rating Mean?" panel lists all six rating levels from 5 to 0, each with a colour-coded score badge and a short description. A Full Guide link at the base of the panel provides navigation to the Rating Guide page.

Below the two-column grid, the conditional status notice panels are shown. The "A new rating is pending" notice uses a yellow background with a hourglass icon. The "Awaiting Inspection" notice uses a light purple background with a magnifying glass icon. The "Exempt from Rating" notice uses a light blue background with an information icon. Each notice is rendered only when the relevant condition is true for the business being viewed.

<img width="380" height="737" alt="Screenshot 2026-03-16 at 14 57 40" src="https://github.com/user-attachments/assets/2c603dc8-77d7-45ea-ac91-9ec53db407ea" />


---

### 3.5.5 Rating Guide High-Fidelity Mockup

The rating guide mockup transforms the simple wireframe list into a structured and visually engaging layout. A full-width dark green hero banner carries the heading "Rating Guide" and the subtitle "Understanding Food Hygiene Ratings" in white text, maintaining visual consistency with the homepage.

A bordered introductory panel beneath the banner explains that food hygiene ratings are issued by local authorities in the United Kingdom following inspections of food businesses and that scores range from 0 to 5.

Each of the six numeric rating levels is presented in its own card. Every card contains a large colour-coded score badge on the left, the rating label in bold, a short description of the hygiene standards that level represents, and a "What This Means" sub-panel in a bordered grey box providing practical consumer guidance on whether to visit the establishment. This additional layer of guidance goes beyond the wireframe structure and was added during the mockup stage to improve the usability of the page for users who are unfamiliar with what each score means in practice.

The Special Statuses section at the bottom of the page contains three side-by-side cards for Awaiting Inspection, New Rating Pending, and Exempt. Each card uses a title, an icon, and a short explanation. These cards are particularly relevant given that 443 premises in the Bristol dataset are currently awaiting their first inspection, meaning a significant proportion of search results may carry one of these statuses rather than a numeric rating.

<img width="314" height="737" alt="Screenshot 2026-03-16 at 14 58 19" src="https://github.com/user-attachments/assets/0ece60a3-982d-4b2f-910d-28f5216c522f" />


---

## 3.6 Wireframe and High-Fidelity Mockup Comparison

The side-by-side comparisons below illustrate how each page evolved from the low-fidelity wireframe stage to the final high-fidelity mockup. The structural layout, element positioning, and content hierarchy established in each wireframe are preserved in the corresponding mockup without exception. The mockup stage adds colour, typography, iconography, and spacing to produce the final intended appearance, but does not alter the structural decisions made at the wireframe stage. This confirms that the two stages of the design process functioned correctly as intended.

- **Homepage:** Wireframe establishes the hero-search-category-ratings-footer hierarchy. Mockup adds dark green hero, statistics bar, illustrated category
icons, and colour-coded rating badges.

  <img width="425" height="732" alt="Screenshot 2026-03-16 at 14 56 31" src="https://github.com/user-attachments/assets/1afbfb98-0847-4c61-bd21-7360827c8600" />

  <img width="400" height="715" alt="Screenshot 2026-03-16 at 14 51 51" src="https://github.com/user-attachments/assets/99044e23-01d3-4932-80cf-b6567c1b2e3f" />


- **Search Results:** Wireframe establishes the two-column filter-plus-results layout with documented empty and error states. Mockup adds colour-coded result cards, active filter tags, a result count per filter option, and styled empty and error state panels.
  
<img width="316" height="718" alt="Screenshot 2026-03-16 at 14 56 56" src="https://github.com/user-attachments/assets/a51b90c0-cd9e-49c8-8cc0-e4de18b8e59e" />

<img width="323" height="732" alt="Screenshot 2026-03-16 at 14 52 39" src="https://github.com/user-attachments/assets/98b8ae5d-3185-42af-af70-f53361c4fca7" />

  
- **Business Details:** Wireframe establishes the two-column business-data-plus-rating-panel layout with conditional notices documented below. Mockup adds the official Food Hygiene Rating sticker graphic, colour-coded status badges, and the styled conditional notice panels.

<img width="380" height="737" alt="Screenshot 2026-03-16 at 14 57 40" src="https://github.com/user-attachments/assets/d5b60db4-d36a-42a8-bbb7-1cf21e7e02a4" />

<img width="372" height="732" alt="Screenshot 2026-03-16 at 14 53 23" src="https://github.com/user-attachments/assets/3d855d80-8a5a-4542-a518-dfc3ea918eb2" />

- **Rating Guide:** Wireframe establishes the linear scroll-based rating list with a special statuses section below. Mockup adds colour-coded rating cards with "What This Means" sub-panels, a hero banner, and an introductory panel.

<img width="314" height="737" alt="Screenshot 2026-03-16 at 14 58 19" src="https://github.com/user-attachments/assets/18f2aa1a-6bbc-4921-99fb-1377059c01d6" />

<img width="304" height="732" alt="Screenshot 2026-03-16 at 14 55 06" src="https://github.com/user-attachments/assets/d0388156-222b-46f9-8adc-30ed02a5e2f8" />

---

## 3.7 Design Decisions and Justifications

The table below documents every significant design decision made during this phase, the rationale behind it, and the requirement or use case it serves.

| Design Decision | Rationale | Requirement Addressed |
|---|---|---|
| Green colour scheme | Green is universally associated with safety, cleanliness, and food hygiene in the United Kingdom. The choice reinforces the platform's values and creates a coherent visual identity consistent with food safety branding conventions. | NFR3 |
| Hero search bar on the homepage | Placing the search bar as the dominant element in the hero section minimises the number of steps required for the user to complete their primary task. | FR1 |
| Category tiles as an alternative entry point | Allows users who prefer to browse by business type to reach filtered results without typing a query. | FR6 |
| Colour-coded rating badges | Using a distinct colour for each rating level allows users to interpret a score at a glance without reading the numeric value, improving both scannability and accessibility. | US7 |
| Sidebar filter panel with result counts | Displaying result counts alongside each filter option prevents users from making selections that would return zero results. | FR5 |
| Active filter chips above the results list | Gives users immediate visibility of applied filters and allows individual filters to be removed without returning to the panel. | FR7 |
| Conditional status notices on the details page | Displaying only the notice relevant to the specific business keeps the interface clean and avoids presenting irrelevant information. | FR14, FR15, FR16 |
| Rating explanation panel on the details page | Allows users to interpret the displayed rating without navigating away from the details page, reducing unnecessary navigation steps. | FR17 |
| No login required | All hygiene rating information is public and should be accessible without creating an account, reducing friction for all users. | FR10 |
| Retry button on the error state | Provides users with a clear and immediate recovery action when data cannot be loaded, rather than leaving them on a blank or broken page. | NFR7 |
| Official Food Hygiene Rating sticker graphic | Using the nationally recognised graphic on the details page provides a familiar reference point that users may recognise from physical premises. | FR12 |
| Back to Results preserves filter and search state | Allows users to return to their previous results without having to re-enter their query or re-apply their filters, supporting efficient multi-business comparison. | UC2 |
| Twelve-column CSS grid | Provides a consistent structural foundation that supports the multi-column layouts on desktop whilst allowing the layout to adapt gracefully to narrower viewports. | NFR5 |
| Desktop-first design approach | The mockups were designed for desktop browsers first, reflecting the primary use case of users researching businesses before visiting. The grid-based layout can be adapted for smaller viewports during implementation. | NFR5 |

---

## 3.8 Accessibility Considerations (WCAG 2.1 Level AA)

Accessibility was considered throughout the design phase in accordance with WCAG 2.1 Level AA guidelines. The following considerations are reflected in the high-fidelity mockups and will be carried through to the implementation phase.

Colour contrast ratios between text and background colours meet or exceed the WCAG 2.1 minimum ratio of 4.5:1 for normal text and 3:1 for large text throughout the application. Colour is never used as the sole means of conveying information: every rating badge displays both a colour and a numeric value, and every status badge displays both a colour and a text label, ensuring the information remains accessible to users with colour vision deficiencies.

All images and icons will include appropriate alternative text attributes. Form inputs will include visible labels and accessible error messages that are announced by screen readers. The application will support full keyboard navigation, allowing users to tab through interactive elements in a logical order without requiring a mouse. A skip navigation link will be provided to allow keyboard and screen reader users to bypass the navigation bar and reach the main content directly.

All layouts are fully responsive and will reflow correctly across desktop, tablet, and mobile viewports as described in the grid layout section.

---

## 3.9 Design Tools and Process

All wireframes, wireflow diagrams, and high-fidelity mockups were created using Figma. Figma was selected for this project because it supports component-based design, enabling shared components such as the navigation bar, footer, rating badge, and status badge to be defined once and reused across all four pages consistently. It also enables interactive prototype connections between frames, which was used to validate navigation paths during the wireflow stage. Additionally, Figma produces shareable links that allow design artefacts to be reviewed and submitted without requiring the assessor to install any additional software.

### 3.9.1 Design Process Steps

The design process followed the steps below in order.

1. **Requirements review:** All functional requirements, non-functional requirements, and use cases from Phase 2 were reviewed to identify every screen, every user journey, and every edge-case state that the design must address.
2. **Low-fidelity wireframes:** Structural wireframes were sketched and then produced in Figma for all four pages, establishing layout, element positioning, and content hierarchy without any visual styling.
3. **Wireflow connections:** Navigation arrows and annotations were added between all wireframe screens in Figma to produce the complete wireflow diagram, validating that every use case and functional requirement is addressed by the navigation model.
4. **Design system definition:** The colour palette, typography, spacing scale, border radii, and shadow values were defined as a shared design system before any high-fidelity mockup work began, ensuring consistency across all pages.
5. **High-fidelity mockups:** The validated wireframe layouts were used as the structural foundation for the high-fidelity mockups. The design system was applied to produce the final visual appearance of all four pages, including all component states, edge-case panels, and conditional elements.
6. **Design validation:** The completed mockups were reviewed against the requirements specification and the wireflow diagram to confirm that every functional requirement, non-functional requirement, and use case is represented in the final design.

---

## 3.10 Figma Links Summary

All design artefacts produced during this phase are hosted on Figma and can be accessed at full resolution using the links below.

| Artefact | Figma Link |
|---|---|
| Wireflow Diagram | https://www.figma.com/design/cDzHoE1BvKaEpMsooiBrOb/High-Fidelity-MockUp?node-id=2071-507&t=36W43D7d1QbB3XwJ-1 |
| Wireframe — All Pages | https://www.figma.com/design/0V6qioQcKcWNtVy9fG22DS/WireFrame-finished---Desktop?node-id=0-1&t=rGD7ReVYtfm3j7XF-1 |
| High-Fidelity Mockup — All Pages | https://www.figma.com/design/cDzHoE1BvKaEpMsooiBrOb/High-Fidelity-MockUp?t=rGD7ReVYtfm3j7XF-1 |
