# Testing

## Bristol Food Hygiene Ratings — Phase 5: Testing

| Field | Detail |
|---|---|
| Module | UFCF9F-30-1 Information Systems Development |
| Author | Nadira Robleh |
| Version | 1.0.0 |
| Date | 06 April 2026 |
| Application | Bristol Food Hygiene Ratings Web Application |

---

## 1. Introduction

This document forms the testing phase of the Bristol Food Hygiene Ratings portfolio. It describes the testing approach taken, provides a complete set of thirty structured test cases covering every functional and non-functional requirement, records the outcome of each test run, and presents a Requirements Traceability Matrix (RTM) that maps each requirement to its corresponding test case(s).

The application is a client-side, multi-page web application built in HTML5, CSS3, and vanilla JavaScript. All 3,867 business records are embedded in data.js, so the application functions entirely without a back-end server or live API connection. Testing is therefore wholly manual and carried out against the locally served application.

All test cases are designed to be reproducible by any tester with a modern browser and access to the project source files. No specialist tools beyond Chrome DevTools and the WAVE accessibility browser extension are required.

---

## 2. Testing Scope

The following areas are within scope for this test phase:

- All seventeen functional requirements (FR1-FR17) derived from Use Cases UC1 and UC2.
- All relevant non-functional requirements (NFR1-NFR10), including usability, responsiveness, accessibility, performance, reliability, security, and maintainability.
- All use case steps and documented variations and edge-case states from the requirements specification.
- Cross-browser rendering on Google Chrome (primary) and Mozilla Firefox (secondary).
- Responsive behaviour at mobile (390 px), tablet (768 px), and desktop (1440 px) viewport widths.

The following are outside scope for this test phase:

- Server-side load testing and concurrent user simulation (NFR5 and NFR6 are addressed by architectural argument given the static hosting model).
- HTTPS certificate configuration (NFR9 is a deployment concern, not an application code concern).
- Automated unit testing frameworks - all testing is manual at this stage.

---

## 3. Test Data

The following test data records are referenced throughout the test cases. All records are drawn from the ALL_BUSINESSES array embedded in data.js.

| ID | Description | Dataset Values |
|---|---|---|
| TD1 | Fully rated business | rating: 5, ratingStatus: "" (empty string), newRatingPending: false |
| TD2 | Lowest rated business | rating: 0, ratingStatus: "" (empty string) |
| TD3 | Awaiting inspection | rating: null, ratingStatus: "AwaitingInspection" (440 records in dataset) |
| TD4 | New rating pending | newRatingPending: true |
| TD5 | Exempt business | rating: null, ratingStatus: "Exempt" (158 records in dataset) |
| TD6 | Multi-record search term | "Clifton" - matches many records across multiple business types and ratings |
| TD7 | Zero-result search term | "zzznonexistent999" - guaranteed to return no matching records |
| TD8 | Empty input | Empty string - submitted with no characters in the search bar |
| TD9 | Combined filter target | businessType: "Restaurant/Cafe/Canteen", rating: 5, address containing "Clifton" |

---

## 4. Prerequisites

The following conditions must be met before any test case is executed:

- The application is served via a local static file server (e.g. the serve package configured by serve.json) from the project root directory, or opened directly in the browser from the file system.
- A supported browser is used: Google Chrome 122 or later (primary), or Mozilla Firefox 123 or later (secondary).
- JavaScript is enabled in the browser.
- All source files are present: index.html, Search.html, Business-Detail.html, Rating-Guide.html, Main.js, data.js, and Style.css.
- All asset files (logo, category tile icons, certification badge images) are present in the assets/ directory.
- The WAVE browser extension is installed in Chrome for accessibility tests TC24 and TC25.

---

## 5. Test Plan

Thirty test cases are defined below. Each test case is uniquely identified (TC1-TC30) and structured consistently to allow any tester to reproduce the test independently. Each case documents the requirement(s) being validated, the relevant use case, the test data used, a numbered sequence of steps, and the expected result.

---

### TC1 - Homepage Loads and Renders All Sections

| Field | Detail |
|---|---|
| Requirement(s) | FR1, NFR1, NFR2, NFR10 |
| Use Case | UC1 |
| Test Data | No input required. Dataset: ALL_BUSINESSES (3,867 records embedded in data.js). |

**Steps:**

1. Open index.html via the local static file server.
2. Verify the page renders in the browser with no JavaScript console errors.
3. Confirm the hero section is visible and contains a labelled search bar and a Search button.
4. Confirm the statistics bar displays four populated numeric values derived from the live dataset (e.g. total businesses, number rated 5, number awaiting inspection).
5. Confirm the Browse by Business Type category tiles are rendered (including Restaurant/Cafe, Takeaway, Pub/Bar, School, Hotel, etc.).
6. Confirm the rating summary section displays rating pill links for scores 0 through 5.
7. Confirm the primary navigation bar links to Home, Search, Detail, and Rating Guide.
8. Confirm the footer is present and displays the copyright notice and Bristol Open Data attribution.

**Expected Result:** All sections render correctly with no console errors or broken assets. The statistics bar values match the known dataset distribution (3,867 total, 2,450 rated 5, 440 awaiting inspection, 600 unrated). The page is fully functional before any user interaction.

**Outcome:** Pass

---

### TC2 - Search Bar Accepts Input and Navigates to Results

| Field | Detail |
|---|---|
| Requirement(s) | FR1, FR2, FR3, NFR1 |
| Use Case | UC1 |
| Test Data | TD6 - search term "Clifton" (address area with many matching records across multiple business types). |

**Steps:**

1. On index.html, click inside the hero search bar and type "Clifton".
2. Submit the search by pressing Enter or clicking the Search button.
3. Verify the browser navigates to Search.html.
4. Inspect the URL and confirm it contains a query parameter encoding the search term (e.g. ?q=Clifton).
5. Verify the results list is populated with business records whose name, address, or postcode contains "Clifton".
6. Select one result card and confirm it displays: business name, address, business type, hygiene rating (numeric or "Awaiting Inspection"), and rating date.

**Expected Result:** The browser navigates to Search.html with the search term passed via URL query parameter. The results list is populated with matching businesses. Each card displays all fields required by FR3.

**Outcome:** Pass

---

### TC3 - Empty Search Input Validation

| Field | Detail |
|---|---|
| Requirement(s) | FR9, NFR8 |
| Use Case | UC1 - Variation 3a |
| Test Data | TD8 - empty string (no input entered). |

**Steps:**

1. On index.html, leave the search bar completely empty.
2. Click the Search button or press Enter.
3. Observe the page behaviour.
4. Confirm the browser does not navigate away from index.html.
5. Confirm a visible validation prompt or error message is displayed below or near the search bar, instructing the user to enter a valid search term.
6. Confirm no data query is triggered.

**Expected Result:** The system remains on the homepage. A clear, user-readable validation message is shown. No navigation occurs and no search is performed. FR9 and NFR8 are satisfied.

**Outcome:** Pass

---

### TC4 - No Results State Displayed Correctly

| Field | Detail |
|---|---|
| Requirement(s) | FR8 |
| Use Case | UC1 - Variation 5a |
| Test Data | TD7 - search term "zzznonexistent999" (guaranteed to return zero matching records). |

**Steps:**

1. On index.html, enter "zzznonexistent999" into the search bar and submit.
2. On Search.html, observe the results area.
3. Confirm that no business result cards are displayed.
4. Confirm a clear "no results" message is shown, suggesting the user broaden their search or try different terms.
5. Confirm the filter panel remains visible so the user can adjust their criteria without returning to the homepage.

**Expected Result:** The results container is replaced by the no-results state panel. The message clearly explains that no matching businesses were found. The filter panel is still accessible. FR8 is satisfied.

**Outcome:** Pass

---

### TC5 - Filter Results by Hygiene Rating Score

| Field | Detail |
|---|---|
| Requirement(s) | FR5, FR7 |
| Use Case | UC1 |
| Test Data | TD6 ("Clifton"), then apply rating filter for score 5. Dataset contains 2,450 businesses rated 5. |

**Steps:**

1. Navigate to Search.html?q=Clifton (or submit the Clifton search from the homepage).
2. Locate the Hygiene Rating section in the sidebar filter panel.
3. Tick the checkbox for rating 5.
4. Observe the results list update without a full page reload.
5. Confirm all displayed result cards show a hygiene rating of exactly 5.
6. Confirm an active filter chip labelled "Rating: 5" (or equivalent) appears above the results list.
7. Confirm the displayed result count decreases to reflect the filtered set.

**Expected Result:** Only businesses with a hygiene rating of 5 are shown. The active filter chip is visible. The result count updates correctly. Results update immediately without a full page reload. FR5 is satisfied.

**Outcome:** Pass

---

### TC6 - Filter Results by Business Type

| Field | Detail |
|---|---|
| Requirement(s) | FR6, FR7 |
| Use Case | UC1 |
| Test Data | TD6 ("Clifton"), then apply business type filter "Restaurant/Cafe/Canteen". |

**Steps:**

1. Navigate to Search.html?q=Clifton.
2. Locate the Business Type section in the sidebar filter panel.
3. Tick the checkbox labelled "Restaurant / Cafe" (or "Restaurant/Cafe/Canteen").
4. Observe the results list update.
5. Confirm only businesses of type Restaurant/Cafe/Canteen are displayed.
6. Confirm an active filter chip for the selected business type appears above the results list.
7. Confirm the result count decreases to reflect the filtered set.

**Expected Result:** Only Restaurant/Cafe/Canteen businesses matching the search term are shown. The active filter chip is present. Results update immediately. FR6 is satisfied.

**Outcome:** Pass

---

### TC7 - Combined Rating and Business Type Filters Applied Simultaneously

| Field | Detail |
|---|---|
| Requirement(s) | FR7 |
| Use Case | UC1 |
| Test Data | TD9 - businesses of type Restaurant/Cafe/Canteen with rating 5 in Clifton. |

**Steps:**

1. Navigate to Search.html?q=Clifton.
2. Apply rating filter 5 (as per TC5).
3. Additionally apply business type filter "Restaurant / Cafe" (as per TC6).
4. Observe the results list.
5. Confirm all displayed businesses satisfy both conditions: rating = 5 AND type = Restaurant/Cafe/Canteen.
6. Confirm two active filter chips are displayed simultaneously above the results list.
7. Confirm the result count reflects the combined filter criteria.

**Expected Result:** Both filters are active at the same time. All results satisfy both criteria. Two filter chips are visible. The result count reflects the combined filter. FR7 is satisfied.

**Outcome:** Pass

---

### TC8 - Remove an Individual Filter Using the Active Filter Chip

| Field | Detail |
|---|---|
| Requirement(s) | FR5, FR6, FR7 |
| Use Case | UC1 |
| Test Data | Continuation of TC7 (two active filters: Rating 5 and Restaurant/Cafe). |

**Steps:**

1. With both filters active from TC7, locate the "Type: Restaurant / Cafe" active filter chip above the results list.
2. Click the x (remove) icon on that chip.
3. Observe the results list update.
4. Confirm the business type filter is removed and the corresponding chip disappears.
5. Confirm the rating filter (Rating: 5) remains active and its chip is still visible.
6. Confirm the results list expands to include all businesses rated 5 regardless of type.

**Expected Result:** Removing an individual filter chip removes only that filter. The remaining filter continues to apply. The results list updates accordingly. FR7 is satisfied.

**Outcome:** Pass

---

### TC9 - Category Tile on Homepage as Alternative Entry Point

| Field | Detail |
|---|---|
| Requirement(s) | FR6, NFR1 |
| Use Case | UC1 - Variation 6a |
| Test Data | No text input required. User selects a category tile (e.g. "Restaurants"). |

**Steps:**

1. On index.html, locate the Browse by Business Type section.
2. Click a category tile (e.g. "Restaurants").
3. Verify the browser navigates to Search.html.
4. Inspect the URL and confirm it contains a business type filter query parameter.
5. Confirm the results list shows only businesses of the selected type.
6. Confirm an active filter chip for that business type is shown.
7. Confirm no text search query is required or displayed.

**Expected Result:** Clicking a category tile navigates directly to Search.html with the appropriate business type pre-applied as a filter, and no text search term. UC1 Variation 6a is satisfied. NFR1 is satisfied (user reaches filtered results in one click from the homepage).

**Outcome:** Pass

---

### TC10 - Rating Pill Links on Homepage Navigate to Filtered Results

| Field | Detail |
|---|---|
| Requirement(s) | FR5, NFR1 |
| Use Case | UC1 |
| Test Data | No text input required. User selects the rating 5 pill. |

**Steps:**

1. On index.html, locate the rating summary section listing pill links for ratings 0 through 5.
2. Click the pill labelled "5 - Very Good".
3. Verify the browser navigates to Search.html.
4. Confirm the URL contains a rating filter query parameter for rating 5.
5. Confirm all displayed results have a rating of 5.
6. Confirm an active filter chip for Rating: 5 is shown.

**Expected Result:** Each rating pill navigates to Search.html pre-filtered to the selected rating. The pill links provide a fast alternative entry point to filtered results without requiring a text search. NFR1 is satisfied.

**Outcome:** Pass

---

### TC11 - Business Details Page Displays All Required Fields

| Field | Detail |
|---|---|
| Requirement(s) | FR11, FR12, FR17, NFR1 |
| Use Case | UC2 |
| Test Data | TD1 - any business with rating 5 and ratingStatus empty string (fully rated). |

**Steps:**

1. From Search.html with any search results visible, click on any result card.
2. Verify the browser navigates to Business-Detail.html with the selected business id as a URL query parameter.
3. In the left column, confirm the following are displayed: business name (bold), business type badge, status badge showing "Rated", and full street address.
4. In the description list below the card, confirm all required fields are present: business name, full address, postcode, business type, hygiene rating, rating date, rating status, and new rating pending indicator.
5. In the right column, confirm the official FSA Food Hygiene Rating Scheme sticker graphic is loaded and displayed.
6. Below the graphic, confirm the "What Does This Rating Mean?" panel is present, listing all six rating levels (5 to 0) with colour-coded badges and plain-language descriptions.
7. Confirm the panel includes a "Full Guide" link that navigates to Rating-Guide.html.

**Expected Result:** All fields listed in FR11 are displayed correctly. The FSA rating graphic loads (FR12). The rating explanation panel is present and complete (FR17). The page loads without any errors. NFR1 is satisfied (business details reachable in three clicks from the homepage).

**Outcome:** Pass

---

### TC12 - Rating Graphic Fallback When Image Fails to Load

| Field | Detail |
|---|---|
| Requirement(s) | FR13 |
| Use Case | UC2 - Variation 3c |
| Test Data | Any business record containing a valid rating graphic URL. External domain ratings.food.gov.uk is blocked via DevTools. |

**Steps:**

1. Open Business-Detail.html?id=[id] for any rated business.
2. Open Chrome DevTools and navigate to the Network panel.
3. Add a request block rule for the domain "ratings.food.gov.uk".
4. Reload the page.
5. Observe the right column where the rating graphic should appear.
6. Confirm that the graphic does not load but that the page does not display an error, broken image icon, or blank space.
7. Confirm the onerror fallback activates and displays the numeric rating value as styled text in place of the image.

**Expected Result:** The image fails gracefully. The numeric rating value is shown as a styled fallback. The rest of the page remains fully functional and informative. FR13 is satisfied.

**Outcome:** Pass

---

### TC13 - Awaiting Inspection Status Notice and Badge Replacement

| Field | Detail |
|---|---|
| Requirement(s) | FR4, FR14, FR16 |
| Use Case | UC2 - Variation 3a |
| Test Data | TD3 - a business with ratingStatus: "AwaitingInspection" (440 such records in dataset). Locate via Search.html filtered to show unrated businesses. |

**Steps:**

1. Locate a business with ratingStatus "AwaitingInspection" by filtering results or navigating directly to its Business-Detail.html?id=[id].
2. Confirm the numeric rating badge in the left column is replaced by the label "Awaiting Inspection" rather than a score.
3. Confirm the status badge shows "Awaiting Inspection" in a clearly distinguishable colour.
4. Confirm a conditional notice panel (purple or similar) is displayed on the page.
5. Read the notice panel content and confirm it explains in plain English that the business has not yet been inspected and that no hygiene rating is currently available.
6. Confirm no numeric rating value appears anywhere on the page for this business.

**Expected Result:** The awaiting inspection status is clearly communicated throughout the page. No misleading numeric rating is shown. The conditional notice panel appears with an appropriate plain-language explanation. FR4, FR14, and FR16 are all satisfied.

**Outcome:** Pass

---

### TC14 - New Rating Pending Notice Displayed Correctly

| Field | Detail |
|---|---|
| Requirement(s) | FR15 |
| Use Case | UC2 - Variation 3b |
| Test Data | TD4 - a business with newRatingPending: true in the dataset. |

**Steps:**

1. Navigate to Business-Detail.html?id=[id] for a business with newRatingPending set to true.
2. Confirm a yellow (or similarly distinct) conditional notice panel is displayed on the page.
3. Read the notice panel and confirm it informs the user that the currently displayed rating may be subject to change because a new rating is pending publication.
4. Confirm the existing numeric rating is still displayed (it is not replaced, only qualified by the notice).

**Expected Result:** The new rating pending notice panel is visible and clearly communicates the possibility of an imminent rating change. The existing rating remains displayed alongside the notice. FR15 is satisfied.

**Outcome:** Pass

---

### TC15 - Exempt Status Notice Displayed Correctly

| Field | Detail |
|---|---|
| Requirement(s) | FR16 |
| Use Case | UC2 - Variation 3d |
| Test Data | TD5 - a business with ratingStatus: "Exempt" (158 such records in dataset). |

**Steps:**

1. Navigate to Business-Detail.html?id=[id] for a business with ratingStatus "Exempt".
2. Confirm no numeric rating value is displayed.
3. Confirm a light blue (or similarly distinct) conditional notice panel is displayed.
4. Read the notice panel and confirm it explains in plain language that this business is not required to participate in the Food Hygiene Rating Scheme and that no numeric rating will be assigned.

**Expected Result:** The exempt status is clearly communicated. No numeric rating is shown. The conditional notice panel provides an appropriate explanation. FR16 is satisfied.

**Outcome:** Pass

---

### TC16 - Rating Guide Page Contains Full Content

| Field | Detail |
|---|---|
| Requirement(s) | FR17 |
| Use Case | UC2 |
| Test Data | No test data required. |

**Steps:**

1. Navigate to Rating-Guide.html via the primary navigation bar.
2. Confirm the page renders with a green hero banner and introductory panel.
3. Confirm an in-page table of contents or anchor links are present.
4. Confirm six rating level cards are displayed (ratings 5 down to 0), each showing: the rating number, the rating label (e.g. "Very Good", "Urgent Improvement Required"), a colour-coded left-border accent, and a "What This Means" sub-panel with a plain-language description.
5. Confirm a Special Statuses section is present at the bottom explaining Awaiting Inspection, New Rating Pending, and Exempt in plain language.

**Expected Result:** The Rating Guide page loads without errors and provides a comprehensive explanation of all six rating scores and all three special statuses. FR17 is fully satisfied.

**Outcome:** Pass

---

### TC17 - Rating Guide Accessible from Three Entry Points

| Field | Detail |
|---|---|
| Requirement(s) | FR17, NFR1 |
| Use Case | UC2 |
| Test Data | No test data required. |

**Steps:**

1. From index.html, click the "View Full Guide" button at the bottom of the rating summary section. Confirm the browser navigates to Rating-Guide.html.
2. Navigate to any Business-Detail.html page and click the "Full Guide" link at the base of the rating explanation panel. Confirm the browser navigates to Rating-Guide.html.
3. From any page, click "Rating Guide" in the primary navigation bar. Confirm the browser navigates to Rating-Guide.html.

**Expected Result:** All three routes navigate correctly to Rating-Guide.html. There are no dead links. NFR1 is satisfied across all three entry points.

**Outcome:** Pass

---

### TC18 - Back to Results Preserves Search Query and Filter State

| Field | Detail |
|---|---|
| Requirement(s) | UC2 Step 6, Design Decision (Phase 3) |
| Use Case | UC2 |
| Test Data | TD6 ("Clifton") with rating filter 5 applied. Any result card clicked. |

**Steps:**

1. Perform a search for "Clifton" on the homepage and navigate to Search.html.
2. Apply a rating filter of 5 using the filter panel.
3. Note the result count and list of visible businesses.
4. Click any result card to navigate to Business-Detail.html.
5. On Business-Detail.html, click the "Back to Results" button.
6. Confirm the browser returns to Search.html.
7. Confirm the search term "Clifton" is still active and visible.
8. Confirm the rating filter of 5 is still active and the filter chip is visible.
9. Confirm the results list is identical to the list seen in step 3.

**Expected Result:** All search and filter state is preserved via URL query parameters. The user is returned to exactly the same view they left without needing to re-enter their search or re-apply any filters. The design decision from Phase 3 is correctly implemented.

**Outcome:** Pass

---

### TC19 - All Features Accessible Without Login or Registration

| Field | Detail |
|---|---|
| Requirement(s) | FR10 |
| Use Case | UC1, UC2 |
| Test Data | No test data required. |

**Steps:**

1. Open each of the four pages directly in a browser (index.html, Search.html, Business-Detail.html, Rating-Guide.html).
2. On each page, confirm that no login prompt, registration form, account creation wall, or authentication modal is displayed.
3. Confirm that all features on each page - search, filtering, viewing business details, and reading the rating guide - are immediately accessible.

**Expected Result:** Every page and every feature is accessible to any visitor with no barriers. No login, registration, or account creation is required at any point. FR10 is fully satisfied.

**Outcome:** Pass

---

### TC20 - Responsive Layout at Mobile Viewport (390 px)

| Field | Detail |
|---|---|
| Requirement(s) | NFR2, US8 |
| Use Case | UC1, UC2 |
| Test Data | Chrome DevTools device emulation: iPhone 14 (390 x 844 px). |

**Steps:**

1. Open index.html in Chrome with device emulation set to iPhone 14 (390 x 844 px).
2. Confirm the desktop navigation links are hidden and the hamburger toggle button is visible.
3. Click the hamburger button. Confirm the navigation panel slides open below the header.
4. Press Escape. Confirm the navigation panel closes and keyboard focus returns to the hamburger button.
5. Confirm the hero search bar, category tiles, and statistics bar reflow to a single-column layout with no horizontal scrollbar.
6. Navigate to Search.html. Confirm the filter panel and results list stack vertically.
7. Navigate to Business-Detail.html. Confirm the two-column layout collapses to a single column.
8. Verify no content overflows the viewport horizontally on any page.

**Expected Result:** All four pages display correctly at 390 px width. Layouts reflow to a single column. No horizontal scrolling. The mobile navigation toggle works correctly. NFR2 and US8 are satisfied.

**Outcome:** Pass

---

### TC21 - Responsive Layout at Tablet Viewport (768 px)

| Field | Detail |
|---|---|
| Requirement(s) | NFR2 |
| Use Case | UC1, UC2 |
| Test Data | Chrome DevTools device emulation: iPad (768 x 1024 px). |

**Steps:**

1. Open index.html in Chrome with device emulation set to iPad (768 x 1024 px).
2. Confirm the layout uses an intermediate column structure appropriate to a tablet width.
3. Navigate to Search.html. Confirm the filter panel and results list layout correctly at this width.
4. Navigate to Business-Detail.html. Confirm the layout adapts appropriately.
5. Verify no content overflows the viewport horizontally on any page.

**Expected Result:** All pages display correctly at tablet width. No broken layouts, overflowing elements, or horizontal scrollbars are present. NFR2 is satisfied.

**Outcome:** Pass

---

### TC22 - Full Keyboard Navigation Without a Mouse

| Field | Detail |
|---|---|
| Requirement(s) | NFR3 - WCAG 2.1 Level AA |
| Use Case | UC1, UC2 |
| Test Data | No test data required. Tested on all four pages. |

**Steps:**

1. Open index.html. Press Tab. Confirm the skip link is the first focusable element and has a visible focus indicator.
2. Activate the skip link (Enter). Confirm focus jumps directly to the #main-content area.
3. Continue tabbing through the page. Confirm all interactive elements (nav links, search bar, Search button, category tiles, rating pills) receive a visible focus indicator in logical order.
4. Navigate to Search.html. Confirm all filter checkboxes, result cards, and pagination controls are reachable by keyboard.
5. Navigate to Business-Detail.html. Confirm all interactive elements including the Back to Results link and Full Guide link are keyboard-reachable.
6. Navigate to Rating-Guide.html. Confirm all anchor links are keyboard-reachable.

**Expected Result:** The entire application can be navigated and operated using only the keyboard. Focus is always clearly visible. The skip link functions correctly. No interactive element is unreachable by tabbing. NFR3 is satisfied.

**Outcome:** Pass

---

### TC23 - Mobile Navigation ARIA State Management

| Field | Detail |
|---|---|
| Requirement(s) | NFR3 - WCAG 2.1 Level AA |
| Use Case | UC1 |
| Test Data | Tested in Chrome at 390 px viewport width. Main.js handles all ARIA toggling. |

**Steps:**

1. Open index.html at a mobile viewport width (390 px or below the 767 px breakpoint).
2. Open DevTools and inspect the #nav-toggle button element.
3. Before clicking, confirm aria-expanded="false" and aria-label="Open navigation menu".
4. Click the hamburger button. Confirm aria-expanded="true" and aria-label="Close navigation menu".
5. Click the backdrop area behind the nav panel. Confirm the panel closes, aria-expanded returns to "false", and keyboard focus returns to the toggle button.
6. Open the nav again by clicking the toggle. Press Escape. Confirm the panel closes, ARIA attributes are restored, and focus returns to the toggle button.
7. At a desktop viewport width (above 767 px), confirm the toggle button is hidden and the nav panel displays in desktop mode with no ARIA toggling occurring.

**Expected Result:** ARIA attributes correctly reflect the open and closed state of the navigation panel at all times. Focus management works correctly on both Escape and backdrop click. Desktop breakpoint resets the nav correctly. NFR3 is satisfied.

**Outcome:** Pass

---

### TC24 - Colour Contrast - WCAG 2.1 Level AA Compliance

| Field | Detail |
|---|---|
| Requirement(s) | NFR3 - WCAG 2.1 Level AA (minimum 4.5:1 normal text, 3:1 large text) |
| Use Case | UC1, UC2 |
| Test Data | Audited using WAVE browser extension and Chrome DevTools Accessibility panel across all four pages. |

**Steps:**

1. Open index.html in Chrome and run a WAVE accessibility audit.
2. Note any colour contrast failures and record the elements affected.
3. Pay specific attention to: white text on green rating badges; body text on white card backgrounds; status badge text; footer text on dark backgrounds.
4. Repeat the audit for Search.html, Business-Detail.html, and Rating-Guide.html.
5. For any flagged elements, use the Chrome DevTools colour picker to confirm the contrast ratio.

**Expected Result:** All text elements pass the WCAG 2.1 Level AA colour contrast minimum. No contrast failures are reported by the WAVE audit. Colour is never used as the sole means of conveying information - all rating and status badges display both colour and a text label. NFR3 is satisfied.

**Outcome:** Pass

---

### TC25 - Image Alternative Text Audit

| Field | Detail |
|---|---|
| Requirement(s) | NFR3 - WCAG 2.1 Level AA |
| Use Case | UC1, UC2 |
| Test Data | Inspected via Chrome DevTools Accessibility panel and WAVE audit on all four pages. |

**Steps:**

1. Open each page and use DevTools to inspect all img elements.
2. For decorative images (e.g. the logo in the header brand link, category tile illustrations), confirm aria-hidden="true" and alt="".
3. For informative images (e.g. the FSA rating graphic on Business-Detail.html, certification logos in the footer), confirm a descriptive alt attribute is present that conveys the content of the image.
4. For the footer certification badges (CIEH, R-SPA, ISO 22000), confirm alt text accurately describes each logo.
5. Confirm no img element is missing an alt attribute entirely.

**Expected Result:** All images have appropriate alternative text. Decorative images are hidden from assistive technology. Informative images have descriptive alt text. No images are missing the alt attribute. NFR3 is satisfied.

**Outcome:** Pass

---

### TC26 - Graceful Error State When Data Initialisation Fails

| Field | Detail |
|---|---|
| Requirement(s) | NFR7 |
| Use Case | UC1 - Variation (error state) |
| Test Data | Simulated runtime error introduced before initSearchPage() completes, using a breakpoint and manual exception throw in DevTools. |

**Steps:**

1. Open Search.html in Chrome.
2. Open DevTools and set a breakpoint at the beginning of initSearchPage() in data.js.
3. When the breakpoint is hit, use the DevTools console to throw a new Error to simulate an unexpected failure.
4. Resume script execution.
5. Observe the results container area of the page.
6. Confirm the results container is replaced by a styled error state panel.
7. Confirm the error panel displays a user-friendly warning message (no raw stack trace or technical error details).
8. Confirm a "Retry" button is present.
9. Click the Retry button and confirm the page reloads and re-initialises cleanly.

**Expected Result:** The error state panel is displayed with a clear, non-technical message and a Retry button. The page does not show a blank screen, a broken layout, or any raw error output. NFR7 is satisfied.

**Outcome:** Pass

---

### TC27 - Input Sanitisation - XSS Attack Prevention

| Field | Detail |
|---|---|
| Requirement(s) | NFR8 |
| Use Case | UC1 |
| Test Data | Malicious input string: `<script>alert("xss")</script>` |

**Steps:**

1. On index.html, click the search bar and type the following string exactly: `<script>alert("xss")</script>`
2. Submit the search.
3. On Search.html, observe the results area and any active filter chips.
4. Confirm no alert dialogue appears at any point.
5. Inspect the DOM using DevTools and confirm the injected string is not rendered as executable HTML - it should appear either as escaped literal text or result in a no-results state.
6. Repeat the test by appending the same string to the URL manually (e.g. Search.html?q=%3Cscript%3Ealert%281%29%3C%2Fscript%3E).

**Expected Result:** The script tag is never executed. The input is either escaped before DOM insertion or produces a no-results state. No XSS vulnerability is present. NFR8 is satisfied.

**Outcome:** Pass

---

### TC28 - Navigation Bar Functions Correctly on All Pages

| Field | Detail |
|---|---|
| Requirement(s) | NFR1, NFR10 |
| Use Case | UC1, UC2 |
| Test Data | No test data required. |

**Steps:**

1. From index.html, click "Search" in the navigation bar. Confirm Search.html loads.
2. From Search.html, click "Rating Guide". Confirm Rating-Guide.html loads.
3. From Rating-Guide.html, click "Home". Confirm index.html loads.
4. From index.html, click "Detail". Confirm Business-Detail.html loads.
5. On each page, confirm the navigation bar is consistently positioned and styled across all four pages.

**Expected Result:** All four navigation bar links function correctly on every page. No broken links. All pages are reachable from the navigation bar from any starting page. NFR1 and NFR10 are satisfied.

**Outcome:** Pass

---

### TC29 - Search Results Rendered Within Two Seconds

| Field | Detail |
|---|---|
| Requirement(s) | NFR4, NFR5 |
| Use Case | UC1 |
| Test Data | TD6 ("Clifton"). Tested on a local static file server. Performance measured in Chrome DevTools Performance panel. |

**Steps:**

1. Open Chrome DevTools and navigate to the Performance panel.
2. Begin a recording.
3. Load Search.html?q=Clifton directly in the browser.
4. Stop the recording once results are visible in the DOM.
5. Identify the total time from navigation start to the first meaningful paint of result cards.
6. Repeat the measurement five times and calculate the average time.
7. Confirm the average time is below two seconds.

**Expected Result:** Because data is embedded in data.js (no network API request is needed), results are rendered well within two seconds even on modest hardware. The application easily meets NFR4 under normal conditions. NFR5 is met because the static architecture places no shared server under concurrent load.

**Outcome:** Pass

---

### TC30 - Statistics Bar Values Match Known Dataset Distribution

| Field | Detail |
|---|---|
| Requirement(s) | FR3, NFR10 |
| Use Case | UC1 |
| Test Data | Expected values from implementation specification: 3,867 total; 2,450 rated 5; 440 awaiting inspection; 600 unrated. |

**Steps:**

1. Open index.html.
2. Read the four values displayed in the statistics bar.
3. Cross-reference against the documented dataset distribution: Total businesses = 3,867; Businesses rated 5 = 2,450; Awaiting Inspection = 440; Unrated (null) = 600.
4. Confirm each displayed value matches the corresponding expected figure exactly.

**Expected Result:** The statistics bar values match the known dataset distribution precisely. Values are derived from the live ALL_BUSINESSES array at runtime and are not hardcoded. NFR10 is supported in that the code is data-driven and maintainable.

**Outcome:** Pass

---

## 6. Test Runs

All tests were executed against version 1.0.0 of the application on Google Chrome 124, served via the local static file server. Date of testing: 6 April 2026.

| TC ID | Test Name | Notes | Requirement(s) | Status |
|---|---|---|---|---|
| TC1 | Homepage Loads and Renders All Sections | All four sections rendered. Statistics bar shows correct dataset values. | FR1, NFR1, NFR2, NFR10 | Pass |
| TC2 | Search Bar Accepts Input and Navigates to Results | URL parameter correctly passed. All FR3 fields visible on result cards. | FR1, FR2, FR3, NFR1 | Pass |
| TC3 | Empty Search Input Validation | Validation prompt displayed. No navigation occurred. | FR9, NFR8 | Pass |
| TC4 | No Results State Displayed Correctly | No-results panel shown with suggestion. Filter panel remained visible. | FR8 | Pass |
| TC5 | Filter Results by Hygiene Rating Score | Rating filter applied correctly. Active chip displayed. Count updated. | FR5, FR7 | Pass |
| TC6 | Filter Results by Business Type | Business type filter applied. Active chip displayed. Count updated. | FR6, FR7 | Pass |
| TC7 | Combined Rating and Business Type Filters Applied Simultaneously | Both filters applied simultaneously. Two chips shown. Results satisfied both criteria. | FR7 | Pass |
| TC8 | Remove an Individual Filter Using the Active Filter Chip | Type chip removed. Rating chip remained. Results expanded correctly. | FR5, FR6, FR7 | Pass |
| TC9 | Category Tile on Homepage as Alternative Entry Point | Category tile navigated to Search.html with pre-applied type filter. | FR6, NFR1 | Pass |
| TC10 | Rating Pill Links on Homepage Navigate to Filtered Results | Rating pill navigated to filtered results without text search input. | FR5, NFR1 | Pass |
| TC11 | Business Details Page Displays All Required Fields | All FR11 fields displayed. FSA graphic loaded. Explanation panel present. | FR11, FR12, FR17, NFR1 | Pass |
| TC12 | Rating Graphic Fallback When Image Fails to Load | onerror handler fired. Numeric rating shown as fallback. Page remained functional. | FR13 | Pass |
| TC13 | Awaiting Inspection Status Notice and Badge Replacement | "Awaiting Inspection" label shown. No numeric rating. Purple notice panel displayed. | FR4, FR14, FR16 | Pass |
| TC14 | New Rating Pending Notice Displayed Correctly | Yellow notice panel shown. Existing rating remained visible alongside notice. | FR15 | Pass |
| TC15 | Exempt Status Notice Displayed Correctly | Light blue notice panel shown. No numeric rating displayed for exempt business. | FR16 | Pass |
| TC16 | Rating Guide Page Contains Full Content | All six rating cards and Special Statuses section rendered without errors. | FR17 | Pass |
| TC17 | Rating Guide Accessible from Three Entry Points | All three entry points navigated correctly to Rating-Guide.html. | FR17, NFR1 | Pass |
| TC18 | Back to Results Preserves Search Query and Filter State | Search term and filter preserved via URL parameters. Identical result list shown. | UC2 Step 6 | Pass |
| TC19 | All Features Accessible Without Login or Registration | No authentication prompt appeared on any page. All features immediately accessible. | FR10 | Pass |
| TC20 | Responsive Layout at Mobile Viewport (390 px) | Single-column layout correct at 390 px. Mobile nav toggle functional. No horizontal scroll. | NFR2, US8 | Pass |
| TC21 | Responsive Layout at Tablet Viewport (768 px) | Intermediate layout correct at 768 px. No broken layouts or overflowing content. | NFR2 | Pass |
| TC22 | Full Keyboard Navigation Without a Mouse | Skip link functional. All interactive elements reachable. Focus indicators visible. | NFR3 | Pass |
| TC23 | Mobile Navigation ARIA State Management | ARIA attributes toggled correctly. Escape key and backdrop click both managed focus. | NFR3 | Pass |
| TC24 | Colour Contrast - WCAG 2.1 Level AA Compliance | No contrast failures reported by WAVE. All badges use colour and text together. | NFR3 | Pass |
| TC25 | Image Alternative Text Audit | All decorative images have aria-hidden and empty alt. Informative images have descriptive alt text. | NFR3 | Pass |
| TC26 | Graceful Error State When Data Initialisation Fails | Error panel displayed with user-friendly message and Retry button. No raw errors shown. | NFR7 | Pass |
| TC27 | Input Sanitisation - XSS Attack Prevention | Script tag was never executed. Input rendered as escaped text or produced no-results state. | NFR8 | Pass |
| TC28 | Navigation Bar Functions Correctly on All Pages | All four nav links functional on all pages. Consistent header styling across pages. | NFR1, NFR10 | Pass |
| TC29 | Search Results Rendered Within Two Seconds | Results rendered in under 300 ms on local server. Comfortably within the 2-second threshold. | NFR4, NFR5 | Pass |
| TC30 | Statistics Bar Values Match Known Dataset Distribution | Statistics bar values matched documented dataset distribution exactly. | FR3, NFR10 | Pass |

---

## 7. Requirements Traceability Matrix

The Requirements Traceability Matrix below maps every functional requirement (FR1-FR17) and non-functional requirement (NFR1-NFR10) from the Software Requirements Specification to its source use case and to the test case(s) that validate it. This confirms that every requirement has been addressed by at least one test case, and that the test suite provides complete coverage of the specification.

| Use-Case ID | Requirement ID | Requirement Summary | Test Case(s) | Status |
|---|---|---|---|---|
| UC1 | FR1 | Search bar on homepage accepting name, postcode, or address | TC1, TC2 | Pass |
| UC1 | FR2 | System queries dataset using the submitted search term | TC2, TC4 | Pass |
| UC1 | FR3 | Results list shows name, address, type, rating, and date for each business | TC2, TC11 | Pass |
| UC1 | FR4 | "Awaiting Inspection" shown in place of a numeric rating in results | TC13 | Pass |
| UC1 | FR5 | Filter results by hygiene rating score (0-5) | TC5, TC7, TC10 | Pass |
| UC1 | FR6 | Filter results by business type category | TC6, TC7, TC9 | Pass |
| UC1 | FR7 | Apply rating and type filters simultaneously; results update to reflect all active filters | TC7, TC8 | Pass |
| UC1 | FR8 | Clear no-results message displayed with suggestion to broaden the search | TC4 | Pass |
| UC1 | FR9 | Validate and prompt the user if the search input is empty or invalid | TC3 | Pass |
| UC1, UC2 | FR10 | All features accessible without login, registration, or account creation | TC19 | Pass |
| UC2 | FR11 | Business details page displays all required dataset fields | TC11 | Pass |
| UC2 | FR12 | Official FSA rating graphic loaded and displayed from the dataset URL | TC11 | Pass |
| UC2 | FR13 | Numeric rating displayed as fallback if the graphic fails to load | TC12 | Pass |
| UC2 | FR14 | Clear notice displayed when business is marked Awaiting Inspection | TC13 | Pass |
| UC2 | FR15 | Notice displayed when a new rating is pending publication | TC14 | Pass |
| UC2 | FR16 | Rating status (Rated, Exempt, Awaiting Inspection) shown in plain language | TC13, TC15 | Pass |
| UC2 | FR17 | Rating explanation section covering scores 0-5, accessible from multiple pages | TC11, TC16, TC17 | Pass |
| UC1, UC2 | NFR1 | Three-click access to any information from the homepage | TC1, TC2, TC9, TC10, TC17 | Pass |
| UC1, UC2 | NFR2 | Fully responsive layout on mobile, tablet, and desktop | TC20, TC21 | Pass |
| UC1, UC2 | NFR3 | WCAG 2.1 Level AA accessibility (contrast, keyboard, ARIA, alt text) | TC22, TC23, TC24, TC25 | Pass |
| UC1 | NFR4 | Search results rendered within two seconds under normal conditions | TC29 | Pass |
| UC1 | NFR5 | Capable of supporting 100+ concurrent users without degradation | TC29 (static architecture) | Pass |
| UC1, UC2 | NFR6 | 99% availability during operating hours (06:00-23:00 GMT) | N/A | N/A |
| UC1 | NFR7 | Graceful handling of data failures with user-friendly error message and Retry button | TC26 | Pass |
| UC1 | NFR8 | All user inputs validated and sanitised to prevent XSS and injection attacks | TC3, TC27 | Pass |
| UC1, UC2 | NFR9 | All pages served over HTTPS in production deployment | N/A | N/A |
| UC1, UC2 | NFR10 | Modular, clearly commented, maintainable code (0 JSLint warnings) | TC28, TC30, code review | Pass |

NFR6 (availability) and NFR9 (HTTPS) are marked N/A because they are deployment-environment concerns rather than application code concerns. NFR6 availability depends on the hosting provider chosen at deployment time, which falls outside the scope of this development phase. NFR9 requires an SSL certificate to be configured on the server, which is not within the remit of the static client-side application itself. Both requirements are noted and would be verified separately during a formal deployment acceptance test.

---

## 8. Summary and Conclusions

| Metric | Value |
|---|---|
| Total test cases | 30 |
| Tests passed | 28 |
| Tests not applicable (N/A) | 2 |
| Tests failed | 0 |
| Functional requirements covered | 17 / 17 (100%) |
| Non-functional requirements covered | 8 / 10 (100% in scope) |
| Use cases covered | 2 / 2 (100%) |

All thirty test cases were executed successfully against version 1.0.0 of the Bristol Food Hygiene Ratings application. Every functional requirement was validated and passed. The two N/A entries (NFR6 and NFR9) are not failures - they represent requirements that are outside the scope of client-side application testing and would be verified separately during deployment.

The test suite confirms that the application correctly handles all normal user journeys through UC1 (Search and Filter) and UC2 (View Detailed Business Information), as well as every documented variation including empty search input, zero-result states, awaiting inspection notices, new rating pending notices, exempt status notices, and the rating graphic fallback on image load failure.

Accessibility testing (TC22-TC25) confirmed compliance with WCAG 2.1 Level AA across all four pages, including correct ARIA state management in the mobile navigation, visible focus indicators for keyboard users, sufficient colour contrast ratios throughout, and appropriate alternative text on all images.

The application is considered ready for submission. No defects or blocking issues were identified during testing.
