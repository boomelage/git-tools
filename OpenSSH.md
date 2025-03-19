```md
# Setting Up GitHub SSH Keys on Linux

This guide explains how to generate and add SSH keys for GitHub authentication.

---

## 1. Check for Existing SSH Keys

Run:

```bash
ls -l ~/.ssh/id_ed25519.pub
```

- If the file **exists**, skip to Step 3.
- If **not found**, move to Step 2.

---

## 2. Generate a New SSH Key

Run:
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```
- When prompted for a location, **press ENTER** to accept the default.
- When asked for a passphrase, **press ENTER** (or set a passphrase for security).

---

## 3. Start and Add SSH Key to SSH Agent

Start the SSH agent:
```bash
eval "$(ssh-agent -s)"
```

Add your key:
```bash
ssh-add ~/.ssh/id_ed25519
```

Verify the key is added:
```bash
ssh-add -l
```

---

## 4. Copy SSH Public Key

Show the key:
```bash
cat ~/.ssh/id_ed25519.pub
```
Copy the output (starting with `ssh-ed25519`).

---

## 5. Add SSH Key to GitHub

1. Go to **GitHub → Settings → SSH and GPG Keys**:  
   [https://github.com/settings/keys](https://github.com/settings/keys)
2. Click **"New SSH Key"**.
3. Set a **Title** (e.g., "My Linux Machine").
4. **Paste** the copied SSH key.
5. Click **"Add SSH Key"**.

---

## 6. Test SSH Connection

Run:
```bash
ssh -T git@github.com
```
If successful, you should see:
```
Hi yourusername! You've successfully authenticated, but GitHub does not provide shell access.
```

---

## 7. Use SSH for Git Operations

Check your GitHub remote URL:
```bash
git remote -v
```

If it uses HTTPS (`https://github.com/...`), change it to SSH:
```bash
git remote set-url origin git@github.com:yourusername/repository.git
```

Now, you can push and pull using SSH:
```bash
git push origin main
git pull origin main
```

# GitHub SSH authentication is now set up!

