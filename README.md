# Cedar Tutoring — C3 Business Assistant

A simple business assistant for a fictional tutoring service. It answers from the supplied business documents, collects contact details for follow-up, and records feedback or questions it cannot answer. It uses OpenAI `gpt-4.1-mini` and a Gradio chat interface.

## Run locally

Use Python 3.10 or later. Open a terminal in this folder, then run:

```bash
python -m pip install -r requirements.txt
```

Create a local `.env` file using `.env.example` as a guide:

```dotenv
OPENAI_API_KEY=your_key_here
```

Start the app and open the local address printed in the terminal:

```bash
python app.py
```

You can also run `business_agent.ipynb` from top to bottom in Jupyter. In Google Colab, run the installation cell, upload `about_business.pdf` and `business_summary.txt` when prompted, and enter your API key in the hidden input prompt.

The app needs an internet connection and a working OpenAI API key. Keep `.env` private. Never include it in GitHub or a demo recording. The API key and local logs are excluded by `.gitignore`.

## How it works

1. Read the PDF and text summary into the system prompt.
2. Classify each new message as `general_question`, `lead_collection`, or `feedback`, using the recent conversation for context.
3. Send the separate persona and instructions, business facts, recent history, and available tools to the model.
4. Execute any requested tools, return their results to the model, and display its reply.

The assistant keeps the latest 20 history messages and allows up to four tool rounds per reply. It collects a name, email, and request before recording a lead. A lead is a request for human follow-up, not a confirmed booking. Unknown business facts must be recorded instead of invented.

The fictional business email is `hello@cedartutoring.example`; it does not receive messages.

## Tool definitions

Both tools have JSON schemas in the app and notebook. The model requests a tool; Python performs the action. Each successful call prints a trace and appends one JSON record to a local file.

| Tool | Required string inputs | Expected result | Log file |
| --- | --- | --- | --- |
| `record_customer_interest` | `email`: customer email; `name`: customer name; `message`: requested service or follow-up notes | Confirmation that the interest was recorded, or a validation error | `logs/leads.jsonl` |
| `record_feedback` | `question`: feedback text or an unanswered question | Confirmation that the feedback/question was recorded, or a validation error | `logs/feedback.jsonl` |

Use fictitious customer details for the assignment demo. Logs are created when the tools run and stay on the machine running the app.

## Requirement-to-file map

| Assignment requirement | Where to find it |
| --- | --- |
| Business name, mission, services, team, and unique value | `me/about_business.pdf` and `me/business_summary.txt` |
| Separate, labeled persona and instructions | `business_agent.ipynb` and `app.py` |
| Three routing paths | Router in `business_agent.ipynb` and `app.py` |
| Two callable tools, schemas, and logging | Tool sections in `business_agent.ipynb` and `app.py`; table above |
| Prompt includes PDF/text business content | Document-loading and system-prompt sections |
| OpenAI, short-term memory, tool execution, and final replies | Chat function in the notebook and app |
| Gradio `ChatInterface` | Final notebook cell and `app.py` |
| Dependencies and local key configuration | `requirements.txt`, `.env.example`, and your private `.env` |
| Demonstration video | Record your own demonstration using `DEMO_SCRIPT.md` and submit it with the repository link |
| GitHub repository | Published at https://github.com/Mohamad-HK22/Cedar_Tutoring; private API keys and local logs are excluded |

The handout uses both `summary.txt` and `business_summary.txt`. This project uses `business_summary.txt` to match its folder layout and submission checklist. It uses the current OpenAI Python client method, `client.chat.completions.create`, rather than the older `openai.ChatCompletion` name printed in the handout. See the official [function-calling guide](https://developers.openai.com/api/docs/guides/function-calling) and [GPT-4.1 mini documentation](https://developers.openai.com/api/docs/models/gpt-4.1-mini).

Optional reflection and Hugging Face deployment are outside this simple version.

## Verification and submission

- Live verification: passed on 18 October 2026. The executed notebook includes actual OpenAI replies for all seven demo messages. All three routes and both tools were exercised.
- Offline verification: 10 tests passed (`python -m unittest -v test_app.py`); dependency check passed.
- Demonstration video: record your own video following `DEMO_SCRIPT.md`. No video is currently included in the repository.
- Git repository: published at https://github.com/Mohamad-HK22/Cedar_Tutoring. Submit the repository link with your demonstration video.

The notebook and browser demo have been run. You can reproduce the cases in `DEMO_SCRIPT.md` and inspect the activity accordion and local logs. Submit the GitHub repository link and demonstration video. Check that the repository includes the notebook, app, both business documents, dependency file, README, and demo script, but no API key or real customer details.
