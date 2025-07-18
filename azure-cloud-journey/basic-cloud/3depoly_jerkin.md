# 🚀 Jenkins Setup on a Virtual Machine

This guide documents the step-by-step process for installing **Jenkins** on a newly created **Linux Virtual Machine** and accessing it via a web browser.

---

## 🖥️ Prerequisites

- A running **Linux VM** (Ubuntu/Debian-based)
- SSH access to the VM
- Port **8080** open in the firewall/security group

---

## 🔐 Step 1: SSH into the VM

```bash
ssh -i ~/path_to_your_key.pem username@your_vm_ip
🔄 Step 2: Update Packages
bash
Copy
Edit
sudo apt update
sudo apt upgrade -y
☕ Step 3: Install Java (Jenkins Requirement)
bash
Copy
Edit
sudo apt install openjdk-17-jdk -y
java -version
📦 Step 4: Add Jenkins Repository and GPG Key
bash
Copy
Edit
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null

echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
⚙️ Step 5: Install Jenkins
bash
Copy
Edit
sudo apt update
sudo apt install jenkins -y
▶️ Step 6: Start and Enable Jenkins
bash
Copy
Edit
sudo systemctl start jenkins
sudo systemctl enable jenkins
sudo systemctl status jenkins
🔓 Step 7: Allow Port 8080 Through the Firewall
bash
Copy
Edit
sudo ufw allow 8080
sudo ufw reload
🔑 Step 8: Get Jenkins Admin Password
bash
Copy
Edit
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
🌐 Step 9: Open Jenkins in Browser
Visit:

cpp
Copy
Edit
http://<your_vm_ip>:8080
Enter the password retrieved in Step 8.

✅ Step 10: Finish Jenkins Setup
Choose “Install Suggested Plugins”

Create an admin user

Start using Jenkins!

🧱 Notes
Make sure your cloud VM (AWS/Azure/etc.) has port 8080 open in the security group.

You can change Jenkins port later by editing:

bash
Copy
Edit
sudo nano /etc/default/jenkins
🎉 Jenkins is now installed and ready!
yaml
Copy
Edit

---

Let me know if you want a `bash` script version of this too!








Ask ChatGPT



Tools


