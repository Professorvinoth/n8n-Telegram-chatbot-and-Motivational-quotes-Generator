# n8n-Telegram-chatbot-and-Motivational-quotes-Generator

** AI-powered Telegram chatbot**

1. Project Overview
You are building an AI-powered Telegram chatbot that:
•	Listens to user messages on Telegram 
•	Sends the message to AI (GPT) 
•	Generates a smart reply 
•	Sends the reply back instantly 
In short:
Telegram → AI → Telegram (real-time conversation loop)
________________________________________
2. Tools & Technologies Used
Core Stack:
•	n8n
Controls automation logic 
•	Telegram
User interface (chatbot lives here) 
•	BotFather
Creates your bot + gives API token 
•	OpenAI (GPT model)
Generates intelligent responses 
________________________________________
3. Requirements (Non-Negotiable)
Before starting:
Accounts Needed:
•	Telegram account 
•	OpenAI API key 
•	n8n account 
Critical Setup:
•	Create Telegram bot via BotFather 
•	Copy bot token 
•	Add OpenAI API key in n8n 
________________________________________
4. Workflow Architecture (Understand This First)
Telegram Trigger → AI Agent → Telegram Send Message
Breakdown:
1.	User sends message 
2.	Workflow triggers 
3.	AI processes message 
4.	Reply is sent back 
 If this loop isn’t clear, don’t proceed.
________________________________________
5. Step-by-Step Procedure

 Step 1: Create Telegram Bot
Open Telegram
Search → BotFather
Commands:
/start
/newbot
Then:
•	Give bot name → e.g. Motivation AI Bot 
•	Give username → must end with bot (e.g. motivation_ai_bot) 
You’ll get:
HTTP API Token (IMPORTANT)
________________________________________
Step 2: Create Workflow in n8n
•	Open n8n 
•	Click New Workflow 
________________________________________
Step 3: Add Telegram Trigger
•	Add node → Telegram Trigger 
•	Event: On Message 
Setup:
•	Create credentials 
•	Paste bot token 
👉 Test:
•	Send “Hi” to your bot 
•	Click Execute Workflow 
•	You should see message data 
________________________________________
Step 4: Add AI Agent (GPT Response)
•	Add node → AI Agent / OpenAI Chat 
Configure:
•	Model: GPT-4 Mini (or similar) 
•	Prompt source: Define below 
Input:
Drag Telegram message into prompt:
{{$json["message"]["text"]}}
👉 Test:
•	You should get AI reply 
________________________________________
Step 5: Add Telegram Send Message Node
•	Add node → Telegram 
•	Action: Send Message 
Configure:
Chat ID:
{{$json["message"]["chat"]["id"]}}
Text (AI Response):
{{$node["AI Agent"].json["text"]}}
________________________________________
Step 6: Connect Nodes Properly
Flow should be:
Telegram Trigger
        ↓
     AI Agent
        ↓
Telegram Send Message
________________________________________
Step 7: Test the Bot
•	Activate workflow 
•	Go to Telegram 
•	Send message: 
Example:
Give me productivity tips
👉 Expected:
Bot replies instantly
________________________________________
Step 8: Remove Attribution (Optional)
•	Open Telegram node 
•	Disable: 
o	“Append attribution” 
________________________________________
🔷 6. Final Workflow Summary
Your chatbot now:
•	Listens in real-time 
•	Understands messages 
•	Responds intelligently 
•	Works automatically


**Generates a motivational quote using AI**


•	Fetches email addresses from Google Sheets 
•	Sends the quote via email (Gmail) 
•	Runs automatically every day at 7 AM 


AI + Automation + Email + Scheduling = Daily Motivation System
________________________________________
🔷 2. Tools & Technologies Used
You’re combining multiple systems. If you don’t understand each role, you’ll get stuck fast.
Core Tools:
•	n8n 
o	Automation platform (like Zapier, but more powerful) 
o	Controls the entire workflow 
•	OpenAI (GPT-4 Mini) 
o	Generates motivational quotes 
•	Gmail 
o	Sends emails to users 
•	Google Sheets 
o	Stores recipient email addresses 
________________________________________
🔷 3. Requirements (Don’t skip this or things WILL break)
Before starting:
Accounts Needed:
•	Google account (for Gmail + Sheets) 
•	OpenAI API key 
•	n8n account (cloud or self-hosted) 
Setup Requirements:
•	Connect Gmail credentials in n8n 
•	Connect OpenAI API in n8n 
•	Create a Google Sheet with emails: 
Example:
Email
user1@gmail.com
user2@gmail.com
________________________________________
🔷 4. Workflow Architecture (Understand before building)
This is the actual logic:
Trigger → AI Generate Quote → Get Emails → Send Emails
Breakdown:
1.	Trigger starts workflow 
2.	AI generates content 
3.	System fetches recipients 
4.	Email is sent to each person 
________________________________________

 Step-by-Step Procedure (Beginner Friendly)
 Step 1: Create New Workflow in n8n

•	Open n8n 
•	Click New Workflow 
________________________________________
 Step 2: Add Manual Trigger (Testing Phase)

Why? Because debugging scheduled workflows is painful.
•	Add node → Manual Trigger 
•	Click Execute Workflow 
•	You should see it turn green 
________________________________________
 Step 3: Add AI Quote Generator

•	Add node → Basic LLM Chain 
•	Connect it to Manual Trigger 
Configure:
•	Model: GPT-4 Mini 
•	Prompt: 
Create a motivational quote. Only return the quote. No extra text.
 Test it:
•	Click Execute 
•	You should see a quote output 
________________________________________
 Step 4: Add Google Sheets (Fetch Emails)

•	Add node → Google Sheets 
•	Operation: Read Rows 
Configure:
•	Select your spreadsheet 
•	Select sheet (Sheet1) 

 Output:
•	Multiple items (one per email) 

 Important Concept:
n8n automatically loops through items → no manual loop needed
________________________________________
Step 5: Add Gmail Node (Send Email)

•	Add node → Gmail 
•	Action: Send Message 
Configure:
•	To: Drag email field from Google Sheets 
•	Subject: Motivational Quote 
•	Message: Drag quote output from AI node 
👉 Test:
•	Execute workflow 
•	Check inbox 
________________________________________
Step 6: Remove Gmail Footer (Optional but Clean)

•	Gmail Node → Options 
•	Disable: 
o	“Add n8n attribution” 
________________________________________
Step 7: Replace Manual Trigger with Schedule

Now automation begins.
•	Delete Manual Trigger 
•	Add Schedule Trigger 
Configure:
•	Mode: Daily 
•	Time: 7:00 AM 
Critical:
•	Set correct timezone in n8n settings 
________________________________________
 Step 8: Activate Workflow

•	Click Activate 
 Now it runs automatically every day.
________________________________________
🔷 6. Final Workflow Summary
Your system now:
•	Runs at 7 AM 
•	Generates a fresh quote 
•	Reads email list 
•	Sends quote to all users
 

 

 
 
