# Terminal Cheatsheet

> A serverless, zero-database command repository and interactive web app built for developers, sysadmins, and macOS power users.

**Terminal Cheatsheet** turns a static GitHub repository into a fully interactive, cloud-synced command management tool. It requires no external servers, no traditional databases, and zero monthly upkeep costs. All data is stored in a clean `commands.json` file inside your repository and rendered dynamically via GitHub Pages.

---

## ⚡ Key Features

* **Serverless CRUD Architecture:** Add, edit, remove, and search terminal commands directly from the browser without running a backend server.
* **Granular Access Security:** Public visitors can view, search, and click to copy commands. Only the repository owner with a Personal Access Token (PAT) can commit changes to the database.
* **Client-Side Cross-Device Sync:** Authenticate once in your local browser storage (`localStorage`) to update your commands seamlessly across any personal device.
* **Instant Search & High-Contrast UI:** Dark-mode interface with zero-latency client-side filtering for fast script lookups.
* **Zero Infrastructure Overhead:** Hosted completely free using native GitHub Pages and GitHub REST APIs.

---

## 🚀 Live Demo (A work in progress🚀❤️)

Check out the live public cheatsheet:
👉 **[poporobright.github.io/terminal-cheatsheet](https://www.google.com/search?q=https://poporobright.github.io/terminal-cheatsheet/)**

---
<div align="center">
## 🛠️ How It Works

```
┌────────────────────────────────────────┐
│         GitHub Pages Web App           │
│   (index.html + Vanilla JavaScript)    │
└───────────────────┬────────────────────┘
                    │
      ┌─────────────┴─────────────┐
      ▼                           ▼
┌──────────────┐         ┌─────────────────┐
│ Public Users │         │ Repo Owner      │
│ (Read-Only)  │         │ (Write Access)  │
└──────┬───────┘         └────────┬────────┘
       │                          │
       │ GET commands.json        │ PUT (REST API + Token)
       ▼                          ▼
┌────────────────────────────────────────┐
│            GitHub Repository           │
│            (commands.json)             │
└────────────────────────────────────────┘

```
</div>

1. **Reading Data:** On load, the app sends a request to the GitHub REST API to pull the latest `commands.json` array and renders the command cards dynamically.
2. **Writing Data:** When the owner submits or updates an entry, the app encodes the new data array into Base64 and sends a `PUT` request to GitHub's contents API using the owner's PAT.
3. **Cache Invalidation:** API queries include a cache-busting timestamp parameter (`?t=timestamp`) to ensure fresh data is always fetched across different devices and browsers.

---

## 💻 Self-Hosting & Deployment

Want your own cloud-synced cheatsheet? Fork or deploy this project in under 2 minutes:

### 1. Repository Setup

1. Fork or clone this repository.
2. Enable GitHub Pages in your repository settings:
* Go to **Settings** > **Pages**.
* Under **Build and Deployment**, set **Branch** to `main` and **Folder** to `/ (root)`.
* Click **Save**.



### 2. Generate a Personal Access Token (For Editing)

1. Go to **GitHub Settings** > **Developer Settings** > **Personal Access Tokens (classic)**.
2. Generate a token with the **`repo`** scope checked.
3. Open your live GitHub Pages site.
4. Expand **⚙️ Sync Settings** at the bottom of the page, enter your GitHub Username, Repository Name, and Token, then click **Save Sync Settings**.

---

## 📈 Future Expansion Roadmap

This lightweight proof-of-concept lays the foundation for a larger CLI ecosystem:

* [ ] **Native CLI Integration:** Build a terminal tool (`sheet search <keyword>`) that queries your repository's `commands.json` straight from your shell.
* [ ] **Tag & Category Support:** Filter commands by environment (e.g., `#macOS`, `#docker`, `#git`, `#networking`).
* [ ] **Multi-line Bash Support:** Expand card rendering to support multi-step shell scripts with Markdown code blocks.
* [ ] **Team Organization Repos:** Adapt the REST API sync logic for GitHub Organizations to build shared operational runbooks.

---

## 📜 License

Distributed under the MIT License. See `LICENSE` for more information.

Created with ❤️ by **[poporobright](https://github.com/poporobright)**
