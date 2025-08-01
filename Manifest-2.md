## ✅ 1. `"action"` – Toolbar Button Behavior

**Purpose:**
Defines what happens when the user **clicks the extension icon** in the browser toolbar.

**Key Uses:**

* Show a popup UI (mini app)
* Set an icon or title dynamically
* Add default behavior on click

**Example:**

```json
"action": {
  "default_popup": "popup.html",
  "default_icon": {
    "16": "icons/icon16.png"
  },
  "default_title": "Click to open Assistant"
}
```

> 🧠 Think of this as the **"entry point"** UI when someone clicks your extension icon.

---

## ✅ 2. `"background"` – Runs Logic Behind the Scenes

**Purpose:**
Runs code **in the background**, even when your popup or UI isn't open.

**Key Uses:**

* Listen to browser events (`tabs`, `runtime`, `alarms`)
* Inject scripts dynamically
* Handle API calls or notifications

**Manifest V3 Format:**

```json
"background": {
  "service_worker": "background.js"
}
```

> ⚙️ Think of this like a **"hidden brain"** of your extension — no UI, just logic.

---

## ✅ 3. `"content_scripts"` – Modifies Web Pages (DOM Access)

**Purpose:**
Automatically injects JS or CSS into **real webpages** to modify or observe them.

**Key Uses:**

* Highlight text
* Modify buttons or layout
* Scrape data from a page

**Example:**

```json
"content_scripts": [
  {
    "matches": ["https://*/*"],
    "js": ["content.js"],
    "run_at": "document_idle"
  }
]
```

> 🧩 This is how your extension **interacts with webpages** directly. Use when you need DOM access.

---

## ✅ 4. `"permissions"` – What Chrome APIs You Can Use

**Purpose:**
Explicitly asks Chrome to let your extension access powerful browser features.

**Key Uses:**

* Read current tab info
* Store data
* Use scripting APIs

**Example:**

```json
"permissions": ["activeTab", "storage", "scripting"]
```

| Permission  | Why It’s Needed                          |
| ----------- | ---------------------------------------- |
| `activeTab` | Read content from the active tab         |
| `storage`   | Store extension settings or cache        |
| `scripting` | Inject JavaScript dynamically into pages |
| `sidePanel` | Use Chrome’s modern side panel UI        |

> 🔒 Be selective. Too many permissions = privacy concern = users may not install it.

---

## ✅ 5. `"host_permissions"` – What Websites You Can Access

**Purpose:**
Specifies which domains (websites) your extension is allowed to interact with.

**Key Uses:**

* Inject scripts into pages (`content.js`, etc.)
* Access or modify specific site content

**Example:**

```json
"host_permissions": [
  "https://example.com/*",
  "https://*.wikipedia.org/*"
]
```

You can also use:

```json
"host_permissions": ["<all_urls>"]
```

> 🌐 This is needed **even if you use `activeTab`**. Without this, scripts won’t run on real sites.

---

## 🧠 TL;DR – When to Use Each?

| Feature            | Use It When...                                       |
| ------------------ | ---------------------------------------------------- |
| `action`           | You want a toolbar button with popup or title        |
| `background`       | You need logic to run silently or in the background  |
| `content_scripts`  | You want to **read/modify** webpage DOM              |
| `permissions`      | You need browser features (tabs, storage, scripting) |
| `host_permissions` | You want to interact with specific **websites**      |
