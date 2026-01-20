# Full n8n Crash Course: Build 5 Real-World Automation Projects

This repository contains all the workflow JSON files, code snippets, and resources for the "Full n8n Crash Course" on YouTube. This course is designed to take you from a complete beginner to building complex, AI-powered automation workflows.

## Course Overview

In this course, we build five distinct projects ranging from basic automation to advanced AI agents. Each folder corresponds to a specific project module in the video.

## Projects Included

## Project 1: Workflow Automation
```
   <!DOCTYPE html>
<html>
<head>
    <title>Contact Form</title>
</head>
<body>
    <h2>Contact Form</h2>
    <form id="contactForm">
        <input type="text" name="name" placeholder="Your Name" required><br><br>
        <input type="email" name="email" placeholder="Your Email" required><br><br>
        <textarea name="message" placeholder="Your Message" required></textarea><br><br>
        <button type="submit">Submit</button>
    </form>

    <script>
        document.getElementById('contactForm').addEventListener('submit', async function(e) {
            e.preventDefault();
            
            const formData = {
                name: e.target.name.value,
                email: e.target.email.value,
                message: e.target.message.value
            };

            const response = await fetch('YOUR WEBHOOK URL', {
                method: 'POST',
                headers: {'Content-Type': 'application/json'},
                body: JSON.stringify(formData)
            });

            if(response.ok) {
                alert('Form submitted successfully!');
                e.target.reset();
            }
        });
    </script>
</body>
</html> 
```
## Project 2: AI Chatbot Agent**
    
## Project 3: YouTube Content Automation**
    
## Project 4: Data Analysis Workflow**
    
## Project 5: Advanced Complex Workflow**

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
