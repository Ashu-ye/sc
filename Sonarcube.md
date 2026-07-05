# Complete Guide: SonarQube Setup and Custom Code Analysis

Follow these step-by-step instructions to deploy SonarQube via Docker, configure custom quality parameters, and scan your local source code.

---

## Step 1: Run the SonarQube Container
Deploy the official SonarQube community image with an automatic restart policy.
```bash
docker run -d --name sonarqube-custom --restart unless-stopped -p 9000:9000 sonarqube:community
```
*Note: Wait 1–2 minutes for the system backend and search indexing to fully initialize.*

---

## To remove sonarcupe if it already prensent 
```
sudo docker rm -f sonarqube-custom

sudo docker rmi sonarqube:community
```
---
## Step 2: Initialize the Dashboard & Create Project
1. Open your browser and navigate to `http://localhost:9000` (or `http://your-server-ip:9000`).
2. Log in using the default administrative credentials:
   * **ID**: `admin`
   * **Pass**: `admin`
3. *Security Note:* You will be prompted to change this default password immediately.
4. Go to the **Projects** section -> Click **Create Project** -> Select **Locally**.
5. Fill in your project configurations:
   * **Project display name**: `ditiss`
   * **Project key**: `ditiss`
   * **Main branch name**: `main`
6. Click **Next** -> Choose **Use the global setting** (instance defaults) -> Click **Create Project**.

---

## Step 3: Generate Token & Choose Analysis Method
1. Under **Analysis Methods**, select **Locally**.
2. Under **Provide a token**, choose **Generate a token**. 
3. Enter a name for the token, click **Generate**, and **copy the secret token** immediately to a safe place. Click **Continue**.
4. Under **Run analysis on your project**:
   * Select **Other (for Go, PHP, ...)** to get a universal CLI block.
   * Choose **Linux** as the developer machine OS.
   * Keep this browser window open or save the provided execution string (`sonar-scanner -Dsonar.token=...`).

---

## Step 4: Install Sonar Scanner on Developer Machine
Execute these terminal commands on your host/developer machine to download the scanner and configure a global system soft link safely.

```bash
# 1. Create a tools directory and enter it
mkdir -p ~/sonar && cd ~/sonar

# 2. Download your application source code (Replace with your actual link)
wget Your_code_link

# 3. Download the specific Sonar Scanner binary bundle
wget https://sonarsource.com

# 4. Unzip the downloaded package (Install unzip first if missing: sudo apt install unzip)
unzip sonar-scanner-cli-8.0.1.6346-linux-x64.zip

# 5. Create a system-wide soft link using an absolute path to avoid broken references
sudo ln -sf \$(pwd)/sonar-scanner-8.0.1.6346-linux-x64/bin/sonar-scanner /usr/bin/sonar-scanner
```

---

## Step 5: Configure Custom Quality Profile
Modify rule sets to tailor the scanner to your engineering goals instead of utilizing rigid defaults.

1. Click on **Quality Profiles** in the top main navigation menu.
2. Locate the row for the **Python** programming language -> look for the default **Sonar way** profile.
3. Click the **three vertical dots (:)** on the right side of the row -> Click **Copy**.
4. Name your new rule profile: `ditiss_q_p1`.
5. Click on your newly created `ditiss_q_p1` profile to open its details.
6. Click the numerical counter next to **Inactive** rules to view unapplied rules.
7. Click the **Bulk Change** button in the upper right -> Select **Activate In ditiss_q_p1** -> Confirm your selection.

---

## Step 6: Configure Custom Quality Gate
1. Click on **Quality Gates** in the top main navigation menu.
2. Click **Create** or **Copy** at the top right of the page.
3. Assign a name to your new threshold: `ditiss_gate`.
4. Adjust individual operational metric rules as required for your project workflow.
5. Click the **three vertical dots (:)** next to your new gate -> Select **Set as Default**.

---

## Step 7: Map Custom Profile to the Project
1. Navigate back to the **Projects** menu and open your **ditiss** project dashboard.
2. Go to **Project Settings** (top-right gear icon or menu dropdown) -> Select **Quality Profile**.
3. If an old or incorrect profile mapping exists for your language, delete it.
4. Click **Add Language** -> Select **Python** -> Choose your custom `ditiss_q_p1` profile -> click **Save**.

---

## Step 8: Run the Code Analysis Scan
On your terminal, change directories into your downloaded application code directory and execute the analyzer tool.

```bash
cd /path/to/your/downloaded-code/

sonar-scanner \
  -Dsonar.projectKey=ditiss \
  -Dsonar.sources=. \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.token=your_copied_secret_token_here
```

After the console execution finishes, refresh your dashboard at `http://localhost:9000` to review your newly processed bugs, security metrics, and code smells!
