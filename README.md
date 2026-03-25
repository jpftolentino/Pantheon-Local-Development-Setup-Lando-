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

## 📦 2. Clone the Pantheon Repository

From the Pantheon dashboard, copy the **Dev Git URL**, then run:

```bash
git clone YOUR_PANTHEON_GIT_URL chancellorscircle
cd chancellorscircle

```

----------

## 🔑 3. Configure Pantheon Machine Token in Lando

Set your Pantheon machine token globally in Lando:

```bash
lando config set pantheon.machine.token YOUR_MACHINE_TOKEN --global

```

> You can generate a machine token from your Pantheon account dashboard.

----------

## ⚙️ 4. Initialize Lando with Pantheon

Inside your project directory:

```bash
lando init --source pantheon

```

Follow the prompts:

-   Select your Pantheon account
    
-   Select your site (e.g. `chancellorscircle`)
    
-   Confirm the framework (WordPress/Drupal)
    

This will generate a proper `.lando.yml` file.

----------

## 🚀 5. Start the Local Environment

```bash
lando start

```

----------

## 🔄 6. Pull Database and Files

Pull from the Dev environment:

```bash
lando pull --database=dev --files=dev

```

Or pull from Live (recommended for real content):

```bash
lando pull --database=live --files=live

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

### List users

```bash
lando wp user list

```

### Reset password

```bash
lando wp user update YOUR_USERNAME --user_pass=newpassword

```

### Create a new admin user

```bash
lando wp user create admin admin@example.com --role=administrator --user_pass=password

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

git clone YOUR_PANTHEON_GIT_URL chancellorscircle
cd chancellorscircle

lando config set pantheon.machine.token YOUR_MACHINE_TOKEN --global
lando init --source pantheon
lando start
lando pull --database=dev --files=dev
lando open

```

----------

## 🧠 Notes

-   `lando pull` requires the Pantheon recipe (auto-configured via `lando init`)
    
-   Database credentials are managed by Lando
    
-   MariaDB version warnings can be ignored unless upgrading
    
-   Always pull DB/files after cloning to get a working site
    

----------

## ✅ You’re Done!

You now have a fully working local copy of your Pantheon site.
