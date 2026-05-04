# 🚀 Setup Guide: Claude + Codex Code Review Workflow

Follow these steps to integrate automated **code review + security checks** into your WordPress plugin workflow.

---

## 📁 Step 1: Add Required Files

- Extract the template ZIP.
- Copy the `.claude` folder into your **plugin root directory**.
- Copy `.github/workflows/claude-manual-review.yml` into the same root directory.

✅ Final structure should look like:

```
your-plugin/
 ├── .claude/
 ├── .github/
 │    └── workflows/
 │         └── claude-manual-review.yml
 ├── your-plugin.php
 └── other files...
```

---

## Step 2: Exclude Review Files from Production ZIP

After adding these files, make sure they are **not included in your final plugin ZIP**.

### Update `.gitattributes`

```
.github/ export-ignore
.claude/ export-ignore
fix-issues-files.txt export-ignore
fix-issues.csv export-ignore
```

### Update `.distignore`

```
.github/
.claude/
fix-issues-files.txt
fix-issues.csv
```

## Why this is important

- Prevents internal review files from going into production  
- Keeps plugin ZIP clean and lightweight  
- Avoids exposing internal rules and configs to users  

---

## ⚙️ Step 3: Setup Codex in Your IDE

- Install the **Codex extension** (VS Code / Cursor).
- Login using your ChatGPT account.
- Make sure the extension is active and working.

---

## 🔍 Step 4: Run Local Code & Security Review (Codex)

- Open `codex-prompt.txt` from the template.
- Copy the prompt and paste it into the Codex chat panel.
- Run the review on your plugin code.

👉 Codex will generate a file:

```
fix-issues.csv
```

### CSV Format:

```
File Name | Priority | Risk Type | Issue Type | Line No | Existing Code | Risk / Problem | Fix Code Suggestion
```

- Open it using:
  - Excel / Google Sheets  
  - Or online viewer: https://csv-viewer-online.github.io/

---

## 🛠️ Step 5: Fix Issues Before Commit

- Go through all issues listed in `fix-issues.csv`.
- Fix:
  - Missing sanitization / escaping  
  - Missing nonce verification  
  - Capability checks  
  - SQL issues  
  - WordPress coding standard problems  

✅ Always complete this step **before committing or creating a PR**.

---

## Step 6: Manual Code Review & Testing (Important)

- **After applying AI fixes, manually verify everything before creating a PR:**

- Review all changes carefully (do not blindly trust AI fixes)
- Test the plugin functionality:
  - Ensure existing features are NOT broken
  - Check both admin (backend) and frontend
  - Enable debugging: WP_DEBUG and WP_DEBUG_LOG
  - Check debug.log for errors
  - Use tools: Activate Query Monitor plugin
  - Check browser console for JS errors
  - Verify: No PHP warnings/notices
  - No JS errors
  - No UI breakage
  - No performance issues

✅ Only proceed if everything is working correctly and no new issues are introduced.

---

## 🔁 Step 7: Create Pull Request

- After fixing issues, create a **Pull Request (PR)**.
- In the PR comment box, add:

```
@claude
```

---

## 🤖 Step 8: Claude Code Review (GitHub)

- Claude will automatically:
  - Review your PR changes  
  - Detect security vulnerabilities  
  - Suggest improvements  

---

## ✅ Step 9: Final Fix & Merge

- Carefully review all Claude suggestions.
- Fix all reported issues.

❗ **Important:**  
Do NOT merge the PR until:
- All security issues are resolved  
- All major suggestions are addressed  

---

## 💡 Best Practice Workflow

1. Run Codex locally  
2. Fix all issues  
3. Create PR  
4. Run Claude review  
5. Fix remaining issues  
6. Merge safely  

---

## 🎯 Benefits

- 🔒 Strong security (sanitization, escaping, nonces)  
- 📏 WordPress coding standards compliance  
- 🚀 Cleaner and production-ready plugins  
