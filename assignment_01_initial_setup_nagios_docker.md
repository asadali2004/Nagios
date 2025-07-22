# ✅ Assignment 1: Initial Setup – Beginner-Friendly Instructions

This assignment will help you:

1. 🧩 Install Docker on your computer
2. 🐳 Run Nagios inside Docker
3. 🌐 Access the Nagios Web Dashboard and log in

> 💡 **Estimated time**: 15–25 minutes (most of it is Docker installation)

---

## 📦 Step 1: Install Docker

Docker lets you run software like Nagios inside isolated environments called **containers**, without installing it directly on your system.

---

### 🪟 Windows

1. Download Docker Desktop from here:
   👉 [https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop)

2. Run the installer and follow the instructions

3. Once installed, open Docker Desktop
   You should see a **“Docker is running”** message.

4. Open **Command Prompt** (press `Win + R`, type `cmd`, hit Enter) and type:

   ```bash
   docker --version
   ```

   If you see something like `Docker version 25.x.x`, you're ready! ✅

---

### 🍎 macOS

1. Download Docker for Mac from:
   👉 [https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop)

2. Install it like any other app.

3. Open Docker Desktop and ensure it’s running.

4. Open **Terminal** (press `Cmd + Space`, search for `Terminal`) and type:

   ```bash
   docker --version
   ```

---

### 🐧 Linux (Ubuntu/Debian)

Open your terminal and run:

```bash
sudo apt update
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
```

Verify installation:

```bash
docker --version
```

> If you're not in the `docker` group, you may need to use `sudo` for every Docker command.

---

## 🐳 Step 2: Run the Nagios Docker Container

### 📝 Create a folder on your machine to store Nagios files

For example:

* **Windows**: `C:\Users\yourname\Desktop\nagios-monitoring`
* **Mac/Linux**: `/home/yourname/nagios-monitoring`

> This folder will store Nagios configuration so you don’t lose changes if the container restarts.

---

### ▶️ Run Nagios using this command

Replace the folder path with your actual one:

```bash
docker run -d \
  --name nagios \
  -p 8080:80 \
  -v /absolute/path/to/nagios/etc:/opt/nagios/etc \
  -v /absolute/path/to/nagios/var:/opt/nagios/var \
  jasonrivers/nagios
```

**Example for Windows (Git Bash or WSL):**

```bash
docker run -d \
  --name nagios \
  -p 8080:80 \
  -v /c/Users/yourname/Desktop/nagios-monitoring/etc:/opt/nagios/etc \
  -v /c/Users/yourname/Desktop/nagios-monitoring/var:/opt/nagios/var \
  jasonrivers/nagios
```

> 📁 If the folder doesn't exist yet, Docker will create it for you.

---

### ✅ Confirm it’s running

Type:

```bash
docker ps
```

You should see something like:

```
CONTAINER ID   IMAGE                NAMES     STATUS         PORTS
abc123...      jasonrivers/nagios   nagios    Up (healthy)   0.0.0.0:8080->80/tcp
```

That means Nagios is running!

---

## 🌐 Step 3: Access the Nagios Web Dashboard

1. Open your browser
2. Visit:

```
http://localhost:8080/nagios
```

3. You’ll be prompted to log in.

### 🔐 Default credentials:

* **Username**: `nagiosadmin`
* **Password**: `nagios`

---

### 🧪 What You Should See

* Nagios web interface
* A menu on the left with options like **Hosts**, **Services**, and **Tactical Overview**
* Default host ("localhost") listed

---

## 🎉 Congratulations!

You’ve completed Assignment 1:

✅ Docker installed
✅ Nagios running inside Docker
✅ Web UI accessible at `http://localhost:8080/nagios`