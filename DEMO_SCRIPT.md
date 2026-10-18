# C3 demonstration script

Use the script below to record your own demonstration of the chatbot.

Aim for about 2–3 minutes. The handout does not require a particular length. Start the app before recording. Show the chat, the “Assignment activity: route and tools” accordion, and the relevant log entries. Use only the fictitious details below and keep `.env` closed.

## 1. Introduce the project — about 20 seconds

Say: “This is Cedar Tutoring, a fictional business assistant. It uses OpenAI and Gradio to answer business questions, collect leads, and record feedback or unanswered questions.”

Briefly show the two business documents and the notebook sections for the separate persona, instructions, router, and tools.

## 2. General questions and document grounding — about 30 seconds

Send:

> What services do you offer, and how much do they cost?

Check that the reply uses the supplied Python and AI/ML service prices. Expand “Assignment activity: route and tools” and show the `general_question` route.

Send:

> Do students receive a practice worksheet after a session?

Check that the answer uses the PDF. This detail tests that the PDF is loaded, rather than only the text summary.

## 3. Lead collection with memory — about 40 seconds

Send these messages one at a time:

> I’m interested in booking a Python tutoring session. Please collect my details for follow-up.

> My name is Sam Demo.

> My email is sam@example.com.

Check that the assistant remembers the Python request and name, asks for missing details, and calls `record_customer_interest` after it has the required information. It should acknowledge a follow-up request without confirming a booking.

Show the `lead_collection` route, tool call trace, and corresponding entry in `logs/leads.jsonl`.

## 4. Unknown question — about 25 seconds

Send:

> What is your refund policy if I cancel a session?

Check that the assistant says this policy is not in its business information and calls `record_feedback` to record the question. It must not invent a refund policy.

Show the route/tool trace and the new entry in `logs/feedback.jsonl`.

## 5. Explicit feedback — about 20 seconds

Send:

> Please record this feedback: I would like weekend tutoring sessions.

Check that the assistant routes this as `feedback`, calls `record_feedback`, and acknowledges it. Show its log entry.

## 6. Close — about 10 seconds

Say: “The notebook contains the implementation, the requirements file lists the dependencies, and the local API key is excluded from GitHub. The two tools write local JSON logs.”

Before submitting, review the recording for readable responses and traces, confirm all five cases were shown, and ensure no key or real personal information appears. Upload the project to GitHub and submit its link with the video.

These scenarios were verified with the real model on 18 October 2026. The notebook retains the executed demo outputs. When recording, use actual replies rather than substituting scripted responses.
