

This script demonstrates how to clone a private/public GitHub repository using SSH authentication from a Red Hat Linux EC2 instance.

---

## 📌 What This Script Does

1. Connects to GitHub using SSH (secure, token-free method)
2. Clones the specified repository to your current directory
3. Verifies authentication with GitHub
4. Useful for automating deployments, CI/CD pipelines, or bulk repo management from cloud servers

---

## 🖥️ Script Content: `repo.sh`

```bash
#!/bin/bash
USER="kkdevopsonline"  # replace with your org/user
TOKEN="ghp_9" # your GitHub personal access token

curl -s -H "Authorization: token $TOKEN" \
"https://api.github.com/users/$USER/repos?per_page=100" | \
grep -o 'git@[^"]*' | while read repo; do
  git clone "$repo"
done
```

---

## 🧱 Prerequisites

✅ Git must be installed on the server:

```bash
sudo yum install -y git
```

✅ SSH key must be generated and added to GitHub:

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
cat ~/.ssh/id_ed25519.pub
```

👉 Add this public key to GitHub:  
Go to **GitHub → Settings → SSH and GPG Keys → New SSH key**

✅ Verify SSH connection:

```bash
ssh -T git@github.com
```

Expected output:
```
Hi kkdevopsonline! You've successfully authenticated, but GitHub does not provide shell access.
```

---

## 📂 Expected Output

When you run:

```bash
sh repo.sh
```

You will see:

```
Cloning into 'ttttt'...
warning: You appear to have cloned an empty repository.
```

And you’ll find a new directory named `ttttt/` created in your EC2 instance.

---

## ⚠️ Common Errors & Fixes

| Error | Reason | Fix |
|-------|--------|-----|
| `Permission denied (publickey)` | SSH key not set up | Add your SSH key to GitHub |
| `fatal: repository not found` | Repo name is wrong or private | Double-check repo name and access |
| `fatal: not a git repository` | Not inside a repo | Use `cd` to move into a valid repo directory |

---

## 🔁 Optional: Push First Commit After Clone

If the repo is empty (no README, etc.), you can push the first commit:

```bash
cd ttttt
echo "# ttttt" > README.md
git add README.md
git commit -m "Initial commit from EC2"
git push origin main
```

---

## ✅ Use Case

Ideal for:
- Red Hat EC2 instance GitHub integrations
- Teaching students how to work with SSH + Git
- Automation of code fetch during deployment
- Setup of CI/CD pipelines where cloning is needed before build

---

📘 Maintained by: **KK FUNDA – DevOps & Cloud Training contact: 9676831734**
```

---
