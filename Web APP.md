Below is a **clear, step-by-step guide** to help you create an **Azure Web App** and deploy your **Node.js project** on it.
I’ll explain from scratch — *creating resource → deploying code → testing*.

---

# 🚀 **How to Create Azure Web App & Deploy Node.js Project**

---

## ✅ **1. Create Azure Web App (App Service)**

### **Step 1: Login to Azure Portal**

Go to: [https://portal.azure.com](https://portal.azure.com)
Search → **“App Services”** → **Create**

---

## ✅ **2. App Service Configuration**

### **Step 2: Basics Tab**

Fill details:

| Field                | Value                                     |
| -------------------- | ----------------------------------------- |
| **Subscription**     | Select your subscription                  |
| **Resource Group**   | Create new (example: `my-node-rg`)        |
| **Name**             | Your app name (example: `rahul-node-app`) |
| **Runtime Stack**    | **Node.js 18 LTS or 20 LTS**              |
| **Operating System** | **Linux** (preferred for Node.js)         |
| **Region**           | Select nearest region                     |
| **Pricing Plan**     | `B1` or `F1` (Free tier)                  |

Click **Next: Deployment** → Skip
Next → **Monitoring** → Skip

Click **Review + Create** → **Create**

---

## ⏳ **Wait 20–30 seconds for deployment**

Then click **Go to Resource**.

---

# 🎯 **3. Deploy Node.js App on Azure**

You can deploy in 3 ways:

### ✔ Option A: Deploy using **ZIP Upload**

### ✔ Option B: Deploy using **GitHub Actions (CI/CD)**

### ✔ Option C: Deploy using **VS Code Azure Extension**

I’ll explain the easiest first.

---

# ✔ **OPTION A – Deploy Node.js using ZIP upload**

### Step 1: Create your ZIP

Structure must look like:

```
server.js
package.json
package-lock.json
node_modules/   (optional)
```

If you don’t upload node_modules, Azure will auto-install using `npm install`.

Then zip the folder.

---

### Step 2: Go to Azure → App Service

Left sidebar → **Deployment Center**

Select:

* **Source**: *Zip*
* **Upload ZIP* file → *Select your .zip file*
* Click **Deploy**

Azure will deploy and restart automatically.

---

# ✔ **OPTION B – Deploy with GitHub Actions (CI/CD)**

### Step 1: Push your Node.js project to GitHub repo

### Step 2: In Azure App Service

Left sidebar → **Deployment Center**

Choose:

* **Source**: GitHub
* Select Repo
* Select Branch
* Build: **Node.js**
* Select Node version
* Click **Save**

Azure will create a `.github/workflows/azure-node.yml` automatically.

Every push to GitHub = automatic deployment.

---

# ✔ **OPTION C – Deploy from VS Code**

### Step 1: Install extension

Open VS Code → Extensions → search:

**Azure App Service** → Install

### Step 2: Login

Press:

```
Ctrl + Shift + P  
```

Type:

```
Azure: Sign In
```

### Step 3: Deploy

Right-click your App Service → **Deploy to Web App**
Select your project folder → Deploy.

---

# 🌐 **4. Configure Start Command (IMPORTANT)**

Azure requires your project to have a start script.

In **package.json**:

```json
{
  "name": "nodeapp",
  "version": "1.0.0",
  "main": "server.js",
  "scripts": {
    "start": "node server.js"
  }
}
```

If your server uses port:

```js
app.listen(process.env.PORT || 3000)
```

Azure will automatically inject its PORT.

---

# 🧪 **5. Test Your Deployment**

Go to your App Service overview page.
Click **Browse**.

Your webapp URL will look like:

```
https://rahul-node-app.azurewebsites.net
```

---

# 🎉 You're Done!

---

If you want, I can also help you with:

✅ Creating VM and deploying Node.js manually
✅ Adding environment variables
✅ Adding MongoDB/Redis support
✅ Creating CI/CD YAML file
✅ Adding a custom domain + HTTPS

Just tell me what exactly you need next.
