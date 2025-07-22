# 🧪 Beginner-Friendly Nagios Monitoring with Docker

Welcome! This guide will walk you through how to **set up Nagios using Docker**, monitor your websites (like a portfolio or web app), **verify your config**, and clean everything up safely.

✅ Perfect for total beginners
🚫 No Linux system setup required
🧱 Just install Docker and follow this guide

---

## 🧰 What You'll Learn

| Step | What You'll Do                            |
| ---- | ----------------------------------------- |
| 1️⃣  | Run Nagios in Docker                      |
| 2️⃣  | Access Nagios Dashboard                   |
| 3️⃣  | Add website monitoring (Hosts & Services) |
| 4️⃣  | Validate config & restart Nagios          |
| 5️⃣  | Troubleshoot common issues                |
| 6️⃣  | Clean up Docker environment               |
| 📝   | Practice tasks to reinforce learning      |

---

## ✅ Prerequisites

* 🧩 [Install Docker](https://www.docker.com/products/docker-desktop)
* 💻 Basic terminal usage (command line)

---

## 1️⃣ Set Up Nagios in Docker

### 🔧 Run this command:

```bash
docker run -d \
  --name nagios \
  -p 8080:80 \
  -v /your/local/path/nagios/etc:/opt/nagios/etc \
  -v /your/local/path/nagios/var:/opt/nagios/var \
  jasonrivers/nagios
```

> 📝 Replace `/your/local/path/` with your real path. Example on Windows:
> `C:\Users\yourname\Desktop\nagios-monitoring`

This command:

* Pulls the Nagios image
* Runs the container in background (`-d`)
* Maps ports so you can access Nagios at `http://localhost:8080`
* Saves config and logs on your machine

---

## 2️⃣ Access Nagios Web Dashboard

### 🌐 Open your browser and go to:

```
http://localhost:8080/nagios
```

### 🔐 Login credentials:

* **Username**: `nagiosadmin`
* **Password**: `nagios`

You’ll see the Nagios dashboard showing system monitoring details. 🎉

---

## 3️⃣ Add Hosts and Services (Websites You Want to Monitor)

You can monitor websites like your portfolio (`asadali.live`) or an app (`chatmate-ivory.vercel.app`).

### 📝 Open the config file:

```bash
/your/local/path/nagios/etc/objects/localhost.cfg
```

> Use any text editor (e.g., VS Code, Notepad++, nano)

---

### 🔹 A. Add a website as a Host (Example: Vercel App)

```cfg
define host {
    use                     generic-host
    host_name               chatmate-vercel
    alias                   ChatMate App on Vercel
    address                 chatmate-ivory.vercel.app
    check_command           check_http!-H chatmate-ivory.vercel.app
}
```

---

### 🔸 B. Add a Service to check that site

```cfg
define service {
    use                     generic-service
    host_name               chatmate-vercel
    service_description     HTTP Check - ChatMate App
    check_command           check_http!-H chatmate-ivory.vercel.app
}
```

> Make sure `host_name` matches exactly between the host and service.

---

### ➕ Add Another Example (Portfolio Site)

```cfg
define host {
    use                     generic-host
    host_name               asadali-live
    alias                   Asad Ali Portfolio
    address                 www.asadali.live
    check_command           check_http!-H www.asadali.live
}

define service {
    use                     generic-service
    host_name               asadali-live
    service_description     HTTP Check - Portfolio Site
    check_command           check_http!-H www.asadali.live
}
```

---

## 4️⃣ Validate Nagios Config (Check for Errors)

### 🔍 Run this inside the container:

```bash
docker exec -it nagios /bin/bash
/usr/local/bin/nagios -v /opt/nagios/etc/nagios.cfg
```

You should see:

```
Things look okay - No serious problems were detected
```

---

## 5️⃣ Restart Nagios and View the Results

### 🔁 Restart Nagios inside the container:

```bash
docker exec -it nagios /bin/bash
service nagios restart
```

---

### 🧪 Check the Dashboard

* Refresh `http://localhost:8080/nagios`
* You should see your websites listed under “Hosts” and “Services”
* Nagios will automatically start checking and show statuses:

  * ✅ OK
  * ⚠️ WARNING
  * ❌ CRITICAL
  * ⏳ PENDING (waiting for first check)

---

## 🛠️ Common Troubleshooting Tips

| Problem                  | Solution                                         |
| ------------------------ | ------------------------------------------------ |
| Host/service not showing | Check for typos in `host_name`                   |
| Stuck in PENDING         | Try restarting Nagios or reduce `check_interval` |
| `check_ping` fails       | Use `check_http` instead (some hosts block ping) |
| Website doesn’t respond  | Try in browser manually to confirm it’s up       |

---

## 6️⃣ Clean Up When You’re Done

### 🛑 Stop the container:

```bash
docker stop nagios
```

### ❌ Remove the container:

```bash
docker rm nagios
```

### 🧼 (Optional) Remove the Docker image:

```bash
docker rmi jasonrivers/nagios
```

### 🧻 (Optional) Delete config files:

```bash
rm -rf /your/local/path/nagios
```

---

## 📝 Practice Assignments (Optional but Recommended)

Try these tasks on your own:

### ✅ Assignment 1: Initial Setup

* [ ] Install Docker
* [ ] Run the Nagios container
* [ ] Access the dashboard and log in

### 🌍 Assignment 2: Add Monitoring

* [ ] Add a host for your own portfolio (e.g., `asadali.live`)
* [ ] Add a second host (e.g., `github.io`, `netlify.app`, etc.)
* [ ] Add services for each using `check_http`

### 🔍 Assignment 3: Validation

* [ ] Run config validation
* [ ] Fix errors if any (copy-paste errors are common)
* [ ] Restart Nagios and check if everything shows up

### 🧹 Assignment 4: Cleanup

* [ ] Stop & remove the container
* [ ] Delete the Docker image and config if no longer needed

---

## 🚀 Bonus: Advanced Check (String Match)

Try this in your service to confirm a keyword exists on your site:

```cfg
check_command           check_http!-H www.asadali.live -u / -s "Welcome"
```

This will fail if “Welcome” is not found in the homepage content.

---

## 🎉 You Did It!

By following this guide, you now know how to:

✅ Set up Nagios using Docker
✅ Monitor live websites
✅ Validate and troubleshoot Nagios config
✅ Clean up your environment
✅ Practice on your own

Let me know if you'd like help with:

* Email/Slack alerts
* Docker Compose version
* Monitoring server metrics (CPU, RAM, Disk)

Happy monitoring! 🖥️📊