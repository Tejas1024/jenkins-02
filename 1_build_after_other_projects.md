# 1_build_after_other_projects.md

# Build After Other Projects Are Built

This trigger is useful when your current Jenkins job depends on another job.

## Example:
Suppose you have two projects:
- Maven → builds your code
- Sample → deploys your code

You can set Jenkins to automatically build Sample only after the Maven job finishes successfully.

---

## ⚙️ Steps:
1. Go to your downstream project (e.g., Sample).
2. Click on Configure → scroll to **Build Triggers**.
3. Check ✅ "Build after other projects are built".
4. In the text box, enter the upstream project name (e.g., Maven).
5. Click on Apply and Save.

💡 Now, when Maven completes, Sample starts automatically.

---

## ✅ Comparison with Poll SCM

| Trigger Type             | Description                          | Example                      |
|-------------------------|------------------------------------|------------------------------|
| Poll SCM                | Triggers build when Git repo changes | Git push triggers build      |
| Build after other projects | Triggers build when another Jenkins job finishes | When Maven finishes, run Sample |
