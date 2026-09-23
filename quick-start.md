---
description: Quick start with docker.
---

# Quick Start

## Docker

🔴 __IMPORTANT__: This is not recommended setup for production/live servers!
Use only for local development!

### Prerequisites:
* __docker__
* __git__
* myaac __develop__ branch

### Commands
```bash
git clone https://github.com/slawkens/myaac.git
git checkout develop
cd myaac
cd docker/full
docker compose up --build
```

It can take few minutes to setup everything.

After that you will have full local development setup.

### Access

* myaac: [http://localhost:8001](http://localhost:8001)
* phpmyadmin: [http://localhost:8002](http://localhost:8002) (you should be logged in automatically)
* mailpit: [http://localhost:8025](http://localhost:8025) (here you can view emails sent, for testing purposes)

### Emails
To test emails locally you can configure Mailing in the Admin Panel of MyAAAC with following settings:

Go to Admin Panel -> Settings -> Mailing

* Option: __SMTP__
* Host: __mailpit__ (this is the domain)
* Port __1025__
* Auth: __no__
* Username & password: __leave empty__
* Security: __None__