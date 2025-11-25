Here is a **very clear, step-by-step guide** to create, upload, and run a **Node.js project on an Azure Virtual Machine** (Linux).
This is the **same process real companies use**.

---

# ⭐ **STEP 1 — Create Azure Virtual Machine (Ubuntu)**

1. Log in to Azure Portal → [https://portal.azure.com](https://portal.azure.com)
2. Search **“Virtual Machines”**
3. Click **Create → Azure Virtual Machine**
4. Choose:

   * **Image:** Ubuntu 20.04 LTS
   * **Size:** Standard B1s (cheap, enough for testing)
   * **Authentication:** SSH (recommended) or Password
5. Allow **Inbound Ports:**

   * SSH (22)
   * HTTP (80)
   * Custom TCP 3000 (if your Node app runs on 3000)
6. Click **Create**

---

# ⭐ **STEP 2 — Connect to VM (SSH)**

If you used SSH key:

```bash
ssh -i yourkey.pem azureuser@VM_PUBLIC_IP
```

If password login:

```bash
ssh azureuser@VM_PUBLIC_IP
```

---

# ⭐ **STEP 3 — Install Node.js + npm on VM**

Run inside VM:

```bash
sudo apt update
sudo apt install -y nodejs npm
```

Check versions:

```bash
node -v
npm -v
```

---

# ⭐ **STEP 4 — Install Git (to pull your project)**

```bash
sudo apt install -y git
```

---

# ⭐ **STEP 5 — Upload your Node.js project to VM**

You have **3 options**:

---

## **Option A — Clone from GitHub (best)**

On your VM:

```bash
git clone https://github.com/yourusername/your-node-project.git
cd your-node-project
npm install
```

---

## **Option B — Upload ZIP from local using SCP**

On your local system:

```bash
scp -i yourkey.pem project.zip azureuser@VM_PUBLIC_IP:/home/azureuser
```

Then on VM:

```bash
unzip project.zip
cd yourproject
npm install
```

---

## **Option C — Use SFTP (drag & drop)**

Use **FileZilla** → connect with SSH → upload project folder.

---

# ⭐ **STEP 6 — Start Node.js App**

```bash
node server.js
```

(or whichever is your main file)

But this stops when you close SSH.
So use **PM2** to run permanently.

---

# ⭐ **STEP 7 — Install PM2 (Recommended)**

```bash
sudo npm install -g pm2
```

Start your app:

```bash
pm2 start server.js
pm2 save
pm2 startup
```

---

# ⭐ **STEP 8 — Open Port in Azure**

Go to:

Azure Portal → Virtual Machine → **Networking** → Add inbound rule

Add:

| Port | Protocol | Purpose     |
| ---- | -------- | ----------- |
| 3000 | TCP      | Node.js app |
| 80   | TCP      | HTTP        |

---

# ⭐ **STEP 9 — Access App in Browser**

```
http://VM_PUBLIC_IP:3000
```

(Or port 80 if you reverse-proxy with Nginx)

---

# ⭐ **STEP 10 (Optional) — Setup Nginx Reverse Proxy**

```bash
sudo apt install nginx -y
sudo nano /etc/nginx/sites-available/default
```

Replace with:

```nginx
server {
    listen 80;

    location / {
        proxy_pass http://localhost:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

Save → restart:

```bash
sudo systemctl restart nginx
```

Now your app runs on:

```
http://VM_PUBLIC_IP
```

No port needed.

---

# 🎉 **You have deployed Node.js on Azure VM successfully!**

---

# If you want, I can help you with:

✔ Complete folder structure for deployment
✔ Azure Storage for file uploads
✔ Deploy a React frontend on same VM
✔ CI/CD from GitHub → VM
✔ SSL setup (HTTPS)

Just tell me!
