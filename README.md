# 🌟 Tools in Data Science — LLM Code Deployment Project 

> 🚀 *"From prompt to deployment — an AI-powered pipeline that builds, updates, and evaluates itself!"*

<img width="1584" height="396" alt="app (2)" src="https://github.com/user-attachments/assets/72d1a020-292f-4d3c-8e9f-38acc6fcdacb" />


This project was built as part of the **Tools in Data Science (Sep 2025) for IITMadras Project 1** course dued on 17th October, 2025.  
It demonstrates a **complete AI-assisted DevOps workflow**, integrating **Large Language Models (LLMs)**, **GitHub automation**, and **evaluation APIs** — all tied together with a simple, elegant backend.

---
## Hugging Face Url 

### Huggging Face Code Space : [https://huggingface.co/spaces/AyusmanSamasi/TDSProject](https://huggingface.co/spaces/AyusmanSamasi/TDSProject)

### Hosted App : [https://ayusmansamasi-tdsproject.hf.space/](https://ayusmansamasi-tdsproject.hf.space/)

### Github : [https://github.com/Hariswar8018/TDS-Project/](https://github.com/Hariswar8018/TDS-Project/)
---

## 🧩 Overview

This application is an **LLM-based auto-deployer** that:
1. Receives a `POST` request containing an app brief and task.
2. Verifies a secure secret key.
3. Uses an **LLM-assisted generator** to automatically build the required app.
4. Creates and pushes a GitHub repository programmatically.
5. Publishes the app using **GitHub Pages**.
6. Notifies the instructor’s **evaluation API** with repo metadata.
7. Supports **round 2 updates** — allowing feature additions and re-deployment automatically.

All of this happens through a single API endpoint.  
It’s like giving an LLM a project description… and watching it code, deploy, and report — completely hands-free! 🤯

---

## 🛠️ Tech Stack

| Category | Tools Used |
|-----------|-------------|
| **Backend** | FastAPI (Python) |
| **Automation** | GitHub API (PyGithub) |
| **Deployment** | GitHub Pages + Render/Vercel |
| **Evaluation** | RESTful Evaluation API (Instructor provided) |
| **AI Assistance** | LLM-assisted code generation (templated) |
| **Security** | Environment variable secrets (`.env` file) |

---

## ⚙️ System Workflow

```text
┌──────────────────────────────────────────────┐
│   Instructor System                          │
│  (Sends Task Request via JSON POST)          │
└───────────────┬──────────────────────────────┘
                │
                ▼
      ┌────────────────────────────-┐
      │  FastAPI Endpoint           │
      │  /api-endpoint              │
      │  • Verifies secret          │
      │  • Parses brief & files     │
      │  • Calls LLM (optional)     │
      │  • Builds minimal app       │
      └────────────────────────────-┘
                │
                ▼
      ┌───────────────────────────-─┐
      │ GitHub Automation           │
      │ • Creates public repo       │
      │ • Adds LICENSE + README     │
      │ • Pushes app code           │
      │ • Enables GitHub Pages      │
      └────────────────────────────-┘
                │
                ▼
      ┌────────────────────────────-┐
      │ Evaluation API              │
      │ • Receives repo details     │
      │ • Runs automated LLM checks │
      │ • Sends next-round request  │
      └───────────────────────────-─┘
```

## 🧠 Example Task Flow
### Input JSON:

```
{
  "email": "student@example.com",
  "secret": "mysecret123",
  "task": "markdown-to-html",
  "round": 1,
  "nonce": "xyz-123",
  "brief": "Publish a static page that converts Markdown to HTML using marked.js.",
  "evaluation_url": "https://example.com/eval",
  "attachments": []
}
```
### Output JSON:
```
{
  "status": "ok",
  "repo": "https://github.com/ayus123/markdown-to-html-xyz",
  "pages_url": "https://ayus123.github.io/markdown-to-html-xyz/"
}
```

# 🧰 Setup & Installation
## 1️⃣ Clone the Repository
```
git clone https://github.com/Hariswar8018/TDS-Project.git
cd TDS-Project
```
## 2️⃣ Install Dependencies
```
pip install -r requirements.txt
```
## 3️⃣ Set Environment Variables

Create a .env file in the project root:
```
GITHUB_TOKEN=ghp_YourTokenHere
GITHUB_OWNER=yourgithubusername
SECRET_student_example_com=mysecret
```

Or set them manually:
```
export GITHUB_TOKEN="..."
export GITHUB_OWNER="..."
export SECRET_student_example_com="..."
```
## 4️⃣ Run the Server
### 🔸 We are using FastAPI
```
uvicorn server:app --reload
```

```
The app will be live at http://127.0.0.1:8000.
```
### 🔍 Testing

You can test your endpoint using curl:
```
curl http://127.0.0.1:8000/api-endpoint \
  -H "Content-Type: application/json" \
  -d '{"email":"you@example.com","secret":"mysecret","task":"demo","round":1,"nonce":"abc","brief":"hello","evaluation_url":"https://httpbin.org/post","attachments":[]}'
```

### If successful, you’ll receive:
```
{"status": "ok", "repo": "...", "pages_url": "..."}
```
## 🧩 Deployment
🌐 On Render
```
Connect repo → “New Web Service”

Runtime: Python 3.10+
```
Build command:
```
pip install -r requirements.txt
```

Start command:
```
uvicorn server:app --host 0.0.0.0 --port 10000
```

Add environment variables → Deploy 🚀

### ⚡ On Vercel

Include vercel.json:
```
{
  "builds": [{ "src": "server.py", "use": "@vercel/python" }],
  "routes": [{ "src": "/(.*)", "dest": "server.py" }]
}
```

Then run:
```
vercel deploy
```

## 🧮 Evaluation Metrics

| 🧠 Stage | 🔍 Type | 📋 Description |
|-----------|----------|----------------|
| 🧱 **Static Checks** | 🧾 License & Docs | Checks for MIT License, proper README, and clean repo structure. |
| ⚡ **Dynamic Checks** | 🌐 Live Validation | Ensures GitHub Pages site loads successfully (**HTTP 200**). |
| 🤖 **LLM Checks** | 🧩 Code Review | Uses LLM-based evaluation for clarity, structure, and explanation quality. |
| 🔁 **Round 2** | 🚀 Feature Update | Confirms enhancements or bug fixes were applied correctly. |

---

# 🔒 Security Notes

* All secrets are stored in environment variables.

* No sensitive data is pushed to Git history.

* Uses gitleaks for final repo scanning.

* MIT License ensures open-source distribution with protection.

---

# 💡 Key Learnings

* Automated end-to-end deployment using APIs.

* Understanding of CI/CD pipelines through GitHub automation.

* Secure use of tokens and secrets in real environments.

* Using evaluation APIs for dynamic testing.

* Building maintainable, documented projects — the professional way.

---

# 🧾 License

This project is licensed under the MIT License — see the LICENSE
 file for details.

---

# 🧑‍💻 Author

### 👩‍🎓 Ayusman Samasi

🌸 Cheerful Data Science explorer with a dream of building intelligent systems!

🧠 Math + Physics + Biology enthusiast

### 🇯🇵 Preparing for Japan Tech Career

### 💻 Passionate about AI, App Dev, and Creative Science

“Data tells stories — I just teach machines to listen.” 💫


---
---
---

## 🌈 Acknowledgments

### Special thanks to the Tools in Data Science course instructors
for designing such an innovative hands-on project connecting LLMs, automation, and deployment pipelines! 🙌
