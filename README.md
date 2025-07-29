Summary
Tool	Free?	Account Required?	Notes
Cursor IDE	✅ Free	❌ No	Uses local files
GitHub	✅ Free	✅ Yes	Create a free account for repo access
Docker Compose	✅ Free	❌ No	Install Docker Desktop
n8n (Self-host)	✅ Free	❌ No	Use via http://localhost:5678
n8n.cloud	⚠️ Paid	✅ Yes	30-day free trial only

Absolutely, let's build a complete **n8n Agent demo project** that fetches **today's gold price using an AI agent**, with deployment via **Docker** and **GitHub Actions**, all using **free resources**.

---

### ✅ Project Overview

* **Goal**: AI Agent in n8n to fetch today's gold price
* **Tools**:

  * **n8n** (open-source, self-hosted)
  * **Free APIs** (e.g., [metals.live](https://metals.live) or scraping)
  * **Docker** (for local & cloud deployment)
  * **GitHub Actions** (for CI/CD)
  * **GitHub** (free private/public repo)

---

## ✅ STEP 1: Create GitHub Repo Structure

**Directory structure**:

```
gold-price-n8n-agent/
├── .github/
│   └── workflows/
│       └── docker-deploy.yml
├── docker-compose.yml
├── README.md
└── workflows/
    └── gold_price_agent.json
```

---

## ✅ STEP 2: `docker-compose.yml`

```yaml
version: "3"

services:
  n8n:
    image: n8nio/n8n
    ports:
      - "5678:5678"
    environment:
      - GENERIC_TIMEZONE=Asia/Kolkata
    volumes:
      - ./n8n:/home/node/.n8n
```

Run locally using:

```bash
docker-compose up -d
```

Visit `http://localhost:5678` to use the n8n UI.

---

## ✅ STEP 3: Build AI Agent to Fetch Gold Price

**Option A: Using Metals API (Free, No Auth)**
URL: `https://metals-api.com` or [https://metals.live](https://metals.live)

**Option B: Scrape Google Result (Free)**

### 🧠 n8n Workflow (example steps)

You can create this manually or import a `JSON` workflow.

#### ✳️ Example Steps:

1. **Trigger**: `Cron` (daily or manual)
2. **HTTP Request**:

   * Method: `GET`
   * URL: `https://www.google.com/search?q=gold+price+today`
3. **Extract Data**:

   * Use `HTML Extract` or `Function` node
4. **Send to Telegram / Email / Console / Webhook**

---

## ✅ STEP 4: Export n8n Workflow

After building your workflow in UI:

* Go to the workflow menu
* Click **Export**
* Save it to `workflows/gold_price_agent.json`

---

## ✅ STEP 5: GitHub Actions – `.github/workflows/docker-deploy.yml`

```yaml
name: Deploy n8n Agent

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Set up Docker
        uses: docker/setup-buildx-action@v3

      - name: Build Docker image
        run: docker build . --tag n8n-gold-agent

      - name: Run Docker container
        run: |
          docker run -d -p 5678:5678 n8n-gold-agent
```

📝 This just builds & runs Docker (locally for demo purposes). To deploy online (like Render, Fly.io, etc.), extra steps are needed.

---

## ✅ STEP 6: Run Locally

```bash
git clone https://github.com/YOUR_USERNAME/gold-price-n8n-agent.git
cd gold-price-n8n-agent
docker-compose up
```

Then open `http://localhost:5678`, import `workflows/gold_price_agent.json`.

---

## ✅ STEP 7: (Optional) Free Hosting Options

If you want to deploy the container online for free:

* [Render.com](https://render.com) (free plan)
* [Fly.io](https://fly.io)
* [Railway](https://railway.app)

Or simply run it on your local machine or Raspberry Pi.

---

## ✅ Sample `README.md`

```md
# n8n Gold Price Agent (Free AI Project)

This is a demo AI Agent using n8n that fetches today's gold price using a free HTTP request and automation. It uses:

- Open-source n8n
- Free data sources (Google or Metals.live)
- Docker for deployment
- GitHub Actions for CI/CD

## Usage

1. Clone the repo
2. Run `docker-compose up`
3. Open `http://localhost:5678`
4. Import `gold_price_agent.json` from `workflows/`

###vs code
code .
##cursor ide
cursor .
###push code to github
cd /d D:/your-project-folder

# Initialize git repo
git init

# Add all files
git add .

# Commit changes
git commit -m "Initial commit"

# Connect to GitHub (replace with your GitHub URL)
git remote add origin https://github.com/your-username/your-repo-name.git

# Push to GitHub
git branch -M main
# Step 1: Pull the latest changes from GitHub and merge
git pull origin main --allow-unrelated-histories
:wq (if editor opens)
# Step 2: Now push your local files
git push origin main



#########set up
Is Docker Compose Free? How to Set Up and Run
✅ Yes, Docker Compose is completely free.
✅ Install Docker + Docker Compose:

    Download Docker Desktop: https://www.docker.com/products/docker-desktop

    It includes both Docker Engine and Docker Compose.

🔧 Set Up and Run

    In your project folder, create a file called docker-compose.yml.

Example:

version: "3"

services:
  n8n:
    image: n8nio/n8n
    ports:
      - "5678:5678"
    environment:
      - GENERIC_TIMEZONE=Asia/Kolkata
    volumes:
      - ./n8n:/home/node/.n8n

    Run:

docker-compose up -d

    Open your browser and go to:
    👉 http://localhost:5678

✅ 3. Is n8n Free? Do You Need an Account?
✅ Yes, n8n is open-source and 100% free when you self-host it.

You can run it:

    Locally via Docker or npm

    On your own VM (AWS EC2, GCP, etc.)

    No login required if self-hosted

🔧 Do You Need an Account?

    Self-hosted n8n (via Docker) → ❌ No account needed

    Cloud version at n8n.cloud → ✅ Requires paid subscription after free trial

To use the n8n UI:

    Just go to http://localhost:5678 after running Docker Compose.

    From there, you can:

        Create workflows using drag-and-drop

        Import/export JSON files

        Trigger workflows manually or via API


### trouble shooting
PS D:\demo-projects-2025\n8n-agent-gold-price> docker-compose up -d
empty compose file

https://codebeautify.org/yaml-validator
docker-compose -f ./docker-compose.yml up -d

Open a terminal in your n8n directory (where Docker is running).

2. issue
Run the following command inside the Docker container:

docker exec -it n8n-agent-gold-price-n8n-1 n8n install n8n-nodes-html-extract

(If your container is not named n8n, replace n8n with your container name from docker ps.)

Restart the container:

    docker restart n8n

    Now go to the UI again and search for “HTML Extract” node.



docker ps

docker-compose down
docker-compose up -d

## Screenshot

![Gold Price Workflow](## Screenshot

![Gold Price Workflow](https://n8n agent.png




