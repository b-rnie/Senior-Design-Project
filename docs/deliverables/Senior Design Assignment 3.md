# **HIGH-LEVEL SYSTEM DIAGRAM** 

<u>Schematic Diagram</u> 



**Client Presentation Layer** : The front End is a single React Native mobile app that serves both user bases. The Adopter view handles the swipeable video feed and filtering. The Shelter view allows staff to record and upload videos directly from their phones. 

**Application & API Layer** : The backend is built on Node.js. It acts as our core API gateway, routing requests and handling business logic. It also contains our AI Intake Controller, which manages the data handoff between the media storage location and the LLM. 

**External Cloud Services** : We integrate third-party APIs like Supabase Auth to manage secure JWT session tokens. Cloudinary serves as our media host and CDN, keeping massive video files off our Node server. Gemini 2.5 Flash acts as our multimodal AI engine to analyze the videos and extract behavioral data. 

**Data Persistence Layer** : We use a PostgreSQL database (hosted via Supabase) to handle all relational data, securely linking Users, Shelters, Animals, and Adoption Applications. 

### **Data Flow Pipelines** 

### **Pipeline 1: B2B In-App Intake Flow** 

1. A shelter worker records an animal video in the mobile app and taps upload. 

2. The app authenticates the user's session directly via Supabase Auth. 

3. To prevent backend crashes from media files, the app requests an upload URL from 

3 

Node.js, then uploads the video directly to Cloudinary. 

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

Finally, PostgreSQL is selected as our database because there is familiarity in using it with some team members. It can provide reliable responses, future scalability and relational data support through ACID compliant transactions. It will be capable of managing users, video content, metadata, adoption status’, 

4 

recommendations, and more for the app. To ensure that development costs remains lower or free, we will host PostgreSQL with a DBaaS like Supabase or Render. 

Third party APIs will include services for our AI integration using Gemini’s API that can be integrated within the backend for the AI video extraction behavioral tagging for our B2B client’s. We also justify this choice because Gemini offers good free tiers for developers. Additionally, other third party APIs like Cloudinary could be used for video hosting and CDN delivery. Since video streaming can easily rack up costs too, using this API should protect our team from unexpected bills from testing or development for now. Finally, we will not reinvent the wheel and will be using Supabase Auth API for a secure and free authentication service for managing session tokens and user logins than building security services from scratch. 

# **UI/UX WIREFRAMES & USER FLOWS** 



<!-- Start of picture text -->
N /<br>\ PetLoo<br>/<br>\<br>_—/<br><!-- End of picture text -->



<!-- Start of picture text -->
€ Q Search Search<br>Piven .<br>O history 2 .<br>O history 3 5<br><!-- End of picture text -->



<!-- Start of picture text -->
/<br>Va<br>Va<br>Va<br>/\<br>y fo<br>fo<br>JL<br>fo<br>Deepipton ><br><!-- End of picture text -->



<!-- Start of picture text -->
Likes € Pet Profile a<br>NJ<br>\VA<br>Pet Name \<br>\ /<br>J\<br>J \<br>/\<br>/\<br>y \<br>J \<br>Pet et N Name VA \<br>\/ <...> \\<br>Pet Name contact) @<br>Pet Name PetinfoInputted Description<br>|<br>a<br><!-- End of picture text -->



<!-- Start of picture text -->
><br>S<br>/<br>\\ J/<br>NZ J<br>oN<br>Lo \<br>y, \\<br>4 ‘<br><!-- End of picture text -->

5 

6 

# **REQUIREMENTS TEST MATRIX** 

|Requirement|Requirement<br>Description|**Verification Method**|Test Scenario|Expected Results|
|---|---|---|---|---|
|FR-AUTH-01|Shelter Login|**Unit Test + Input Inspection**|Enter an<br>unregistered<br>email and<br>password, then<br>submit the login<br>form.|The system denies<br>access and<br>displays an<br>"Invalid<br>Credentials"<br>error<br>message.|
|FR-AUTH-02|User account<br>creation|**Unit Test + UI Inspection**|Enter a valid,<br>unregistered<br>email and<br>password, then<br>submit the<br>registration<br>form.|The system<br>successfully<br>creates a new user<br>account.|
|FR-AUTH-03|Password<br>recovery|**Unit Test + UI Inspection**|Select "Forgot<br>Password" for<br>an existing<br>account and<br>follow the<br>recovery<br>instructions.|The system<br>provides a<br>password recovery<br>process through<br>the registered<br>email or phone<br>number.|
|FR-AI-01|AI-generated pet<br>tags|Unit Test + Input Inspection|Upload a valid<br>pet video<br>and<br>process it<br>through the|When the API<br>returns a<br>successful<br>200 OK<br>response, the|



7 

||||Gemini<br>API|system<br>displays at<br>least three<br>editable<br>behavioral<br>tags.|
|---|---|---|---|---|
|FR-AI-02|AI video content<br>moderation|**Input Inspection**|Upload a video<br>containing<br>inappropriate,<br>harmful, or non-<br>pet-related<br>content and<br>submit it for AI<br>review.|The system<br>identifies<br>questionable<br>content and flags<br>the video for<br>further review<br>before publication.|
|FR-AI-03|AI chatbot|**Unit Test + Input Inspection**|Open the<br>chatbot and ask<br>a question about<br>a pet's breed or<br>species.|The chatbot<br>accepts the<br>question and<br>provides a relevant<br>response about the<br>animal.|
|FR-AI-04<br>FR-FEED-01|AI tag validation<br>Vertical video|**Unit Test**<br>**Unit Test + UI Inspection**|Submit three AI-<br>generated tags<br>that fail<br>validation<br>Open the|The system<br>informs the user<br>that no tags were<br>verified and allows<br>them to add tags<br>manually.<br>The current video|



8 

||discovery feed||discovery feed<br>and swipe<br>vertically to the<br>next pet video.|unloads, and the<br>next video plays<br>automatically.|
|---|---|---|---|---|
|FR-FEED-02|View pet profile|**UI Inspection**|Select a pet<br>profile from the<br>discovery feed.|The system<br>displays the<br>selected pet's<br>information.|
|FR-FEED-03|Responsive<br>mobile interface|**UI Inspection**|Open PetLoop<br>on a phone and<br>tablet with<br>different screen<br>sizes.|The interface<br>automatically<br>adjusts to fit each<br>device's screen.|



9 

|FR-<br>INTERACT-0<br>1|Save favorite<br>pets|**Unit Test + UI Inspection**|Log in and<br>swipe right on a<br>pet video to<br>save it.|The system saves<br>the pet to the user's<br>favorites database<br>and returns a 201<br>Created response.|
|---|---|---|---|---|
|FR-<br>INTERACT-0<br>2|View saved pets|Unit Test + UI Inspection|Save a pet and<br>open the saved<br>pets section.|The system<br>displays the user's<br>previously saved<br>pets.|
|FR-<br>INTERACT-0<br>3|Report<br>misleading pet<br>listings|Unit Test + UI Inspection|Select the<br>Report button<br>on a misleading<br>pet listing,<br>complete the<br>report form, and<br>submit it.|The system<br>records the report<br>and sends it to<br>administrators for<br>review.|



10 

|FR-<br>INTERACT-0<br>4|View shelter<br>contact<br>information|Unit Test + UI Inspection|Open a pet<br>profile and<br>locate the<br>shelter's contact<br>details.|The system<br>displays the<br>shelter's name,<br>phone number,<br>email, and address.|
|---|---|---|---|---|
|NFR-<br>INTERACT-0<br>5|Administrator<br>content review<br>notification|Unit Test + UI Inspection|Have a staff<br>member upload<br>a video, then<br>open the<br>administrator's<br>account.|The administrator<br>receives a<br>notification about<br>videos awaiting<br>review.|
|NFR-<br>INTERACT-0<br>6|Search pets by<br>tags|UI Inspection + Functionality<br>Test|Search for a tag<br>such as<br>#smalldogs|The system returns<br>videos relevant to<br>the searched tag|
|NFR-<br>INFRA-01|Video streaming<br>performance|Load & Benchmark Testing|Request a video<br>from the<br>discovery feed<br>using a standard<br>mobile<br>connection|The video<br>response time is<br>less than 600<br>milliseconds.|
|NFR-<br>INFRA-02|Pet availability<br>status|Unit Test + UI Inspection|Change a pet’s<br>availability<br>status and check<br>the displayed|The system checks<br>for updates every<br>minute and<br>displays the pet’s|



11 

||||status.|current<br>availability.|
|---|---|---|---|---|
|NFR-<br>INFRA-03|User data<br>security|Security Audit + Inspection|Attempt to<br>access protected<br>user data<br>without<br>authorization.|The system denies<br>access and logs the<br>unauthorized<br>attempt.|
|FR-ALGO-01|Personalized<br>video<br>recommendations|Integration Test + UI<br>Inspection|Set user<br>preferences or<br>interact with pet<br>profiles, then<br>open the<br>discovery feed.|The system uses<br>the user's<br>preferences and<br>interactions to<br>select pets for the<br>feed.|



12 

|FR-ALGO-02|Personalized<br>video<br>recommendations|Automated Integration Test|Like a pet video<br>and allow the<br>recommendation<br>algorithm to<br>process the<br>interaction|The system<br>recommends more<br>videos similar to<br>those more<br>previously liked|
|---|---|---|---|---|
|FR-<br>INGEST-01|Upload pet<br>videos|Unit Test + UI Inspection|Upload a valid<br>pet video to a<br>pet profile|The system saves<br>the video to the<br>selected pet's<br>profile.|
|FR-<br>INGEST-02|Cloud video<br>storage|Automated Integration Test|Upload a pet<br>video and check<br>the cloud<br>storage system.|The video is saved<br>in cloud storage<br>and remains<br>available until the<br>post is deleted.|



13 

|FR-<br>INGEST-03|Video format and<br>size validation|Unit Test|Attempt to<br>upload a video<br>in an<br>unsupported<br>format or larger<br>than 500 MB.|The system rejects<br>videos that are not<br>MP4/MOV or<br>exceed 500 MB.|
|---|---|---|---|---|
|FR-<br>INGEST-04|Required video<br>for pet profiles|Input Inspection|Attempt to<br>submit a pet<br>profile without<br>uploading a<br>video.|The system blocks<br>submission and<br>displays a message<br>requiring a video.|



# **INITIAL SCHEDULE & OPERATIONAL PROCESS LAYOUT** Initial project milestone timeline 

**Milestone 1 – Project Brand:** We drafted our initial project ideas and decided on one- pet adoption. We then thought about how we can make our idea unique, separate, and more engaging than the modern adoption processes, resulting in the unification of traditional adoption systems with social media. We chose to do a TikTok inspired app featuring scrollable videos to increase engagement with potential adopters while making the online environment 

14 

fun for both parties. Our target audience is primarily 20s to 50s, as most of our users would likely be users that are very familiar with social media while also having income to afford a pet. In addition, our team talked about what roles, skills, and other assets we have and applied them to various roles and responsibilities. 

**Milestone 2 – Technical Specifications:** We compiled a list of features, action-items, policies, etc., regarding the ideal finalized project outcome. Functionality is the first-most list of features to be thought of: creating a profile, uploading videos, database structure, etc. After functionality, we come up with things in the middle layer that are essential to think about. This includes security measures, data privacy, marketing, profit margins, etc. Lastly, we came up with features that would be nice to have that would help make our application more attractive, such as custom gestures for efficiency or UI details. We research into which tech stack makes the most sense for the project alongside the confidence of the team to confirm our tech stack. 

**Milestone 3 – Initial Draft Feedback and Refinement:** Exposing our project for review allows us to acknowledge our strong points, weak points, and overall extra feedback for our project before developing a prototype. Ideally, this would be good from adoption centers, but we had a peer group review our initial draft. We received critiques that allowed us to rework some of our user-case scenarios as well as modify/add/remove any necessary features to strengthen our foundation. This mainly included adding fallback procedures for our functionality requirements and changing priority statuses. 

**Milestone 4 – Developing a Minimal Viable Product (MVP):** Once we have confirmed the foundation of our brand, requirements, and specifications, we start developing a prototype for our app in the rawest form, focusing mostly on requirements. This will primarily be used for visualization and testing demonstration purposes. Allowing a product to be viewed and tested makes room for a lot of potential improvement, reworks, and refinement from the team as well as public review. 

**Milestone 5 – Building out PetLoop:** This is where most of the app development comes in. Using our MVP, feedback, and finalized requirements and features, we develop our app: UI, front-end, back-end, database, algorithms, etc. This stage represents multiple sub-milestones that will likely cycle through a series of developing certain stages of the app, forwarding it for review, and adjusting as needed. 

**Milestone 6 – QA and Beta Testing:** Once the application is complete, it will be handled with basic internal team testing first. Following this would be either peer or public review for any final critiques, bugs, or any other concerns. 

**Milestone 7 – Launch:** Launching our application! Our team would still need to post-monitor activity following the deployment for any consumer difficulty as well as monitor any live systems affecting the app. 

# Workflow Methodologies: 

**Cycles:** Our check-in cycle occurs weekly, focusing on the next piece of the project timeline with each member having deliverables to share. These deliverables can range from simple verbal confirmation on what the team member is working on to code blocks, formulated algorithms, and more. While the focus is primarily on progression, our weekly cycle also includes any ideas, compromises, and other relevant information to share. These cycles are 

15 

usually documented on our discord server, organized by different channels, and led by the team lead. 

**Meeting Cadence:** We typically have sporadic meetings depending on what the current objective is that needs to be done. Recently, we have been doing an initial check in during the beginning of the week that covers what needs to be done, dividing the responsibilities, and addressing any questions and/or concerns. We then have a mid-check in where members can address any issues they are having, any adjustments to be made, etc. Lastly, we have our final check in to review our piece with everyone’s work consolidated before submitting our work and moving on to the next piece in our timeline. 

**Communication Channels:** We have a dedicated discord server to discuss anything pertaining to the project. In addition, we have alternate forms of secondary communication for higher priority communication. For assignment collaboration documents and files, this is mainly done through cloud sharing the files via student emails. Our team lead is usually in charge of file sharing and granting authorization access. 

