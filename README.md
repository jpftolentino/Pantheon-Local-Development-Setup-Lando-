
# Pantheon Local Development Setup (Lando)

A quick guide to setting up a local development environment from a Pantheon site using **Git**, **Terminus**, and **Lando**.

----------

## 🧰 Prerequisites

Make sure you have the following installed:

### Git

```bash
git --version

```

### Terminus (Pantheon CLI)

```bash
terminus --version

```

### Lando

```bash
lando version

```

----------

## 🔐 1. Authenticate with Pantheon

Log into Pantheon via Terminus:

```bash
terminus auth:login

```

Verify your sites:

```bash
terminus site:list

```

----------

## ⚙️ 2. Configure Pantheon Machine Token in Lando

Set your Pantheon machine token globally in Lando:

```bash
lando config set pantheon.machine.token YOUR_MACHINE_TOKEN --global

```

> You can generate a machine token from your Pantheon account dashboard.

----------

## 🚀 3. Initialize Lando with Pantheon

From the directory where you want the local project to live, run:

```bash
lando init --source pantheon

```

Follow the prompts:

-   Select your Pantheon account
    
-   Select your site
    
-   Confirm the framework if prompted
    
-   Choose the local app name and destination directory if prompted
    

This will generate the project locally with a proper `.lando.yml` file.

----------

## ▶️ 4. Start the Local Environment

```bash
lando start

```

----------

## 🔄 5. Pull Database and Files

Pull from the Dev environment:

```bash
lando pull --database=dev --files=dev

```

Or pull from Live if needed:

```bash
lando pull --database=live --files=live

```

----------

## 🌿 6. Create a Git Branch (Important)

By default, the Pantheon repository uses the `master` branch.

> ⚠️ IMPORTANT: Do NOT make changes directly on `master`.

Create a new branch before starting any development work:

```bash
git checkout -b your-feature-branch-name

```

----------

## 🌐 7. Open the Local Site

```bash
lando open

```

Or manually visit:

```
https://my-site.lndo.site

```

----------

## 🔐 8. WordPress Login Helpers

```bash
lando open

```

Or manually visit:

```
https://my-site.lndo.site

```

----------

## 🔐 8. WordPress Login Helpers

After pulling the database, you may not have access to an existing admin account locally.

### List users

```bash
lando wp user list

```

### Create a new admin user (recommended)

```bash
lando wp user create localadmin local@example.com --role=administrator --user_pass=password

```

### Reset password (optional)

```bash
lando wp user update YOUR_USERNAME --user_pass=newpassword

```

### Disable 2FA (Wordfence)

Some Pantheon sites enforce Two-Factor Authentication via Wordfence, which can block local login.

Disable it locally:

```bash
lando wp plugin deactivate wordfence

```

> ⚠️ Do NOT commit or push this change. This is for local development only.

### Open admin

```
https://my-site.lndo.site/wp-admin

```

----------

## 🛠 Troubleshooting

### Restart Lando

```bash
lando restart

```

### Rebuild environment

```bash
lando rebuild -y

```

### Destroy and start fresh

```bash
lando destroy -y
lando start

```

### Fix URL issues (WordPress)

```bash
lando wp option update home "https://my-site.lndo.site"
lando wp option update siteurl "https://my-site.lndo.site"

```

----------

## ⚡ Quick Start (All Commands)

```bash
terminus auth:login
terminus site:list

lando config set pantheon.machine.token YOUR_MACHINE_TOKEN --global
lando init --source pantheon
lando start
lando pull --database=dev --files=dev

git checkout -b your-feature-branch-name

lando open
```bash
terminus auth:login
terminus site:list

lando config set pantheon.machine.token YOUR_MACHINE_TOKEN --global
lando init --source pantheon
lando start
lando pull --database=dev --files=dev
lando open

```

----------

## 🧠 Notes

-   `lando pull` requires the Pantheon recipe, which is auto-configured by `lando init --source pantheon`
    
-   Database credentials are managed by Lando
    
-   MariaDB version warnings can usually be ignored unless you are upgrading
    
-   You do not need to clone the repository separately when initializing directly from Pantheon with Lando
    
-   Always pull the database and files after initialization to get a working site
    

----------

## ✅ You’re Done!

You now have a fully working local copy of your Pantheon site.
