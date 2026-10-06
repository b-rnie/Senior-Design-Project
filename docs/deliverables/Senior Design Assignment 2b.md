# Assignment 2b: Top-Down Requirements & Specifications
Renee Amaya, Jennifer Le, Benny Pham, Miranda Salazar

School of Computing, Computer Science, Wichita State University

CS-598-14146 Senior Design Project 1

 Cody Farlow

October 3, 2026

Hierarchical top-down system decomposition

Domains (Category)

- **Identity & Access** **(AUTH):** Responsible for secure authentication, authorization, and session management for both B2B shelter accounts and B2C user profiles.

- **Media Ingestion** **(INGEST):** Responsible for securely handling raw, short-form video file uploads from shelter staff and storing them in cloud storage buckets.

- **AI Processing Pipeline** **(AI):** Responsible for interfacing with generative AI to process uploaded videos and automatically extract key features and aspects. 

- **Discovery Feed** **(FEED):** Responsible for rendering the mobile first, full screen vertical video user interface and managing active video playback.

- **User Interaction** **(INTERACT):** Responsible for handling client-side gesture events (saving, skipping, swiping) and managing the user’s personal saved pet database.

- **Recommendation Engine** **(ALGO):** Responsible for tracking interaction telemetry such as watch times and interests and algorithmically curating the feed queue to align with user preferences.

- **Core Infrastructure & Streaming** **(INFRA):** Responsible for ensuring video streaming efficiency, content delivery network routing, and overall system performance and security.



| # **Key** **[Type]-[Category]-[Number]**
 | # **Domain**
 | # **User Story & Specification**
 | # **MVP Scope**
 | # **Verification Method**
 |
| :--- | :--- | :--- | :--- | :--- |
| # FR-AUTH-01
 | # Identity & Access
 | # Story: As a shelter staff member, I want to securely log in so that I can access the B2B intake dashboard.
# 
# Specification: Enforce firebase authentication with standard email/password validation and secure token generation.
**Acceptance Criteria:****Given** an unregistered email is entered,**When** the user submits the login form,**Then** the system rejects access and displays an "Invalid Credentials" error message. | # Must-Have
 | # Unit Test + Input Inspection
 |
| # FR-AUTH-02
 | # Identity & Access
 | # Story: As a new user, I want to create an account so that I can use PetLoop features.
# Specifications: The system allows users to create a unique account using an email and password with an email not yet registered.
# Acceptance Criteria: 
# Given: a new user enters valid account, information, 
# When: the registration form is submitted
# Then: the system creates the user’s account.
 | # Must-Have
 | # Unit Test + UI inspection 
 |
| # FR-AUTH-03
 | # Identity & Access
 | # Story: As an existing user, I want to be able to change my password so that I can recover my account if I forget my password.
**Specifications:** System allows users to reset their password via email or phone number that is registered upon initial account creation. **Acceptance Criteria:** **Given:** An existing user forgets their password,**When:** the user clicks on "Forgot Password"**Then:** The system provides a recovery process to create a new password for the user. | # Must-Have
 | # Unit Test + UI inspection
 |
| # FR-AI-01
 | # AI Processing Pipeline
 | # Story: As a shelter staff member, I want the system to extract traits from my uploaded video so that I bypass manual data entry.
# Specification: Pass video payloads to the Gemini API to extract a minimum of 3 text-based behavioral tags.
# Acceptance Criteria:
# Given a processed video payload,
# When the Gemini API returns a successful 200 OK response,
# Then the UI populates with at least 3 editable text tags.
# 
 | # Must-Have
 | # Unit Test + Input Inspection
 |
| # FR-AI-02
 | # AI Processing Pipeline
 | # Story:
As an admin, I want to ensure that uploaded videos are pet related, safe, and do not include any inappropriate imagery or malicious software so that questionable videos are flagged before being available to users.**Specification:**The video shall be inspected by Gemini API to determine whether the video is pet-related and obeys the safety requirements. If they do not qualify, they are flagged for review.**Acceptance Criteria:**Given a video has been uploaded to the platformWhen the video is processed through the AI reviewThen Gemini API shall determine whether the video is pet-related and safe or contains harmful or malicious imageryAnd allow it to pass into the database or hold it for further review. | # Should-Have
 | # Input Inspection
 |
| # FR-AI-03
 | # AI Processing Pipeline
 | # Story: As a user, I want to learn more details about the pet breed/species so that I can better understand if the pet disposition is suitable.
**Specification:** A button/utility should appear on videos that allow users to ask questions to a chat bot to allow users to learn more about the animal.**Acceptance Criteria:****Given:** A user wants to learn more about a breed or animal**Then:** The system provides an AI chatbot that takes natural language input and provides detailed output. | # Should-Have
 | # Unit Test + Input Inspection
 |
| # FR-FEED-01
 | # Discovery Feed
 | # Story: As a prospective adopter, I want to view a vertical feed of pet videos so that I can quickly experience their personalities.
# Specification: The frontend renders a full-screen vertical view that triggers autoplay upon rendering.
# Acceptance Criteria:
# Given the user is actively viewing the feed,
# When a vertical swipe gesture is executed,
# Then the current video unloads 
# And the next video in the array auto plays immediately.
 | # Must-Have
 | # Unit Test + UI Inspection
 |
| # FR-FEED-02
 | # Discovery Feed
 | **Story:**As a prospective adopter, I want to view a pet's profile so that I can learn more about the pet.**Specification:**The system displays the selected pet's profile with its available information.**Acceptance Criteria:****Given** a user is viewing a pet in the feed,**When t**he user opens the pet's profile,**Then** the system displays the pet's information. | # Must-Have
 | # UI Inspection
 |
| # FR-FEED-03
 | # Discovery Feed
 | **Story:** As an admin, I want to make sure that the UI is compatible with a majority of mobile devices so that users can use the app on a variety of different devices. **Specification:** The screen should be responsive and fill the entire span of the mobile device's screen.**Acceptance Criteria:** **Given:** A user has multiple devices such as a tablet and phone**When:** The user opens the app**Then:** The system automatically detects what size to display the app. | # Should-Have
 | # UI Inspection
 |
| # FR-INTERACT-01
 | # User Interaction
 | # Story: As a prospective adopter, I want to swipe right on a video so that I can save the animal to my favorites list.
# Specification: A right-swipe triggers a POST request to save the pet to the user's relational database table.
# Acceptance Criteria:
# Given an authenticated user swipes right on a profile,
# When the client-side gesture completes,
# Then the backend writes the pet to the saved pets table and returns a 201 Created status.
# 
 | # Must-Have
 | # Unit Test + UI Inspection
 |
| # FR-INTERACT-02
 | # User Interaction 
 | # Story: As a prospective adopter, I want to view my saved pets so that I can return to pets I am interested in.
# Specification:
# The system displays pets that the user has previously saved.
# Acceptance Criteria:
# Given a user has saved at least one pet,
# When the user opens their saved pets,
# Then the system displays the saved pet(s).
 | # Must-Have
 | # Unit Test + UI Inspection 
 |
| # FR-INTERACT-03
 | # User Interaction
 | # Story:
As an adopter, I want to report posts that I feel are misleading or contain information that does not accurately represent the pet.**Specification:**Users can press a report button which opens a fillable prompt that logs the gathered information and sends it to moderators/administrators as a log.**Acceptance Criteria:** Given user views a post containing misinformationWhen user scrolls through postsThen user clicks the report button and fills necessary infoAnd the report log is sent to administrators. | # Should-Have
 | # Unit Test + UI Inspection
 |
| # FR-INTERACT-04
 | # User Interaction
 | # Story:
# As an adopter, I want to view a specific pet’s adoption shelter contact information so that I can contact them for more information.
**Specification:**Pet profile should contain contact information responsible for the pet, which includes the shelter’s name, number, email and physical address**Acceptance Criteria:**Given an adopter is viewing a pet’s postWhen the user clicks on the pet profileThen the shelter’s contact information should be displayed and available. | # Must-Have
 | # Unit Test + UI Inspection
 |
| # NFR-INTERACT-05
 | # User Interaction
 | # Story: As an Admin, I want to be able to review content before it is posted from my organization.
# Specifications:  A upload post triggers an alert to admin to review content being posted via notification.
# Acceptance Criteria:
# Given a staff member has uploaded a video.
# When the Admin opens the app they receive a notification reminder on their app.
# Then the system displays a notification to approve the following videos in queue.
 | # Nice-to-Have
 | # Unit Test + UI Inspection
 |
| # NFR-INFRA-01
 | # Core Infrastructure & Streaming
 | # Story: As an administrator, I want videos served efficiently so that mobile users do not experience buffering.
# Specification: Video content must be served via a Content Delivery Network ensuring optimal mobile latency.
# Acceptance Criteria:
# Given a standard mobile connection,
# When a video is requested from the feed,
# Then response time measures under 600 milliseconds.
# 
 | # Should-Have
 | # Load & Benchmark Testing
 |
| # NFR-INFRA-02
 | # Core Infrastructure & Streaming
 | # Story: As an admin, I want to make sure the database is accurate so that potential adopters can be sure of which pets are available or unavailable. 
**Specification:** Integrate a live synchronous database that tracks availability of pets **Acceptance Criteria:** **Given:** A prospective adopter wants to see if a pet is available to adopt, foster, or already adopted**When:** The user checks the status **Then:** The database updates every minute to check if the pet is available and displays status. | # Must-have
 | # Unit Test + UI Inspection
 |
| # NFR-INFRA-03
 | # Core Infrastructure & Streaming
 | # Story:
As an admin, I want to ensure that user data is safe and protected from being compromised, modified, or accessed without their approval, so that user information remains secure and private.**Specification:** The system shall protect user data from being mishandled using user authentication, encryption, and safeguarded data handling.**Acceptance Criteria:** Given user data is securely stored within the systemWhen an unauthorized user attempts to access the dataThen access to the data is deniedAnd the system logs the attempt. | # Must-Have
 | # Security Audit + Inspection
 |
| # FR-ALGO-01
 | # Recommendation Engine
 | # Story: As a prospective adopter, I want to see pets that match my interests so that I can more easily find pets I may like.
**Specification:**The system uses user preferences and interactions to help determine which pets appear in the discovery feed.**Acceptance Criteria:**Given the user has provided preferences or interacted with pet profiles,**When** the discovery feed is loaded,**Then** the system uses that information when selecting pets for the feed. | # Should-Have
 | # Integration Test + UI Inspection
 |
| # FR-ALGO-02
 | # Recommendation Engine
 | # Story: As a user, I want to view recommended videos so that I can view pets that may be closer to my wants and needs. 
**Specification:** A machine learning algorithm uses unsupervised learning and clustering to provide a personalized feed for each user based on their likes, saves, shares, etc. **Acceptance Criteria:****Given:** A user likes a video,**When:** The algorithm derives similarities from the video alongside earlier liked videos,**Then:** The user's feed will show more similar content. | # Should-Have
 | # Automated Integration Test
 |
| # FR-INGEST-01
 | # Media Ingestion
 | # Story: As a shelter staff member, I want to upload a pet video so that users can view the pet in the discovery feed.
# Specification: The system allows shelter staff to upload a short video to a pet profile.
# Acceptance Criteria: 
# Given a shelter staff member selects a valid video,
# When the video is uploaded,
# Then the system saves the video to the pet's profile.
 | # Must-Have
 | # Unit Test +UI Inspection
 |
| # FR-INGEST-02
 | # Media Ingestion
 | # Story: As an admin, I want to make sure every uploaded video is always available so that a user can always come back to it.
**Specification:** When a video is uploaded, the video gets saved to a cloud-based storage**Acceptance** **Criteria:****Given:** A user wants to upload a video**When:** The video gets uploaded**Then:** The video gets saved to cloud storage unless the user deletes the post.  | # Must-Have
 | # Automated Integration Test
 |
| # FR-INGEST-03
 | # Media Ingestion
 | # Story: As an admin, I want to make sure that the media uploaded is in MP4 or MOV format, as well as size not exceeding 500MB.
**Specification:** When a shelter or user is uploading a video, the system checks file type and size.**Acceptance** **Criteria:** **Given:** A user wants to post a video**When:** The video is pending upload**Then:** The system does validation checks to ensure the file size doesn't exceed 500MB and is the correct format. | # Should-Have
 | # Unit Test 
 |
| # FR-INGEST-04
 | # Media Ingestion
 | # Story: 
As an admin, I want to require that every pet profile upload contains at least one video so that it meets requirements and can be displayed in the user feed**Specification:**The system shall require every pet profile upload to contain at least one valid video before the profile can be submitted and broadcasted on the feed.**Acceptance Criteria:**Given a user is creating or uploading a pet profileWhen the user attempts to submit the profile upload without inputting a videoThen the system shall prevent the profile from successfully submittingAnd display a message indicating that a video must be inputted before the profile can upload. | # Should-Have
 | # Input Inspection
 |
# 
# 
# 
# 
# 
# 
# 
# 
# 
# 
# 
# 

