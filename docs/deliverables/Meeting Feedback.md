**Writing Style & Tone Constraints**

- **Pronouns:** Remove "we" entirely. Remove personal pronouns like "their" (except when referencing adopter goals in user stories).
- **Professionalism:** No contractions. Remove exclamation marks (!)
- **Conciseness:** It’s perfectly fine if a point only takes one sentence. Make it concise.
- **Ethical Language:** Do not use bold text in the ethical & legal assessment. Avoid absolute statements like "we will not do this."
- **Persona Rewording:** Adjust the customer personas to emphasize that *videos allow users to see interactions that an image cannot* before rehoming an animal.

**Document Formatting & Structure**

- **Headings & Layout:** Restate the document title. Remove the "User Journey and Interaction Scenarios" table. Do not use the color green for text or formatting.
- **Bullet Points:** Use bullets to *support* your narrative, not replace it. In general, DO NOT RECCOMEND.
- **Citations:** Include publication dates (or last published date). In-text citations are encouraged to show exactly where info is pertinent (no minimum citation count needed).
- **Tables & Figures:** Format all tables to APA standards. If a diagram is blurry, put it in the appendix or provide an APA-formatted citation with a GitHub link to a clear version.

**Project Management & Deliverables**

- **Cost Document:** Send a document breaking down costs ($50/student x 4 students, and $20/student x 4 students). Note that surplus funds can be reallocated to another team if needed.
- **Midterm & Assignment 3:** Include peer reviews and a full final requirements table in the midterm (an improved midterm section will override the previous grade). Make sure all concerns are addressed for Assignment 3.
- **Scheduling:** Identify specific dates for each milestone, spanning from next semester's MVP midterms as a possible date refence to the Final.
- **Critical Path:** Map out dependencies clearly. For example, if the database is complex and takes 3 weeks and another component relies on this and takes a 1 week, identify exactly what depends on it and what might be delayed.
- **Cody’s Tip on Meetings:** Use AI meeting notes on Discord or the built-in tool on Microsoft Teams to track discussions.

### 🧠 Part 2: Requirements & Core Concepts (Cody's Feedback)

**App Logic & Technical Specifications**

- **Define Your Terms:** Specify exactly what "standard" and "secure" mean in your specs. If you mention encryption, name the exact encryption protocol being used.
- **Top-Down Requirements:** Write your requirements using a top-down approach and clearly define your domains to help organize them.
- **Authentication & Validation (fr-auth-02):** Define exactly what an "email" means in your requirements (overlook current regex concerns). Figure out how to validate emails and phone numbers *beforehand* (e.g., sending a verification text/email).
- **Performance:** Address latency issues on the first click in your testing requirements. Users will delete the app over slow loading times.

**AI & Feed Optimization**

- **Bias & Tagging:** Do not let the feed optimization algorithm simply choose what is popular—the goal is to avoid bias. Maintain your Gemini-generated behavior tags, but assign *less weight* in the algorithm to the tags users manually choose for themselves.
- **AI Hallucinations:** You don't need to take accountability for AI hallucinations, but you *must* include a disclaimer and actively try to remove ambiguity.

**Business Model & Ethics**

- **App Purpose:** Clarify the business model. Is the app a non-profit for the public good, or is the goal to make money from shelters?
- **Advertising:** If using ads, acknowledge that 3rd party cookies are required, which means using data you cannot control.
- **The Reality of Rehoming:** Discuss deeply in the ethics section that rehoming takes time and is not easy. Be honest. Do *not* use viral mechanics to push people to adopt animals on a whim; encourage intentionality.
- **Animal Welfare:** Account for "Pets" as users of the app in the customer personas. How does this affect an anxious animal that is forced into uncomfortable situations just to get a video? Find a way to show the "best" of an animal while remaining totally honest about its negatives.
- Add government as a persona of the app as well.

**Edge Cases & Moderation**

- **User Workflows:** Define exactly what happens when someone tries to give away/rehome a cat. If multiple people interact with the listing, is it first-come, first-serve?
- **Content Moderation:** Clearly define who you *don't* want on the app (e.g., breeders, or users trying to move DMs off-platform).
- **Bad Actors:** Always design with bad actors in mind (without assuming the worst of everyone). People will upload evil/abusive videos, so you may need designated human reviewers.
- **Shelter Liability:** Decide on the boundary lines. For instance, if a shelter (kill or no-kill) isn't using the app correctly, determine that it is *not* your team's problem to solve.