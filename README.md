# n8n Full Course

# Full n8n Crash Course: Build 5 Real-World Automation Projects

This repository contains all the workflow JSON files, code snippets, and resources for the "Full n8n Crash Course" on YouTube. This course is designed to take you from a complete beginner to building complex, AI-powered automation workflows.

## Course Overview

In this course, we build five distinct projects ranging from basic automation to advanced AI agents. Each folder corresponds to a specific project module in the video.

### Projects Included

1.  **Project 1: Foundation & Basics**
    * **Goal:** Introduction to nodes, connections, and basic data flow.
    * **Key Nodes:** Webhook, Set, HTTP Request.
    * **Location:** `/project-01-basics`

2.  **Project 2: AI Chatbot Agent**
    * **Goal:** Building a conversational AI agent using LLMs.
    * **Key Nodes:** AI Agent, OpenAI/Gemini Chat Model, Memory Buffer.
    * **Location:** `/project-02-ai-agent`

3.  **Project 3: YouTube Content Automation**
    * **Goal:** Automating video metadata generation and uploading.
    * **Key Nodes:** YouTube API, Google Sheets, HTTP Request.
    * **Location:** `/project-03-youtube-automation`

4.  **Project 4: Data Analysis Workflow**
    * **Goal:** Processing datasets and visualizing data automatically.
    * **Key Nodes:** Code Node (Python), Spreadsheet File, Email.
    * **Location:** `/project-04-data-processing`

5.  **Project 5: Advanced Complex Workflow**
    * **Goal:** A full-scale enterprise automation scenario with error handling.
    * **Key Nodes:** Merge, Switch, Error Trigger, Split In Batches.
    * **Location:** `/project-05-advanced-workflow`

## Prerequisites

Before running these workflows, ensure you have the following:

* **n8n Installed:** You can use the self-hosted version (npm/Docker) or n8n Cloud.
* **API Keys:** Required for services used in the projects (e.g., OpenAI, Google Cloud Console, Telegram, etc.).
* **Basic JavaScript/Python Knowledge:** Helpful for the Code Node sections but not strictly mandatory.

## How to Use This Repository

1.  **Clone the Repo:**
    ```bash
    git clone [https://github.com/yourusername/n8n-crash-course.git](https://github.com/yourusername/n8n-crash-course.git)
    ```

2.  **Import Workflows:**
    * Open your n8n dashboard.
    * Create a new workflow.
    * Click on the three dots in the top right corner > **Import from File**.
    * Select the `.json` file from the respective project folder (e.g., `project-01-basics/workflow.json`).

3.  **Configure Credentials:**
    * Double-click nodes that require authentication.
    * Select **Create New Credential** and input your specific API keys.

## Setup & Installation (Self-Hosted)

If you are running n8n locally using npm:

```bash
npm install n8n -g
n8n start
