<!-- ═══════════════════════════ HEADER ═══════════════════════════ -->
<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:3b0764,50:7c3aed,100:db2777&height=230&section=header&text=StoryGram&fontSize=64&fontColor=ffffff&fontAlignY=36&desc=Where%20readers%2C%20writers%20and%20AI%20share%20one%20shelf&descAlignY=58&descSize=18&animation=fadeIn" alt="StoryGram banner" />
</p>

<p align="center">
  <img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=600&size=20&duration=2800&pause=700&color=C084FC&center=true&vCenter=true&width=680&lines=A+social+network+for+book+lovers+%F0%9F%93%9A;Libraries+%E2%80%A2+Reviews+%E2%80%A2+Friends+%E2%80%A2+Auctions;Stories+co-written+with+Llama+3+%E2%9C%A8;Illustrated+by+Stable+Diffusion+%F0%9F%8E%A8" alt="Typing intro" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/React_18-20232A?style=for-the-badge&logo=react&logoColor=61DAFB" alt="React" />
  <img src="https://img.shields.io/badge/Ant_Design-0170FE?style=for-the-badge&logo=antdesign&logoColor=white" alt="Ant Design" />
  <img src="https://img.shields.io/badge/Express-000000?style=for-the-badge&logo=express&logoColor=white" alt="Express" />
  <img src="https://img.shields.io/badge/MongoDB-47A248?style=for-the-badge&logo=mongodb&logoColor=white" alt="MongoDB" />
  <img src="https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white" alt="FastAPI" />
  <img src="https://img.shields.io/badge/Llama_3-0467DF?style=for-the-badge&logo=meta&logoColor=white" alt="Llama 3" />
  <img src="https://img.shields.io/badge/Stable_Diffusion-8B5CF6?style=for-the-badge&logo=huggingface&logoColor=white" alt="Stable Diffusion" />
</p>

<p align="center">
  <img src="https://img.shields.io/github/languages/top/anthonio-alex-dcosta/StoryGram?style=flat-square&color=7c3aed" alt="Top language" />
  <img src="https://img.shields.io/github/repo-size/anthonio-alex-dcosta/StoryGram?style=flat-square&color=db2777" alt="Repo size" />
  <img src="https://img.shields.io/github/last-commit/anthonio-alex-dcosta/StoryGram?style=flat-square&color=a855f7" alt="Last commit" />
  <img src="https://img.shields.io/badge/course-CSE471-6d28d9?style=flat-square" alt="CSE471" />
</p>

---

## ✨ The idea

> *Reading is solitary. Talking about books shouldn't be.*

**StoryGram** puts a reader's whole life with books in one place. You can build a personal library, lend and review books, find friends with similar taste, bid on rare copies in live auctions, and, when you'd rather write than read, **draft your own story with a local LLM and illustrate it with AI-generated art**.

It runs as **three cooperating services**: a React client, an Express/MongoDB API that handles identity and social data, and a Python AI service that does the generative work.

---

## 🧭 Feature map

<table>
  <tr>
    <td width="33%" valign="top">
      <h3>📚 Library</h3>
      <ul>
        <li>Add books to a personal shelf</li>
        <li>Browse your collection</li>
        <li>Lend books to the community</li>
      </ul>
    </td>
    <td width="33%" valign="top">
      <h3>⭐ Reviews</h3>
      <ul>
        <li>Post reviews on any title</li>
        <li>Read what others think</li>
        <li>Discover books through your network</li>
      </ul>
    </td>
    <td width="33%" valign="top">
      <h3>🤝 Social graph</h3>
      <ul>
        <li>Friend requests and suggestions</li>
        <li>Profile pages with friend cards</li>
        <li>A community built around books</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td width="33%" valign="top">
      <h3>🔨 Auctions</h3>
      <ul>
        <li>Create auctions for books</li>
        <li>Live list of active auctions</li>
        <li>Place bids in real time</li>
      </ul>
    </td>
    <td width="33%" valign="top">
      <h3>🪄 AI storytelling</h3>
      <ul>
        <li><b>Llama 3</b> via Ollama + LangChain</li>
        <li><b>Stable Diffusion v1.5</b> art</li>
        <li>Save and revisit your stories</li>
      </ul>
    </td>
    <td width="33%" valign="top">
      <h3>🔐 Accounts</h3>
      <ul>
        <li><b>bcrypt</b>-hashed passwords</li>
        <li><b>JWT</b> sessions</li>
        <li>Password reset with emailed codes</li>
      </ul>
    </td>
  </tr>
</table>

---

## 🏗️ Architecture

```mermaid
flowchart LR
    U(["👤 Reader"]) --> FE

    subgraph FE["⚛️ Frontend · React 18 + Ant Design"]
        direction TB
        P1["Library & Reviews"]
        P2["Profile & Friends"]
        P3["Auctions"]
        P4["Story Studio"]
    end

    subgraph BE["🟢 Backend · Express"]
        direction TB
        R1["/books"]
        R2["/auction"]
        R3["/ (users, friends)"]
        AUTH["JWT · bcrypt · Nodemailer"]
    end

    subgraph AI["🐍 AI Service · FastAPI"]
        direction TB
        L["/llama → Llama 3 (Ollama)"]
        I["/image → Stable Diffusion"]
    end

    DB[("🍃 MongoDB")]

    P1 & P2 & P3 --> BE
    P4 --> AI
    BE --> DB
    AI --> DB
```

<details>
<summary><b>📂 Project structure</b></summary>

```text
StoryGram/
├── frontend/                 React client (CRA + Ant Design)
│   └── src/components/
│       ├── Auction/          create, list and bid on auctions
│       ├── mybooks/          add and show personal books
│       ├── own_story/        AI story input and saved stories
│       ├── profile/          profile, friends, requests, suggestions
│       ├── review/           post and read reviews
│       ├── registration/     sign in and sign up
│       └── forget password/  email → code → new password flow
├── backend/                  Express + Mongoose REST API
│   ├── models/               users, books, reviews, stories, friends, auctions
│   ├── controller/           business logic per domain
│   └── routes/               route modules mounted in index.js
└── ai/                       FastAPI generative service
    └── app/routers/chat.py   Llama 3 text + Stable Diffusion images
```

</details>

---

## 🚀 Getting started

> **Prerequisites:** Node.js 18+, Python 3.9+, MongoDB, [Ollama](https://ollama.com) with `llama3` pulled, and a CUDA GPU for image generation.

```bash
# 1 · Backend  →  http://localhost:3500
cd backend
npm install
cp .env.example .env   # then fill in MONGO_URI, JWT_SECRET, EMAIL_USER, EMAIL_PASS
npm start

# 2 · AI service  →  http://127.0.0.1:8010
cd ../ai
cp .env.example .env
pip install -r requirements.txt
ollama pull llama3
python run.py

# 3 · Frontend  →  http://localhost:3000
cd ../frontend
npm install
npm start
```

---

## 🧠 Under the hood

| Layer | Choice | Why |
| :-- | :-- | :-- |
| UI | React 18 · Ant Design 5 · React Router 6 | Ready-made components for a content-heavy social UI |
| API | Express 4 · Mongoose 8 | Flexible documents suit books, reviews and social links |
| Auth | bcrypt · jsonwebtoken · Nodemailer | Stateless sessions and self-service password recovery |
| AI text | LangChain · Ollama · Llama 3 | Runs locally, so no per-token cost and stories stay private |
| AI images | 🤗 Diffusers · Stable Diffusion v1.5 | 512×512 illustrations generated in 50 inference steps |

---

<p align="center">
  <a href="https://github.com/anthonio-alex-dcosta"><img src="https://img.shields.io/badge/Built_by-Anthonio_Alex_D_Costa-7c3aed?style=for-the-badge&logo=github&logoColor=white" alt="Author" /></a>
  <a href="https://anthonio-alex-dcosta.github.io/portfolio/"><img src="https://img.shields.io/badge/Portfolio-db2777?style=for-the-badge&logo=googlechrome&logoColor=white" alt="Portfolio" /></a>
</p>

<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:db2777,50:7c3aed,100:3b0764&height=120&section=footer" alt="footer" />
</p>
