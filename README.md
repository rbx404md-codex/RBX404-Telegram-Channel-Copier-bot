🔴 TELEGRAM COPIER

Advanced Telegram Channel Backup & Migration Manager

<p align="center">
  <b>⚡ POWERED BY PYTHON • ASYNCIO • PYROGRAM</b>
</p><p align="center">
  A modern asynchronous Telegram channel backup and migration toolkit with resumable jobs, intelligent deduplication, customizable content processing, and a premium interactive interface.
</p><p align="center">
  <img src="https://img.shields.io/badge/Python-3.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/Telegram-MTProto-26A5E4?style=for-the-badge&logo=telegram&logoColor=white" />
  <img src="https://img.shields.io/badge/Database-SQLite-003B57?style=for-the-badge&logo=sqlite&logoColor=white" />
  <img src="https://img.shields.io/badge/Architecture-Asynchronous-FF304F?style=for-the-badge" />
</p><p align="center">
  <b>Developed by RBX404</b>
</p>---

📌 TABLE OF CONTENTS

- "Overview" (#-overview)
- "Features" (#-features)
- "Architecture" (#-architecture)
- "Core Modules" (#-core-modules)
- "Message Selection" (#-message-selection)
- "Content Processing" (#-content-processing)
- "Security" (#-security)
- "Database Architecture" (#-database-architecture)
- "Installation" (#-installation)
- "Configuration" (#-configuration)
- "Getting Started" (#-getting-started)
- "Commands" (#-commands)
- "Deployment" (#-deployment)
- "Project Structure" (#-project-structure)
- "Troubleshooting" (#-troubleshooting)
- "FAQ" (#-frequently-asked-questions)
- "Disclaimer" (#-disclaimer)

---

🚀 OVERVIEW

Telegram Copier is an asynchronous Python-based Telegram channel backup and migration manager.

It combines:

- Pyrogram (MTProto): Telegram user-account connectivity.
- AsyncTeleBot: Interactive Telegram Bot API interface.
- SQLite: Persistent job states, statistics, and deduplication.
- Asyncio: Non-blocking task management.
- AES-256 + HMAC-SHA256: Authenticated encryption for stored session credentials.

The project is designed for channel owners and authorized administrators who need reliable content archiving, backup, and migration workflows.

🎯 Project Goals

Goal| Description
Performance| Efficient asynchronous processing
Reliability| Resumable jobs and checkpoints
Security| Encrypted session storage
Flexibility| Custom filters and text processing
Usability| Interactive Telegram dashboard
Persistence| SQLite-based state management

---

✨ FEATURES

⚡ 01. Asynchronous Processing

- Non-blocking Telegram operations.
- Configurable batch processing.
- Controlled task concurrency.
- Background job execution.
- Live progress reporting.

📦 02. Flexible Message Selection

- Complete authorized message history.
- Latest 100 messages.
- Latest 500 messages.
- Latest 1,000 messages.
- Custom message ID ranges.
- Custom date ranges.

🧠 03. Intelligent Deduplication

- SHA-256 content hashing.
- Telegram "file_unique_id" support.
- Duplicate detection across jobs.
- Persistent SQLite hash storage.
- Configurable duplicate handling.

🔄 04. Resumable Jobs

- Automatic checkpoint creation.
- Job interruption recovery.
- Persistent progress tracking.
- Resume from the last committed state.
- Job history and statistics.

✍️ 05. Advanced Text Processing

- Find and replace.
- Case-insensitive matching.
- URL removal.
- Mention removal.
- Hashtag removal.
- Custom headers.
- Custom footers.
- Dynamic template variables.

🛡️ 06. Reliability & Rate Management

- Configurable request pacing.
- Telegram FloodWait handling.
- Exponential backoff where appropriate.
- Automatic job pausing.
- Network failure recovery.
- Safe shutdown and checkpoint commits.

🔐 07. Security

- Encrypted session credentials.
- Authenticated encryption.
- Environment-based configuration.
- Restricted administrative access.
- Sensitive information protection.

---

🏗️ ARCHITECTURE

flowchart TD
    A["Telegram User"] --> B["AsyncTeleBot Interface"]
    B --> C["Authentication & Access Control"]
    C --> D["Job Controller"]
    D --> E["Pyrogram MTProto Client"]
    E --> F["Message Reader"]
    F --> G["Content Processor"]
    G --> H["Deduplication Engine"]
    H --> I["Rate Management"]
    I --> J["Destination Channel"]
    D --> K[("SQLite Database")]
    K --> L["Checkpoint Manager"]
    L --> D
    D --> M["Progress Dashboard"]
    M --> A

    style A fill:#171717,stroke:#ff304f,color:#fff
    style B fill:#171717,stroke:#ff304f,color:#fff
    style J fill:#171717,stroke:#ff304f,color:#fff
    style K fill:#171717,stroke:#ff304f,color:#fff

Processing Pipeline

1. User selects an authorized source.
2. User selects an authorized destination.
3. The controller validates access permissions.
4. The message reader retrieves eligible messages.
5. Content processing applies configured rules.
6. Deduplication checks previously processed content.
7. The transfer engine processes permitted messages.
8. SQLite stores job progress.
9. The dashboard updates job statistics.

---

⚙️ CORE MODULES

Module| Responsibility
"bot.py"| Main application
"auth.py"| Authentication management
"client.py"| Telegram client management
"copier.py"| Message processing
"filters.py"| Content filtering
"transform.py"| Text manipulation
"database.py"| SQLite operations
"checkpoint.py"| Job recovery
"dedup.py"| Duplicate detection
"security.py"| Encryption utilities
"proxy.py"| Optional network configuration
"config.py"| Application configuration

---

📂 MESSAGE SELECTION

Available Modes

Mode| Description
All Messages| Process the complete accessible history
Last 100| Process the latest 100 messages
Last 500| Process the latest 500 messages
Last 1,000| Process the latest 1,000 messages
Custom ID| Select a message ID range
Date Range| Select messages by publication date

Example

Start ID: 100
End ID:   500

Date selection:

Start: 2024-01-01
End:   2024-06-30

Messages are processed in chronological order by default.

---

🎛️ CONTENT PROCESSING

Supported Content Filters

- All accessible content
- Photos
- Videos
- Documents
- Audio
- Stickers
- Text-only messages
- Media captions

Caption Extraction

Extract captions from media messages and save them as standalone text entries.

Text Transformation

Example input:

Welcome to @oldchannel!

Visit: https://example.com

#Technology

Possible processed output:

Welcome to our community!

Technology

Find & Replace

Example rules:

Find| Replace
"@oldchannel"| "@newchannel"
"Old Brand"| "New Brand"
"Welcome"| "Hello"

Rules are applied sequentially.

Header & Footer Templates

Header:

📢 {channel}


Footer:

━━━━━━━━━━━━━━
Powered by RBX404

Supported variable:

- "{channel}": Source channel title.

The application should validate Telegram message and caption length limits before sending.

---

🛡️ SECURITY & RELIABILITY

Security is a core part of the project.

Session Protection

Session credentials must be protected using authenticated encryption.

Recommended design:

- AES-256 encryption.
- HMAC-SHA256 authentication.
- Secure key generation.
- Separate encryption keys and encrypted data.
- Restricted database file permissions.

Important: Never store API hashes, OTP codes, or two-step verification passwords in plaintext. Authentication should happen through a trusted and secure login flow, not by collecting credentials in an ordinary bot conversation.

Rate Management

Telegram imposes platform-level limits.

The application should:

- Respect Telegram API restrictions.
- Handle "FloodWait" responses.
- Pause jobs when required.
- Avoid aggressive concurrent transfers.
- Persist progress before shutdown.
- Never attempt to evade spam restrictions.

Job Recovery

When a job stops unexpectedly:

1. Save the last successfully committed message.
2. Persist the job configuration.
3. Record the current processing state.
4. Restore the job after restart.
5. Verify previous results before continuing.

---

🗄️ DATABASE ARCHITECTURE

The application uses SQLite for persistent storage.

1. Deduplication Database

File: "dedup.db"

CREATE TABLE IF NOT EXISTS copied_hashes (
    user_id INTEGER,
    src_chat_id INTEGER,
    file_hash TEXT,
    copied_at REAL,
    PRIMARY KEY (user_id, file_hash)
);

2. Job Statistics

File: "stats.db"

CREATE TABLE IF NOT EXISTS job_stats (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    user_id INTEGER,
    src_title TEXT,
    dst_title TEXT,
    total INTEGER,
    copied INTEGER,
    skipped_dup INTEGER,
    failed INTEGER,
    duration_sec REAL,
    avg_speed REAL,
    created_at REAL
);

3. Daily Statistics

CREATE TABLE IF NOT EXISTS daily_stats (
    user_id INTEGER,
    date_str TEXT,
    messages_copied INTEGER,
    jobs_completed INTEGER,
    PRIMARY KEY (user_id, date_str)
);

4. Checkpoint Storage

CREATE TABLE IF NOT EXISTS job_checkpoints (
    user_id INTEGER PRIMARY KEY,
    src INTEGER,
    dst INTEGER,
    src_title TEXT,
    dst_title TEXT,
    total INTEGER,
    copied_count INTEGER,
    current_index INTEGER,
    skipped_dup INTEGER,
    range_label TEXT,
    content_type TEXT,
    signature TEXT,
    created_at REAL,
    updated_at REAL
);

Recommended SQLite settings:

PRAGMA journal_mode=WAL;
PRAGMA foreign_keys=ON;
PRAGMA busy_timeout=5000;

---

💻 INSTALLATION

Requirements

- Python 3.10+
- Linux, macOS, Windows, or compatible hosting.
- Telegram Bot Token.
- Telegram API ID.
- Telegram API Hash.
- Authorized access to source and destination chats.

Step 01: Clone Repository

git clone https://github.com/your-username/telegram-copier-bot.git

cd telegram-copier-bot/telegram_copier_bot

Step 02: Create Virtual Environment

Linux / macOS:

python3 -m venv venv

source venv/bin/activate

Windows:

python -m venv venv

.\venv\Scripts\Activate.ps1

Step 03: Install Dependencies

python -m pip install --upgrade pip

pip install -r requirements.txt

Step 04: Configure Environment

Create ".env":

BOT_TOKEN=YOUR_BOT_TOKEN

DB_ENCRYPTION_KEY=YOUR_GENERATED_SECRET_KEY

DATABASE_PATH=stats.db

LOG_LEVEL=INFO

Keep ".env" private.

Step 05: Start Application

python bot.py

Expected startup log:

[INFO] Initializing Telegram Copier...
[INFO] Loading application configuration...
[INFO] Connecting to database...
[INFO] Initializing Telegram client...
[INFO] Starting bot polling...
[INFO] Application started successfully.

---

🤖 GETTING STARTED

Step 01: Open the Bot

Send:

/start

Step 02: Authenticate

Complete the secure Telegram account authentication process using the application's supported trusted authentication flow.

Do not share your OTP or two-step verification password with other people.

Step 03: Select Source

Choose a channel where your account has authorized access.

Step 04: Select Destination

Choose an authorized destination channel, group, or supported personal storage location.

Step 05: Configure Job

Select:

- Message range.
- Content filter.
- Text transformation.
- Duplicate handling.

Step 06: Start Processing

Review the configuration and start the authorized backup or migration job.

Step 07: Monitor Progress

The dashboard can display:

Metric| Description
Total| Total eligible messages
Completed| Successfully processed
Skipped| Duplicate or filtered
Failed| Unsuccessful operations
Speed| Average processing rate
Elapsed| Total running time
ETA| Estimated completion time

---

🎮 BOT COMMANDS

Command| Description
"/start"| Open dashboard
"/help"| Display help
"/status"| View active job
"/pause"| Pause current job
"/resume"| Resume saved job
"/cancel"| Cancel current job
"/logout"| Disconnect account securely

---

🚀 PRODUCTION DEPLOYMENT

Linux VPS / systemd

Create a service:

sudo nano /etc/systemd/system/telegram-copier.service

Configuration:

[Unit]
Description=Telegram Copier Service
After=network.target

[Service]
Type=simple
User=ubuntu

WorkingDirectory=/home/ubuntu/telegram_copier_bot

ExecStart=/home/ubuntu/telegram_copier_bot/venv/bin/python bot.py

Restart=on-failure
RestartSec=5

StandardOutput=journal
StandardError=journal

[Install]
WantedBy=multi-user.target

Enable service:

sudo systemctl daemon-reload

sudo systemctl enable telegram-copier

sudo systemctl start telegram-copier

Monitor logs:

sudo journalctl -u telegram-copier -f

---

📁 PROJECT STRUCTURE

telegram_copier_bot/
│
├── bot.py
├── config.py
├── auth.py
├── client.py
├── copier.py
│
├── modules/
│   ├── filters.py
│   ├── transform.py
│   ├── checkpoint.py
│   ├── dedup.py
│   ├── security.py
│   └── proxy.py
│
├── database/
│   ├── database.py
│   ├── models.py
│   └── migrations.py
│
├── assets/
│   ├── logo.png
│   └── screenshots/
│
├── requirements.txt
├── .env
├── .env.example
├── .gitignore
│
├── stats.db
├── dedup.db
│
└── README.md

---

❓ FREQUENTLY ASKED QUESTIONS

<details>
<summary><b>01. Can I copy an entire Telegram channel?</b></summary>You can back up or migrate content you own or have explicit permission to reproduce, subject to Telegram's access controls and API restrictions.

</details><details>
<summary><b>02. Can I resume an interrupted job?</b></summary>Yes. The checkpoint manager stores job progress in SQLite, allowing supported jobs to resume after interruption.

</details><details>
<summary><b>03. Does it support duplicate detection?</b></summary>Yes. SHA-256 hashing and Telegram file identifiers can be used to identify previously processed content.

</details><details>
<summary><b>04. Can I customize captions?</b></summary>Yes. The text transformation engine supports find-and-replace, headers, footers, and configurable text cleanup.

</details><details>
<summary><b>05. Is session data encrypted?</b></summary>The intended security architecture uses AES-256 encryption with HMAC-SHA256 authentication. Actual protection depends on correct implementation and secure key management.

</details><details>
<summary><b>06. Does it work on a VPS?</b></summary>Yes. A Linux VPS or compatible Python hosting environment can run the application continuously.

</details><details>
<summary><b>07. Can I use it with protected channels?</b></summary>The application respects Telegram content protection and access restrictions. It does not implement mechanisms to bypass protected-content controls.

</details>---

🔧 TROUBLESHOOTING

Problem| Suggested Solution
Bot not responding| Check bot token and network
Invalid API credentials| Verify API ID and API Hash
FloodWait| Wait for Telegram's specified duration
Database locked| Review concurrent SQLite writes
Session expired| Re-authenticate securely
Permission denied| Verify destination permissions
Job interrupted| Restore the latest valid checkpoint

---

📜 DISCLAIMER

This project is intended for authorized Telegram channel backup, archiving, and migration.

Users are responsible for:

- Obtaining permission from content owners.
- Respecting copyright and intellectual property.
- Following Telegram's Terms of Service.
- Respecting protected-content restrictions.
- Protecting account credentials and session data.

The developer is not responsible for misuse, unauthorized redistribution, or violations of applicable policies.

---

👨‍💻 DEVELOPER

<p align="center">
  <b>RBX404</b>
</p><p align="center">
  <i>Build • Learn • Automate • Innovate</i>
</p><p align="center">
  <a href="https://t.me/BlackoutZoneRBX404">
    <img src="https://img.shields.io/badge/Telegram-BlackoutZone-26A5E4?style=for-the-badge&logo=telegram" />
  </a>
</p><p align="center">
  <b>© 2026 RBX404. All Rights Reserved.</b>
</p>---

<p align="center">
  <b>🔴 POWERED BY RBX404</b>
  <br/>
  <sub>Technology with purpose. Innovation with responsibility.</sub>
</p>
