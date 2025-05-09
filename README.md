<p align="center">
  <img src="assets/logo.png" alt="A sample image" width="40%">
</p>

# LinkedIn AI Job Applier Ultimate

![Python](https://img.shields.io/badge/python-3.12-blue)
![License](https://img.shields.io/github/license/beatwad/LinkedIn-AI-Job-Applier-Ultimate)
![Stars](https://img.shields.io/github/stars/beatwad/LinkedIn-AI-Job-Applier-Ultimate?style=social)
![Last Commit](https://img.shields.io/github/last-commit/beatwad/LinkedIn-AI-Job-Applier-Ultimate)


🤖 AI-powered bot that **auto-applies** to jobs on **LinkedIn** and **Indeed**. It parses your resume, generates tailored resumes per vacancy, answers application questions using an LLM (Gemini, OpenAI, Claude, Ollama), gathers statistics of the most important for employers skills and delivers detailed
Telegram reports — fully automating your job search.


This is an active fork of the original [Jobs_Applier_AI_Agent_AIHawk](https://github.com/feder-cr/Jobs_Applier_AI_Agent_AIHawk) project, which is currently inactive. This version introduces numerous new features, bug fixes, and performance improvements.

## Disclaimer

This bot uses the LinkedIn and Indeed UIs to apply for jobs. Both sites frequently change their UI, so the bot may lose some of its functionality **AT ANY TIME**.
I don't have time to check this bot every day, so if you face any malfunction or have some questions about the bot - feel free to open an issue or contact me in the Telegram chat. And - **this is important** - if a malfunction happened while applying to a vacancy, **don't forget to include the URL of this vacancy**. It will help me a lot.

Please ⭐ the repository if you find it useful. This is the only thing that motivates me to continue developing the project.

## 🎥 Demo

[![LinkedIn AI Job Applier Ultimate Demo](https://img.youtube.com/vi/HmbeI8u12MU/maxresdefault.jpg)](https://www.youtube.com/watch?v=HmbeI8u12MU)

### ⚠️ Note on Indeed

Indeed support is functional but has important limitations compared to LinkedIn:

- **Most jobs are not Easy Apply.** The vast majority of Indeed listings redirect to external company websites, which the bot cannot reliably handle.
- **CAPTCHAs are frequent.** Indeed aggressively deploys CAPTCHAs that interrupt automated flows, even with bot-detection bypass techniques.
- **Sometimes Indeed is sloooow.** It can take a lot of time to apply for a job on Indeed for some users because sometimes it takes a lot of time for Indeed pages to load.

For these reasons, **LinkedIn is strongly recommended** over Indeed for automated job applications. Indeed support may improve in the future, but currently it is not well-suited for automation.

But if you're planning to use Indeed for searching jobs without auto-applying - it's a great site. You can use it for searching suitable jobs and then apply for them manually.

### LinkedIn AI Job Applier Chat 👇

[![Telegram](https://img.shields.io/badge/Telegram-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white
)](https://t.me/linkedin_auto_job)

---

## 📋 Table of Contents

- [✨ Features](#-features)
- [🚀 Getting Started](#-getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
- [🔧 Configuration](#-configuration)
- [▶️ Usage](#️-usage)
  - [LinkedIn Messages Manager](#linkedin-messages-manager)
  - [Dashboard](#dashboard)
  - [Dashboard Routes And APIs](#dashboard-routes-and-apis)
- [💵 Vacancy application cost](#-vacancy-application-cost)
- [✅ Running Tests](#-running-tests)
- [🐞 Troubleshooting](#-troubleshooting)
- [📨 Telegram Instruction](#-telegram-instruction)
- [🤝 Contributing](#-contributing)
- [📜 License](#-license)
- [🙏 Acknowledgements](#-acknowledgements)

---

## ✨ Features

This project enhances the original codebase with several powerful new features:

*   **🌐 Multi-Platform Support:** Applies to jobs on **LinkedIn** and **Indeed**. Switch between platforms with a single `JOB_SITE` setting in `config/app_config.py`.
*   **🌐 Universal Job Application:** Applies to **ALL** job vacancies on LinkedIn (not just Easy Apply) thanks to the [browser-use](https://github.com/browser-use/browser-use) library.
*   **🔒 Data Anonymization:** Protects your privacy by replacing personal data with mock information before sending it to the LLM provider, ensuring your sensitive information remains secure.
    *   *Note: Auto resume parsing and applying of Non-Easy Apply vacancies don't use anonymization. Additionally, country, city, and birth date are not anonymized to maintain the quality of LLM responses.*
*   **🎯 Improved Intelligent Resume Generation:** Uses AI to tailor every generated resume to the current vacancy for maximum match, adapting skills, experience, projects and achivements to the job description.
*   **🎭 Patchright Integration:** Now uses [Patchright](https://github.com/Kaliiiiiiiiii-Vinyzu/patchright) (a patched build of Playwright) instead of Selenium/Playwright for faster, more reliable and undetectable browser automation. Patchright patches Chromium's automation detection signals to bypass Cloudflare and other bot-detection systems.
*   **🖥️ Headless Mode:** Run the bot in headless mode if you want to use the bot in server environment or while working with your computer. This allows the bot to operate without a visible browser window while maintaining full functionality.
*   **⏸️ Pause/Resume Control:** Pause the bot at any time by pressing `Ctrl+X` and continue when ready, giving you full control over execution without stopping the entire process.
*   **📊 Skill Statistics:** Analyzes job descriptions to identify the most in-demand skills, helping you tailor your resume effectively.
*   **🧠 Intelligent Error Handling:** If LinkedIn's Easy Apply feature encounters errors (e.g., incorrectly filled fields), the bot will attempt to fix them automatically.
*   **📈 Local Monitoring Dashboard:** Includes a local web dashboard for live monitoring, run history, screenshot review, config editing, bot controls, and JSON export of individual runs.
*   **💬 LinkedIn Messages Manager:** Includes a separate inbox triage workflow for classifying LinkedIn conversations, drafting replies, archiving spam, starring recruiter outreach, applying the `Jobs` label, and recording all message decisions to a persistent ledger for dashboard review.
*   **🤝 Automated Networking:** Includes a powerful tool to search for and connect with "Open Networkers" (LIONs) automatically, expanding your professional network with people likely to accept your requests.
*   **☑️ Smart Checkbox Handling:** Automatically detects and answers checkbox questions in LinkedIn Easy Apply forms with intelligent context-aware responses.
*   **🔗 Contextual Question Processing:** Considers previous answers when responding to follow-up questions like "If yes/no, who/when/where?" for more accurate and relevant responses.
*   **🤖 AI-Powered Resume Parsing:** Automatically parses your resume from a text file into a structured format using an LLM (Large Language Model).
*   **📄 Auto Resume Text Generation:** If `data/resumes/resume_text.txt` is missing but a PDF resume is present in `data/resumes/`, the bot automatically extracts the text from the PDF and generates a properly formatted `resume_text.txt` using the LLM — no manual transcription needed.
*   **📄 New Resume Style:** Includes the modern "FAANGPath" resume style for generating professional-looking resumes.
*   **📲 Telegram Integration:** Delivers comprehensive reports and error notifications directly to your Telegram chat after each run.
*   **💡 Resume Recommendations:** Provides AI-generated suggestions to improve your resume based on job market trends.
*   **🌐 Proxy Support:** Supports using proxies for both Gemini, OpenAI and OpenRouter models.
*   **🏗️ Robust Configuration:** Uses Pydantic models for validating configuration, resume, and other data structures, reducing runtime errors.
*   **🚀 Improved LLM Logic:**
    *   Utilizes improved system instructions and prompts for higher-quality LLM responses.
    *   Employs Gemini or OpenRouter as the default LLM, which is often more cost-effective (sometimes even free!) than OpenAI.
    *   Enhances question-answering logic to avoid LLM "hallucinations" by skipping questions where it lacks sufficient information.
*   **🔐 Secure Secrets Management:** Stores sensitive keys and credentials in a `.env` file for better security.
*   **🕒 Automated Scheduling:** A built-in timer allows the bot to run automatically every 24 hours.
*   **💻 Numerous improvements that simplify development and debugging:** advanced logging, pre-commit hooks, fast and easy installation using uv, etc.


## 🚀 Getting Started

### Prerequisites

*   Python 3.12
*   Git
*   [uv](https://github.com/astral-sh/uv) (optional, for faster installation)

### Installation

#### Option 1: Local Installation

1.  **Clone repository and create virtual environment**

    ```bash
    # Clone the repository
    git clone https://github.com/beatwad/LinkedIn-AI-Job-Applier-Ultimate.git
    cd LinkedIn-AI-Job-Applier-Ultimate
    ```

2.  **Install dependencies**
    ```bash
    uv sync
    ```

3.  **Install additional software**
    ```bash
    # Install Chromium browser for Playwright
    playwright install chromium
    ```

#### Option 2: Docker Installation

1.  **Clone repository**

    ```bash
    git clone https://github.com/beatwad/LinkedIn-AI-Job-Applier-Ultimate.git
    cd LinkedIn-AI-Job-Applier-Ultimate
    ```

2.  **Build Docker image**

    ```bash
    docker build -t linkedin .
    ```

3.  **Run Docker container**

    ```bash
    docker run -v $(pwd)/data:/app/data \
               -v $(pwd)/browser_session:/app/browser_session \
               -v $(pwd)/logs:/app/logs \
               linkedin
    ```

    **⚠️ IMPORTANT:** When running from Docker:
    - You **MUST** set `HEADLESS_MODE = True` in `config/app_config.py`. Docker containers don't support graphical interfaces, so the browser must run in headless mode.
    - The **Ctrl+X pause/resume feature will not work** in Docker (keyboard control requires an X server). The bot will run continuously without the ability to pause.
    - **Resume style selection is automatic** - the bot will use the default style (FAANGPath) instead of prompting for selection, since Docker doesn't support interactive prompts.

## 🔧 Configuration

1.  **Secrets (`.env` file):**
    Create a `.env` file in the root directory by copying the example file:
    ```bash
    cp .env_example .env
    ```
    Now, fill in the required values in your `.env` file:
    ```env
    # Your LinkedIn credentials (used when JOB_SITE="linkedin" in app_config.py)
    linkedin_email="your_linkedin_email@example.com"
    linkedin_password="your_linkedin_password"

    # Your Indeed credentials (used when JOB_SITE="indeed" in app_config.py)
    indeed_email="your_indeed_email@example.com"

    # Your LLM API Key (e.g., Gemini)
    llm_api_key="your_llm_api_key"

    # Optional proxy for LLM requests
    llm_proxy="http://your_proxy_url:port"

    # LLM endpoint URL (required for "openai_compatible", optional for "ollama")
    llm_api_url="http://localhost:8000/v1"

    # Your Telegram Bot Token for sending error messages and reports
    tg_token="your_telegram_bot_token"

    # Address of your chat in format "@name_of_your_chat"
    tg_chat_id="@name_of_your_chat"

    # ID of topic where bot will send error messages
    # You can find out ID of the topic by copying the link to the topic in Telegram app and extracting the number before the last slash
    # For example, if the link to the topic is https://t.me/channel_name/123/321, the ID of the topic is 123
    tg_err_topic_id="[ID of error topic]"

    # ID of topic where bot will send everyday report on the job applies done
    tg_report_topic_id="[ID of report topic]"
    ```

    Telegram options are optional. You can remove them from .env file and application will still be able to work but won't be able to set reports and error messages via Telegram.

2.  **Job Search Parameters (`config/search_config.yaml`):**
    Copy this file from `examples/config/search_config.yaml` and customize your job search by editing this file.
    You can define job titles, locations, experience levels and more.
    Example of search_config file can be found in `examples/config/search_config.yaml`

    ```yaml
    # Example: search for Mid-Senior level remote software engineer roles
    positions: # the only mandatory setting in search_config file
      - Software engineer

    remote: true
    hybrid: false
    onsite: false

    experience_level:
      mid_senior_level: true
    ```

3.  **Application Settings (`config/app_config.py`):**
    Copy this file from `examples/config/app_config.py` and fine-tune the bot's behavior in this file.
    Key settings include:
    *   `JOB_SITE`: The job platform to use. Set to `"linkedin"` (default) or `"indeed"`. Make sure to provide the matching credentials in your `.env` file.
    *   `MAX_APPLIES_NUM`: The maximum number of jobs to apply for in a single run.
    *   `HEADLESS_MODE`: If this mode is activated - the browser will be launched in headless mode. Convenient if you plan to
    use your computer while bot is working + everything works faster.
    *   `MONKEY_MODE`: If `True`, applies to all jobs found. If `False`, the LLM selects only the most suitable jobs.
    *   `TEST_MODE`: If `True`, the bot generates resumes and cover letters but does not actually submit applications.
    *   `COLLECT_INFO_MODE`: If `True`, the bot doesn't apply to the jobs or create resumes and cover letters, only gathers information for interesting jobs and their skill statistics and saves them to the files data/output/interesting_jobs.yaml and data/output/skill_stat.yaml.
    *   `UPLOAD_RESUME`: *(Indeed only)* If `False`, the bot selects your Indeed on-site resume instead of uploading a file. If `True`, the bot uploads a resume file (ready-made PDF or auto-generated).
    *   `INDEED_DOMAIN`: *(Indeed only)* The Indeed country domain to search on. Defaults to `"www.indeed.com"` (US) — set it to your own country's domain (e.g. `"ch.indeed.com"`, `"de.indeed.com"`, `"uk.indeed.com"`) or the search will return US jobs.
    *   `INDEED_SEARCH_RADIUS`: *(Indeed only)* Search radius around each configured location, in the units the chosen domain uses (miles on `www.indeed.com`, kilometres on most others). Leave as `None` to keep Indeed's default radius.
    *   `EASY_APPLY_ONLY_MODE`: *(LinkedIn only)* If `True`, bot applies only the jobs with Easy Apply. Else bot will apply to the jobs with Easy Apply and try to apply to the jobs with 3rd party applications. **WARNING**: applying to the jobs with 3rd-party applications is not guaranteed to be successful, but is guaranteed to consume at least 10-100x more tokens!
    *   `RESTART_EVERY_DAY`: *(LinkedIn only)* If `True`, bot will automatically restart the search every 24 hours when LinkedIn resets the search limits. So you don't have to restart it manually - just run & forget.
    *   `JOB_IS_INTERESTING_THRESH`: LLM evaluated the 'interest' level of the job from 1 to 100. If job 'interest' level not below this threshold - the job is considered interesting for bot. Otherwise not. Because of LinkedIn limits number of daily applications to 50, recommended value of this setting is 70+, so the bot will apply only to vacancies that match your resume
    *   `MINIMUM_WAIT_TIME_SEC`: Minimum time spent on one job application, this setting help to prevent ban for too frequent job applies
    *   `FREE_TIER`: If `True`, the bot will try to decrease RPM (requests per minute) to avoid rate limit errors when using free tier LLM services.
    *   `FREE_TIER_RPM_LIMIT`: desired RPM limit, application will try not to exceed this limit
    *   `DASHBOARD_OUTPUT_APP_LOGS`: If `True`, bot process log output is printed to the dashboard console (in addition to the log file `logs/dashboard_bot_stdout.log`). Useful for debugging when running the bot from the dashboard.
    *   `LLM_MODEL_TYPE`: Choose your LLM provider (e.g., "gemini").
    *   `EASY_APPLY_MODEL`: Specify the exact model to use for Easy Apply vacancies (e.g., "gemini-2.0-flash").
    *   `APPLY_AGENT_MODEL`: *(LinkedIn only)* Specify the exact agent model to use for Non-Easy Apply vacancies (e.g., "gemini-2.5-flash").
    *   `READY_MADE_RESUME_PATH`: Path to a ready-made resume PDF (e.g. `"data/resumes/resume.pdf"`). If set, the bot uses this file for every application instead of generating a new resume. If empty, a tailored resume is generated for each vacancy.
    *   `RESUME_STYLE`: Resume style to use for generated resumes. If set, skips the interactive style selection prompt. If `None`, prompts interactively (or falls back to default in Docker/headless mode). Possible values: `"FAANGPath"`, `"Cloyola Grey"`, `"Modern Blue"`, `"Modern Grey"`, `"Default"`, `"Clean Blue"`.

    **Supported LLM models**

    The bot supports multiple LLM providers. Configure them in `config/app_config.py` using `LLM_MODEL_TYPE` and `EASY_APPLY_MODEL`.

    **Gemini (Google)**
    - Set: `LLM_MODEL_TYPE = "gemini"`
    - Examples: `gemini-3.1-flash-lite`, `gemini-3.1-flash`

    **OpenAI**
    - Set: `LLM_MODEL_TYPE = "openai"`
    - Examples: `gpt-4o`, `gpt-4o-mini`

    **OpenRouter**
    - Set: `LLM_MODEL_TYPE = "openrouter"`
    - Examples: `google/gemini-3.1-flash-lite`, `google/gemini-3.1-flash`, `openai/gpt-4o-mini`

    **Claude (Anthropic)**
    - Set: `LLM_MODEL_TYPE = "claude"`
    - Examples: `claude-3-5-sonnet`, `claude-4-opus` (use any valid Claude model ID)

    **Ollama (local/server)**
    - Set: `LLM_MODEL_TYPE = "ollama"`
    - Examples: `llama3`, `qwen2.5` (any model available in your Ollama)

    **OpenAI-compatible endpoint (vLLM, LM Studio, llama.cpp server, etc.)**
    - Set: `LLM_MODEL_TYPE = "openai_compatible"`
    - Set the endpoint URL in `.env` as `llm_api_url` (e.g. `http://localhost:8000/v1`)
    - Examples: any model name served by your endpoint; if the endpoint doesn't require an API key, `llm_api_key` can be set to any placeholder value

    Notes:
    - Recommended models: gemini + gemini-3.1-flash-lite or openai + gpt-5-mini - both are fast, clever and cheap (gemini models can be even free!)
    - Provide your API key in `.env` as `llm_api_key`. Optionally set `llm_proxy`.
    - Model pricing used in reports is taken from an internal map for common models; others fall back to default per-token prices.

4.  **Connection Searcher Settings (`config/linkedin_connection_searcher_config.yaml`):**
    Copy this file from `examples/config/linkedin_connection_searcher_config.yaml` and fine tune the automated networking tool behaviour in this file.
    *   `main_search_words`: Keywords like "Open Networker" or "LION" used to find networking-oriented profiles.
    *   `additional_search_words`: Keywords to narrow down the search to your specific field (e.g., "ai", "ml", "data science").
    The bot will search for every combination of these words and attempt to connect with users whose profiles indicate they are open networkers (while intelligently skipping those profiles where the keywords appear only in "mutual connections").

5.  **LinkedIn Messages Manager Settings (`config/linkedin_messages_manager_config.yaml`):**
    This is a separate configuration file for the LinkedIn inbox triage workflow launched by `uv run python linkedin_messages.py`.

    It controls things like:
    *   dry run versus execute mode
    *   whether archives are allowed
    *   whether replies are allowed
    *   unread-only scanning
    *   whether recruiter messages are auto-starred
    *   whether recruiter messages are auto-labeled as `Jobs`
    *   reply tone and formatting rules
    *   how old-message apology context should work

    Because this feature is more nuanced than the main job application flow, it has dedicated documentation:

    `docs/linkedin-messages-manager.md`

6.