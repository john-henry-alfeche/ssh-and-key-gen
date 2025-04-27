# SSH Setup for GitHub - Step-by-Step Guide

This guide will help you set up SSH to authenticate with GitHub, so you can push and pull without being prompted for your username and password every time.

## 1. **Generate an SSH Key**
   To begin, generate a new SSH key using the following steps:

   1. Open your terminal and run the command below:
   
      ```bash
      ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
      ```

      Replace `"your_email@example.com"` with the email associated with your GitHub account.

   2. When prompted to specify the location, press **Enter** to accept the default path (`/home/youruser/.ssh/id_rsa`).

      ```
      Enter file in which to save the key (/home/youruser/.ssh/id_rsa):
      ```

   3. Set a **passphrase** (optional):
      - If you want extra security, enter a passphrase.
      - If you don’t want a passphrase, just press **Enter** to leave it empty.

      ```
      Enter passphrase (empty for no passphrase):
      ```

      A passphrase adds extra security to your key but requires you to enter it each time you use the key. Decide whether you want it based on your security needs (see below for guidance).

---

## 2. **Add Your SSH Key to the SSH Agent**
   After creating the SSH key, you need to add it to the SSH agent so it can manage your SSH keys.

   1. Start the SSH agent:

      ```bash
      eval "$(ssh-agent -s)"
      ```

      This will start the agent and return something like:
      
      ```
      Agent pid 12345
      ```

   2. Add the SSH private key to the agent:

      ```bash
      ssh-add ~/.ssh/id_rsa
      ```

---

## 3. **Add the SSH Key to Your GitHub Account**

   1. Copy your public SSH key to the clipboard:
   
      ```bash
      cat ~/.ssh/id_rsa.pub
      ```

      This will display the public key. Select and copy the entire output (starting from `ssh-rsa` to your email).

   2. Go to **GitHub** and log in.

   3. In the top-right corner of GitHub, click on your profile picture, then select **Settings**.

   4. In the left sidebar, click on **SSH and GPG keys**.

   5. Click on the **New SSH key** button.

   6. Paste the copied SSH key into the **Key** field.

   7. Give your key a **Title** (e.g., `My Laptop` or `Work PC`) and then click **Add SSH Key**.

---

## 4. **Update the Remote URL of Your GitHub Repository**

   1. Navigate to your GitHub repository folder on your local machine.

   2. Change the remote URL from HTTPS to SSH using this command:
   
      ```bash
      git remote set-url origin git@github.com:yourusername/yourrepository.git
      ```

      Replace `yourusername/yourrepository` with your actual GitHub username and repository name.

   3. Verify that the remote URL has been updated correctly:

      ```bash
      git remote -v
      ```

      The output should look like:

      ```
      origin  git@github.com:yourusername/yourrepository.git (fetch)
      origin  git@github.com:yourusername/yourrepository.git (push)
      ```

---

## 5. **Test Your SSH Connection**

To make sure everything is set up correctly, run the following command:

```bash
ssh -T git@github.com
