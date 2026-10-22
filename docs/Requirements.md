# DETAILED REQUIREMENTS
## A. Author Portal (Author-Facing)
A simple dashboard where an author can log in and interact with their BookLeaf account.
- Authentication: Email-based login. No need for OTP or social login—simple email/password is
fine. Each author should only see their own data.
- My Books: A page showing the author’s published books with key details: title, ISBN,
genre, publication date, status, MRP, total copies sold, total royalty earned, royalty paid, and
royalty pending.
- Submit a Support Query: A form where the author can raise a ticket. The form should include: a
dropdown to select which book the query is about (or “General / Account Level”), a subject line, a
detailed description field, and optional file attachment support (UI only—actual upload is bonus, not
required).
- My Tickets: A page showing all tickets the author has submitted, with current status (Open, In
Progress, Resolved, Closed), the original query, and any responses from the admin team. Tickets
should update in real time or near-real time—if an admin responds, the author should see it without
refreshing the page.
## B. Admin Portal (Admin-Facing)
An internal dashboard for the BookLeaf operations team to manage incoming support queries.

- Ticket Queue: A list of all incoming tickets across all authors, filterable by status, category, priority,
and date. The most urgent and oldest unresolved tickets should be easy to spot.
- AI-Powered Auto-Classification: When a new ticket comes in, the system should automatically
classify it into one of these categories using an AI model: Royalty & Payments, ISBN & Metadata
Issues, Printing & Quality, Distribution & Availability, Book Status & Production Updates, or General
Inquiry. The admin should be able to override the AI’s classification if it’s wrong.
- AI-Generated Priority Score: Each ticket should get an automatic priority score (Critical / High /
Medium / Low) based on the content. For example, a “I haven’t received any royalty for 6 months”
should be flagged higher than “Can I update my author bio?” The admin should be able to override
this too.
- AI-Drafted Response: When an admin opens a ticket, the system should present an AI-generated
draft response based on the query content AND the BookLeaf Knowledge Base provided below.
The admin should be able to edit the draft before sending. The sent response should appear on
the author’s ticket view.
- Ticket Management: Admins should be able to update ticket status, add internal notes (not visible
to the author), and assign tickets to themselves.
## C. API Layer
The frontend and backend should communicate through a clean REST API. We expect:
- Properly structured endpoints with consistent naming conventions.
- Authentication middleware protecting all routes.
- Role-based access control: authors can only access their own data; admins can access everything.
- Input validation and meaningful error responses (not generic 500s).
- API documentation—either a Swagger/OpenAPI spec, a Postman collection, or a
well-structured README section explaining every endpoint.
## D. AI Integration Details
This is a critical part of the evaluation. We want to see how you think about integrating AI into a
production application, not just that you can make an API call.
1. Prompt Engineering: Your prompts should be well-structured, use the Knowledge Base context
we’ve provided, and produce responses that sound like a real BookLeaf support
representative—not generic AI fluff.
2. API Key Security: API keys must be stored in environment variables, never hardcoded or exposed
to the frontend. We will check for this.
3. Error Handling: What happens when the AI API is down or rate-limited? The system should
degrade gracefully—tickets should still be created, and admins should be able to write responses
manually.
4. Cost Awareness: Are you sending the entire ticket history + knowledge base on every call, or are
you being smart about token usage? We want to see evidence that you’ve thought about this.

5. Model Choice: You may use OpenAI, Anthropic, or any other LLM API you prefer. Justify your
choice briefly in your documentation.