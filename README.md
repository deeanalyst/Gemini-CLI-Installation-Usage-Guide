# Installing the Gemini CLI

This guide provides instructions on how to install and set up the Gemini CLI to interact with Gemini services from your terminal.

## 1. Prerequisites

Before you begin, ensure you have the following installed on your system:

*   **A compatible operating system:** Linux, macOS, or Windows (with WSL).
*   **A package manager:** Depending on the installation method, you will need either `npm` (which comes with Node.js) or `pip` (which comes with Python).

---

## 2. Installation

Choose one of the following installation methods. The appropriate method depends on how the Gemini CLI is packaged and distributed.

### Method A: Using NPM (for Node.js)

If the Gemini CLI is distributed as a Node.js package, you can install it using `npm`.

1.  **Install Node.js:** If you don't have Node.js, download and install it from [nodejs.org](https://nodejs.org/). It is recommended to use the latest LTS version.
2.  **Install the CLI:** Open your terminal and run the following command. The `-g` flag installs it globally, making the `gemini` command available system-wide.
    ```bash
    npm install -g @google/gemini-cli
    ```
    *(Note: The package name `@google/gemini-cli` is an example. Please replace it with the actual package name if it's different.)*

### Method B: Using Pip (for Python)

If the Gemini CLI is distributed as a Python package, you can install it using `pip`.

1.  **Install Python:** If you don't have Python, download and install it from [python.org](https://python.org/). Version 3.8 or higher is recommended.
2.  **Install the CLI:** Open your terminal and run the following command:
    ```bash
    pip install google-gemini-cli
    ```
    *(Note: The package name `google-gemini-cli` is an example. Please replace it with the actual package name if it's different.)*

### Method C: Using a Shell Script

For some distributions, you might be provided with a direct installation script. This is common for pre-compiled binaries.

1.  **Download the script:** Use `curl` or `wget` to download the installation script.
    ```bash
    curl -sS https://example.com/install.sh -o install-gemini.sh
    ```
    *(Note: Replace `https://example.com/install.sh` with the actual URL of the installation script.)*
2.  **Make the script executable:**
    ```bash
    chmod +x install-gemini.sh
    ```
3.  **Run the script:**
    ```bash
    ./install-gemini.sh
    ```

---

## 3. Post-Installation Steps

### Verify the Installation

After the installation is complete, verify that the CLI is accessible from your terminal by checking its version.

```bash
gemini --version
```

If you get a "command not found" error, you may need to restart your terminal or adjust your system's `PATH` environment variable to include the directory where the package was installed.

### Authentication

The first time you run a command, you will likely be prompted to authenticate with your Google account.

```bash
gemini login
```

Follow the on-screen instructions to complete the authentication process. This will typically involve signing in through a web browser and granting the necessary permissions. Your credentials will be stored locally for future sessions.

---

You are now ready to use the Gemini CLI! For a guide on how to use the CLI's features, please refer to the `GEMINI_CLI_GUIDE.md` document.


# A Guide to Using the Gemini CLI Agent

Welcome! This guide will help you effectively use the Gemini CLI agent for your software engineering tasks.

## 1. How It Works: The Core Loop

My primary goal is to help you with your development tasks safely and efficiently. The interaction process follows a consistent pattern:

1.  **You Give a Command:** You ask me to do something (e.g., "Refactor this file," "Find all usages of this function," "Run the tests").
2.  **I Analyze & Plan:** I'll use my tools to understand your codebase, the context of your request, and form a step-by-step plan. I will often check for tests, project dependencies, and existing code conventions.
3.  **I Propose an Action:** I will show you the exact command or code change I intend to make.
4.  **You Approve or Deny:** **No action is taken without your explicit approval.** You will be prompted to confirm each step, giving you complete control over your system and codebase.
5.  **I Execute & Verify:** Once you approve, I run the command. For code changes, I will try to run tests or linters to ensure the changes are safe and correct.

## 2. What I Can Do: Key Capabilities

You can ask me to perform a wide range of tasks.

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

-   **Be Specific:** The more detailed your request, the better I can help. Instead of "Fix the bug," try "The login button isn't working. I think the error is in `auth.js`. Please investigate and fix it."
-   **Provide Context:** Mention relevant filenames, function names, or project goals. This helps me narrow down the search and understand your intent.
-   **Trust the Process:** I am designed to be cautious. I will ask clarifying questions and present a plan before making changes. Work with me through this process to ensure the best outcome.
-   **Use the `/help` command** if you need a refresher on what I can do.

## 4. Example Workflow: Refactoring a File

Here’s a realistic example of how we might work together:

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

I'm ready to help. What would you like to do?
