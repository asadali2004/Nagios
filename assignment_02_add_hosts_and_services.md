# 🌍 Assignment 2: Add Website Monitoring in Nagios

Welcome to your second assignment! In this guide, you’ll learn how to add **your own websites as hosts** in Nagios and configure **HTTP service checks**.

> 👶 This is written for beginners — no Nagios experience required!

---

## 🎯 What You'll Do

* Add two websites (hosts) for monitoring in Nagios
* Attach HTTP checks (services) for both
* Validate your changes
* View your results in the Nagios web dashboard

---

## ✅ Prerequisites

Before continuing, make sure:

* Nagios is running inside Docker (see Assignment 1)
* You can open [http://localhost:8080/nagios](http://localhost:8080/nagios)
* You know where your config folder is on your system

---

## 📁 Step 1: Open the Nagios Config File

Nagios stores all host and service definitions in `.cfg` files.

Open the file named `localhost.cfg` inside your config folder.

### Example paths:

* **Windows**:
  `C:\Users\yourname\Desktop\nagios-monitoring\etc\objects\localhost.cfg`

* **Mac/Linux**:
  `/home/yourname/nagios-monitoring/etc/objects/localhost.cfg`

Open this file using a code editor (e.g., VS Code, Notepad++, Sublime Text).

---

## 🖥️ Step 2: Add a Host for Your Portfolio Website

We’ll tell Nagios to treat your portfolio (e.g., `asadali.live`) as a monitored "host".

### 🔧 Paste this into `localhost.cfg`:

```cfg
# Host: Asad Ali Portfolio Website
define host {
    use                     generic-host
    host_name               asadali-live
    alias                   Asad Ali Portfolio
    address                 www.asadali.live
    check_command           check_http!-H www.asadali.live
    max_check_attempts      3
    check_interval          2
    retry_interval          1
    check_period            24x7
    notification_interval   30
    notification_period     24x7
    contact_groups          admins
}
```

> 💡 `host_name` is a label. `address` is your real website’s domain.

---

## 🔍 Step 3: Add a Service Check for Your Portfolio

This tells Nagios **how** to monitor the host (in this case, using `check_http`).

### 🔧 Add below your host block:

```cfg
define service {
    use                     generic-service
    host_name               asadali-live
    service_description     HTTP Check - Portfolio
    check_command           check_http!-H www.asadali.live
    max_check_attempts      3
    check_interval          2
    retry_interval          1
    check_period            24x7
    notification_interval   30
    notification_period     24x7
    contact_groups          admins
}
```

---

## 🌐 Step 4: Add Another Host (e.g., GitHub Pages, Netlify)

Let’s say you want to monitor `example.github.io`.

### 🔧 Add this second host block:

```cfg
# Host: GitHub Pages Site
define host {
    use                     generic-host
    host_name               github-site
    alias                   GitHub Page
    address                 example.github.io
    check_command           check_http!-H example.github.io
}
```

### 🔧 And add this service block:

```cfg
define service {
    use                     generic-service
    host_name               github-site
    service_description     HTTP Check - GitHub Page
    check_command           check_http!-H example.github.io
}
```

> 🧠 You can change `example.github.io` to any other domain like `yourname.netlify.app` or `vercel.app`.

---

## 🧪 Step 5: Validate Your Configuration

You **must validate your changes** before restarting Nagios.

### ✅ Run this command:

```bash
docker exec -it nagios /bin/bash
/usr/local/bin/nagios -v /opt/nagios/etc/nagios.cfg
```

If everything is OK, you’ll see:

```
Things look okay - No serious problems were detected during the pre-flight check
```

---

## 🔁 Step 6: Restart Nagios

Still inside the container, restart Nagios to apply changes:

```bash
service nagios restart
exit
```

---

## 📊 Step 7: View Your Hosts and Services

Now open your browser and visit:

```
http://localhost:8080/nagios
```

### Check:

* Click **"Hosts"** → you should see `asadali-live` and `github-site`
* Click **"Services"** → you should see two HTTP checks

Status should show:

* ✅ OK (if website is online)
* ❌ CRITICAL (if it’s down)
* ⏳ PENDING (waiting for first check)

---

## 🛠️ Troubleshooting Guide

| Problem                  | Fix                                            |
| ------------------------ | ---------------------------------------------- |
| Host doesn’t show up     | Check for typos in `host_name`                 |
| Config validation fails  | Make sure `{}` blocks are closed and indented  |
| Always shows "PENDING"   | Try refreshing, or restart Nagios again        |
| “CRITICAL” on valid site | Make sure domain is reachable (try in browser) |
| Nothing updates          | Make sure you're editing the right config file |

---

## ✅ Assignment Completion Checklist

* [x] Host for your portfolio added to `localhost.cfg`
* [x] HTTP service check added for it
* [x] Second host (e.g., GitHub Pages or Netlify) added
* [x] Validated config with no errors
* [x] Restarted Nagios and confirmed in web UI

---

## 🏆 Bonus Practice

Want to try more?

* [ ] Add a service that checks for a **specific word** on the homepage:

```cfg
check_command check_http!-H www.asadali.live -u / -s "Welcome"
```

* [ ] Try using a fake domain (e.g., `invalidtest123.com`) to simulate CRITICAL alerts

---
