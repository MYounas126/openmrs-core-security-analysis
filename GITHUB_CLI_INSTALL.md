# GitHub CLI Installation and SARIF Download Guide
## Manual Installation and Usage

**Author:** Muhammad Younas  
**Date:** July 31, 2025

---

## 🛠️ **Manual GitHub CLI Installation**

### **Step 1: Download GitHub CLI**

1. **Go to:** [https://cli.github.com/](https://cli.github.com/)
2. **Click "Download for Windows"**
3. **Download the latest version** (usually a `.msi` file)
4. **Run the installer** and follow the installation steps

### **Step 2: Verify Installation**

Open a new PowerShell window and run:
```powershell
gh --version
```

You should see something like:
```
gh version 2.x.x (xxxxxxx)
```

### **Step 3: Authenticate with GitHub**

```powershell
gh auth login
```

Follow the prompts to authenticate with your GitHub account.

---

## 📥 **Download SARIF File Using GitHub CLI**

### **Method 1: Download Latest Run**

```powershell
# Navigate to your project directory
cd "C:\Users\u2022456.giki\Downloads\Project\openmrs-core"

# List recent workflow runs
gh run list --repo MYounas126/openmrs-core-security-analysis --workflow "CodeQL Analysis"

# Download artifacts from the latest successful run
gh run download --repo MYounas126/openmrs-core-security-analysis --name codeql-results
```

### **Method 2: Download Specific Run**

```powershell
# Get the run ID from the list above, then:
gh run download <RUN_ID> --repo MYounas126/openmrs-core-security-analysis --name codeql-results
```

---

## 🌐 **Alternative: Web Browser Download**

### **Step-by-Step Manual Process:**

1. **Open your browser** and go to:
   [https://github.com/MYounas126/openmrs-core-security-analysis](https://github.com/MYounas126/openmrs-core-security-analysis)

2. **Click on "Actions" tab**

3. **Look for "CodeQL Analysis" workflow** with ✅ green checkmark

4. **Click on the workflow run** to open details

5. **Scroll down to "Artifacts" section**

6. **Click on the artifact name** (e.g., `codeql-results`)

7. **File will download automatically**

8. **Extract the ZIP file** to get the SARIF file

---

## 🔧 **Troubleshooting**

### **If GitHub CLI Installation Fails:**

1. **Download manually from:** [https://github.com/cli/cli/releases](https://github.com/cli/cli/releases)
2. **Look for the latest Windows release**
3. **Download the `.msi` file**
4. **Run as administrator**

### **If Authentication Fails:**

```powershell
# Try different authentication methods
gh auth login --web
# or
gh auth login --with-token
```

### **If Download Fails:**

1. **Check if the workflow completed successfully**
2. **Verify you have access to the repository**
3. **Try the web browser method instead**

---

## 📋 **Expected Results**

### **After Successful Download:**

1. **ZIP file** containing SARIF results
2. **Extracted folder** with SARIF files
3. **File size:** ~2-5 MB (similar to your original 2.57 MB)

### **SARIF File Contents:**

- **Raw CodeQL analysis results** in JSON format
- **Detailed vulnerability information**
- **File locations and line numbers**
- **Severity levels and descriptions**
- **CVE/CWE references**

---

## 🎯 **Quick Commands Reference**

### **GitHub CLI Commands:**

```powershell
# Check version
gh --version

# Login to GitHub
gh auth login

# List workflow runs
gh run list --repo MYounas126/openmrs-core-security-analysis

# Download artifacts
gh run download --repo MYounas126/openmrs-core-security-analysis --name codeql-results

# View run details
gh run view <RUN_ID> --repo MYounas126/openmrs-core-security-analysis
```

### **PowerShell Commands:**

```powershell
# Navigate to project
cd "C:\Users\u2022456.giki\Downloads\Project\openmrs-core"

# Extract downloaded ZIP
Expand-Archive -Path "codeql-results.zip" -DestinationPath "sarif_results" -Force

# List extracted files
Get-ChildItem -Path "sarif_results" -Recurse
```

---

## 💡 **Pro Tips**

### **For Regular Downloads:**

1. **Create a PowerShell script** to automate the download process
2. **Set up scheduled downloads** for regular monitoring
3. **Use GitHub Actions** to automatically process SARIF files

### **For Analysis:**

1. **Compare SARIF files** from different runs
2. **Track vulnerability trends** over time
3. **Generate compliance reports** from SARIF data

---

## 🆘 **Still Having Issues?**

### **Contact Support:**

1. **GitHub CLI Issues:** [https://github.com/cli/cli/issues](https://github.com/cli/cli/issues)
2. **GitHub Actions Issues:** [https://github.com/actions/runner/issues](https://github.com/actions/runner/issues)
3. **CodeQL Issues:** [https://github.com/github/codeql-action/issues](https://github.com/github/codeql-action/issues)

### **Alternative Solutions:**

1. **Use the web interface** (most reliable)
2. **Contact GitHub support** for technical issues
3. **Use third-party tools** for SARIF processing

---

**Next Steps:** Install GitHub CLI and try the download commands above. If you still have issues, use the web browser method as it's the most reliable approach. 