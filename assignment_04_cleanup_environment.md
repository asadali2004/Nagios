Great! Let’s finish strong with **Assignment 4: Clean Up the Nagios Docker Environment** — the final step in your practice cycle.

This one teaches you how to **stop, remove, and clean up everything** you created using Docker and Nagios.

As always, this guide is:

✅ Beginner-friendly
✅ Includes all commands
✅ Explains every step
✅ Includes cleanup options based on your needs

---

# 🧹 Assignment 4: Clean Up the Nagios Docker Environment

After you're done testing or learning Nagios, it's a good practice to **clean up** to save system resources and avoid clutter.
This assignment shows you how to safely **stop the Nagios container**, **remove it**, and (optionally) **delete images and config files**.

---

## 🎯 What You'll Learn

* How to stop the Nagios Docker container
* How to remove the container and Docker image
* How to remove Nagios config files from your system (optional)

---

## ✅ Prerequisites

Before starting this assignment:

* You’ve already installed and run Nagios in Docker
* Your container is named `nagios` (if not, change the name in the commands below)

---

## 📄 Suggested File Name

```bash
assignment_04_cleanup_environment.md
```

---

## 1️⃣ Step 1: Stop the Nagios Docker Container

Stopping the container will shut down the Nagios server.

### 🔧 Command:

```bash
docker stop nagios
```

> 💡 If your container has a different name, replace `nagios` with that name.

You should see something like:

```
nagios
```

This means the container has stopped.

---

## 2️⃣ Step 2: Remove the Container

Removing the container deletes the running instance — **but your files remain**, because we used Docker volumes.

### 🔧 Command:

```bash
docker rm nagios
```

Expected output:

```
nagios
```

> ⚠️ Don’t worry — this does NOT delete your config files or image yet.

---

## 3️⃣ Step 3: (Optional) Remove the Docker Image

This step removes the downloaded **Nagios image** from your computer. Do this only if you don’t plan to use Nagios again soon.

### 🔧 Command:

```bash
docker rmi jasonrivers/nagios
```

Expected output:

```
Untagged: jasonrivers/nagios:latest
Deleted: sha256:xxxxxxxxxxxxxxxxxxxxxxx
...
```

---

## 4️⃣ Step 4: (Optional) Delete Config Files from Your System

If you created a folder for Nagios configs (like we did in Assignment 1), you can delete it manually if you don’t need it anymore.

### Example Paths:

* **Windows**:
  `C:\Users\yourname\Desktop\nagios-monitoring`

* **Mac/Linux**:
  `/home/yourname/nagios-monitoring`

### 🧼 Command to remove on Linux/macOS:

```bash
rm -rf /path/to/nagios-monitoring
```

> ⚠️ This permanently deletes the config files you wrote (like `localhost.cfg`)

---

## 📊 Summary of Commands

| Task                            | Command                                  |
| ------------------------------- | ---------------------------------------- |
| Stop container                  | `docker stop nagios`                     |
| Remove container                | `docker rm nagios`                       |
| Remove Docker image             | `docker rmi jasonrivers/nagios`          |
| Delete config folder (optional) | `rm -rf /your/path/to/nagios-monitoring` |

---

## 🎉 Assignment Completion Checklist

* [x] Nagios container is stopped
* [x] Container removed from Docker
* [x] Docker image removed (optional)
* [x] Config files deleted (optional)

---

## 🏁 Done! What’s Next?

If you've completed Assignments 1 to 4:

✅ You can install Docker
✅ Run Nagios in Docker
✅ Add and monitor websites
✅ Fix errors and validate configs
✅ Clean up everything after use

---

## 🔁 Optional Practice

Want to start fresh?

* Re-do Assignment 1 to rebuild your environment
* Try a new site (like a friend's portfolio or a status page)
* Experiment with different check types (`check_ping`, `check_http`, `check_tcp`)

---