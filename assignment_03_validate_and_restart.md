# ✅ Assignment 3: Validate Config and Restart Nagios

In this assignment, you will **verify that your Nagios configuration files are correct** and then **restart the Nagios service** to apply changes. You’ll also learn how to fix common issues if things go wrong.

---

## 🎯 What You'll Learn

* How to check for errors in Nagios config files
* How to restart the Nagios service inside the Docker container
* How to fix common configuration mistakes
* How to confirm that your changes appear in the Nagios dashboard

---

## ✅ Prerequisites

Before continuing, make sure you’ve:

* ✅ Completed Assignment 2
* ✅ Added at least one host and one service
* ✅ Your Docker container (`nagios`) is running

---

## 📄 Suggested File Name

```bash
assignment_03_validate_and_restart.md
```

---

## 🔍 Step 1: Open a Terminal

You’ll run a few commands in your terminal (Command Prompt, Terminal, Git Bash, or WSL depending on your OS).

---

## 🧪 Step 2: Enter the Nagios Docker Container

Nagios is running inside a Docker container, so we need to "enter" that container to interact with it.

### Run this command:

```bash
docker exec -it nagios /bin/bash
```

* `exec` = execute a command
* `-it` = run it interactively (so you can type commands)
* `nagios` = name of your container

You should now be inside the container. Your prompt may look like this:

```
root@1234567890ab:/#
```

---

## ✅ Step 3: Validate the Nagios Configuration

Now let’s verify the config file (`nagios.cfg`) to make sure there are no syntax or logical errors.

### Run this command inside the container:

```bash
/usr/local/bin/nagios -v /opt/nagios/etc/nagios.cfg
```

---

### 🧾 What to Expect

If everything is correct, you’ll see something like:

```
Reading configuration data...
   Read main config file okay...
   Read object config files okay...

Running pre-flight check on configuration data...

Checking services...
Checking hosts...
...

Things look okay - No serious problems were detected during the pre-flight check
```

✅ That means you’re good to go!

---

### 🛠️ If You See an Error

Here are common problems and how to fix them:

| Error Message                       | What it Means                                            | How to Fix                                                  |
| ----------------------------------- | -------------------------------------------------------- | ----------------------------------------------------------- |
| `Error: Could not find host`        | You used a `host_name` in the service that doesn't exist | Make sure `host_name` in the service matches a defined host |
| `Unexpected token` or `missing '}'` | There’s a typo or missing brace                          | Check for a missing `}` or semicolon                        |
| `check_http not defined`            | The plugin wasn’t written correctly                      | Use `check_http!-H domain.com` with correct syntax          |

Fix the config file on your computer (in `localhost.cfg`), save it, and then re-run the validation command.

---

## 🔁 Step 4: Restart Nagios

Once validation is successful, restart the Nagios service inside the container.

### Run this command:

```bash
service nagios restart
```

You’ll see:

```
[ ok ] Restarting nagios (via systemctl): nagios.service.
```

✅ This means your changes have been applied.

Now exit the container:

```bash
exit
```

---

## 🌐 Step 5: Refresh the Web Interface

Open your browser and visit:

```
http://localhost:8080/nagios
```

* Click on **“Hosts”** → You should see all the hosts you added
* Click on **“Services”** → You should see the new checks
* Check their status (OK, WARNING, CRITICAL, or PENDING)

---

## 🛠️ Troubleshooting Checklist

| Problem                   | Possible Fix                                                 |
| ------------------------- | ------------------------------------------------------------ |
| Services not showing      | Restart Nagios and double-check config                       |
| Host not appearing        | Make sure `host_name` matches exactly in host & service      |
| Validation fails          | Carefully read the line number in the error and check syntax |
| Status stuck on "PENDING" | Wait 1–2 minutes or restart container again                  |
| Dashboard doesn’t change  | Try a hard refresh (Ctrl+F5 or Cmd+Shift+R)                  |

---

## 🎉 Assignment Completion Checklist

* [x] Entered the Docker container
* [x] Ran the config validation command
* [x] Fixed any errors if shown
* [x] Restarted the Nagios service
* [x] Confirmed that your hosts/services appeared in the web dashboard

---

## 🏁 Bonus (Optional): Try Breaking Things

Break and fix — that’s how you learn fast!

* ❌ Remove a closing `}` from a host block and see what error appears during validation
* ❌ Mistype a `host_name` in a service block
* ✅ Then fix them and validate again

This will help you get comfortable with reading Nagios errors.

---
