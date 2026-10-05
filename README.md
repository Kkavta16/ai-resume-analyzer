# AI Resume Analyzer (n8n)

An AI-powered hiring tool built with **n8n**. HR posts a job, candidates apply with their resume, and AI scores each resume against the job description. HR then picks candidates from a ranked dashboard and sends emails in one click.

## Demo

https://github.com/user-attachments/assets/257a49d5-d939-4f45-9351-5a3ddb44eb13

## How it works

1. **HR Job Posting** – HR fills a form with the job details and job description (text or PDF). The job is saved and AI writes a LinkedIn post with the apply link.
2. **Candidate Application** – The candidate opens the apply link, fills a form and uploads a resume (PDF/TXT). AI reads the resume, compares it with the job, and gives a **match score**, **verdict** (Shortlist / Maybe / Reject), matched and missing skills, and a short summary.
3. **Results Dashboard** – Shows all candidates ranked by score. HR can view or download each resume.
4. **Candidate Emails** – HR clicks **Reject** to send a rejection email, or **Select** to have AI write an email with the next step (interview / assignment). Every email is logged.

```
HR Form → Save Job → AI LinkedIn Post
Apply Form → Upload Resume → Extract Text → AI Recruiter Agent → Save Result → Dashboard → Email
```

## Tech Stack

n8n · AI Agent (LangChain) · Groq LLM (Llama 3.3 70B) · n8n Data Tables · Webhooks · SMTP · JavaScript

## Setup

1. **Import** all 5 JSON files in n8n (Workflows → Import from File).
2. **Run** *0 - Setup Data Tables* once. It creates the jobs, applications and email_log tables. No external database needed.
3. **Add credentials:**
   - **Groq** API key on the Groq Chat Model nodes
   - **SMTP** on the Send Email node (for Gmail, use an [App Password](https://myaccount.google.com/apppasswords) with smtp.gmail.com, port 465, SSL on)
4. **Set your values:** N8N_BASE_URL in the *Prepare Job* node and SENDER_EMAIL in the *Compose Email* node.
5. **Activate** the workflows and open:
   - HR form: *your-n8n-url*/form/hr-post-job
   - Dashboard: *your-n8n-url*/webhook/results

## Notes

- **LinkedIn posting** is turned off by default. The AI-written post is shown on screen so you can copy it to LinkedIn yourself.
- **Public links:** localhost only works on your own computer. To share the apply link, use n8n Cloud or a tunnel like ngrok.
- **Resume formats:** only PDF and TXT are supported (n8n can't read Word files directly).
- **Closing a job:** change its status in the jobs table to anything other than *Open*.
