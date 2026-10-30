# **HIGH-LEVEL SYSTEM DIAGRAM** 

Schematic Design: \
<img width="445" height="1007" alt="image" src="https://github.com/user-attachments/assets/9c6fe8f5-92ae-4efc-968e-441913071136" />



**Client Presentation Layer** : The front End is a single React Native mobile app that serves both user bases. The Adopter view handles the swipeable video feed and filtering. The Shelter view allows staff to record and upload videos directly from their phones. 

**Application & API Layer** : The backend is built on Node.js. It acts as our core API gateway, routing requests and handling business logic. It also contains our AI Intake Controller, which manages the data handoff between the media storage location and the LLM. 

**External Cloud Services** : We integrate third-party APIs like Supabase Auth to manage secure JWT session tokens. Cloudinary serves as our media host and CDN, keeping massive video files off our Node server. Gemini 2.5 Flash acts as our multimodal AI engine to analyze the videos and extract behavioral data. 

**Data Persistence Layer** : We use a PostgreSQL database (hosted via Supabase) to handle all relational data, securely linking Users, Shelters, Animals, and Adoption Applications. 

### **Data Flow Pipelines** 

### **Pipeline 1: B2B In-App Intake Flow** 

1. A shelter worker records an animal video in the mobile app and taps upload. 

2. The app authenticates the user's session directly via Supabase Auth. 

3. To prevent backend crashes from media files, the app requests an upload URL from Node.js, then uploads the video directly to Cloudinary. 

4. Once uploaded, Node.js takes the new Cloudinary media URL and sends it to the Gemini API, prompting it to extract physical and behavioral traits from the video. 

5. Gemini returns a structured JSON object which the backend then writes this metadata, along with the video URL to the PostgreSQL database. 

### **Pipeline 2: B2C Video Discovery Flow** 

1. An adopter opens the app, which sends a request to the Node.js backend for a batch of feed results based on their set filters. 

2. The backend queries the PostgreSQL database for matching animals that the user hasn't seen yet. 

3. The database returns the animal metadata and the Cloudinary video URLs. 

4. The mobile app uses those URLs to stream the videos directly from the Cloudinary CDN. This ensures speedy playback for a smooth swiping experience without putting too much bandwidth concerns on the Node.js server. 

## **TECHNOLOGY STACK JUSTIFICATION** 

React Native was selected because it would allow for a single repository for the application code, supporting primary initial iOS app development and future Android platforms if needed. This will save time and eliminate tech debt as well to have a single codebase for development rather than separate options for iOS and Android support. We also justify our choice because our team has Windows devices that do not support Xcode options. By using React Native with the Expo EAS cloud API, our team can compile an iOS app on free cloud servers rather than needing to buy Mac devices for Xcode development. Finally, several members additionally have previous experience with Native framework already. 

Node.js was chosen as the backend framework for our development because it is an event driven architecture that handles and supports the API & asynchronous request components required of our app. Since our app will combine real-time streaming, AI integration, and other video services, Node.js will allow our team to use the same language Typescript as our frontend to make development manageable compared to using another backend that forces some members to learn new programming languages like C# found in a ASP.NET backend. 

For our programming languages, React Native and Node.js both support TypeScript. By utilizing TypeScript in our code we can improve our code quality by reducing runtime errors which TypeScript handles better than JavaScript by adding more guardrails for code with strict type-checking. Additionally, using one language across the entire stack simplifies development and understanding across the team for seamless context switching. 

Finally, PostgreSQL is selected as our database because there is familiarity in using it with some team members. It can provide reliable responses, future scalability and relational data support through ACID compliant transactions. It will be capable of managing users, video content, metadata, adoption status’, recommendations, and more for the app. To ensure that development costs remains lower or free, we will host PostgreSQL with a DBaaS like Supabase or Render. 

Third party APIs will include services for our AI integration using Gemini’s API that can be integrated within the backend for the AI video extraction behavioral tagging for our B2B client’s. We also justify this choice because Gemini offers good free tiers for developers. Additionally, other third party APIs like Cloudinary could be used for video hosting and CDN delivery. Since video streaming can easily rack up costs too, using this API should protect our team from unexpected bills from testing or development for now. Finally, we will not reinvent the wheel and will be using Supabase Auth API for a secure and free authentication service for managing session tokens and user logins than building security services from scratch. 

# **UI/UX WIREFRAMES & USER FLOWS** 

<INSERT PHOTOS HERE>

# **REQUIREMENTS TEST MATRIX** 

|Requirement|Requirement Description|**Verification Method**|Test Scenario|Expected Results|
|---|---|---|---|---|
|FR-AUTH-01|Shelter Login|**Unit Test + Input Inspection**|Enter an unregistered email and password, then submit the login form.|The system denies access and displays an "Invalid Credentials" error message.|
|FR-AUTH-02|User Account Creation|**Unit Test + UI Inspection**|Enter a valid, unregistered email and password, then submit the registration form.|The system successfully creates a new user account.|
|FR-AUTH-03|Password Recovery|**Unit Test + UI Inspection**|Select "Forgot Password" for an existing account and follow the recovery instructions.|The system provides a password recovery process through the registered email or phone number.|
|FR-AI-01|AI-Generated Pet Tags|**Unit Test + Input Inspection**|Upload a valid pet video and process it through the Gemini API |When the API returns a successful 200 OK response, the system displays at least three editable behavioral tags|
|FR-AI-02|AI Video Content Moderation|**Input Inspection**|Upload a video containing inappropriate, harmful, or non-pet-related content and submit it for AI review.|The system identifies questionable content and flags the video for further review before publication.|
|FR-AI-03|AI Chatbot|**Unit Test + Input Inspection**|Open the chatbot and ask a question about a pet's breed or species.|The chatbot accepts the question and provides a relevant response about the animal.|
|FR-AI-04|AI Tag Validation|**Unit Test**|Submit three AI-generated tags that fail validation|The system informs the user that no tags were verified and allows them to add tags manually.|
|FR-FEED-01|Vertical Video Discovery Feed|**Unit Test + UI Inspection**|Open the discovery feed and swipe vertically to the next pet video.|The current video unloads, and thenext video plays automatically.|
|FR-FEED-02|View Pet Profile|**UI Inspection**|Select a pet profile from the discovery feed.|The system displays the selected pet's information.|
|FR-FEED-03|Responsive Mobile Interface|**UI Inspection**|Open PetLoop on a phone and tablet with different screen sizes.|The interface automatically adjusts to fit each device's screen.|
|FR-INTERACT-01|Save Favorite Pets|**Unit Test + UI Inspection**|Log in and swipe right on a pet video to save it.|The system saves the pet to the user's favorites database and returns a 201 Created response.|
|FR-INTERACT-02|View Saved Pets|**Unit Test + UI Inspection**|Save a pet and open the saved pets section.|The system displays the user's previously saved pets.|
|FR-INTERACT-03|Report Misleading Pet Listings|**Unit Test + UI Inspection**|Select the Report button on a misleading pet listing, complete the report form, and submit it.|The system records the report and sends it to administrators for review.|
|FR-INTERACT-04|View Shelter contact information|**Unit Test + UI Inspection**|Open a pet profile and locate the shelter's contact details.|The system displays the shelter's name, phone number, email, and address.|
|NFR-INTERACT-05|Administrator Content Review Notification|**Unit Test + UI Inspection**|Have a staff member upload a video, then open the administrator's account.|The administrator receives a notification about videos awaiting review.|
|NFR-INTERACT-06|Search Pets by tags|**UI Inspection + Functionality Test**|Search for a tag such as #smalldogs|The system returns videos relevant to the searched tag.|
|NFR-INFRA-01|Video Streaming Performance|**Load & Benchmark Testing**|Request a video from the discovery feed using a standard mobile connection.|The video response time is less than 600 milliseconds.|
|NFR-INFRA-02|Pet Availability Status|**Unit Test + UI Inspection**|Change a pet’s availability status and check the displayed status.|The system checks for updates every minute and displays the pet’s current availability.|
|NFR-INFRA-03|User Data Security|**Security Audit + Inspection**|Attempt to access protected user data without authorization.|The system denies access and logs the unauthorized attempt.|
|FR-ALGO-01|Personalized Video Recommendations|**Integration Test + UI Inspection**|Set user preferences or interact with pet profiles, then open the discovery feed.|The system uses the user's preferences and interactions to select pets for the feed.|
|FR-ALGO-02|Personalized Video Recommendations|**Automated Integration Test**|Like a pet video and allow the recommendation algorithm to process the interaction|The system recommends more videos similar to those more previously liked.|
|FR-INGEST-01|Upload Pet Videos|**Unit Test + UI Inspection**|Upload a valid pet video to a pet profile|The system saves the video to the selected pet's profile.|
|FR-INGEST-02|Cloud Video Storage|**Automated Integration Test**|Upload a pet video and check the cloud storage system.|The video is saved in cloud storage and remains available until the post is deleted.|
|FR-INGEST-03|Video Format and Size Validation|**Unit Test**|Attempt to upload a video in an unsupported format or larger than 500 MB.|The system rejects videos that are not MP4/MOV or exceed 500 MB.|
|FR-<br>INGEST-04|Required Video for Pet Profiles|**Input Inspection**|Attempt to submit a pet profile without uploading a video.|The system blocks submission and displays a message requiring a video.|



# **INITIAL SCHEDULE & OPERATIONAL PROCESS LAYOUT** Initial project milestone timeline 

**Milestone 1 – Project Brand:** We drafted our initial project ideas and decided on one- pet adoption. We then thought about how we can make our idea unique, separate, and more engaging than the modern adoption processes, resulting in the unification of traditional adoption systems with social media. We chose to do a TikTok inspired app featuring scrollable videos to increase engagement with potential adopters while making the online environment fun for both parties. Our target audience is primarily 20s to 50s, as most of our users would likely be users that are very familiar with social media while also having income to afford a pet. In addition, our team talked about what roles, skills, and other assets we have and applied them to various roles and responsibilities. 

**Milestone 2 – Technical Specifications:** We compiled a list of features, action-items, policies, etc., regarding the ideal finalized project outcome. Functionality is the first-most list of features to be thought of: creating a profile, uploading videos, database structure, etc. After functionality, we come up with things in the middle layer that are essential to think about. This includes security measures, data privacy, marketing, profit margins, etc. Lastly, we came up with features that would be nice to have that would help make our application more attractive, such as custom gestures for efficiency or UI details. We research into which tech stack makes the most sense for the project alongside the confidence of the team to confirm our tech stack. 

**Milestone 3 – Initial Draft Feedback and Refinement:** Exposing our project for review allows us to acknowledge our strong points, weak points, and overall extra feedback for our project before developing a prototype. Ideally, this would be good from adoption centers, but we had a peer group review our initial draft. We received critiques that allowed us to rework some of our user-case scenarios as well as modify/add/remove any necessary features to strengthen our foundation. This mainly included adding fallback procedures for our functionality requirements and changing priority statuses. 

**Milestone 4 – Developing a Minimal Viable Product (MVP):** Once we have confirmed the foundation of our brand, requirements, and specifications, we start developing a prototype for our app in the rawest form, focusing mostly on requirements. This will primarily be used for visualization and testing demonstration purposes. Allowing a product to be viewed and tested makes room for a lot of potential improvement, reworks, and refinement from the team as well as public review. 

**Milestone 5 – Building out PetLoop:** This is where most of the app development comes in. Using our MVP, feedback, and finalized requirements and features, we develop our app: UI, front-end, back-end, database, algorithms, etc. This stage represents multiple sub-milestones that will likely cycle through a series of developing certain stages of the app, forwarding it for review, and adjusting as needed. 

**Milestone 6 – QA and Beta Testing:** Once the application is complete, it will be handled with basic internal team testing first. Following this would be either peer or public review for any final critiques, bugs, or any other concerns. 

**Milestone 7 – Launch:** Launching our application! Our team would still need to post-monitor activity following the deployment for any consumer difficulty as well as monitor any live systems affecting the app. 

# Workflow Methodologies: 

**Cycles:** Our check-in cycle occurs weekly, focusing on the next piece of the project timeline with each member having deliverables to share. These deliverables can range from simple verbal confirmation on what the team member is working on to code blocks, formulated algorithms, and more. While the focus is primarily on progression, our weekly cycle also includes any ideas, compromises, and other relevant information to share. These cycles are usually documented on our discord server, organized by different channels, and led by the team lead. 

**Meeting Cadence:** We typically have sporadic meetings depending on what the current objective is that needs to be done. Recently, we have been doing an initial check in during the beginning of the week that covers what needs to be done, dividing the responsibilities, and addressing any questions and/or concerns. We then have a mid-check in where members can address any issues they are having, any adjustments to be made, etc. Lastly, we have our final check in to review our piece with everyone’s work consolidated before submitting our work and moving on to the next piece in our timeline. 

**Communication Channels:** We have a dedicated discord server to discuss anything pertaining to the project. In addition, we have alternate forms of secondary communication for higher priority communication. For assignment collaboration documents and files, this is mainly done through cloud sharing the files via student emails. Our team lead is usually in charge of file sharing and granting authorization access. 

