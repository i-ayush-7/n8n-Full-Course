# Full n8n Crash Course: Build 5 Real-World Automation Projects

This repository contains all the workflow JSON files, code snippets, and resources for the "Full n8n Crash Course" on YouTube. This course is designed to take you from a complete beginner to building complex, AI-powered automation workflows.

## Course Overview

In this course, we build five distinct projects ranging from basic automation to advanced AI agents. Each folder corresponds to a specific project module in the video.

## Project 1: Workflow Automation

![IMG](https://github.com/i-ayush-7/n8n-Full-Course/blob/main/1st.png)

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
## Project 2: Weather Updates Automation

![IMG](https://github.com/i-ayush-7/n8n-Full-Course/blob/main/2nd.png)

**HTTP LINK**
```
https://api.openweathermap.org/data/2.5/weather?q=<YOUR CITY>,IN&appid=<YOUR API KEY>&units=metric
```

## Project 3: Top Deals Finder Automation

![IMG]()

**JSON**
```
{{ $json.message.link_preview_options.url }}

https://serpapi.com/search.json

{{ $json.product_name.split(':')[0].replace(/\n/g, " ").trim() }}
```

**AI AGENT PROMPT**
```
You are a Shopping Assistant.
This {{ JSON.stringify($json) }} is the JSON dataset of Google Shopping results.

YOUR TASK:
1. Analyze the 'shopping_results' list.
2. Filter out used items or accessories.
3. Select the TOP 8 best deals.
4. Output the result strictly in this Telegram-friendly format:

🛍️ *Top Deals for [Product Name]*

1. *[Price]* at [Store Name]
   [Insert the ACTUAL 'link' url from the JSON here]

2. *[Price]* at [Store Name]
   [Insert the ACTUAL 'link' url from the JSON here]

CRITICAL RULES:
- Do NOT write the word "[Link]". You MUST paste the full (google_shopping_url) http URL found in the data.
- If the URL is very long, that is okay. Do not shorten it.
- Prioritize trusted stores (Amazon, Flipkart, BestBuy) over Temu/Alibaba if available.
```

## Project 4: Instagram Automation

![IMG]()

**HTTP REQUEST NODES LINK**
```
https://graph.facebook.com/v18.0/<INSTAGRAM BUSINESS ACCOUNT ID>/media

https://graph.facebook.com/v18.0/{{ $json.id }}/comments

https://graph.facebook.com/v18.0/<INSTA BUSINESS ACC ID>/messages
```
**IF NODE**
``
{{ $json.text.toLowerCase() }}
``
**HTTP REQUEST NODE 2(JSON CODE)**
```
{
  "recipient": {
    "id": "{{ $json.from.id }}"
  },
  "message": {
    "text": "Hey! 👋 Thanks for commenting! Here's your AI guide: [YOUR_LINK] 🚀 Let me know if you have questions!"
  },
  "access_token": "YOUR LONG LIVED TOKEN"
}
```
    
## Project 5: YouTube Content Automation

![IMG]()

**AI AGENT 1&2 PROMPTPS**
```
#1st PROMPT

System Message: You are a backend API processor. You do not speak. You only output raw JSON.

Task: Analyze the {{ $json.message.text }}
1. searchTerm: A single, simple English noun for a video background (e.g., "nature", "city", "coding", "sky"). Avoid adjectives.

2. coverlayText: A short summary of the input (max 6 words).

Rules:

- Output RAW JSON ONLY.

- NO markdown formatting (no json ... ).

- NO intro text (no "Here is your JSON").

- NO nesting keys inside an "output" object.

Example Output: { "searchTerm": "ocean", "overlayText": "Keep moving forward" }


#2nd PROMPT

You are a YouTube Shorts SEO Expert and Viral Strategist.
Your goal is to maximize Click-Through Rate (CTR) and algorithm discoverability.

INPUT VIDEO:{{ $json.video }}

YOUR TASKS:
1. **Title:** Write a clickbaity, emotional, or curiosity-inducing title. MUST be under 50 characters. MUST end with #Shorts.
2. **Description:** Write a 3-line engaging caption followed by 5-8 relevant, high-traffic hashtags.
3. **Tags:** A comma-separated list of 15 broad and niche keywords for the YouTube algorithm.

RULES:
- NO generic titles like "Motivation Video". Use hooks like "Stop doing this..." or "The Truth About..."
- Output valid JSON only.

OUTPUT JSON STRUCTURE:
{
  "title": "String (max 50 chars) #Shorts",
  "description": "String (multiline ok)",
  "tags": "tag1, tag2, tag3"
}
```

**Codes of JavaScript**
```
#1st Code:

// 1. Grab the input data safely
const inputData = items[0].json;

// 2. Hunt for the AI's response text in the most common places
// - 'message.content' (Standard Chat Model)
// - 'text' (Instruct/Completion Model)
// - 'output' (AI Agent/Chain)
let aiText = null;

if (inputData.message && inputData.message.content) {
    aiText = inputData.message.content;
} else if (inputData.text) {
    aiText = inputData.text;
} else if (inputData.output) {
    aiText = inputData.output;
} else if (typeof inputData === 'string') {
     // Sometimes the input is just the string itself
    aiText = inputData;
}

// 3. Safety Check: Did we find anything?
if (!aiText) {
    throw new Error("CRITICAL: Could not find the AI text. Please check the OpenAI node's 'Output' tab to see where the text is hidden.");
}

// 4. Clean the Markdown (Remove ```json and ```)
const cleanJson = aiText.replace(/```json|```/gi, '').trim();

// 5. Parse and Return
try {
    const parsedData = JSON.parse(cleanJson);
    return [{ json: parsedData }];
} catch (error) {
    // If it fails, return the raw text so you can debug it
    return [{
        json: {
            error: "JSON Parsing Failed",
            reason: error.message,
            whatWeTriedToParse: cleanJson
        }
    }];
}


#2nd Code:

const inputData = items[0].json;
let aiText = null;

if (inputData.message && inputData.message.content) {
    aiText = inputData.message.content; 
} else if (inputData.text) {
    aiText = inputData.text; 
} else if (inputData.output) {
    aiText = inputData.output; 
} else if (typeof inputData === 'string') {
    aiText = inputData;
}

if (!aiText) {
    throw new Error("CRITICAL: No text found from the Metadata Agent. Check the Input connection.");
}

const cleanJson = aiText.replace(/```json|```/gi, '').trim();

// 4. Parse & Validate
try {
    const data = JSON.parse(cleanJson);

    
    let finalTags = data.tags;
    if (Array.isArray(finalTags)) {
        finalTags = finalTags.join(',');
    }

    return [{
        json: {
            video_title: data.title,
            video_description: data.description,
            video_tags: finalTags
        }
    }];

} catch (error) {
    return [{
        json: {
            error: "JSON Parsing Failed",
            reason: error.message,
            raw_ai_output: aiText
        }
    }];
}
```

**HTTP REQUEST LINKS**
```
https://api.pexels.com/videos/search

https://api.cloudinary.com/v1_1/<USER ID>/video/upload

https://res.cloudinary.com/dyn04xkkj/video/upload/l_text:Arial_60_bold:{{ $('Code in JavaScript').item.json.coverlayText }},co_white,g_center,w_0.8,c_fit/v1/{{ $json.public_id }}.mp4
```


## Prerequisites

Before running these workflows, ensure you have the following:

* **n8n Installed:** You can use the self-hosted version (npm/Docker) or n8n Cloud.
* **API Keys:** Required for services used in the projects (e.g., OpenAI, Google Cloud Console, Telegram, etc.).
* **Basic JavaScript/Python Knowledge:** Helpful for the Code Node sections but not strictly mandatory.

