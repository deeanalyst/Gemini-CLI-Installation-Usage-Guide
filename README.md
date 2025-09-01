# Installing the Gemini CLI

This guide provides instructions on how to install and set up the Gemini CLI to interact with Gemini services from your terminal.

## 1. Prerequisites

Before you begin, ensure you have the following installed on your system:

*   **A compatible operating system:** Linux, macOS, or Windows (with WSL).
*   **A package manager:** Depending on the installation method, you will need either `npm` (which comes with Node.js) or `pip` (which comes with Python).

### Update & Install system packages & dependecies
```bash
sudo apt-get update && sudo apt-get upgrade -y
sudo apt install curl iptables build-essential git wget lz4 jq make gcc nano automake autoconf tmux htop nvme-cli libgbm1 pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip libleveldb-dev  -y
```
Install `Nodejs` & `npm` in one go
```bash
# 1️⃣ Remove any existing node + npm (optional if you want a clean slate)
sudo apt remove -y nodejs npm

# 2️⃣ Update and install Node.js 22 from NodeSource
curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -
sudo apt install -y nodejs

# 3️⃣ Verify installation
node -v   # should show v22.x
npm -v    # should show ~10.x (latest stable)
```
---

## 2. Installation

Choose one of the following installation methods. The appropriate method depends on how the Gemini CLI is packaged and distributed.

### Method A (Recommended): Using NPM (for Node.js)
**Install the CLI:** Open your terminal and run the following command. The `-g` flag installs it globally, making the `gemini` command available system-wide.
```bash
npm install -g @google/gemini-cli@latest
```
### Method B: Using Pip (for Python)

If the Gemini CLI is distributed as a Python package, you can install it using `pip`.

1.  **Install Python:** If you don't have Python, download and install it from [python.org](https://python.org/). Version 3.8 or higher is recommended.
2.  **Install the CLI:** Open your terminal and run the following command:
```bash
pip install google-gemini-cli
```
---

## 3. Post-Installation Steps

### Verify the Installation

After the installation is complete, verify that the CLI is accessible from your terminal by checking its version.

```bash
source ~/.bashrc
gemini --version
```

<img width="436" height="111" alt="Gemini Version Check" src="https://github.com/user-attachments/assets/efe0b0c1-0692-48a8-8954-f507ab7edf4d" />

### Getting an API Key
- Visit [Google Studio](https://aistudio.google.com/app/u/2/apikey) and sign in or sign up with your Google account.
- Attempt creating an API Key, it might not let you without you creating a default project on Google Console. If it does prompt you to do so? You would need to visit [Google Console](https://console.cloud.google.com/), sign in or sign up with your Google account, then at the top left of your screen you should see a button "**Select Project**" or as in my screenshot where **`testx`** is at the top.
- Click it then on the dialog box that poos up, click "**Create a new project**" on the top right. Name the project whatever you like, don't input a location, just "**Create**".

<img width="624" height="264" alt="Google Console Homepage" src="https://github.com/user-attachments/assets/b669d96a-6b8c-4bd4-8fd9-4bd789a6b863" />

- If you have done this, while still on the Google Console homepage, click on the navigation menu at the top-left of the page.
  Navigate this way: **`APIs & Services >> Enabled APIs & services`**
- Click on the **`+ Enable APIs & services`** button to enable an API.
- Search for **`Gemini API`**, it should be the first option on the list, click it & enable it.
- Now, go back to `Google Studio` and refresh the page, you should now be able to get an API key by choosing your project which you created in `Google Console` and creating an API key. Copy the key and do this in your terminal.

### Export your API Key to use Gemini CLI
```bash
echo 'export GEMINI_API_KEY="YOUR_API_KEY"' >> ~/.bashrc
source ~/.bashrc
```
Replace `YOUR_API_KEY` with the API Key you copied from `Google Studio`
> `NB`: You must always use `source ~/.bashrc` whenever you restart your terminal so you don't meet the login interface.

> `NB`: If you ever exhaust your daily quota of requests you either use another Google mail to generate a new API Key or you wait for the day to reset. 😂😂😂

> `NB`: If your terminal restarts or you quit `Gemini` the CLI loses memory, so always make sure you have a good internet connection and try to document your queries so you can easily remind it about what it had done for you in the past.

### Start the Gemini CLI
```bash
gemini
```
You run this command from either your `root` directory or the particular folder you are trying to work with. Now, `Gemini` recommends the latter because it helps it to pinpoint your needs and reduces waste of time and resources.

### Authentication
The first time you run the command or any time you start Gemini without running `source ~/.bashrc` after previously exporting your API Key to the `.bashrc` file, you will be prompted to choose between three (3) methods you would prefer to use to firing up the Gemini CLI service.

<img width="576" height="284" alt="Gemini Login Screen" src="https://github.com/user-attachments/assets/ac8ee84b-790c-408a-b8b4-8287a2e08607" />

Recommended Option: **`2. Use Gemini API Key`**  (Based on how this guide is tailored)

Follow the on-screen instructions using your arrow keys to choose an option amongst the 3 you were given, to complete the authentication process.

---

# A Guide to Using the Gemini CLI Agent

Welcome! This guide will help you effectively use the Gemini CLI agent for your software engineering tasks.

## 1. How It Works: The Core Loop

The primary goal is to help you with your development tasks safely and efficiently. The interaction process follows a consistent pattern:

1.  **You Give a Command:** You ask Gemini to do something (e.g., "Refactor this file," "Find all usages of this function," "Run the tests").
2.  **It Analyzes & Plans:** Gemini will use its tools to understand your codebase, the context of your request, and form a step-by-step plan. It will often check for tests, project dependencies, and existing code conventions.
3.  **It Propose an Action:** It will show you the exact command or code change it intends to make.
4.  **You Approve or Deny:** **No action is taken without your explicit approval.** You will be prompted to confirm each step, giving you complete control over your system and codebase.
5.  **It Executes & Verifies:** Once you approve, it runs the command. For code changes, it will try to run tests or linters to ensure the changes are safe and correct.

## 2. What It Can Do: Key Capabilities

You can ask Gemini to perform a wide range of tasks.

### Code Interaction
- **Read & Analyze Code:** "What does the `calculate_totals` function in `src/utils.py` do?"
- **Write & Refactor Code:** "Add a new function to `UserService.ts` that deletes a user." or "Refactor `data_processor.js` to use async/await instead of promises."
- **Search the Codebase:** "Where is the `API_ENDPOINT` variable defined?" or "Find all files that import the `requests` library."
- **Write Tests:** "Write a unit test for the `format_date` function in `utils.js`."

### System & Project Interaction
- **Run Shell Commands:** "List all files in the `scripts` directory." or "Run the database migration script."
- **Run Tests, Linters, and Builds:** "Run the test suite." or "Run `npm run lint` and fix any errors."
- **Manage Files:** "Create a new file named `config.json` in the `src/` directory." or "Delete all `.log` files."

### Knowledge & Planning
- **Answer Technical Questions:** "What's the difference between a `let` and `const` in JavaScript?"
- **Explain Complex Code:** "Can you explain the authentication flow in this project?"
- **Create New Applications:** "Scaffold a new React application with TypeScript and a Node.js backend."

## 3. Best Practices for Effective Use

To get the best results, follow these tips:

-   **Be Specific:** The more detailed your request, the better it can help. Instead of "Fix the bug," try "The login button isn't working. I think the error is in `auth.js`. Please investigate and fix it."
-   **Provide Context:** Mention relevant filenames, function names, or project goals. This helps it narrow down the search and understand your intent.
-   **Trust the Process:** Gemini is designed to be cautious. It will ask clarifying questions and present a plan before making changes. Work with it through this process to ensure the best outcome.
-   **Use the `/help` command** if you need a refresher on what it can do.

## 4. Example Workflow: Refactoring a File

Here’s a realistic example of how you both might work together:

**You:**
> "Refactor `src/api/http.js` to use the `axios` library instead of the native `fetch` API."

**Me (Gemini):**
> Okay, I can do that. First, I'll check if `axios` is already a project dependency.
> `[TOOL CALL: read_file for /root/project/package.json]`

**(After seeing axios is in `package.json`)**
> Great, `axios` is available. Now, I'll read the contents of the file to be changed.
> `[TOOL CALL: read_file for /root/project/src/api/http.js]`

**(After analyzing the file)**
> I have a plan to refactor the file. I will replace the `fetch` call with an `axios.get` call and adjust the error handling. I will then run the project's linter to ensure style consistency.
> `[TOOL CALL: replace in /root/project/src/api/http.js with the new code]`

**(You approve the change)**

**Me (Gemini):**
> The file has been updated. Now, I'll run the linter to verify the changes.
> `[TOOL CALL: run_shell_command for 'npm run lint']`

**(After tests pass)**
> All checks passed. The refactoring is complete.

---

I hope this guide is useful to your development process. 🫡
