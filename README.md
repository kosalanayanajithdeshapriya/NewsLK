

# 📰 NewsLK – News Web Application

## 📌 Project Overview
<img width="1899" height="904" alt="image" src="https://github.com/user-attachments/assets/9f4b0b04-f69d-4e79-9b7e-b05525587dbd" />

**NewsLK** is a web-based news application that delivers up-to-date news articles in a clean and user-friendly interface.
The platform allows users to browse news by category, search for specific topics, and stay informed with real-time updates.

This project demonstrates skills in:

* Web development
* API integration
* Backend development
* UI/UX design
* Data handling
* Deployment (if applicable)

---
🤖 AI Image Generation Pipeline

AI Image Creation Pipeline
For imagery, you’ve built a multi‑provider AI image generation pipeline that sits on top of the news layer and turns text‑only articles into visually rich cards:
Here is a generated image with pipeline includes in the news thumbnail.
<img width="1876" height="906" alt="image" src="https://github.com/user-attachments/assets/a97242a2-e24c-4037-93f2-3ec5b2abd39b" />

Prompt Construction from Article Data

For each article, you build a contextual prompt using the headline, summary, category, and sometimes location.

Prompts are normalized (language, length, style) so different providers receive a consistent description.

Primary Generation with Gemini Vision

Gemini Vision is used as the primary image engine when available.

It receives either the text prompt alone or a combination of text and existing thumbnails to perform image recreation / enhancement.

The output is validated (dimensions, format, content) before being accepted.

Three‑Tier Fallback Chain
When the primary call fails (quota exceeded, timeout, validation failure), you automatically cascade through a three‑step fallback:

Tier 1 – Pollinations: First backup provider for fast, prompt‑based generation.

Tier 2 – DeepAI: Second fallback when Pollinations is unavailable or rate‑limited.

Tier 3 – Craiyon: Final safety net to ensure you almost always get an image, even under heavy load.

Each step checks for:

HTTP/transport errors.

Provider‑level error codes (including rate‑limit responses).

Basic validity (non‑empty, decodable image data).

Rate‑Limit Detection & Smart Retries

You inspect status codes and response bodies to detect rate‑limit conditions.

On rate‑limit detection, you skip to the next provider instead of hammering a failing endpoint.

Optional backoff is used where appropriate to avoid cascading failure.

Firebase Storage for Persistence

Once an image is successfully generated, it is uploaded to Firebase Storage under a deterministic path (for example, keyed by article ID and provider).

A lightweight metadata record (article ID, provider used, timestamp, URL) can be stored (e.g., Firestore or your own DB) so that:

The same article never triggers regeneration unnecessarily.

You can quickly switch providers in the future without migrating old data.

Subsequent page loads read directly from Firebase URLs, eliminating repeat generation costs and latency.

UI Integration

Cards and article pages first check for a stored Firebase image.

If not available, they trigger the pipeline in the background and display a graceful placeholder until the image is ready.

Provider choice and fallback behavior are completely abstracted away from the UI; components receive a single, clean image URL.

3️⃣ Rate-Limit Detection & Caching
Implemented rate-limit monitoring
Used Firebase storage for image caching
Prevents unnecessary repeated API calls
Reduces cost and improves performance
Enhances scalability

Cached images are reused when the same news content appears.

## 🎯 Features

* 🗞️ Latest news updates
* 🔎 Search functionality
* 📂 Category-based filtering (e.g., Technology, Business, Sports, etc.)
* 🌐 API-based dynamic content
* 📱 Responsive design (mobile-friendly)
* ⚡ Fast and lightweight interface
* 🔄 Real-time data fetching

---

## 🛠️ Technologies Used

*(Modify this section according to your actual stack)*

### Frontend:

* HTML5
* CSS3
* JavaScript
* Bootstrap / Tailwind (if used)
* React (if applicable)

### Backend:

* Python (Flask / Django) or Node.js (if used)
* REST API integration

### Database (if used):

* MySQL / MongoDB / SQLite

### APIs:

* News API (or any external news provider)

---

## 🏗️ Project Architecture

```
NewsLK/
│
├── static/              # CSS, JS, images
├── templates/           # HTML files (if using Flask/Django)
├── app.py / server.js   # Backend entry point
├── requirements.txt
├── package.json
├── README.md
└── database/             # (if applicable)
```

---

## 🚀 How to Run the Project

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/kosalanayanajithdeshapriya/NewsLK.git
cd NewsLK
```

### 2️⃣ Install Dependencies

#### If Python:

```bash
pip install -r requirements.txt
```

#### If Node.js:

```bash
npm install
```

### 3️⃣ Run the Application

#### Python:

```bash
python app.py
```

#### Node.js:

```bash
npm start
```

### 4️⃣ Open in Browser

```
http://localhost:5000
```

(or the port specified in your project)

---

## 🔑 API Configuration (If Applicable)

If your project uses a News API:

1. Create an account on the news provider platform.
2. Generate an API key.
3. Add it to your environment variables:

Example:

```bash
API_KEY=your_api_key_here
```

---

## 📸 Screenshots

*(Add screenshots of your homepage, category page, and search results here for better presentation.)*

---

## 💡 Future Improvements

* User authentication system
* Bookmark/save articles feature
* Dark mode support
* Personalized news recommendations
* Admin panel for content management
* Deployment on cloud (AWS / Render / Vercel / Heroku)
* Mobile app version

---

## 🧠 Learning Outcomes

Through this project, I improved my skills in:

* API integration
* Asynchronous data handling
* Full-stack development
* Responsive UI design
* Project structuring
* Git & GitHub workflow

---

## 👨‍💻 Author

**Kosala Nayanajith Deshapriya**
Computer Engineering Undergraduate
GitHub: [https://github.com/kosalanayanajithdeshapriya](https://github.com/kosalanayanajithdeshapriya)

---

## 📜 License

This project is licensed under the MIT License.

