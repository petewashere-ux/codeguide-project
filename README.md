# CodeGuide — Streamlit Stage 1

A beginner-friendly research prototype for **SWEN1006 Research Methods for Software Engineers**. The application takes a programming assignment, an optional marking rubric, and student Java code. In **live mode**, it sends them to an existing OpenAI model and asks for a short hint rather than a complete answer.

**Current scope:** this first version does **not** compile Java, run tests, track revisions, collect survey data, or validate whether feedback is accurate. The example mode displays a **fixed, prewritten** hint; it is not a real model output and must not be counted as experimental evidence.

## Easiest way: publish it from your browser

1. Sign into [GitHub](https://github.com). Create a new repository named `codeguide-project`. Choose a public repository if you only want the simplest deployment; a private repository may require extra authorization in Streamlit Cloud. Do not upload any API keys.
2. Select **Add file → Upload files** and upload `app.py`, `requirements.txt`, and `README.md`. Commit the changes. (The `.gitignore` file is useful too, but not essential for cloud deployment.)
3. Open [Streamlit Community Cloud](https://share.streamlit.io/), sign in with GitHub, and select **Create app** / **Deploy an app**.
4. Select your repository and `app.py` as the main file.
5. First deploy **without secrets**. Open the app and choose **Try the example (no API needed)**. This should display the prewritten hint; no API request is made.
6. To enable real AI feedback, get an **API key and available API credits** from [OpenAI](https://platform.openai.com/api-keys). In your Streamlit app settings under **Secrets**, enter:

   ```toml
   OPENAI_API_KEY = "your-real-key-here"
   APP_PASSWORD = "make-up-a-strong-demo-password"
   ```

7. Save secrets and reboot the app if Streamlit prompts you. Select **Get live AI feedback**, enter an assignment, Java code, and your own **APP_PASSWORD**. Do not put the API key into the app's text fields.

### Keep this safe

- Never commit API keys or `secrets.toml` to GitHub, even in a private repo.
- A public app's live mode is protected with a simple password to reduce accidental API costs. This is a classroom prototype, **not enterprise-grade access control**. Avoid publishing the live password and set an API spending limit.
- Only use sample Java code (or properly consented, de-identified code) for testing. Do not put students' real names or student IDs into requests.
- A public website can be viewed by others, but they cannot use live AI feedback without your APP_PASSWORD. Keep it private for instructor demonstration.

## How the app works (for your report)

- **Design:** a Streamlit web interface; an OpenAI API client; a short-hint prompting rule.
- **Input:** assignment, optional rubric, and student Java code.
- **Processing:** the server sends those inputs to a GPT model, asking for guidance instead of a completed solution.
- **Output:** a short hint on the page.
- **Limitation:** the model is reading code as text. This stage cannot verify runtime behaviour and should never claim it executed Java.

## Next development stages

1. Add multiple progressive hint levels and support for revised submissions.
2. Add safe validation of Java code (isolated compiler and test runner); never run strangers' Java code unisolated in the Streamlit server.
3. Prepare controlled test cases with known errors and record accuracy and response-time measurements.
4. With university approval, conduct an optional small student evaluation and survey. Record actual findings only.

## Optional: local development

If you choose to use your own computer later, install Python and then run `pip install -r requirements.txt` and `streamlit run app.py`. Local credentials can be stored in `.streamlit/secrets.toml` (never upload that file).
